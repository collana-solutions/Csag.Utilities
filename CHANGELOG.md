# Changelog

This file lists the releases up to 2.1.0, published as `Neolution.Utilities`, `Neolution.Utilities.AspNetCore` and `Neolution.Utilities.EntityFrameworkCore`. From 3.0.0 on, the packages are published as `Csag.Utilities`, `Csag.Utilities.AspNetCore` and `Csag.Utilities.EntityFrameworkCore`, and each package has its own `CHANGELOG.md` in its project folder.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [2.1.0] - 2026-09-14

### Added

- `IServiceCollectionExtensions.AddOptions` with custom section name
- `IConfigurationExtensions.GetValue` with strongly typed key

## [2.0.0] - 2026-05-05

### Changed

- Upgraded target framework to .NET 10.0
- Updated dependencies to latest versions

## [1.0.0] - 2026-05-05

### Added

- `FileSize` utility with method to display bytes in a human-readable way
- `CultureInfo` extension method to get the language code of a culture
- `IEnumerable` extension methods
- `IConfiguration` extension methods
- `IServiceCollection` extension methods
- `String` extension methods
- `DateTime` extension methods
- `StringBuilder` extension methods
- `IFormFile` extension method (AspNetCore package only)
- `DbSet` extension methods for ISortableEntity interface (EntityFrameworkCore package only)

[2.1.0]: https://github.com/neolution-ch/Neolution.Utilities/compare/v2.0.0...v2.1.0
[2.0.0]: https://github.com/neolution-ch/Neolution.Utilities/compare/v1.0.0...v2.0.0
[1.0.0]: https://github.com/neolution-ch/Neolution.Utilities/compare/v1.0.0-rc.1...v1.0.0
