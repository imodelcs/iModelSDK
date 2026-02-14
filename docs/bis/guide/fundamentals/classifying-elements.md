# Classifying Elements

> 注意：此页面内容可能在源网站上已更改或暂时不可用。请参考官方文档获取最新信息。

有关 BIS 中语义与几何分类的更多信息，请参阅 Categories 页面。

Elements 可以通过以下方式分类：

1. **通过 ECClass** - Element 的类（继承自 `Element`）定义了它是什么类型的实体
2. **通过 Category** - 对于 GeometricElements，Category 对其几何进行分类以用于显示目的
3. **通过 TypeDefinition** - Elements 可以与 TypeDefinitionElement 关联以共享公共属性值

## 语义与几何分类

在 BIS 中，区分语义分类和几何分类很重要：

- **语义分类** 由 Element 的 ECClass 层次结构确定。这定义了 Element 表示什么类型的现实世界实体。
- **几何分类** 由 Element 的 Category 确定（仅适用于 GeometricElements）。这控制 Element 的几何如何显示。

## Category 与 ECClass 的关系

- Category 用于显示目的（可见性、样式等）
- ECClass 用于语义目的（Element 表示什么）
- 多个不同的 ECClass 可以使用相同的 Category
- 一个 Element 属于恰好一个 Category

---

> 此页面内容可能需要从官方 iTwin.js 文档获取更详细的信息。

| 下一篇：Type Definitions
|:---
