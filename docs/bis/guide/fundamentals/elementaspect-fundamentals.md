# ElementAspect 基础

## 简介

`ElementAspect` 是 EC 类，通常为其定义 EC 属性。ElementAspects 通常用于创建可选的属性集。

ElementAspects 与 Elements 有特殊关系。每个 ElementAspect 实例通过 EC 关系与恰好一个 Element 实例关联。ElementAspect 实例从不在 Element 实例之间共享。Element 拥有其 ElementAspects；如果删除 Element，其 ElementAspects 也会被删除。

![ElementAspects](https://www.itwinjs.org/media/elementaspect-fundamentals.png)

## 核心 ElementAspect 类型

此类层次结构中有三个核心 ElementAspect 类：

![ElementAspect core classes](https://www.itwinjs.org/media/elementaspect-base-classes.png)

这三个类都是抽象的，因此从不实例化。

ElementAspect 预期不会有比此处显示的两个子类更多的子类。

ElementUniqueAspect 和 ElementMultiAspect 将有许多子类。

### ElementUniqueAspect

`ElementUniqueAspect` 用作基类，当单个 Element 可能拥有零个或一个（但绝不会超过一个）完全相同 ECClass 的 ElementAspect 时。

关系 `ElementOwnsUniqueAspect` 用于将 Element 连接到 ElementUniqueAspect。

### ElementMultiAspect

`ElementMultiAspect` 用作基类，当单个 Element 可能拥有零个、一个或多个相同 ECClass 的 ElementAspects 时。

关系 `ElementOwnsMultiAspects` 用于将 Element 连接到其 ElementMultiAspects。

## ElementAspects 与标识

ElementAspects 主要从拥有 ElementAspect 的 Element 派生其标识。

对于 ElementUniqueAspect，子类和 Element 标识的组合唯一标识 ElementUniqueAspect。

对于 ElementMultiAspect，子类和 Element 标识的组合标识 ElementMultiAspects 列表。如果需要引用单个 ElementMultiAspect 实例，每个 ElementMultiAspect 还有一个私有 Id。

ElementAspects 也可用于根据其适用性分隔属性组。考虑从一组对象捕获 `Shape` 和相关维度属性的需求。适用于每个对象的维度属性列表取决于其特定的 `Shape`。这种情况可以通过 ElementAspect 类层次结构建模，该层次结构捕获此类系统要支持的所有 `Shape` 及其各自的属性。

![ElementAspect hierarchy example](https://www.itwinjs.org/media/elementaspect-shapeaspect-hierarchy.png)

在这种情况下，`ShapeAspect` 基类应用作键类来唯一标识此类层次结构的具体方面的实例。在这种情况下这是必需的，以确保对象在任何给定时间只拥有 `ShapeAspect` 层次结构中三个具体类中的一个方面。

## ElementAspects 与关系

ElementOwnsUniqueAspect 和 ElementOwnsMultiAspects 关系用于定义 Elements 对 ElementAspects 的所有权，但其他 ElementAspect 关系呢？ElementAspects 可能拥有的唯一其他关系是"向外"关系，这些关系有效地映射到 ElementAspect 中的单个外键。这种关系在 ECSchemas 中作为导航属性实现。ElementAspects 不能成为任何其他关系的目标。

例如，防火 ElementAspect 可能具有 Thickness 属性和通过导航属性与 FireproofingMaterial 的关系。

BIS 关系的一般行为和用法在 Relationship Fundamentals 中讨论。

## 涉及 ElementAspects 的常见策略

因为 ElementAspects 是 ECClasses，它们具有固定的 schema。

这使它们具有与 Elements 相同的第一类报告功能。

当需要为位于类层次结构不同部分的 Elements 存储相同的属性集时，通常使用 ElementAspects。

但是，如果数据更临时，则 Element `JsonProperties` 可能更合适。

---

| 下一篇：Mixins
|:---
