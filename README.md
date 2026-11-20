# Csag.Utilities

This is a collection of utilities that we have created to help with our development process. We have decided to open source these utilities in the hopes that they will be useful to others.

## Packages

| Package | Contents |
| --- | --- |
| [`Csag.Utilities`](Csag.Utilities/README.md) | Extension methods for `string`, `StringBuilder`, `DateTime`, `CultureInfo`, `IEnumerable<T>`, `IConfiguration` and `IServiceCollection`, and the `FileSize` helper |
| [`Csag.Utilities.AspNetCore`](Csag.Utilities.AspNetCore/README.md) | `IFormFile` extensions |
| [`Csag.Utilities.EntityFrameworkCore`](Csag.Utilities.EntityFrameworkCore/README.md) | `ISortableEntity` and `DbSet<T>` extensions for sort orders |

Up to 2.1.0 the packages were published as `Neolution.Utilities`, `Neolution.Utilities.AspNetCore` and `Neolution.Utilities.EntityFrameworkCore`. The [3.0.0 release notes](https://github.com/collana-solutions/Csag.Utilities/releases) describe the switch to the new package IDs and namespaces.

## Usage

Add the NuGet package to your project and reference the desired classes in your source code.

```bash
dotnet add package Csag.Utilities
```

## Additional Packages

This library includes specialized packages that extend the core utilities for specific frameworks and third-party libraries. These packages are deliberately separated from the base `Csag.Utilities` package to maintain its framework-agnostic and dependency-free nature, ensuring it can be used in any .NET project without forcing unwanted dependencies.

## Contributing

If you would like to contribute to this project, please submit a pull request.

### Namespace Organization

To ensure clear and unambiguous contribution guidelines, organize utilities into the following namespaces based on their structure:

- **`Csag.Utilities.Extensions`** - for all extension methods
- **`Csag.Utilities.Abstractions`** - for interfaces, base classes, and abstractions
- **`Csag.Utilities.Helpers`** - for static utility classes

### File Naming Guidelines

- **Extensions**: Always `{Type}Extensions.cs` (e.g., `StringExtensions.cs`)
- **Abstractions**: Use descriptive names (e.g., `IValidator.cs`, `RetryPolicy.cs`)
- **Helpers**: Use clear, descriptive names that indicate the class purpose

### Cross-Namespace Dependencies

Extensions can reference Helpers and Abstractions when it makes sense for code reuse and maintainability.

### Extension Method Policy

Create utility methods as extension methods by default for discoverability and ease of use.

**Exceptions - Use static helper classes for:**

- All CLR primitives (`bool`, `byte`, `sbyte`, `short`, `ushort`, `int`, `uint`, `long`, `ulong`, `nint`, `nuint`, `char`, `double`, `float`)
- Selected System .NET types: `decimal`, `object`, and `Enum`

**Exception to the exception:** Custom string representation methods (e.g., `ToCurrencyString()`, `ToHexString()`) are permitted as extension methods on the above types, using the `ToXyzString()` naming convention where `Xyz` describes the output format.

### Test Coverage

Add comprehensive unit tests that cover various usage scenarios, edge cases, and parameter combinations. Strive for high code coverage to ensure reliability.

## Build and Test

### Prerequisites

- The .NET SDK pinned in [global.json](global.json) (10.0.4xx, a newer 10.0 SDK rolls forward).
- Node.js 24 with Corepack, for the changesets tooling: run `corepack enable` and then `pnpm install` once in the repository root.

### Build

```bash
dotnet restore --locked-mode
dotnet build --configuration Release --no-restore
```

Every project has a `packages.lock.json`, and CI restores in locked mode. After changing a package reference, run `dotnet restore` without `--locked-mode` and commit the updated lock files.

### Run Tests

```bash
dotnet test --configuration Release --no-build
```

### Pack

```bash
dotnet pack --configuration Release --no-build -o ./nupkgs
```

## Preview packages

Each pull request to `main` or to a `release/**` branch publishes all three packages to a public preview feed on feedz.io. A draft PR, a PR from a fork and a PR from Dependabot publish no preview. The version is one patch above the current release, for example `3.0.1-pr.42.183` (PR 42, workflow run 183). The **"chore: version packages"** PR publishes a release candidate of the upcoming version instead, for example `3.1.0-pr.73.190`, so the changes of the next release can be tested before it ships. In prerelease mode the version in `package.json` is a prerelease such as `4.0.0-rc.0`, and the preview extends it, for example `4.0.0-rc.0.pr.42.183`. That version sorts after the prerelease and before the next one. A comment on the PR gives the version of its latest push. The feed removes previews after 30 days. Releases go to nuget.org only.

To use a preview in an application, add the feed to the `nuget.config` of the application. The feed needs no credentials:

```xml
<packageSources>
  <clear />
  <add key="nuget.org" value="https://api.nuget.org/v3/index.json" />
  <add key="csag-utilities-previews" value="https://f.feedz.io/collana-solutions/csag-utilities/nuget/index.json" />
</packageSources>
<packageSourceMapping>
  <packageSource key="nuget.org">
    <package pattern="*" />
    <package pattern="Csag.Utilities*" />
  </packageSource>
  <packageSource key="csag-utilities-previews">
    <package pattern="Csag.Utilities*" />
  </packageSource>
</packageSourceMapping>
```

The `Csag.Utilities*` pattern is also necessary under nuget.org. NuGet looks for a package only in the sources of its most specific pattern, so without it the released versions do not restore.

To test a preview:

1. Set every `Csag.Utilities*` package to the preview version.
2. If the application restores in locked mode, update its `packages.lock.json` files.
3. Add the feed only on the branch that tests the preview. The main branch of the application then does not need feedz.io to restore.

## Releases

Due to the nature of this project as a loosely connected collection of utilities, it's important to be strict about following [SemVer](https://semver.org/) to communicate possible breaking changes to the users of this library via version number.

Equally as important is to be precise about the changes made in each release, so users of this library can see easily where changes were made. This repository follows the [collana-solutions release playbook](https://github.com/collana-solutions/release-playbook) (Changesets, NuGet variant):

1. Every PR that changes a package needs a changeset. Run `pnpm changeset`, pick the packages the change affects, choose the bump type and describe the change for consumers of the packages. The three packages are a fixed group, so they always share one version. A change that ships nothing, such as CI or repository documentation, needs an empty changeset: `pnpm changeset --empty`. CI's **Changeset Check** fails a PR without one.
2. On merge to `main`, the Release workflow keeps a **"chore: version packages"** PR up to date. It bumps the versions in the `package.json` files, writes them into the `.csproj` files with `scripts/sync-versions.mjs` and updates the `CHANGELOG.md` file of each package.
3. Merging that PR creates the git tags and the GitHub Releases. The release of `Csag.Utilities` starts the **NuGet Publish** workflow, which packs all three packages and pushes them to nuget.org through trusted publishing.

Dependabot PRs get their changesets automatically. Do not edit the `CHANGELOG.md` files of the packages or the `<Version>` in the `.csproj` files by hand. The [CHANGELOG.md](CHANGELOG.md) in the repository root lists the releases up to 2.1.0.
