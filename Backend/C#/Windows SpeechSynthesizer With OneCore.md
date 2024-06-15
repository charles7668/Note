# Windows SpeechSynthesizer With OneCore

In Windows 10 or newer versions, installed speech voice information is stored in two places within the registry:

1. `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Speech\Voices`
2. `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Speech_OneCore\Voices`

In C#, we can use `SpeechSynthesizer` from `System.Speech` to utilize these voices. However, by default, `GetInstalledVoices` only retrieves installed voices from the first location.

To include all voices, there are two implementation methods:

1. Copy all data from the second location to the first.
2. Use reflection to add all information into the `SpeechSynthesizer` `_installedVoices` field.

Here is a C# helper class that uses reflection to add all OneCore voices to a `SpeechSynthesizer` instance:

```c#
public static class SpeechApiReflectionHelper
{
    private const string PROP_VOICE_SYNTHESIZER = "VoiceSynthesizer";
    private const string FIELD_INSTALLED_VOICES = "_installedVoices";

    private const string ONE_CORE_VOICES_REGISTRY = @"HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Speech_OneCore\Voices";

    private static readonly Type ObjectTokenCategoryType = typeof(SpeechSynthesizer).Assembly
        .GetType("System.Speech.Internal.ObjectTokens.ObjectTokenCategory")!;

    private static readonly Type VoiceInfoType = typeof(SpeechSynthesizer).Assembly
        .GetType("System.Speech.Synthesis.VoiceInfo")!;

    private static readonly Type InstalledVoiceType = typeof(SpeechSynthesizer).Assembly
        .GetType("System.Speech.Synthesis.InstalledVoice")!;


    public static void InjectOneCoreVoices(this SpeechSynthesizer synthesizer)
    {
        var voiceSynthesizer = GetProperty(synthesizer, PROP_VOICE_SYNTHESIZER);
        if (voiceSynthesizer == null) throw new NotSupportedException($"Property not found: {PROP_VOICE_SYNTHESIZER}");

        var installedVoices = GetField(voiceSynthesizer, FIELD_INSTALLED_VOICES) as IList;
        if (installedVoices == null)
            throw new NotSupportedException($"Field not found or null: {FIELD_INSTALLED_VOICES}");

        if (ObjectTokenCategoryType
                .GetMethod("Create", BindingFlags.Static | BindingFlags.NonPublic)?
                .Invoke(null, new object?[] {ONE_CORE_VOICES_REGISTRY}) is not IDisposable otc)
            throw new NotSupportedException($"Failed to call Create on {ObjectTokenCategoryType} instance");

        using (otc)
        {
            if (ObjectTokenCategoryType
                    .GetMethod("FindMatchingTokens", BindingFlags.Instance | BindingFlags.NonPublic)?
                    .Invoke(otc, new object?[] {null, null}) is not IList tokens)
                throw new NotSupportedException($"Failed to list matching tokens");

            foreach (var token in tokens)
            {
                if (token == null || GetProperty(token, "Attributes") == null) continue;

                var voiceInfo =
                    typeof(SpeechSynthesizer).Assembly
                        .CreateInstance(VoiceInfoType.FullName!, true,
                            BindingFlags.Instance | BindingFlags.NonPublic, null,
                            new object[] {token}, null, null);

                if (voiceInfo == null)
                    throw new NotSupportedException($"Failed to instantiate {VoiceInfoType}");

                var installedVoice =
                    typeof(SpeechSynthesizer).Assembly
                        .CreateInstance(InstalledVoiceType.FullName!, true,
                            BindingFlags.Instance | BindingFlags.NonPublic, null,
                            new object[] {voiceSynthesizer, voiceInfo}, null, null);

                if (installedVoice == null)
                    throw new NotSupportedException($"Failed to instantiate {InstalledVoiceType}");

                installedVoices.Add(installedVoice);
            }
        }
    }

    private static object? GetProperty(object target, string propName)
    {
        return target.GetType().GetProperty(propName, BindingFlags.Instance | BindingFlags.NonPublic)?.GetValue(target);
    }

    private static object? GetField(object target, string propName)
    {
        return target.GetType().GetField(propName, BindingFlags.Instance | BindingFlags.NonPublic)?.GetValue(target);
    }
}
```

## Reference

- [c# - SpeechSynthesizer doesn't get all installed voices 3 - Stack Overflow](https://stackoverflow.com/questions/51811901/speechsynthesizer-doesnt-get-all-installed-voices-3)
