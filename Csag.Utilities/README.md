# Csag.Utilities

Extension methods and helpers for everyday .NET code. The package does not depend on any framework beyond `Microsoft.Extensions.Options.ConfigurationExtensions`, so it fits into any .NET project.

## Installation

```bash
dotnet add package Csag.Utilities
```

## Contents

Namespace `Csag.Utilities.Extensions`:

- `StringExtensions.Truncate`: shortens a string to a maximum length, optionally ending with a suffix such as `...`.
- `StringBuilderExtensions.AppendLine(value, padding)`: appends a line indented by the given number of spaces.
- `DateTimeExtensions`: `IsMidnight`, `IsEndOfMonth` and `IsInRange`.
- `CultureInfoExtensions.GetLanguageCode`: the neutral culture of a culture, for example `de` for `de-CH`.
- `EnumerableExtensions`: `ForEach`, and `StructFirstOrDefault`, which returns `null` instead of a default value when no struct matches.
- `IConfigurationExtensions`: `GetOptions<TOptions>()` and `GetSection<T>()` read the section named after the type, `GetValue<T, TEnum>(key)` reads a value by an enum key.
- `IServiceCollectionExtensions.AddOptions<TOptions>(configuration)`: configures options from the section named after the type, or from a section name you pass.

Namespace `Csag.Utilities.Helpers`:

- `FileSize.GetHumanReadableFileSize`: formats a number of bytes, for example `1.5 KB`.

The [repository README](https://github.com/collana-solutions/Csag.Utilities#readme) lists the other packages.
