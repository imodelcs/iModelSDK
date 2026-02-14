# 规则与建议

在制定 BIS 名称时，应遵循以下规则和建议 [rec.]。这包括 Domain、Schema、Namespace、Class 和 Properties 名称以及别名。

> **注意**：以下项目并非按重要性排序，而是按相关概念分组。

## 通用规则

_BIS 命名约定比 EC 命名更加严格：所有 BIS 名称都是有效的 EC 名称，但并非所有 EC 名称都是有效的 BIS 名称。_

|  | 描述 | 备注 |
| --- | --- | --- |
| 规则 | 仅使用字母数字字符 |  |
| 规则 | 名称中不要使用下划线 | 即使有助于可读性也不要使用下划线：使用 `OrderLineItem` 而不是 `Order_LineItem` |
| 规则 | 名称不能以数字开头 | 例如，`3dGeometry` 是不允许的 |
| 规则 | 名称不能仅大小写不同 | 例如，如果已经有一个名为 `Pricelist` 的名称，则不能再定义一个名为 `PriceList` 的新名称 |
| 规则 | 使用 PascalCase 命名 | PascalCase 表示单词连接在一起，每个单词的首字母大写。例如，`OrderLineItem` |
| 规则 | 使用美式英语拼写 | 例如，使用 `Organization` 而不是 `Organisation` |
| 建议 | 使用最广泛接受和最具描述性的名称 | 在创建新词之前请查阅当前词典。 |
| 建议 | 使用描述实体的单个单词 | 例如，使用 `Person` 而不是 `HumanBeing` |
| 规则 | 不要添加多余的术语 | 如果一个名词可以同样表达其含义，就不要使用两个名词。例如，使用 `Vehicle` 而不是 `TransportationVehicle`。对于 Relationship，我们通常可以从源名称推断出目标的类型。因此，使用 `PhysicalElementIsOfType` 而不是 `PhysicalElementIsOfPhysicalType`（因为 Element 只能是 Physical 类型！） |
| 建议 | 不要向实体添加任何不必要的前缀或后缀 | 特别是像 `Object`、`Instance`、`Entity` 和 `Property` 这样的术语。例如，使用 `Note` 而不是 `NoteEntity`（作为 Class 名称）或 `NoteProperty`（作为 Property 名称）。 |
| 建议 | 单词应少于 30 个字符 |  |
| 建议 | 谨慎使用缩写和首字母缩略词 | 仅在常见且完全明确的情况下使用缩写和首字母缩略词。如果缩写/首字母缩略词不广为人知，请不要使用！尽量限制使用那些出现在缩写和首字母缩略词列表中的词汇，不要使用"不要使用"部分列出的词汇。两个字母的首字母缩略词应两个字母都大写，前提是每个字母代表一个不同的单词。例如，`UI`（"User Interface"）和 `IO`（"Input/Output"）因为两个单词都大写，但 `Db` 因为"Database"是_一个复合词_。三个或更多字母的首字母缩略词仅首字母大写。例如，`Html` 或 `Guid`。单个单词的缩写仅首字母大写。例如，`Id`（"Identification"） |
| 建议 | 谨慎使用数字 | 避免使用 `One21` 和 `Door2Door` 这样的名称。一个众所周知的例外是术语 `1d`、`2d` 和 `3d`（维度）。这些可以用来形成新术语，前提是不违反"名称不能以数字开头"的规则。例如，可接受的名称有 `Spatial1d`、`Model2d` |
| 建议 | 谨慎使用特殊词汇 | 具体来说，确保充分理解特殊术语的语义含义。例如，`List`、`Item`、`Set` 等...参见特殊术语列表。如果它不是 `Aspect`，就不要在名称中放入 `Aspect`。 |
| 规则 | 不要使用 New、Old、Tmp 或 Temp | 当你做某事时看似"新"的东西，在你进行下一次更改时就会变成"旧"的。 |
| 建议 | 避免在 Class 名称中使用 'Base' | 例如，使用 `RasterModel` 而不是 `RasterBaseModel` |
| 建议 | 避免使用组织名称 | 如果需要前缀，优先使用 Domain 而不是组织。例如，使用 `TransportElement` 而不是 `ExorElement` |
| 建议 | 避免使用产品名称 | 例如，避免使用 `eB`、`OpenPlant`、`STAAD`、`Dgn`、`ConnectedProject` 等前缀 |
| 建议 | 避免在术语中使用 Domain 名称 | 例如，`PlanningElement`、`ConceptualElement`、`PlantElement`、`PlantArea` 和 `Area` |
| 建议 | 避免使用版本号或代际名称 | 例如，`V8iFile` |
| 建议 | 优先使用实例而非定义 | 即，如果你需要区分 Entity Definition 和 Entity Instance，并且没有合适的词汇可以区分它们，请为定义添加后缀而不是实例：用户使用实例的频率高于定义。例如，为定义使用 `AttributeDefinition`，为值使用 `Attribute`。**注意**：ECProperty 是一个没有遵循此建议的例子。没有更改它的计划——抱歉。 |

## ECSchema / BIS Domain 名称

|  | 描述 | 备注 |
| --- | --- | --- |
| 规则 | 所有 EcSchema/BIS Domain 名称必须向 BIS 工作组注册以避免冲突。这包括别名。 | 例如，`BisCore`（Schema 名称）和 `bis`。参见 BIS Schema 列表 |
| 规则 | BIS Schema 别名必须是小写 |  |
| 规则 | BIS Schema 别名必须少于 7 个字符 |  |

## Class

|  | 描述 | 备注 |
| --- | --- | --- |
| 规则 | 使用单数形式 | 例如，`File` 而不是 `Files` |
| 规则 | 组合术语时，按重要性递增顺序排列 | 例如，`CableCar`、`AnalogWaterMeter`。**例外**：`2d` 和 `3d`，因为名称不能以数字开头 |
| 建议 | `bis:ElementAspect` 的直接或间接特化的名称应以 `Aspect` 结尾 |  |
| 建议 | 不要使用介词，如 `Of`、`With`、`On`、`An`、`In`、`From` 等 |  |

## Property（包括 "Navigation" Property）

|  | 描述 | 备注 |
| --- | --- | --- |
| 规则 | 当属性是集合时使用名称的复数形式，否则使用单数形式 | `Document.AddedBy`（一个 Document 可以由一个人添加）但可以有多个 Note，所以使用 `Document.Notes` |
| 建议 | 尝试创建与其底层类型同名的属性 | `Document.Lock` 的类型是 `Lock`。**例外**：当实体有多个该类型的属性，或者为了提高可读性时：`Document.AddedBy` 而不是 `Document.Person` |
| 建议 | 不要在名称中包含原始数据类型（int、string） | **例外**：日期。由于 `Date` 既是数据类型又是一个更有意义的名词，像 `DateAdded` 这样的名称是可以接受的，但 `NoteBlob` 不行。 |
| 规则 | 不要在属性名称中包含属性所有者名称 | 例如，`Document.Id` 而不是 `Document.DocumentId`，`Person.Name` 而不是 `Person.PersonName` |
| 规则 | Boolean 名称以 `Is`、`Has`、`Can`、`May` 为前缀 | 例如，`IsUnderChange`、`HasOtherRevision`、`MayChange` |
| 规则 | 当字段表示位掩码时，使用单词的复数形式 | 例如，`StateHints`、`HasFlags` |
| 规则 | 对于 `NavigationProperties`，优先使用相关 `ECClass` 的名称作为属性名称 | 如果需要进一步限定，请考虑使用角色标签中的前缀词。 |

## Relationship

Relationship 命名规则由于相互竞争的关注点而变得困难。

Relationship Class 名称清晰且明确很重要，这样才能理解 Relationship 的目的和约束。

但是，同样重要的是要注意 Relationship Class 名称中的字符数量，因为这是开发者或高级用户在使用 ECSQL 时必须输入的内容。

太长的名称令人沮丧，但模糊的名称也令人沮丧。

以下规则和建议试图平衡这些关注点：

|  | 描述 | 备注 |
| --- | --- | --- |
| 规则 | **使用 Source-Verb-Target** | 例如，`ElementOwnsUniqueAspects`、`OrganizationSellsProducts`。在大多数情况下，"source/target" 只是对象的名称。在这些情况下，添加形容词可能会有帮助：`ElementOwnsChildElements` 中的 `Child` |
| 规则 | **完全指定源约束** 通常，使用源约束的完整 Class 名称作为 Relationship 名称的_源_部分。在某些情况下，如果源约束 Class 名称的后缀无助于理解 Relationship 的目的，可以省略它。 | 例如，"`PhysicalElement`IsOfType"、"`PhysicalSystem`ServicesElements" |
| 规则 | **尝试使用特定的面向动作的动词** 像 _aggregates_、_holds_、_groups_、_represents_、_services_ 这样的动词更具面向动作性，而像 _has_ 或 _relates to_ 这样的动词更被动，不能标识 Relationship 的目的。 | 例如，"DrawingGraphic`Represents`Element"、"PhysicalElement`Services`Elements" |
| 规则 | **使用与 Relationship 强度一致的动词** | - `Owns`、`Contains` 或 `Aggregates` 暗示 _embedding_ - `Represents` 或 `Groups` 暗示 _referencing_。参见 Relationship 强度列表 |
| 规则 | **尽可能缩短目标部分** 使用 Relationship 中的_角色_或目标约束 Class 的缩短形式。 | 例如，"PhysicalElementIsOf`Type`"。在这种情况下，完全指定 `PhysicalType` 的目标约束会使 Relationship Class 名称更长，而不会增加太多清晰度，因为源约束给出了目标约束的强烈提示。 |
| 规则 | **Relationship 名称应指示多重性** 源始终是单数的，目标指示多重性。 | 例如，`ElementOwnsChildElements` (1:N)、`ElementHasLinks` (N:N)、`PhysicalElementIsOfType` (N:1) |
| 规则 | **不要使用连词** 不要使用单数名词或动词，即使它清楚地定义了一个 Relationship。始终使用名词-动词-名词 | 例如，不要使用 `Marriage` 或 `ManAndWoman`；使用 `PersonIsMarriedToPerson` |

## Enumeration

|  | 描述 | 备注 |
| --- | --- | --- |
| 建议 | 通常，使用描述性名称，不带后缀 | 例如，`SurfaceVariation`、`CoordinateSystem` 或 `ExternalSourceAttachmentRole` |

---

**原文**: [Rules and Recommendations](https://www.itwinjs.org/bis/guide/naming-guidelines/rules-and-recommendations/)

**最后更新**: 2025年6月11日
