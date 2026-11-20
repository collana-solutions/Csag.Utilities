---
"@collana-solutions/csag-utilities": major
"@collana-solutions/csag-utilities-asp-net-core": major
"@collana-solutions/csag-utilities-entity-framework-core": major
---

The packages move to new IDs and namespaces. The API and the behavior are the same as in 2.1.0.

**New package IDs:**

| Up to 2.1.0 | From 3.0.0 |
| --- | --- |
| `Neolution.Utilities` | `Csag.Utilities` |
| `Neolution.Utilities.AspNetCore` | `Csag.Utilities.AspNetCore` |
| `Neolution.Utilities.EntityFrameworkCore` | `Csag.Utilities.EntityFrameworkCore` |

**New namespaces:**

| Up to 2.1.0 | From 3.0.0 |
| --- | --- |
| `Neolution.Utilities.Extensions` | `Csag.Utilities.Extensions` |
| `Neolution.Utilities.Helpers` | `Csag.Utilities.Helpers` |
| `Neolution.Utilities.AspNetCore.Extensions` | `Csag.Utilities.AspNetCore.Extensions` |
| `Neolution.Utilities.EntityFrameworkCore.Abstractions` | `Csag.Utilities.EntityFrameworkCore.Abstractions` |
| `Neolution.Utilities.EntityFrameworkCore.Extensions` | `Csag.Utilities.EntityFrameworkCore.Extensions` |

**To migrate:**

1. Replace each `Neolution.Utilities*` package reference with the `Csag.Utilities*` package of the same name, at 3.0.0 or later.
2. Replace `Neolution.Utilities` with `Csag.Utilities` in your `using` directives, in global usings (`<Using Include="..." />`) and in fully qualified type names.

The type and method names stay the same. `GetOptions<T>`, `GetSection<T>` and `AddOptions<T>` still look up the configuration section by the name of the options type, without its namespace, so existing configuration keeps working.

The `Neolution.Utilities*` IDs get deprecated on nuget.org, with the `Csag.Utilities*` packages as the alternates. Their existing versions stay available, but they get no new releases.
