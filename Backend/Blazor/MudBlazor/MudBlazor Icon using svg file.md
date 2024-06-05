# Using SVG File as Icon in MudBlazor

use the image tag to load SVG file in MudBlazor. Here's an example of how to achieve this:

```C#
<MudIcon Icon="@icon">

@code{
    string icon = "<image height='20px' width='20px' xlink:href='your-svg-file'/>"
}
```

## Reference

- [How to use an image as a custom icon · MudBlazor/MudBlazor · Discussion #5737](https://github.com/MudBlazor/MudBlazor/discussions/5737)
