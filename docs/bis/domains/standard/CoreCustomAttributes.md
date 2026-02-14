# CoreCustomAttributes (Core Custom Attributes) Schema

**Alias:** CoreCA

**Version:** 1.0.4

用于表示核心 EC 概念的自定义属性，可能包含用于核心自定义属性的 Struct 类。

## 目录

- Struct Classes
  - SchemaNameAndPurpose
  - SchemaReference
- Custom Attribute Classes
  - ClassHasCurrentTimeStampProperty
  - DateTimeInfo
  - Deprecated
  - DynamicSchema
  - Extension
  - HiddenClass
  - HiddenProperty
  - HiddenSchema
  - IsMixin
  - Localizable
  - NotSubclassableInReferencingSchemas
  - PartialSchema
  - ProductionStatus
  - SupplementalProvenance
  - SupplementalSchema
- Enumerations
  - DateTimeComponent
  - DateTimeKind
  - ProductionStatusValue

### SchemaNameAndPurpose _Sealed_ StructClass

用于定义补充 Schema 及其用途

#### 属性

| 名称 | 描述 | 标签 | 类别 | 只读 | 优先级 |
| --- | --- | --- | --- | --- | --- |
| SchemaName | 补充 Schema 的全名 |  |  | false | 0 |
| Purpose | 补充 Schema 的用途 |  |  | false | 0 |

### SchemaReference (Schema Reference) _Sealed_ StructClass

对 Schema 的引用，包括名称和版本

#### 属性

| 名称 | 描述 | 标签 | 类别 | 只读 | 优先级 |
| --- | --- | --- | --- | --- | --- |
| SchemaName | Schema 名称，不包括版本 | Schema Name |  | false | 0 |
| MajorVersion | [This].[Write].[Minor] | Major Version |  | false | 0 |
| MinorVersion | [Major].[Write].[This] | Minor Version |  | false | 0 |
| WriteVersion | [Major].[This].[Minor] | Write Version |  | false | 0 |

## Custom Attribute Classes

### ClassHasCurrentTimeStampProperty _Sealed_ CustomAttributeClass

**适用于：** EntityClass

#### 属性

| 名称 | 描述 | 标签 | 类别 | 只读 | 优先级 |
| --- | --- | --- | --- | --- | --- |
| PropertyName |  |  |  | false | 0 |

### DateTimeInfo _Sealed_ CustomAttributeClass

DateTime 类型 ECProperty 的可选附加元数据。

**适用于：** PrimitiveProperty, ArrayProperty

#### 属性

| 名称 | 描述 | 标签 | 类别 | 只读 | 优先级 |
| --- | --- | --- | --- | --- | --- |
| DateTimeKind | 可以是 Utc、Local 或 Unspecified。默认值：Unspecified。指定 DateTimeKind 时，通常不需要指定 DateTimeComponent，因为 DateTimeKind 隐含了 DateTimeComponent 'DateTime'。 |  |  | false | 0 |
| DateTimeComponent | 可以是 DateTime 或 Date。默认值：DateTime。指定 'Date' 通常意味着 DateTimeKind 无关紧要，因为日期（没有时间）不需要任何时区信息。 |  |  | false | 0 |

### Deprecated _Sealed_ CustomAttributeClass

将 Schema 或 Schema 中的项标识为已弃用。已弃用的内容不应再使用。

**适用于：** Any

#### 属性

| 名称 | 描述 | 标签 | 类别 | 只读 | 优先级 |
| --- | --- | --- | --- | --- | --- |
| Description | 提供关于如何避免使用已弃用项的建议或与该项弃用相关的其他有用信息。 |  |  | false | 0 |

### DynamicSchema (Dynamic Schema) _Sealed_ CustomAttributeClass

将 Schema 标识为由应用程序动态生成的。相似版本的 Schema 可能不同，且无法保证合并时不会发生冲突。

**适用于：** Schema

### Extension _Sealed_ CustomAttributeClass

用于指示应用了此自定义属性的属性是扩展属性。

**适用于：** AnyProperty

#### 属性

| 名称 | 描述 | 标签 | 类别 | 只读 | 优先级 |
| --- | --- | --- | --- | --- | --- |
| Origin | 扩展来源。 |  |  | false | 0 |

### HiddenClass _Sealed_ CustomAttributeClass

标识设计为在用户界面中隐藏的类。隐藏其应用的类及所有派生类

**适用于：** AnyClass

#### 属性

| 名称 | 描述 | 标签 | 类别 | 只读 | 优先级 |
| --- | --- | --- | --- | --- | --- |
| Show | 如果设置为 true，则显示隐藏的类。默认为 False。允许派生类在其基类被隐藏的情况下仍然显示 |  |  | false | 0 |

### HiddenProperty _Sealed_ CustomAttributeClass

标识设计为在用户界面中隐藏的属性

**适用于：** AnyProperty

#### 属性

| 名称 | 描述 | 标签 | 类别 | 只读 | 优先级 |
| --- | --- | --- | --- | --- | --- |
| Show | 如果设置为 true，则显示隐藏的属性。默认为 False。允许属性重写在派生类中显示隐藏的属性 |  |  | false | 0 |

### HiddenSchema _Sealed_ CustomAttributeClass

标识设计为在用户界面中隐藏的 Schema。默认情况下，Schema 中的所有类也会被隐藏。

**适用于：** Schema

#### 属性

| 名称 | 描述 | 标签 | 类别 | 只读 | 优先级 |
| --- | --- | --- | --- | --- | --- |
| ShowClasses | 如果为 true，Schema 中的类将被显示。默认为 False。如果设置为 true，可以使用 HiddenClass 自定义属性隐藏个别类 |  |  | false | 0 |

### IsMixin (Is Mixin) _Sealed_ CustomAttributeClass

应用于作为普通 ECEntityClass 的次要基类的抽象 ECEntityClass。

**适用于：** EntityClass

#### 属性

| 名称 | 描述 | 标签 | 类别 | 只读 | 优先级 |
| --- | --- | --- | --- | --- | --- |
| AppliesToEntityClass | 此 Mixin 只能应用于从该类派生的实体类。类名应完全指定为 'alias:ClassName' |  |  | false | 0 |

### Localizable (Localizable) _Sealed_ CustomAttributeClass

应用于属性以指示使用该属性的自定义属性可以被本地化。

**适用于：** PrimitiveProperty

### NotSubclassableInReferencingSchemas _Sealed_ CustomAttributeClass

使类在包含该类的 Schema 之外变为"密封的"

**适用于：** AnyClass

#### 属性

| 名称 | 描述 | 标签 | 类别 | 只读 | 优先级 |
| --- | --- | --- | --- | --- | --- |
| Exceptions | 可选地允许其他 Schema 中的特定类继承此类。使用格式 '[SchemaName]:[ClassName]'，例如 'Fruit:Banana' |  |  | false | 0 |

### PartialSchema (Partial Schema) _Sealed_ CustomAttributeClass

标识可能只包含完整 Schema 部分内容的 Schema 文件/对象。相似版本的 Schema 可能不同，但保证合并时不会发生冲突。

**适用于：** Schema

### ProductionStatus _Sealed_ CustomAttributeClass

声明此 Schema 在生产和其他工作流中的适用性。

**适用于：** Schema

当 Schema 被标记为 `ProductionStatus` 时，iModel 技术栈（或其他情况下的其他技术栈）可以主动阻止 Schema 在不支持的工作流中使用。此 `CustomAttribute` 最明显的两个用途是：

- 防止开发中（`NotForProduction`）的 Schema 发布给客户。
- 防止 `FieldTesting` Schema 用于客户的生产工作流。

所有 Schema 都应使用 `ProductionStatus` `CustomAttribute` 进行标记以启用此错误检查。

#### 属性

| 名称 | 描述 | 标签 | 类别 | 只读 | 优先级 |
| --- | --- | --- | --- | --- | --- |
| SupportedUse | 指示此 Schema 在生产或其他用途中的适用性。 |  |  | false | 0 |
| Checksum | 在 Schema ProductionStatus 设置时设置。用于验证已验证的 Schema 在该点之后未被修改。 |  |  | false | 0 |

### SupplementalProvenance _Sealed_ CustomAttributeClass

**适用于：** Schema

#### 属性

| 名称 | 描述 | 标签 | 类别 | 只读 | 优先级 |
| --- | --- | --- | --- | --- | --- |
| SupplementalSchemaNamesAndPurposes |  |  |  | false | 0 |

将 Schema 标识为补充 Schema，并存储补充 Schema 所需的额外元数据

**适用于：** Schema

#### 属性

| 名称 | 描述 | 标签 | 类别 | 只读 | 优先级 |
| --- | --- | --- | --- | --- | --- |
| PrimarySchemaReference | 引用此补充 Schema 应应用到的主 Schema | Primary Schema Reference |  | false | 0 |
| Precedence | 定义此补充 Schema 优先级的正整数。较高优先级覆盖较低优先级。主 Schema 被认为具有介于 199 和 200 之间的优先级。 |  |  | false | 0 |
| Purpose | 表示此补充 Schema 功能的字符串。补充 Schema 的标准命名格式为 _Supplemental_ |  |  | false | 0 |

## Enumerations

### DateTimeComponent Enumeration

**基础类型：** string

**严格：** true

| 标签 | 值 | 描述 |
| --- | --- | --- |
|  | DateTime |  |
|  | Date |  |
|  | TimeOfDay |  |

### DateTimeKind Enumeration

**基础类型：** string

**严格：** true

| 标签 | 值 | 描述 |
| --- | --- | --- |
|  | Unspecified |  |
|  | Utc |  |
|  | Local |  |

### ProductionStatusValue Enumeration

**基础类型：** string

与 ProductionStatus 一起使用，声明 Schema 作者对该 Schema 的预期和支持的工作流。

**严格：** true

| 标签 | 值 | 描述 |
| --- | --- | --- |
|  | NotForProduction | 此 Schema 正在开发中，不应用于生产工作流。使用此 Schema 创建的数据不受支持，可能无法升级。 |
|  | FieldTesting | 此 Schema 适用于生产工作流的现场测试。使用此 Schema 创建的数据不受长期支持，可能无法升级。 |
|  | Production | 此 Schema 适用于生产工作流。使用此 Schema 创建的数据将获得长期支持（可能通过转换）。 |
|  | Deprecated | 此 Schema 不再推荐用于生产工作流。存在更好的替代方案，应该使用它们。 |

---

*原文链接：https://www.itwinjs.org/bis/domains/corecustomattributes.ecschema/*

*最后更新：2024年5月15日*
