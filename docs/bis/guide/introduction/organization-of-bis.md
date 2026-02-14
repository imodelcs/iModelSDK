# Organization of BIS（BIS 的组织结构）

**原文链接**: [Organization of BIS](https://www.itwinjs.org/bis/guide/intro/bis-organization/)

---

## A Family of Schemas（Schema 家族）

BIS 不是单一的 schema，而是模块化为一个"domain" Schemas 家族，它们根据依赖约束和特定程度组织成层次。模块化设计允许增量添加新领域。每个 domain 应该在语义上紧密，范围足够小以便由单人拥有。

这些层次如下图所示：

![Image 1: A Family of Schemas](https://www.itwinjs.org/media/a-family-of-schemas.png "A Family of Schemas")

任何层次中的 Schemas 可以引用（依赖于）同一层次或任何较低层次中的 schemas。Schema 层次的层次旨在避免循环依赖，同时仍允许不同 domains 互操作。Bentley Systems 开发的 BIS schemas 在一个公开的开源 GitHub 仓库中维护和演进，其文件夹结构反映了 BIS 生态系统中的这些层次。

### Core Layer（核心层）

此层次的基础是 Core 层。它包含定义"宇宙结构"和一些关键组织策略的 schemas。其他层次中的所有类都继承自 BisCore schema 中的类，使基于 BIS 的软件能够——至少在某种基本层面上——理解所有 BIS schemas，即使它从未见过这些 BIS schemas。

### Common Layer（通用层）

在 Core 之上是 Common 层。此层定义跨越多个学科的抽象或非物质概念和模式。这些概念的示例包括"网格线"、"网络拓扑"、"分配系统"、"线性参考"、"空间组合"等。

iTwin.js Core 以及任何其他通用扩展可以依赖并理解 Core 和 Common 层定义的 schemas 和模式。

### Discipline-Physical Layer（学科-物理层）

在 Common 之上是 Discipline-Physical 层。此层用于定义现实世界的具体物理/空间实体和密切相关的信息，用于 Subjects 的物理建模视角。

### Discipline-Other Layer（学科-其他层）

在 Discipline-Physical 之上是 Discipline-Other 层。在特定学科背景下定义物理以外建模视角概念的 Schemas 属于此层。此层中的 schemas 示例包括功能数据（如 P&ID 图纸背后的过程数据）和分析数据（如用于分析结构的结构行为数据）。

针对特定学科开发的扩展可以依赖并理解适用于其预期用例的 Discipline-Physical 或 Discipline-Other schemas 子集。

### Application Layer（应用层）

顶层是 Application schemas。这些 schemas 包含其他应用程序不需要或不想访问的数据。产品和 iModel Connector schemas 是此层的示例。

## Schema Metadata

BIS schema 应通过应用 BisCustomAttributes schema 中定义的 `SchemaLayerInfo` 自定义属性来声明其作者的预期层次。

## BIS Compatibility Grades for Schemas（BIS Schema 兼容性等级）

产品转换为使用 BIS Domain Schemas 可以增量进行，但基于 BIS 的基础设施生态系统（包括 iModelHub 和 Design Review）正在快速扩展。这创造了短期需求，需要基于 BIS 的"兼容性" schemas，它们没有经过真正 BIS schemas 那样严格的设计，但允许使用 BIS 生态系统并与之有一定程度的互操作性。因此，创建了 BIS schemas 的等级级别：

- _Grade A_: 经过精心设计用于编辑和互操作性的真正 BIS schemas
- _Grade B_: 要么是：
  - 智能转换为 BIS 的遗留"共识" schemas（如 ISM），或
  - 新的 BIS schemas，考虑到单向转换为 BIS，但不打算用于编辑（原生格式）。
- _Grade C_: 具有软件可发现语义的遗留 schema，智能转换以遵循相关 BIS 规则和模式。
- _Grade D_: 具有最少或没有软件可发现语义的遗留 schema，通常自动转换，遵循基本 BIS 规则和模式。

---

| 下一步：Fabric of the Universe
|:---