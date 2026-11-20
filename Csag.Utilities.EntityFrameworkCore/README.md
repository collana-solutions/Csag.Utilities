# Csag.Utilities.EntityFrameworkCore

Entity Framework Core extensions from [Csag.Utilities](https://github.com/collana-solutions/Csag.Utilities). They live in a package of their own, so `Csag.Utilities` stays free of Entity Framework Core.

## Installation

```bash
dotnet add package Csag.Utilities.EntityFrameworkCore
```

## Contents

- `ISortableEntity` (namespace `Csag.Utilities.EntityFrameworkCore.Abstractions`): an entity with an `int SortOrder`.
- `DbSetExtensions.GetNextSortOrderAsync` (namespace `Csag.Utilities.EntityFrameworkCore.Extensions`): the highest `SortOrder` plus one, or `0` when there is no entity. An optional predicate limits the entities it looks at.

```csharp
using Csag.Utilities.EntityFrameworkCore.Extensions;

item.SortOrder = await dbContext.Items.GetNextSortOrderAsync(x => x.ListId == listId, cancellationToken);
```

Two requests that run at the same time can get the same sort order. Where that matters, add a unique constraint and retry, or use a database sequence.

The [repository README](https://github.com/collana-solutions/Csag.Utilities#readme) lists the other packages.
