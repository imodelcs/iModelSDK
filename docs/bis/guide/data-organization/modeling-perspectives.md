# 建模视角

正如在 Modeling with BIS 中所讨论的，现实世界中的对象可以从不同的_建模视角_来思考。建模视角是为了特定目的对现实世界进行概念化的一种方式。例如，一个污水系统可以从多个建模视角来思考：

- 作为具有形态、材料和质量的物理 3D 实体（_物理_视角）
- 作为水文输送系统（_分析_视角）
- 作为一组共同提供足够废水处理能力的组件（_功能_视角）
- 作为图纸和表格中一组 2D 图形（_文档_视角）

## 保持建模视角的分离

每个建模视角都以不同的方式简化现实世界中的对象；这需要为每个视角提供不同的专用数据结构。这在 BIS 类中表现为以下部分所解释的内容。

每个视角的数据（`InformationPartitionElement`s、`Model`s、`Element`s 等）与其他视角的数据分离，以便每个视角能够被优化组织。不同视角的 `Element`s 之间的关系用于表明它们都在建模相同的对象，只是从不同的视角。

### 建模视角与 BIS 类层次结构

建模视角在 BIS 类层次结构中直接表示为：

- `InformationPartitionElement` 子类
- `Model` 子类
- `Element` 子类

对于每个建模视角，都有一个对应的 `InformationPartitionElement` 子类和一个 `Model` 子类。

建模视角也体现在 `Element` 子类中。有一个直接对应于建模视角的 `Element` 子类。放置在 `Model` 中的 `Element`s 需要与 `Model` 具有兼容的建模视角。

Top of the World 讨论 `InformationPartitionElement`s，Model Fundamentals 讨论 `Model`s。

注意，唯一不对应任何特定建模视角的 `Model` 子类是 `RepositoryModel`。

### Partitions、Models 和 Elements 的建模视角一致性

正如 Top of the World 中所描述的，对于每个 Subject，可能有零个或多个 `InformationPartitionElement` 子 `Element`s。每个 `InformationPartitionElement` 实际上是一个建模视角的声明，并启动一个具有该声明建模视角的 `Model` 层次结构。

每个 `InformationPartitionElement` 都有一个具有相同建模视角的子 `Model`。该子 `Model` 只包含具有相同建模视角的 `Element`s。其中一些 `Element`s 可能有自己的子 `Model`s，这些子 `Model`s 必须与它们子建模的 `Element` 具有相同的建模视角。

这些建模视角规则强制执行最低级别的逻辑数据一致性。例如，它们防止将物理消火栓 `Element` 放入剖面图 `Model` 中。

### 抽象、具体和密封的建模视角

建模视角可以被认为是抽象的、具体的或密封的，以对应实现它们的 `InformationPartitionElement` 和 `Model` 子类：

- _抽象_建模视角仅用于逻辑分组更专业的视角，由抽象的 `InformationPartitionElement` 和 `Model` 子类实现。
- _具体_建模视角直接用于对现实建模，由具体的 `InformationPartitionElement` 和 `Model` 子类实现。
- _密封_建模视角是不允许进一步专业化的具体建模视角。密封建模视角由密封的 `InformationPartitionElement` 和 `Model` 子类实现。

## 标准建模视角

不可能预测 BIS 中最终可能需要的所有建模视角。然而，BIS 确实提供了一组核心建模视角，其他建模视角必须从中派生。

下表显示了最常见的核心建模视角，它们是抽象 `InformationPartitionElement` 类的子类，以及每种情况下实现它们的预期 `Model` 子类类型。

| 主要建模视角 | 示例用例 | `InformationPartitionElement` 子类 | `Model` 子类实现者 |
| --- | --- | --- | --- |
| Physical | 碰撞检测、工程量计算 | PhysicalPartition (sealed) | PhysicalModel |
| Functional | 电气或工厂功能模型 | FunctionalPartition (concrete but considered abstract) | appropriate subclass of FunctionalModel |
| Analytical | 结构或水力分析 | AnalyticalPartition (abstract) | appropriate subclass of AnalyticalModel |
| Shared and/or Support data | 组件目录、材料库 | DefinitionPartition (sealed) | DefinitionModel |
| Documents | 图纸和表格 | DocumentPartition (sealed) | DocumentListModel |

下表显示了通常被认为是专业化的其他核心建模视角。

| 建模视角 | 示例用例 | `InformationPartitionElement` 子类 | `Model` 子类实现者 |
| --- | --- | --- | --- |
| Graphics-only (3D) | 位于真实世界坐标中的纯图形 | GraphicalPartition3d (sealed) | appropriate subclass of GraphicalModel3d |
| Grouping Information-only | _命名组_ | GroupInformationPartition (sealed) | appropriate subclass of GroupInformationModel |
| Information records-only | 非图形数据记录 | InformationRecordPartition (sealed) | InformationRecordModel |
| Linked data | 链接到 Reality Data | LinkPartition (sealed) | LinkModel |
| Physical Systems | 冷热水、空调或电气系统 | PhysicalSystemPartition (sealed) | PhysicalSystemModel |
| Spatial Location-only | 建筑网格、道路线形或地块边界。Physical 的子集。 | SpatialLocationPartition (sealed) | SpatialLocationModel |

注意，大多数 `InformationPartitionElement` 子类是_sealed_，除了 FunctionalPartition 和 AnalyticalPartition。由于这些建模视角根据捕获的功能系统或分析类型进行专业化，因此每个具体实现始终需要对适当的 Partition 和 Model 类进行子类化。有关更多信息，请参阅下面的 Functional Modeling Perspectives 和 Analytical Modeling Perspectives。

如果发现需要新的核心建模视角（现有核心建模视角都不适合作为父视角），可以添加新的。

### Physical 建模视角

Physical 建模视角将现实视为具有形态、材料和质量的 3D 空间中的对象。Physical 建模视角值得特别讨论，因为它在 BIS 中扮演如此重要的角色。

对于给定的 `Subject` 实例，有且只有一个 Physical 建模视角。如果现实中有一根污水管，那么该污水管只能有一个物理表示。

Physical 建模视角不能被"子类化"。（由于遗留原因，BIS schemas 中有一些 `PhysicalModel` 的子类，但这些子类从未被使用。）

有关物理建模的详细信息，请参阅 Physical Models and Elements。

#### Physical Backbone（物理骨干）

BIS 中"物理骨干"的原则指出，所有学科都能认同的一件事是物理现实，因此物理视角应该是其他视角之间的"试金石"。代表物理对象非物理视角的 `Elements` 通常会与从 Physical 视角建模对象的 `PhysicalElement` 有关系。

### Functional 建模视角

Functional 建模视角将现实视为旨在执行功能的对象。这些对象通常连接起来形成功能系统。

功能建模视角的一个例子是将过程工厂的互连组件视为执行功能的系统。

有关功能建模的详细信息，请参阅 Functional Models and Elements。

### Analytical 建模视角

Analytical 建模视角将现实视为参与可分析现象的 3D 空间中的对象。

分析建模视角的一个例子是建筑物的热分析，其中建筑物的组件具有热属性，可能是热源或热汇。

任何分析都涉及一个或多个数值求解器，能够根据一组初始条件（输入）预测系统的行为（输出）。虽然某些分析可以直接在 Physical Perspective 数据上执行，但许多类型的分析需要基于自定义视角的现实的并行表示。在后一种情况下，分析的输入数据捕获在 BIS 仓库中适用 `Subject` 的相应分析模型视角中。

注意，BIS 仓库不适合存储分析的结果或输出数据。分析结果集通常是瞬态的且体积庞大，经常或批量创建，因为专业建模器尝试多组初始条件。

有关分析建模的详细信息，请参阅 Analytical Models and Elements。

### Definition Partitions

定义层次结构的顶部从一个 `DefinitionModel` 开始，它对 `DefinitionPartition` 建模。

这允许 `DefinitionElements` 根据它们与 `DefinitionPartition` 的父 `Subject` 的关系进行组织。

`DefinitionPartition` 的 `DefinitionModel` 中可以有多个 `DefinitionContainer` Elements，每个都有一个对应的 `DefinitionModel` 对其进行子建模。这样，定义（`DefinitionElement` 的实例）可以按来源、学科或其他标准分层组织。每个 `DefinitionPartition` 由其 Code 标识。

有关 _DictionaryModel_ 中 repository-global definition elements 的预期组织的详细信息，请参阅 Organizing Repository-global Definition Elements。

### Document Partitions

文档层次结构的顶部从一个 `DocumentListModel` 开始，它对 `DocumentPartition` 进行子建模。

这允许 `Document` elements 根据它们与 `DocumentPartition` 的父 `Subject` 的关系进行组织。

`Drawing` 和 `Sheet` 是 `Document` 的 2 个示例子类。

`Drawings` 和 `Sheets` 进一步被 `DrawingModels` 和 `SheetModels` 子建模，它们以图形方式分解图纸或表格的内容。

下面的实例图描述了一个关于工厂建筑的假设 iModel 的层次结构。显示了两份图纸文档，以及其中一份的 2D 图形与 iModel 的 Physical elements 之间的关联。BIS 提供 `DrawingGraphicRepresentsElement` 关系来解决 _Drawing_ 中的 elements 与不同建模视角中的 elements 之间关联的需求。有关所用约定的详细信息，请参阅实例图约定。

![Document Partitions](https://www.itwinjs.org/media/document-partition.png)

## Domains 与建模视角

一个 domain 可能需要也可能不需要自定义建模视角。需要自定义建模视角对应于需要使用与其他现有建模视角显著不同的概念来建模现实。

结构钢详图是一个___不___需要自己建模视角的 domain 示例。该 domain 需要自定义类来表示对它重要的物理项目，但所有这些项目都从 Physical 建模视角查看。结构钢详图可能还需要一些调度或成本信息；该信息不太可能需要自定义建模视角，因为成本和调度是常见需求。

另一方面，水力分析确实需要自定义建模视角。该视角将现实建模为运输和储存水的系统。现实将被简化为管道网络和其他项目，具有适合水力分析的属性和关系。

## InformationPartition 实例的 Codes

正如 Top of the World 中所解释的，由于 `InformationPartitionElement` 实例旨在让软件理解而不是人类可理解的，它们的_Codes_在业务或基础设施资产的上下文中通常没有意义。通常被认为是 Partition 的子模型"_Name_"的是其父 `Subject` 的_Code_。

话虽如此，作为 `ISubModeledElement` mix-in 的实现者，每个 `InformationPartitionElement` 应该分配一个 Code。以下指南旨在实现其 Codes 的一致性。

通常，`InformationPartitionElement` 实例的 Code 的不同部分应设置如下：

- CodeSpec: "bis:InformationPartitionElement"。
- CodeScope: 按父级（Code 值预期在每个父 `Subject` 中唯一）。
- CodeValue: 根据 `InformationPartitionElement` 的类型。

下表为每个 `InformationPartitionElement` 子类提供了默认 Code Value，用于没有更合适值的情况。

| InformationPartition 子类 | 默认 Code Value |
| --- | --- |
| AnalyticalPartition subclass | <_根据专业分析类型适当的 CodeValue_> |
| DefinitionPartition | "Definitions" |
| DocumentPartition | "Documents" |
| FunctionalPartition subclass | <_根据 Functional 专业化的适当 CodeValue_> |
| GraphicalPartition3d | "Graphics" |
| GroupInformationPartition | "Groups" |
| InformationRecordPartition | "InformationRecords" |
| LinkPartition | "Links" |
| PhysicalPartition | "Physical" |
| PhysicalSystemPartition | "PhysicalSystems" |
| SpatialLocationPartition | "SpatialLocation" |

具有比上面列出的默认值更合适的 Code Value 的示例情况包括：

- "BisCore.DictionaryModel" 用于从 Root `Subject` 进入全局 DictionaryModel 的 `DefinitionPartition`。
- "BisCore.RealityDataSources" 用于从 Root `Subject` 进入全局 LinkModel 的 `LinkPartition`。

---

| 下一篇：Top of the World
|:---
