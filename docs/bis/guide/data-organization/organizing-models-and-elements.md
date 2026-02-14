# 组织 Models 和 Elements

Information Hierarchy 解释了如何将 `Element`s 组织成各种类型层次结构的机制，这些层次结构可以一起用于从各种 Modeling Perspectives 和各种 Modeling Granularities 建模现实世界中的 Entities。

Top of the World 解释了如何在 RepositoryModel 中构建 Elements 以及为什么要这样做，以描述 BIS Repository "关于"什么。`RepositoryModel` 中的"叶节点"是 InformationPartitionElements（以下简称"partitions"），它们为给定的 Subject 建立 Modeling Perspective。

本主题回顾这些基础知识，并为 Domain 作者和客户端开发人员提供关于如何在 partitions 下组织 Models 和 Elements 以及为什么这样做的指导。在深入详细解释之前，我们总结本主题中回顾或建立的规则。

## 使用 BIS 建模的原则和规则总结

这些原则和规则支配如何组织 `Model`s 和 `Element`s 来建模现实世界 Objects。

- BIS 认为现实世界 Object 由多个 Entities 组成，每个来自不同的 Modeling Perspective。
- 一个 `Element` 建模一个 Entity。
- 一个 `Element` 只能放置在兼容 Modeling Perspective 的 `Model` 中。
- 一个 `Element` 的 sub-Model 以更细的粒度建模与 `Element` 相同的 Entity。
- `Model`s 只能对兼容 Modeling Perspective 的 `Element`s 进行子建模。
- 一个父 `Element` 标识一个 Entity 并且可以建模它的一部分，但它与其子 `Element`s 一起建模该 Entity。
- 父 `Element`s 和子 `Element`s 必须在同一个 `Model` 中。
- 单一方应该负责给定 `Model` 中的所有 `Element`s。
- 单一方可以负责多个 `Model`s。
- 建模物理视角：
  - 使用 Spatial Composition 规则和模式来建模将其他 `Element`s 空间组织成空间分解层次结构的 `Element`s。
  - 主要围绕物理系统的实现（实现功能）组织 `PhysicalModel`s 和 `PhysicalElement`s。这些往往会与责任边界保持一致。
  - 当一个物理 Entity 是多个物理系统的一部分时，它应该由主要责任方拥有的 `Model` 中的 `PhysicalElement` 建模。所有方可以使用 `PhysicalSystemGroupsMembers` 关系"共享"该 `PhysicalElement`。
- 在上述约束内，领域作者可以出于领域特定原因施加额外的组织。
- 领域作者应该给用户灵活性以便出于任意原因进一步分区，因此可以在逻辑上在单个 `Model` 中建模的内容可以通过兄弟 `Subject` 分成两部分。
- 软件对 `Element`s 如何组织到 `Model`s 中的预期不应太"僵化"，特别是在物理视角中。Functional 和 analytical `Model`s 可以更僵化，因为它们是高度专业化的。

## 建模 Domain 时的考虑

作为领域作者，您面临许多建模您的领域的选项，下面将描述这些选项。

### 多个领域上下文

将会有针对设计阶段（如设计、施工和运营）以及基础设施主要类别（如城市或建筑物或其他设施）的不同 Digital Twins。这些之间应该有尽可能多的共性，但领域作者必须意识到 Digital Twins 的类型和其领域相关的工作流范围。下面讨论的建模决策发生在这些 Digital Twins 和工作流的上下文中。

领域作者应该研究其他领域 schemas 的示例，看看其他人是如何解决建模挑战的。

### 众多考虑因素

领域作者有一项艰巨的工作。他们必须考虑：

- __Object boundaries__: 考虑现实世界并从概念上将其切分成 Objects
- __Entity boundaries__: 将那些 Objects 切分成 Entities。
- __Whole-part relationships__: 考虑 Entities 之间的整体-部分关系（以及如何建模它们）。
- __Other Relationships__: 考虑 Entities 之间的其他关系（以及如何建模它们）。
- __Attributes__: 考虑 Entities 的属性（以及如何建模它们）。

"Object boundaries"考虑因素对于数据建模者来说是常规工作，这里不会涵盖。

"Entity boundaries"考虑因素在 Modeling Perspectives 的讨论中涵盖。

其余考虑因素将在以下部分中涵盖。

## Whole-Part Relationships

每个 Entity 都将用 `Element` 建模。该 Entity 是否有"部分"值得在给定上下文中单独建模？该问题的答案将导致三个选择之一：

- __"Atomic" Element__: 没有要建模的"部分"。Atomic `Element`s 仍然可以使用 GeometryStream、Properties 和 `ElementAspect`s 建模重要的内部结构。
- __Parent-Child Modeling__: 整个 Entity 建模为由父 `Element` 及其子 `Element`s 组成的"部分"。父和子 `Element`s 的"总和"建模整个 Entity。这些 `Element`s 实现 `IParentElement`。请参阅 Parent-Child Relationships。
- __Spatial-Composition__: 整个 Entity 对应一个在空间上组织其他 `Elements` 的 `Element`。整个 Entity 需要分解为主要体积部分的层次结构，最终组织 `PhysicalElement`s 和 `SpatialLocationElement`s。请参阅 Spatial Composition。
- __Sub-modeling__: "部分"在此 `Element` 的子 `Model` 中建模。被子建模的 `Element` 代表整个 Entity。`Element` 的子 `Model` 中所有 `Element`s 的"总和"也代表整个 Entity，但以更细的粒度。这些 `Element`s 实现 `ISubModeledElement`。

在下图中，Entity 0 是 Spatial Organizer 占据的体积，例如 _Infrastructure Facility_，因此根据 Spatial Composition schema 的规则和模式进行建模。因此，`Element` F-0 代表整个 Entity 0，它_聚合_三个主要 _FacilityParts_，Entities 1、2 和 3，由 `Elements` FP-1、FP-2 和 FP3 建模，它们在空间上分解它。此外，Entities 4 和 5 被 Entity FP-3 _空间组织_，由 `Elements` P-4 和 P-5 建模。

![Whole-Part Mapping](https://www.itwinjs.org/media/organizing-models-and-elements-01.png)

在另一种情况下，如下图所示，Entity 0 用 `ISubModeledElement` 建模，所以 `Element` P-0 代表整个 Entity 0，其子 `Model` 也代表整个 Entity 0，以不同的粒度。Entity 4 被建模为 `IParentElement`，所以 `Element`s P-4、P-5 和 P-6 集体代表 Entity 4 及其部分。

![Whole-Part Mapping](https://www.itwinjs.org/media/organizing-models-and-elements-02.webp)

使用这些问题来确定是使用父子建模、子建模还是空间组合：

![Whole-Part Mapping Flowchart](https://www.itwinjs.org/media/organizing-models-and-elements-03.png)

最后一个问题需要详细说明。用户需要将 Entity 作为一个整体建模，同时也将其建模为细粒度部分的集合，这是什么典型原因？原因包括：

- 根据 SRPP，如果一方确定 X 应该存在于特定位置，但将详细建模 X 的责任委托给第二方，被委托方需要在他们自己的 `Model` 中完成工作。
- 如果某些工作流想要处理 Entity-as-a-whole，但其他工作流（例如用于施工的制造）需要将其作为一组部分处理，制造商需要一个专注于用于制造整体的部分的 `Model`。

作为边界情况，如果其中一个部分明显是"主要"部分，例如一个带有特定添加（焊接）或减去（切割）的"梁"，那么父子关系可能更合适。使用父子建模还是子建模的决定可能相当棘手。如果可能，您应该检查来自类似领域的 schemas 并咨询专家。

---

| 下一篇：Modeling Systems
|:---
