# Modeling with BIS（使用 BIS 建模）

**原文链接**: [Modeling with BIS](https://www.itwinjs.org/bis/guide/intro/modeling-with-bis/)

---

本节描述 BIS 如何建模世界及其原因。首先，我们介绍 BIS 感知现实世界的方式。接下来，我们描述使用 BIS 建模的基本构建块，以及如何使用这些块构建紧密 Digital Twin 的核心模型——这与定义特定应用程序"孤岛"数据库的数据模型的方式有显著不同。

本节使用了一些术语但没有完全定义它们。更详细的定义请参见 BIS Glossary。

## The BIS View of the World（BIS 的世界观）

"建模"现实是以简化的、有目的的方式表示它，我们称之为建模 Perspective（视角）。考虑一个现实世界的物理 Object（对象）。我们可以对其物理形态（Physical Perspective）及其在功能系统中扮演的角色（Functional Perspective）进行建模。BIS 将 Objects 概念化为由多个 Entities（实体）组成，其中每个 Entity 具有 Object 属性的一个子集（与给定 Perspective 相关）。

![Image 1: An Object is comprised of multiple Entities](https://www.itwinjs.org/media/bis-modeling-01.png "An Object is comprised of multiple Entities")

BIS Repository 是一个由 BIS 管理结构和语义的信息存储库。它包含 Entities 的模型，如：

- 建成基础设施的物理形态
- 物理对象在各种系统中扮演的角色
- 支持建成基础设施的设计、施工和运营的无形 Objects（例如文档、需求、电子图纸等）

## Modeling Perspectives（建模视角）

BIS 在一个 BIS Repository 中支持多种建模"Perspectives"。对于物理 Objects，物理 Perspective 是主要的，但还有其他 Perspectives 用于 Object 在不同系统中扮演的角色，例如在功能流程、热力系统、安全分析、空间布局、结构系统、财务系统、物流系统等中。

BIS 还支持在一个 BIS Repository 中以多种 Granularities（粒度）对 Object 进行建模，例如既作为"原子"事物又作为更小部件的集合。

## The BIS Building Blocks and How to Use Them（BIS 构建块及其使用方法）

BIS Repository 中的基本构建块是称为 Model、Element、ElementAspect 和 Relationship 的信息记录。

### Element

Element 对现实世界的 Entity 进行建模。一组紧密相关的 Elements（每个建模组成 Object 的不同 Entity）共同建模完整的 Object。一个 Element 将是"主导"Element，基于被建模 Object 的性质。例如，如果是 Physical Object，则 PhysicalElement（建模 Physical Entity）将是"主导"Element，所有其他 Elements（建模组成 Object 的其他 Entities）将与主导 PhysicalElement 关联。对于纯空间 Object（例如政治边界），SpatialLocationElement 将是"主导"。对于"信息"Object，InformationContentElement 将是"主导"。

![Image 2: Elements model Entities](https://www.itwinjs.org/media/bis-modeling-02.png "Elements model Entities")

### Model

Model 是 Elements 的集合，全部来自 **单一** Perspective。这些 Elements 共同建模某个 Entity，该 Entity 比 Model 中包含的 Elements 所建模的 Entities "更大"。例如，考虑一个包含 PhysicalElements 的 PhysicalModel，这些 PhysicalElements 建模汽车零件的物理形态。它们共同建模汽车整体的 Physical Entity。

![Image 3: Models are collections of Elements with a common Perspective](https://www.itwinjs.org/media/bis-modeling-03.png "Models are collections of Elements with a common Perspective")

不同 Model 中的 Element（见下方的"P-0"）将汽车整体建模为"原子"事物。包含"汽车零件" Elements 的 Model"子建模"建模汽车整体的 Element。换句话说，它将 Element（一个简单、原子的表示）"分解"为更细粒度的 Model。因此，BIS repository 可以紧密地以两种不同的 Granularities 建模汽车——**既**作为"原子"事物，**又**作为细粒度的部件集合。

![Image 4: Models sub-model Elements for finer-grained modeling](https://www.itwinjs.org/media/bis-modeling-04.png "Models sub-model Elements for finer-grained modeling")

建模汽车整体的 Element 也在 Model 中。那个 Model 子建模什么 Element？BIS 通过定义一个不需要子建模其他 Element 的特殊 RepositoryModel 来避免无限回归。RepositoryModel 充当 BIS Repository 的"目录"。它包含一个"Subject" Element，以文本方式引用 BIS Repository 所关于的 Object。RepositoryModel 还包含一个或多个 InformationPartitionElements。每个声明用于建模 Subject 的建模 Perspective。每个 Partition 将被具有相同 Perspective 的 Model 子建模，例如 PhysicalModel 将子建模 PhysicalPartition。

![Image 5: The RepositoryModel acts as the Table of Contents of the BIS Repository](https://www.itwinjs.org/media/bis-modeling-05.png "The RepositoryModel acts as the Table of Contents of the BIS Repository")

### Relationships

在 Model 内或跨越 Models 的 Elements 之间可以存在许多不同类型的 Relationships。`ElementOwnsChildElements` relationship 的各种特化特别重要——它们实现 Elements 之间的父子/整体-部分关系。例如，如果 Object 1 是一扇门，它可能有 DoorHardware 作为 Child。

![Image 6: Within a Model, parent Elements allow child Elements](https://www.itwinjs.org/media/bis-modeling-06.png "Within a Model, parent Elements allow child Elements")

因此，BIS 支持两种建模 Object 及其部件的方式：

1. 建模 Object 的 Element 类可以是"原子"的（不允许任何子 Elements）并被包含在更细粒度"子 Model"中的许多 Elements 子建模。BIS 称之为"子建模 Element"。子建模 Element 故意与其子 Model 中的 Elements 冗余，即子建模 Element 表示整个 Object，其子 Model 中的 Elements 在更细粒度上再次表示 Object。
2. 建模 Object 的 Element 类可以允许"子" Elements，但那样它就不允许被子建模。BIS 称之为"父 Element"——本质上将 Entity 建模为聚合。父 Element 与其子 Elements 不冗余，即父 Element 加上子 Elements"加起来"表示整个 Object，而不是在两个不同粒度上表示它两次。

父 Element 至少表示聚合的身份。可选地，它可以建模聚合的"实质"的一部分，在这种情况下，它的"实质"部分不应与其子 Elements 冗余。例如，DoorElement 的物理几何不应包含门五金的几何（假设它有一个包含该几何的 DoorHardware 子 Element）。你可以通过给父 Element 没有几何来建模"纯"装配 PhysicalElement，并添加持有聚合 Entity 所有几何的子 Elements。

这两个规则意味着给定的 Element 类不能同时被子建模 **和** 作为父 Element。Schema 作者必须选择其中一个（或选择使 Element"严格原子"，意味着它既不能被子建模也不能有子 Elements。）

### ElementAspect

ElementAspects 是增强 Element 属性的灵活方式。它们是一组属性，通常保存在某些上下文中需要的信息，例如在施工阶段或当我们有指向不同存储库中建模 Entity 信息的链接时。ElementAspects 不能单独识别，因此它们只能在 Aspect 上存在指向 Element 的 Navigation Property 的 relationships 中使用。例如，每个 Aspect 都有一个指向拥有它的 Element 的 Navigation Property。

### Identifiers（标识符）

Elements 有一个主要标识符（ElementId）并保存 Element 建模的现实世界 Entity 的两个标识符：Code 和 FederationGuid。

**ElementId** 是一个 64 位整数属性，是 Element 的主要标识符，必须在 BIS Repository 内唯一。不同的 BIS Repository 实现以不同方式管理此标识符。

**Code** 是被表示 Entity 的人类可读字符串标识符。Code 编**码**了一些业务含义。
有三个与 Code 相关的 Element 属性：CodeValue 保存 Code，CodeSpec 管理其编码/解码，CodeScope 定义其唯一性范围。三个 code 相关属性的组合必须在 BIS repository 内唯一，可以被视为 Element 的次要标识符。

**FederationGuid** 是可选的，但可用于识别在许多不同存储库（BIS 或其他）中表示的 Entity。

**UserLabel** 是 Element 的可选属性，可用作 GUI 中的非正式名称，但不必唯一。在某些 GUI 中，如果 UserLabel 为 null，CodeValue 将用作显示标签。

---

| 下一步：BIS Organization
|:---