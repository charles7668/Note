# FlagsAttribute Usage

For people who are familiar with C/C++, the concept of flags is not unfamiliar. Flags are very useful for checking whether something contains a specific feature or not, and flags can help reduce memory usage.

In C#, there is a convenient way to handle flags instead of declaring your flag with the value of the `int` type.

- [FlagsAttribute Usage](#flagsattribute-usage)
  - [1. Create an Enum Type with FlagsAttribute](#1-create-an-enum-type-with-flagsattribute)
  - [2. Usage](#2-usage)

## 1. Create an Enum Type with FlagsAttribute

```c#
[Flags]
enum TestFlag {
    None = 0,
    First = 1,
    Second = 2,
    Third = 4,
    All = First | Second | Third
}
```

Alternatively, you can use the `<<` operator instead of 1, 2, 4, 8...

```c#
[Flags]
enum TestFlag {
    None = 0,
    First = 1,
    Second = 1 << 1,
    Third = 1 << 2,
    All = First | Second | Third
}
```

## 2. Usage

```c#
// Declare a test variable with the Third and Second flags
TestFlag test = TestFlag.Third | TestFlag.Second;

// Check if the value contains the First flag, and it should be false
bool hasFirst = (test & TestFlag.First) == TestFlag.First;
```

By using the `Flags` attribute, you can easily combine and check flags in a more readable and maintainable way.
