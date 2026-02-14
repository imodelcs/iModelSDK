# Schema Design Recommendations and Guidelines（Schema 设计建议和指南）

## 通用建议

- 每个 schema 专注于一个建模视角。即，将专注于 _Physical_ 建模的概念与实现 _Analytical_ 或 _Functional_ 建模的概念分开，各自放入自己的 schema。如果目标 schemas 旨在共享，则这种分离变得强制性的。在这种情况下，生成的 schemas 的目标 schema-layer 将不同（例如 _Discipline-Physical_ 与 _Discipline-Other_）。_Physical_ schema 包含 `SpatialLocationElement` subclasses 和用于物理建模的定义和其他信息类是可以的。
- 某些领域中的一些创作工作流很复杂，需要基于辅助配方类概念的特殊算法。这些复杂算法的输出通常是被建模的现实世界实体。在这种情况下，将这些概念分成不同的 schemas 很重要。即，创作工作流的辅助概念通常被认为是特定于应用程序的，应该在 Application-layer schema 中定义。与被建模的现实世界实体相关的概念应该在单独的 schema 中定义。如果合适，后者通常是在适用的 discipline 的较低 schema-layer（例如 Discipline-Physical 或 Discipline-Other）定义的候选者。
- 一般来说，mixins 不应该在其中定义任何属性。它们会导致 iModels 中的复杂 UNION 查询，从而导致从中检索数据的速度变慢。
- 仅利用 dynamic schemas（在运行时生成）来捕获真正每个 iModel 变化的概念。如果给定的 connector 有一些 connector 特定的固定概念，请在 Application-layer schema 中捕获它们，并让任何 dynamic classes 继承那些 Application-layer classes。这使得下游消费者更容易理解什么是固定的，什么是动态的。

## Element Classification 建议

有关 element-semantics 分类的通用建议，请参阅 Classifying Elements。

## Lower-layer schemas

Core、Common 或 Discipline 层的 Schemas 旨在由多个用例共享。Schema 的层越低，预期使用范围越广。考虑到这一点，以下建议对于共享 schemas 特别有用：

- 研究涵盖感兴趣领域的其他 schema 生态系统和格式以获取灵感。
- 创建领域中主要术语及其定义的列表。它们通常导致主要数据分类方案，这转化为要引入的主要 element-classes。
- 通常，定义为 bis:GeometricElement3d sub-classes 的每个主要数据分类概念可以进一步分类。因此，考虑为 bis:GeometricElement3d class-branch 下定义的每个具体 element-class 引入一个 type-definition class。
- 请记住，lower-layer schemas 可以作为 iModel Connectors 和创作应用程序的目标。前者在将元素组织到从外部源同步的模型中时通常需要更多的灵活性。这是由于 iModel Connectors 必须处理的外部数据中构建的不同程度的语义丰富性。因此，在为领域中的适用 iModel Connectors 引入严格的元素组织规定之前，研究外部格式中对 iModel Connectors 可用的语义。另一方面，基于 BIS 的创作应用程序通常设计为对其领域数据具有高度的语义理解，这使它们更能适应严格的数据结构。

## iModel Connector schemas

- 尽可能使用 Discipline-Physical 或 Discipline-Other 层的 schema 中的现有 element-class 或 type-definition class 作为 iModel Connector 完成的映射目标。
- 适当时使用 Type-Definitions，以避免 schema 中不必要的大量类。
- 将源格式的属性分类为：

  1. __Standard - intrinsic__（标准 - 内在）：属于其拥有概念的主要或次要分类。这些是在 _Element_ 或 _TypeDefinition_ class 上作为 first-class properties 的候选者。
  2. __Standard - not intrinsic__（标准 - 非内在）：不属于其拥有概念的分类。这些是在 _Aspect_ class 中捕获的候选者。
  3. __User-defined__（用户定义）：这些应该在 dynamic schema（在运行时生成）中由 _Aspect_ class 捕获。

  另一种思考方式是问给定的一组属性是否会出现在许多不同的类上。如果对于所有需要这些属性且只有需要这些属性的类，存在一个单一的天然"base class"，那么将这些属性添加到该 _Element Class 或_ 其相关的 _TypeDefinition_ class 是有意义的。否则，使用 _Aspect_ class 可能更好。
- 关于 iModel Connector 理解其语义但在 BIS 的 Discipline-Physical 或 Discipline-Other 层的 schema 中尚没有相应类的概念，建议 Connector 直接继承 `BisCore` schema 的适当 base-class。通常，它们是 `PhysicalElement` 和 `SpatialLocationElement` base-classes。BIS schemas 正在不断演进，因此当缺失的概念添加到 shared-layer schema 时，为先前缺失概念引入单独类的 iModel Connector 只需要将新概念注入为其现有类的 base class。以下两个类图显示了这种情况：

  | 在 shared BIS schema 中引入"concept1"之前 | 在 shared BIS schema 中引入"concept1"之后 |
  | --- | --- |
  | Image 1: Before schema evolution | Image 2: After schema evolution |

  避免在 iModel Connector schema 中为此类类引入中间 base-class。如果 iModel Connector 稍后能够理解概念的语义，它们将妨碍重新定位 Discipline-Physical 或 Discipline-Other 层的 schema 中更合适的 base-class。以下两个类图描述了这种情况：

  | 在 shared BIS schema 中引入"concept1"之前。iModel Connector 为 BIS 中没有目标的已知概念引入了通用 base-class。 | 在 shared BIS schema 中引入"concept1"之后。iModel Connector base-class 在尝试对齐相应的具体类时成为障碍。 |
  | --- | --- |
  | Image 3: Before schema evolution | Image 4: After schema evolution |
- 关于 iModel Connector 不理解其语义的概念，可以通过以下方式处理：

  1. 辨别或做出良好的猜测，关于概念在 _BisCore_ base-classes 方面的通用分类。即，在 `PhysicalElement`、`SpatialLocationElement` 或 `DrawingGraphic` 之间选择。
  2. 要么：

     a) 如果需要在此类概念上引入 Standard-intrinsic 属性，则直接继承 _BisCore_ schema 的选定 base-class，或者，

     b) 从 `Generic` schema 定位适当的类 - 例如 `PhysicalObject` 或 `SpatialLocation`。

  如果稍后，外部格式和 iModel Connector 演进以理解适用于已映射到单个通用类的元素子集的概念，iModel Connector 将必须在 iModel 中以更合适的类重新创建这些元素。此过程可能对其输出的现有消费者造成干扰。请记住以下建议以最小化或减轻其影响：

  1. 尝试重用正在重新创建的元素的 _ElementId_。
  2. 将任何唯一和全局标识符从被删除的元素保留到新元素。此类别中最重要的属性是 `Code` 和 `FederationGuid`。

最后更新：2025年6月11日
