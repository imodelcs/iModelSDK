# 信息层次结构

BIS 仓库中的信息按照由规则控制的层次结构进行排列。有些规则由 schema 明确定义，其他规则则要求创建数据的应用程序遵循标准。

BIS 仓库中的层次结构旨在促进人类和软件对数据的理解。

## 层次结构构造

BIS 中有几种机制可供领域作者利用，以将元素组织成层次结构：

- Subject 层次结构组织 Models。
- 一个 Model 可以包含 Elements。
- 一个 Element 可以被一个 Model 进行子建模（sub-modeled）。
- 一个 Element 可以拥有子 Elements。
- 一个 Element 可以被 _Spatial Organizer_ 按照特定学科空间地组织成层次结构。
- 一个 _Physical System_ 可以将成员 Elements 分组为按子系统组织的层次结构的一部分，根据特定学科。
- 一个 Element 的来源可以追溯到 _External Source_，其组织可能是层次结构的。

每种机制都旨在在特定情况下使用，这将在本章中解释。

### Subject 层次结构组织 Models

RepositoryModel 包含按父子层次结构组织的 `Subject` Elements。所有 Models（RepositoryModel 本身除外）都组织在这些 `Subject` 之下（通过 InformationPartition）。

### Model 包含 Elements

Model 是 Elements 的_容器_。Models 是细分和组织整个仓库的一种方式。每个 Element 都被恰好包含在 1 个 Model 中，由 `ModelContainsElements` 关系定义。

### Model 对 Element 建模

Model 是关于信息层次结构中更高级别 Element 的更多细节。一个 Model 恰好关于 1 个 Element，由 `ModelModelsElement` 关系定义。从 Model 的角度来看，这个更高级别的 Element 被称为 _modeled element_。从 Element 的角度来看，更低级别的 Model 被称为 _SubModel_。_SubModel_ 术语只是指代信息层次结构中相对位置的一种方式。_SubModel_ 没有特殊的类，只有标准的 `Model` 子类。

例如，`DrawingModel` 对 `Drawing` Element 进行子建模，并包含作为整体绘图细节的 `DrawingGraphic` Elements。下面的实例图描述了这种情况。有关所用约定的详细信息，请参阅实例图约定。

![DrawingModel 分解](https://www.itwinjs.org/media/drawing-breakdown.png)

### Element 拥有子 Elements

一个 Element 可以拥有子 Elements。这对于建模_装配_关系或建模一个 Element 独占控制其他 Elements 生命周期的情况很有用。一个 Element 可以有 0 或 1 个父 Elements，由 `ElementOwnsChildElements` 关系定义。没有父级的 Element 被视为_顶级_ Element。有父级的 Element 被视为_子_ Element。这些层次结构可以有 N 层深度，这意味着一个 Element 可以同时是父级和子级。父 Element 及其所有子级必须包含在同一个 model 中。

### Element 由 Spatial Organizer 组织

Spatial Organizer，通常是 `spcomp:SpatialStructureElement` 或 `spcomp:Zone` 的子类，可以_组织_（即_持有_或_引用_）Spatial Elements 并聚合其他 Spatial Structure elements。

这些概念是 SpatialComposition schema 引入的规则和模式的一部分。它们旨在支持基础设施空间结构的建模。

生成的层次结构可以根据需要定义多个级别。这些 Spatial Composition 层次结构可以与上面列出的其他组织机制共存。

例如，`Building` 被建模为 `spcomp:SpatialStructureElement` 的子类，它在空间上聚合其他 Spatial Organizers，如 `Stories` 和 `Spaces`。物理元素如 `Wall`s、`Column`s 和 `Door`s 与 Building 分解中的这些概念相关联（根据情况被持有或引用）。下面的实例图描述了这种情况。有关所用约定的详细信息，请参阅实例图约定。

![Building 分解](https://www.itwinjs.org/media/building-decomposition.png)

有关 BIS 中 Spatial Composition 的更多详细信息，请参阅本章后面的 Spatial Composition 主题。

### Physical System 分组成员

Physical System 可以将成员-Elements 分组，这些成员共同提供特定功能。Physical Systems 可以使用 `bis:PhysicalSystemAggregatesSubSystems` 关系以层次结构方式组织。Physical System 层次结构可以与上面列出的其他组织机制共存。

![Physical Systems](https://www.itwinjs.org/media/physical-systems.png)

有关 BIS 中 Physical Systems 的更多详细信息，请参阅本章后面的 Modeling Systems 主题。

### Element 来自 Source

Element 的来源，由附加在其上的 `bis:ExternalSourceAspect` 捕获，可以引用它来自的 External Source。External Sources 可以以层次结构方式组织，反映它们在外部仓库中的布局方式。这些 External Source 层次结构可以与上面列出的其他组织机制共存。

例如，iModel Connector 从包含 4 个 dgn 文件的 Road 数据集同步数据。这些 dgn 文件之间的 model-attachments 在 iModel 中由 `ExternalSource` 实例组成的层次结构表示，这些实例充当从外部 dgn 文件同步的 iModel 中 elements 的_sources_。下面的实例图描述了这种情况。有关所用约定的详细信息，请参阅实例图约定。

![External Sources 示例](https://www.itwinjs.org/media/external-sources.png)

有关 BIS 中 External Sources 的更多详细信息，请参阅 BIS 中的 Provenance。

## Top of the World（世界之巅）

信息层次结构的顶部受到严格控制，在所有 BIS 仓库中都非常相似。其内容在 Top of the World 中解释。

## 典型的仓库组织

下面描述了仓库组织的两个示例。应该注意的是，单个 BIS 仓库可能有多种用途。当发生这种情况时，每个用途（通常对应于一个应用程序）在 BIS 仓库内的相应 Editing Channel 上添加其层次结构。单个 BIS 仓库的结果总层次结构就是各用途层次结构的并集。

## 示例信息层次结构

下面的实例图描述了一个假设校园的信息层次结构。假设数据由单个应用程序写入，因此被组织到一个 `Editing Channel` 中。它显示了两个主要建模视角的数据组织：Physical 和 Functional，以及 Definition models 中的目录数据和 Document 视角下的关联 Drawings。有关所用约定的详细信息，请参阅实例图约定。

![信息层次结构](https://www.itwinjs.org/media/information-hierarchy.png)

### iModel Connector 仓库组织

iModel Connectors 将外部格式的数据转换为 iModel。作为该工作的一部分，它们需要以人类和软件都能理解的方式组织结果数据。

下面的实例图描述了一个 iModel 中信息的组织，该 iModel 由三个 iModel Connectors（IFC、OpenBuilding Designer 和 Bentley Civil）作为目标，它们从三个不同的数据集同步数据，两个基于 .dgn，一个 .ifc。后两个显示得更详细，包括它们并行的 `Model`、`ExternalSource` 和 `SpatialComposition` 层次结构。因此，BIS 仓库的结果层次结构被组织成三个 `Editing Channels`。

![iModel Connector 仓库组织](https://www.itwinjs.org/media/imodel-connector-repository-organization.png)

由于 iModel Connectors 在没有用户输入的情况下无头运行，它们需要根据对数据的理解来组织写入 iModels 的数据。在上面的示例中，每个 iModel Connector 同步的数据存储在 Subject 层次结构的特定分支下。每个 iModel Connector 根据源数据的结构和可发现语义来布局下一级别。在 dgn 文件的情况下，OpenBuilding Designer 和 Bentley Civil iModel Connectors 都为外部数据集上每个引用的 dgn 和 model 创建子 Subjects，镜像了驱动这些外部产品中数据组织的团队和学科的分工。

有关更多详细信息，请参阅 iModel Connectors。

---

| 下一篇：Modeling Perspectives
|:---
