# Csag.Utilities.AspNetCore

ASP.NET Core extensions from [Csag.Utilities](https://github.com/collana-solutions/Csag.Utilities). They live in a package of their own, so `Csag.Utilities` stays free of the ASP.NET Core framework reference.

## Installation

```bash
dotnet add package Csag.Utilities.AspNetCore
```

## Contents

Namespace `Csag.Utilities.AspNetCore.Extensions`:

- `FormFileExtensions.GetByteArrayAsync`: reads an uploaded `IFormFile` into a byte array.

```csharp
using Csag.Utilities.AspNetCore.Extensions;

byte[] content = await formFile.GetByteArrayAsync(cancellationToken);
```

The [repository README](https://github.com/collana-solutions/Csag.Utilities#readme) lists the other packages.
