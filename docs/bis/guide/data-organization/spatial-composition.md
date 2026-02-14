# 空间组合

## 简介

BIS 的 SpatialComposition Domain Schema 允许 iModel 作者清晰地表达场地/设施的空间结构，并使用该结构来组织 `PhysicalElement`s 和 `SpatialLocationElement`s，无论它们如何被组织到单独的 Models 中。

在建模基础设施资产的空间结构时，可以使用尽可能多的组合级别。`SpatialCompositon` 定义了用于表达基础设施资产主要空间结构的 `SpatialStructureElement` 基类：`Region`、`Site`、`Facility`、`FacilityPart` 和 `Space`。特定学科的领域通过这些基类的子类提供更专业的语义。这些类的实例使用"Aggregates"关系组织成层次结构。

下表显示了一个涉及公交车站建筑物、道路和桥梁的示例基础设施资产。该表列出了现实世界 Entity 的名称以及它映射到的特定学科类（括号中是其 `SpatialComposition` 基类）。

| Entity | 特定学科类标签（`SpatialComposition` 类） |
| --- | --- |
| Bus Terminal | Site (`Site`) |
| -- Bus Terminal Building | Building (`Facility`) |
| ---- First floor | Story (`FacilityPart`) |
| ------ Restroom 1 | Space (`Space`) |
| -- Access Road | Road (`Facility`) |
| ---- Southbound Roadway | Roadway (`FacilityPart`) |
| ------ Travel Lane | Traffic Lane (`FacilityPart`) |
| ---- Median | Central Reserve (`FacilityPart`) |
| ---- Northbound Roadway | Roadway (`FacilityPart`) |
| -- Ramp | Bridge (`Facility`) |
| ---- Superstructure | Bridge Superstructure (`FacilityPart`) |
| ------ Deck | Bridge Deck (`FacilityPart`) |
| ---- Substructure | Bridge Substructure (`FacilityPart`) |
| ------ Pier | Bridge Pier (`FacilityPart`) |

`SpatialComposition` 还定义了一个 `Zone`，可用于表达一些基于空间的替代分组。

## 使用空间结构组织其他 Elements

一旦空间结构被建模，其元素就可以用于使用"Holds"和"References"关系组织任何 `bis:SpatialElement`（`bis:PhysicalElement` 和 `bis:SpatialLocationElement` 的基类）。"Holds"意味着相关元素（或其重要部分，如电梯井的基础）包含在 `SpatialStructureElement` 或 `Zone` 中。"References"意味着某种较弱的关系（例如电梯井穿过该空间）。请参阅"Information Hierarchy"文章的 Element Organized by Spatial Organizer 部分。

下表显示了可以与前面介绍的公交车站示例相关联的 `bis:SpatialElement`s。

| Entity | 空间结构元素 | 物理/空间元素 | 关系 |
| --- | --- | --- | --- |
| Bus Terminal | Site | Holds | 道路线形 |
| -- Bus Terminal Building | Building | Holds | 网格 |
| ---- First floor | Story | Holds | 柱、梁、墙、门 |
| ------ Restroom 1 | Space | Holds | 水槽、厕所 |
| -- Access Road | Road |  |  |
| ---- Southbound Roadway | Roadway | Holds | 路面层 |
| ------ Travel Lane | Traffic Lane | References | 车道标记 |
| ---- Median | Central Reserve | Holds | 护栏 |
| ---- Northbound Roadway | Roadway | Holds | 路面层 |
| -- Ramp | Bridge |  |  |
| ---- Superstructure | Bridge Superstructure | Holds | 梁 |
| ------ Deck | Bridge Deck | Holds | 板、护栏 |
| ---- Substructure | Bridge Substructure |  |  |
| ------ Pier | Bridge Pier | Holds | 柱、基础、帽 |

如上例所示，现实世界基础设施实体可以使用多个并行组织结构进行建模，包括空间组合层次结构、空间区域、物理装配和将元素分区到模型中。每种建模技术独立表达意义的不同方面，为 schema 设计者和最终用户提供灵活性。

---

| 下一篇：Modeling Systems
|:---

最后更新：2025年6月11日
