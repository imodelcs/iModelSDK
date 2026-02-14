# Codes

Code 是 Element 表示的实体的人类可读文本标识符。

Code 向理解字符串结构并因此能够解码它的人员和程序传达信息。

不同的领域和组织有不同的方法将业务信息编码到 Code 中，他们可以将其表示为 Code Specifications。

在 BIS 中，Code 使用 bis:Element 的三个属性进行建模：CodeValue、CodeSpec 和 CodeScope。

## CodeValue 属性

每个 Element 都有一个（可空的）`CodeValue` 字符串属性，用于保存其 Code。

当存在时，`CodeValue` 应该是人类可理解的字符串。

### Code 的示例用途

- 资产跟踪号
- 标签号
- 序列号
- VIN 号码
- 社会安全号
- 文档跟踪号
- 合同号
- 项目号
- RFID
- 门牌号
- 房间号
- 等等。

当被识别的实体本质上是物理的时，它通常会将其 code 物理地附着在上面（如汽车上的 VIN 号码或仪器上的制造商序列号）。

当被识别的实体是物理实体承担的角色时，它可能将其 code 半永久地附着在相关的物理实体上。例如，物理阀门将有其序列号永久附着在上面。阀门在流程中执行的"功能"的"标签号"被印在通过金属丝附着在阀门上的"标签"上。如果阀门被更换为新的（具有新的序列号），则持有功能的"标签号"的标签将移动到新阀门上。

当被识别的实体本质上是纯信息时，它通常会以名称或类似概念的形式分配 code，由领域、组织或软件系统分配。示例包括组织分配给文档的"名称"、从制造商目录中识别特定类型阀门的"型号"或组织中使用的特定线条样式的"名称"。

### Code 的示例误用

- Guid 不是人类可理解的，也不编码业务含义，因此不应用作 `CodeValue`——FederationGuid 用于此目的。
- 由于与上述相同的原因，Hash 不应用作 `CodeValue`。
- 数百个字符长的 `CodeValue` 对人类来说也很难理解，因此应避免使用。事实上，code 管理服务可能会对 `CodeValue` 的长度强制执行硬性限制。例如，iModelHub 目前有 350 个字符的硬性限制。

## CodeSpec

`CodeSpec`（也称为 Code Specification）命名并指定 Code 的新分类。

`CodeSpec` 还捕获将重要业务信息编码到 Code 中和从 Code 中解码的规则。

例如，软件工件（如 ViewDefinitions）的 Code 和设备（如管道组件）的 Code 具有不同的编码规则和唯一性约束，因此每个都有一个单独的 `CodeSpec`。

例如，专注于工业流程工厂的实现可能要求管道组件的 Code 遵循如下规范：[工厂区域代码]-[设备类型代码]-[设备编号]（例如 OIL-AAV-001，它编码了在特定工业工厂的称为"OIL"的区域中特定类型"AAV"的阀门）。

在许多情况下，`CodeSpec` 与 Element 类层次结构的一个分支有很强的相关性，并且通常以定义该分支起点的抽象基类命名。从该基类下降的所有子类（直接或间接）共享相同的 `CodeSpec` 是常见的。

例如，名为"bis:ViewDefinition"的标准 `CodeSpec` 有助于确保 `BisCore:ViewDefinition` Element 类的所有子类的名称唯一。

应用程序中的其他配置可以定义 Element 类与 CodeSpec 之间的关联，允许共享服务（例如"Identification Code Service"）生成和验证 Code。

CodeSpec 还可以规定 Element 类实例的 Code 应为 null。当建模的现实世界实体没有有意义的现实世界标识符（例如踢脚板、一堆土、普通螺栓）时，这是适当的。

> 注意：为确保 `CodeSpec` 名称唯一，应使用命名空间（通常是 schema 的别名），如标准"bis:ViewDefinition" `CodeSpec` 所示。

## CodeSpec 属性

每个 Element 都有一个 `CodeSpec` 导航属性，将其与控制其 Code 的 `CodeSpec` 相关联。单个 BIS Repository（例如 iModel）预期使用许多 Code Specifications——不同类的 Elements 可以有不同的编码约定。

## CodeScope 属性

每个 Element 都有一个 `CodeScope` 导航属性，指向为 Code 提供唯一性范围的另一个 Element。"作用域" Element 可以表示整个 repository、model、assembly 等。

`CodeSpec` 指定可以用作 `CodeScope` 的元素类型。最常见的类型是：

- `Repository` - CodeValues 在整个 repository 中是唯一的。
- `Model` - CodeValues 在 Model 中是唯一的。
- `ParentElement` - CodeValues 在具有相同父级的子级中是唯一的。
- `RelatedElement` - CodeValues 在与相同元素相关的集合中是唯一的。

例如，楼层 Code（如"1"或"2"）必须在建筑物内唯一，但在建筑物之间不唯一。

在此示例中，Building 实例为 Floor 提供 CodeScope。

> 注意："作用域" Element 还可以表示范围大于当前 BIS Repository 的某个实体。在这种情况下，该范围内的唯一性只能由外部"Identification Code Service"强制执行。

## BIS Repository 中的唯一性

对于给定的 Element，其 `CodeSpec`、`CodeScope` 和 `CodeValue` 属性的组合必须在 BIS repository 中唯一。所有 `null` 值被认为是唯一的。

## CodeSpec 创建指南

下表总结了 schema 设计者、Connector 或 Application 开发者以及最终用户和管理员创建 CodeSpec 的典型目的。还展示了每种情况的典型 CodeScope 和 CodeScope-Elements 引用策略。

| 创建者 | CodeSpec 目的 | 典型 CodeScopes | CodeScope-Element 引用 |
| --- | --- | --- | --- |
| 共享领域和创作应用程序 | 类的 Code 分类，通常是 `DefinitionElement`，建模被视为 repository 特定工件的概念，以便：- 确保唯一性（在 Subject 特定和全局范围）或... - 提供一种知名的方式来查找某些实例（在全局范围）。 | 按模型或按父级。 | 通过 ElementId |
| Connectors | 复制源格式中现有的 code/tag/name 唯一性规则（如果有）。 | - 按模型或按父级。- 如果适用，根据源格式按相关元素。- 按 repository 通常无效。 | 通过 ElementId |
| 用户/管理员 | 通过应用程序配置为特定类设置的 Code 分类。Code 唯一性通常预期跨 repository。 | 每种情况适用的任何 CodeScope。 | 通过 FederationGuid |

---

| 下一篇：FederationGuids
|:---
