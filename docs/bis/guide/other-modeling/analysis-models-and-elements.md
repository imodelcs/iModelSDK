# Analysis Models and Elements

> 原文: [Analytical Models and Elements - iTwin.js](https://www.itwinjs.org/bis/guide/other-perspectives/analysis-models-and-elements/)

## 简介 (Introduction)

`AnalyticalModel` 是用于促进基础设施分析的模型。需要 AnalyticalModel 的分析通常是专业化的分析视角，无法直接在 `PhysicalModel` 上执行，因为物理世界过于复杂；这些分析需要简化的几何图形和其他数据。AnalyticalModels 通常以真实世界坐标创建。

通常，每个 AnalyticalModel 只与一种类型的分析相关。一个特定的 PhysicalModel（例如一栋建筑）可能有多个关联的 AnalyticalModels。由 AnalyticalModels 促进的分析示例包括：液压分析、建筑能耗分析、交通分析和结构分析。

任何分析都涉及一个或多个数值求解器，能够基于一组初始条件（输入）预测系统的行为（输出）。虽然某些分析可以直接在 Physical Perspective 数据上执行，但许多类型的分析需要基于自定义视角的现实并行表示。在后一种情况下，分析的输入数据被捕获在 BIS 存储库中适用 `Subject` 的相应分析模型视角中。

请注意，BIS 存储库不适合存储分析的结果或输出数据。分析结果集通常是短暂的且体积很大，当专业建模师尝试多组初始条件时会频繁或批量创建。

## 分析元素 (Analytical Elements)

`AnalyticalElement` 是真实物理基础设施的简化表示。AnalyticalElement 的一个例子是液压分析模型中的 Pipe Segment（管道段，而非物理管道）。这个 Pipe Segment 可能有一个简单的 2D 线段位置，以及一组液压分析属性，其值是专业数值求解器的输入，该求解器基于流体动力学可以预测流体通过时的液压行为。它还将与被分析管道网络中的其他 Hydraulic Analytical Elements 建立关系。请注意，此示例中的单个结果（输出）值，如特定 AnalyticalElement 和模拟时间步长处的 _water velocity_（水流速度）或 _water pressure_（水压），不应存储在 BIS 存储库中。

AnalyticalElements 必须始终包含在 AnalyticalModels 中。AnalyticalElements 通常会与 PhysicalElements 或 SpatialLocationElements 建立 `AnalyticalElementSimulatesSpatialElement` 关系，这些元素模拟相同的现实世界基础设施。然而，这种关系并不总是 1:1 的。

## 分析模型 (Analytical Models)

`AnalyticalModel` 的存在是为了促进基础设施分析。AnalyticalModels 直接或间接地包含单一类型的一项或多项分析所需的所有信息。对于某些 Analytical 域，一个 `PhysicalModel` 可能适合有多个 AnalysisModel。

### 分析模型的内容 (Contents of Analytical Models)

`AnalyticalModel` 包含 `AnalyticalElement`，但也可能包含其他类型的元素。AnalyticalModels 经常包含 `InformationElement`。AnalyticalModels 永远不包含 `PhysicalElement`。

### 模型层次结构中的分析模型 (Analytical Models in Model Hierarchy)

由于 `AnalyticalModel` 用于协助物理基础设施的设计或理解，AnalyticalModels 通常与 `PhysicalModel` 相关联。这种链接通过其元素之间的 `AnalyticalElementSimulatesSpatialElement` 关系来表达。

在 World 的顶层，专业化分析通过 `AnalyticalPartition` 子类引入，该子类由 AnalyticalModel 进行子建模。

## 典型分析模型工作流程 (Typical Analytical Model Workflows)

`AnalyticalModel` 预期在三种基本场景中使用：

1. AnalyticalModel 从 `PhysicalModel` 派生
2. PhysicalModel 从 AnalyticalModel 派生
3. AnalyticalModel 在与 PhysicalModel 没有关系的情况下使用

从 PhysicalModel 派生 AnalyticalModel 预期是一个常见的工作流程。现有或规划中的基础设施经常需要建模和分析。AnalyticalModel 的派生可能是自动的、半自动的或手动的。派生通常会在 `AnalyticalElement` 和 `PhysicalElement` 或 `SpatialLocationElement` 之间创建 `AnalyticalElementSimulatesSpatialElement` 关系。这些关系稍后可用于在 PhysicalModel 更改时协助更新 AnalyticalModel，或在两个模型之间创建信息的双向同步。

从 AnalyticalModel 派生 PhysicalModel 对于新基础设施可能是一个常见的工作流程，当基础设施的分析设计发生在物理设计之前时。从 AnalyticalModel 派生 PhysicalModel 通常是简单的自动操作，但通常不会产生完全详细的 PhysicalModel。与物理到分析的派生一样，通常会创建 `AnalyticalElementSimulatesSpatialElement` 关系。这些关系可用于更新和双向同步。

与 PhysicalModel 无关的独立 AnalyticalModel 是有效的配置。当使用 iModel 的组织只参与分析研究时，可能会使用此配置。

## 示例 - 建筑热分析 (Example - Building Thermal Analysis)

建筑热分析是 `AnalyticalModel` 的一种可能用途。这种专业化分析通过 `AnalyticalPartition` 的子类在模型层次结构中引入。

建筑的外围护结构和内部隔断可能会用 `AnalyticalElement` 的 EnvelopePanel 子类进行建模，该子类将包含面板形状的信息，以及相关的红外辐射透射率、热质量和热绝缘属性。这些 EnvelopePanel 元素将与 `PhysicalModel` 中它们所表示的任何项目相关联。

同样，将创建 AnalyticalElement 子类来表示 HVAC 系统的关键组件。这些也将与其关联的 `PhysicalElement` 相关联。

`InformationElement` 子类将用于记录分析的其他参数，如天气场景和建筑运营假设。

热分析的完整结果可能很大，不应直接存储在 BIS 存储库中。

![分析层次结构](https://www.itwinjs.org/media/analytical-hierarchy.png)

---

| 下一篇: Information Models and Elements
|:---|
