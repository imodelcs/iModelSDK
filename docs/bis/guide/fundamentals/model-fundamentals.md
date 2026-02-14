# Model 基础

`Model` 是拥有 Element 集合的容器。每个 Element 由恰好一个 Model 包含，由 `ModelContainsElements` 关系定义。Models 有助于组织 repository 的整体内容，因为每个 Element 集合都有单独的容器。

Model 内容由以下驱动：

- Model 子类
  - Model 特化可能会限制可以包含的 Elements 类型。
- 粒度或细节级别
  - 整个对象与其更细粒度的分解。
- 用户偏好
  - 一些用户可能按空间位置（东翼与西翼）组织，而其他用户可能按学科（建筑与土木）组织。
- 领域规则
  - 一些规则由代码强制执行，用户无法自定义。

## 核心 Model 类型

下表显示了最常见的核心 model 类型，以及它们可以包含的允许元素类型。

| Model 子类 | 包含的 Elements 类型 |
| --- | --- |
| `PhysicalModel` | PhysicalElements, SpatialLocationElements, GraphicalElement3d 和 InformationContentElements |
| `FunctionalModel` 子类 | FunctionalElements 和 InformationContentElements |
| `AnalyticalModel` 子类 | AnalyticalElements 和 InformationContentElements |
| `DefinitionModel` | DefinitionElements 和 InformationContentElements |
| `DocumentListModel` | Document elements |
| `DrawingModel` | GeometricElement2d elements |
| `SheetModel` | GeometricElement2d elements |

下表显示了其他核心 model 类型，通常被认为是专门的。

| Model 子类 | 包含的 Elements 类型 |
| --- | --- |
| `GraphicalModel3d` | GraphicalElement3d elements |
| `GroupInformationModel` | GroupInformationElements |
| `InformationRecordModel` | InformationRecordElements |
| `LinkModel` | LinkElements |
| `PhysicalSystemModel` | PhysicalSystem elements |
| `SpatialLocationModel` | SpatialLocationElements, GraphicalElement3d 和 InformationContentElements |

### Model 标识

Models 也是 BIS repository 中信息层次结构的关键构建块。向下看信息层次结构，Models 是 Elements 的集合。向上看信息层次结构，Models 是来自更高级别的 Element 的更多细节。这个更高级别的 Element 被称为被建模元素。被建模元素赋予 Model 其标识。model 的 Id 值与被建模元素的 Id 值匹配。

Model 通过 `ModelModelsElement` 关系与其被建模的 Element 相关联。此外，Model 不存储自己的名称。相反，其名称来自被建模元素的 `CodeValue`。

有关更多详细信息，请参阅 Information Hierarchy。

---

| 下一篇：Relationship Fundamentals
|:---

最后更新：2025年6月11日
