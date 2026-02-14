# Schema Production Status（Schema 生产状态）

## Schema Evolution

已发布用于最终用户工作流生产使用的 Schemas 随着时间的推移而演进，添加新功能并进行其他改进。为了管理和跟踪此 schema evolution，使用 schema versioning。有关 BIS schema versioning strategy 的详细信息，请参阅 Schema Versioning and Generations。

尚未发布用于生产的 schema 的单个版本也会演进。Pre-production schema 在发布用于生产之前经历开发和现场测试期间会被扩展和修改。此外，在 schema 发布到生产工作流后，它可能会被弃用。本页面描述 schema evolution 的这个非版本轴的管理和跟踪。

## 动机

正式跟踪 schemas 的 production status 的主要动机是确保它们不会以与 schema author 预期相反的方式使用。本页面描述的机制：

1. 使 schema author 能够明确定义 schema 的预期用途。
2. 使 iModel creator 能够明确定义 iModel 的预期用途。
3. 提供一种机制来确保 iModel 中的 schemas 具有与 iModel 的预期用途兼容的预期用途。

## ProductionStatus Custom Attribute

Schema 的预期用途通过 `ProductionStatus` `CustomAttribute` 跟踪。`ProductionStatus` `CustomAttribute` 可以放置在任何 BIS schema 上。该 `CustomAttribute` 具有一个 `SupportedUse` property，可以具有以下值之一：

| 值 | 含义 |
| --- | --- |
| `Production` | 此 schema 适合在生产工作流中使用。使用此 schema 创建的数据将长期受到支持（可能通过转换）。 |
| `FieldTesting` | 此 schema 适合生产工作流的现场测试。使用此 schema 创建的数据可能不受长期支持，并且可能无法升级。 |
| `NotForProduction` | 此 schema 正在开发中，不应 ever 用于生产工作流。使用此 schema 创建的数据不受支持，可能无法升级。 |
| `Deprecated` | 此 schema 不再推荐用于生产工作流。存在更好的替代方案，应该使用它们。 |

## iModel 对 ProductionStatus 的支持

iModel 生态系统使用 schemas 的 `ProductionStatus` 来确定 schema 是否可以加载到 iModel 中。

### iModel `ProductionStatus` 设置

为了确定 `ProductionStatus` 不是 `Production` 的 schema 是否可以加载到 iModel 中，iModel 技术栈需要了解 iModel 的预期用途。因此，每个 iModel 都包含一个 `ProductionStatus` 设置，声明 iModel 用于生产使用的适用性。此设置的可能值对应于 `ProductionStatus` custom attribute 中的值，尽管它们的定义略有不同：

| 值 | 含义 |
| --- | --- |
| `Production` | 此 iModel 适合在生产工作流中使用。 |
| `FieldTesting` | 此 iModel 适合生产工作流的现场测试。其中包含的数据可能不受长期支持。 |
| `NotForProduction` | 此 iModel 仅适用于开发人员测试，不应 ever 用于生产工作流。其中包含的数据将不受长期支持。 |
| `Deprecated` | （此值不应用于 iModels） |

iModel 的 `ProductionStatus` 设置存储在 be_prop 表中，如下所示：

| 列 | 值 |
| --- | --- |
| NameSpace | "dgn_Db" |
| Name | "ProductionStatus" |
| StrData | "Production"、"FieldTesting" 或 "NotForProduction" |

iModel 的 `ProductionStatus` 值在创建 iModel 时设置。

### Schemas 对 iModels 的兼容性

在 schema 加载时，iModel 技术确认 schema 的 `ProductionStatus` 与 iModel 的 `ProductionStatus` 兼容。这些设置的兼容性如下所示：

| iModel `ProductionStatus` | 兼容的 Schema `ProductionStatus` |
| --- | --- |
| `Production` | `Production`、`Deprecated` |
| `FieldTesting` | `Production`、`FieldTesting`、`Deprecated` |
| `NotForProduction` | `Production`、`FieldTesting`、`NotForProduction`、`Deprecated` |

尝试加载不兼容的 schema 将导致 schema 加载失败。

### 更改 iModel `ProductionStatus`

iModel 的 `ProductionStatus` 在概念上可以"降级"如下：

| iModel `ProductionStatus` | 兼容的降级 `ProductionStatus` |
| --- | --- |
| `Production` | `FieldTesting`、`NotForProduction` |
| `FieldTesting` | `NotForProduction` |
| `NotForProduction` | （无法进一步降级） |

将来，将提供用户降级 iModel 的 `ProductionStatus` 的能力。

iModel 的 `ProductionStatus` 在概念上可以升级如下：

| 升级后的 iModel `ProductionStatus` | 条件 |
| --- | --- |
| `Production` | 没有 `ProductionStatus` 为 `FieldTesting` 或 `NotForProduction` 的 schemas |
| `FieldTesting` | 没有 `ProductionStatus` 为 `NotForProduction` 的 schemas |
| `NotForProduction` | （不能作为升级） |

将来，将提供用户升级 iModel 的 `ProductionStatus` 的能力。

---

| 下一篇：BIS Schema Units
|:---|

最后更新：2022年2月2日
