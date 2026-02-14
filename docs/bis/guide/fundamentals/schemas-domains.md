# Schemas（"Domains"）

## 简介

Domain 是 BIS ECSchema 的同义词。Domains 为自然连贯且范围有限的主题定义数据类型。这种方法旨在避免理解和管理整体或非常大的 schema 相关的问题和复杂性。它高度依赖于多个 BIS 领域设计者之间的协调和合作，以便 BIS 应用程序所需的每个可共享概念都能找到其适当的位置（即 domain），在那里它将被管理和维护。

由于 Domains 是 BIS 中划分世界的主要概念，并且每个 domain 足够小以具有明确的范围和所有者，BIS 也可以被视为"domain" schema 的模块化家族。

## 分层方法

Domains 根据 domain 中 ECSchema 主题的通用性或专业性组织成层。BIS 中最通用的 ECSchema 位于此层次结构的基础——如下图所示——是 BisCore。

任何层中的 schema 可能依赖于同一层或任何更低层的 schema。schema 层次结构的层旨在避免循环依赖，同时仍允许不同的 domains 相互操作。

![A Layered Approach](https://www.itwinjs.org/media/a-family-of-schemas.png)

### BisCore 层

BisCore 定义其他 domains 中所有其他数据类型必须遵循的核心 ECClasses 和组织策略。Model、Element 和 UniqueAspect 等类在 BisCore schema 中。

### Common 层

BIS ECSchema 家族中"Core"之上的下一层是"Common"。那是定义适用于多个学科的广泛概念的地方。例如，建筑"Common" schema 可能包括网格等概念，但不包括建筑细节（如窗户）或结构（如梁）。

"Common"之上的层专注于单个学科（在上图中，共享相同的首字母），同时在其目的上进行区分："Physical"和"Other"（例如 Functional/Analytical）。

### Discipline-Physical 层

"Physical"和"Functional/Analytical" domains 从不同视角建模特定学科。

Discipline-Physical 层根据特定学科定义现实世界的物理实体和密切相关的信息。Pump、Pipe 或 Column 等类在 Discipline-Physical 层。此层还包括根据 Spatial Composition schema 建立的概念和模式引入的学科特定概念，如 Building、Road 或 Bridge。

### Discipline-Other 层

此层定义用于物理以外建模视角的数据类型。启用各种原理图和模拟的功能或分析 schema 是此层的示例。

### Application 层

顶层用于任何需要的应用程序 schema。这些 schema 不包含任何其他应用程序需要访问的数据。产品和 iModel Connector schema 是此层的示例。

### 物理骨干

BIS schema 和 BIS repository 内数据组织的另一个关键组织策略是"物理骨干"。对于 schema 设计，物理世界是一个统一的现实，所有学科在就如何在 BIS 中表示某事达成共识时都可以同意。

在 BIS repository 中，物理世界的表示成为我们可以组织其他数据的框架。BIS repository 中的所有数据预期都与物理基础设施相关或相关。物理基础设施被建模为层次结构，其他非物理信息（例如 Functional 或 Analytical 视角）通常相对于该层次结构存储。但是，预期在某些工作流程中，物理基础设施在其他非物理数据被建模后出现。因此，"物理骨干"的概念，尽管从 BIS repository 开始不是强制的，但应该驱动学科中各个 domain 的设计。

## Domain Handlers

Domain 的 BIS schema 预期对各种客户端有用，设计时考虑多个产品或其他 domain（如果需要）将使用它们。此外，作为 BIS Domain 实现的一部分，可以选择实现跨平台 Typescript 组件——通常称为"Domain Handler"——代表理解 Domain 所关于的 BIS ECSchema 的代码，能够以连贯的方式读取和修改其数据，以及公开提供特殊功能的公共 API，使其 ECSchema 更易于使用且更不容易出错。

## 生命周期考虑

将使用 BIS 的学科通常专注于基础设施资产的整个生命周期。即，概念/详细设计、施工、运营和维护生命周期阶段。BIS 在其核心不打算将 schema 进一步分解为生命周期阶段，而是对它们不可知。因此，domain BIS ECSchema 的设计应使其能够容纳各个阶段的数据。由 ECSchema 建模的任何 BIS 概念的数据质量和/或细节应随着它在生命周期阶段中"流动"而演变。不需要导入/导出工作流程。

向后设计 BIS schema（即首先理解运营和维护所需的概念，同时最后保留概念设计）可能有助于识别所有需要的部分，以实现适用于感兴趣基础设施整个生命周期的 schema。

## 示例

以 Road & Rail 学科为例，下图描绘了它们如何分为各种 BIS domains。

![Example](https://www.itwinjs.org/media/road-rail-schemas.png)

在最底层 - Core - BisCore schema 是最通用的 domain，为所有其他 BIS domains 布局框架和基础。上图中描述的其他 Core 层 schema 包括 PhysicalMaterials、Functional、Analytical 和 Generic。

上一层 - Common - 可以找到针对抽象概念的 domains。这些包括 Linear-Referencing、Network-Topology、Profiles 和 Distribution Systems 等领域。

在 Common 之上，引入了学科特定的层。在 Road & Rail 的情况下，Discipline-Physical 层描绘了引入基本部分的 domains，如 Alignments（基于 Linear-Referencing）、Earthwork 和 Terrain。显示了其他相关的 domains，专注于 Road 和 Railway 基础设施的 Physical-modeling 和 Spatial-Composition，如 Bridges、Tunnels 和 Drainage。

上图中包含的 Road & Rail 学科中专注于其他建模视角的其他 domains 是：Structural Analysis（适用于桥梁和隧道）、Traffic Analysis 和 Hydraulic Analysis。

最后，可以在所有这些 Road & Rail domains 之上构建多个应用程序 schema，包括 iModel Connector schema。这些 Civil 应用程序可能专注于 Road & Rail 学科中的特定资产和生命周期阶段。但是，它们引用的 BIS ECSchemas 预期在 Road & Rail 学科资产的整个生命周期中有用。

---

| 下一篇：Information Hierarchy
|:---
