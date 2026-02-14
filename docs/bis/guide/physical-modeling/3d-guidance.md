# 3D 建模指导

> 原文链接：https://www.itwinjs.org/bis/guide/physical-perspective/3d-guidance/

3D 建模是 BIS 和 iModels 的核心。存在一个 3D 相关建模视角的层次结构。

![3D Perspectives](https://www.itwinjs.org/media/3d-modeling-perspective-hierarchy.png)

对于每个视角，都有相应的 Model 和 Element 类，它们具有类似的继承层次结构。对于部分（但不是全部）视角，有相应的 InformationPartitionElement 子类。

"Spatial" 本质上是"使用现实世界坐标"的同义词。所有从 Geometric3d 继承的视角都使用笛卡尔坐标系，可以在地球上的某处进行空间定位。SpatialModel 的特化总是在现实世界坐标中。GeometricModel3d 的其他特化可以通过设置 IsNotSpatiallyLocated=true 来选择不使用现实世界坐标（和空间索引）。

"Spatial" 视角用于在"真实"空间中建模"真实"的东西，例如物理 Entity 和它们定义或定义它们的空间位置。非 Spatial 视角用于数学抽象或"纯图形"，可能与物理 Object 关系密切，也可能不是。

"Physical" 视角用于建模物理 Entity（具有质量）和空间位置 Entity。什么是"空间位置 Entity"？它是无质量的，但在现实物理世界中表现出来：

- 它们可能与物理 Entity 相关定义，例如两个导体之间的气隙、检修面板周围的空间、物理 Entity 占据的体积，或表示物理 Entity 表面上区域的区域。
- 它们可用于指导物理 Entity 的定位，例如可以通过粉笔线或激光束在施工现场物理呈现的网格线。
- 它们可能是物理后果的抽象，如财产边界或政治边界，通常通过标记、标志或自然边界在物理世界中划定。

我们将"SpatialLocation" 视角定义为"Physical" 视角的严格子集，这样我们就可以拥有不包含任何 PhysicalElement 的 SpatialLocationModel。但是，PhysicalModel 可以包含 SpatialLocationElement。PhysicalModel 和 SpatialLocationModel 还可以包含 GraphicalElement3d Element（用于信息和注释插图）以及非几何 InformationContentElement。

"Analytical" 视角用于建模抽象数学/几何 Entity，这些 Entity 是为特定类型分析而设计的现实世界简化，例如复杂结构钢梁和柱的杆件模型。由于每种分析都代表一个独特的视角，Analytical Partition、Model 和 Element 类都是抽象的，我们期望它们都有针对特定分析的具体子类。

## 3D Elements

![3D Elements](https://www.itwinjs.org/media/3d-elements.png)

Element 类层次结构反映了视角层次结构。关系约束可以在希望源或目标 Element 表示"真实"物理 Entity 或空间位置 Entity 时使用"SpatialElement"。

## 3D Models

![3D Models](https://www.itwinjs.org/media/3d-models.png)

Model 类层次结构也在很大程度上反映了视角层次结构，但它受到遗留的、已弃用类的复杂影响，这些类在上图中用红色删除线表示。

不应该有 bis:PhysicalModel 的特化，尽管在确定 bis:PhysicalModel 应该是"sealed"之前，已经发布了一些 bis:PhysicalModel 的特化。我们使用验证规则来防止额外的特化。

bis:PhysicalElement 的任何特化的实例在技术上可以驻留在任何 bis:PhysicalModel 中，尽管应用程序强制执行的约定可能更具限制性。

当对 bis:SpatialLocationElement 的特化（如"Grid"或"RealityLocationSet"）进行子建模时，使用 bis:SpatialLocationModel。

还有一些与"现实建模"相关的 SpatialModel 的其他现有特化，它们不遵循我们希望推广或继续的模式：PointCloudModel、RasterModel、ScalableMeshModel、ThreeMxModel 和 WebMercatorModel。这些子建模 RepositoryLink Elements，指向"现实数据"的外部存储库。最初预期它们将包含从外部源缓存的 SpatialLocationElement，但实际上这并没有发生。它们有 JsonProperties，保存关于外部存储库中数据的元数据。

## 3D Partitions

bis:Subject 的 bis:PhysicalPartition 包含其"物理骨干"。每个 bis:Subject 不应有超过一个。

类 bis:SpatialLocationPartition 的存在是为了涵盖特殊情况，如道路或铁路 Alignment、Grid 或来自地理信息系统的数据，其元素主要建模为 `SpatialLocation`。但是，由于"SpatialLocation" 视角是"Physical" 视角的子集，通常 SpatialLocationElement 可以是"物理骨干"的一部分。

我们预期 bis:AnalyticalPartition 的具体特化将是针对特定分析的。

通常，给定视角的 Partition 和 Model 应该具有相同的修饰符，例如它们都应该要么是抽象的、具体的或密封的。如果它们是抽象的，它们对应的 Element 类应该是抽象的。Partition/Model 是具体或密封的而对应的 Element 是抽象的也很常见，Physical 和 SpatialLocation 就是这种情况。

InformationPartitionElement 下的类层次结构在很大程度上是"扁平化"的。3D 相关的 Partition 在下面高亮显示。如所示，iModel 作者应避免使用 SpatialLocationPartition。

![3D Partitions](https://www.itwinjs.org/media/3d-partitions.png)

## 新 3D 几何视角特化的指导

如果您的新 Element 正在建模具有质量的 Entity 的物理几何（包括物理材料），它应该是 `PhysicalElement` 的直接或间接特化。您不会创建 `PhysicalPartition` 或 `PhysicalModel` 的特化。

如果您的新 Element 正在建模现实世界中的空间位置，则特化 `SpatialLocationElement`。您的元素将被放置在 `PhysicalModel` 或子建模某个其他 `SpatialLocationElement` 的 `SpatialLocationModel` 中。

如果您的新 Element 正在建模现实世界坐标中某物的 3D 几何抽象，您应该分别特化 `AnalyticalElement`、`AnalyticalModel` 和 `AnalyticalPartition`。

如果您的新 Element 不属于上述任何类别，请咨询 Bentley 的 BIS 专家，以确定是否需要 Geometric3d Partition/Model/Element 的新特化。

在所有情况下，新的相应 Model 和 Partition 类应该具有相同的类限定符。通常，两者都应该是具体的或密封的。

---

| 下一步：Physical Models and Elements
|:---|
