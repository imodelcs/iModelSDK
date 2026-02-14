# Fabric of the Universe（宇宙的结构）

**原文链接**: [Fabric of the Universe](https://www.itwinjs.org/bis/guide/intro/fabric-of-the-universe/)

---

## Introduction（简介）

本节简要描述构成 BIS 基础的少数核心概念。BIS Repository 中的所有信息都使用 `Element`s、`ElementAspect`s、`Model`s 和 relationships 定义。我们将这些核心概念称为"宇宙的结构"。

BIS 使用 EC Information Modeling Language（也称为"使用 ECSchemas"）表达。但是 BIS 施加了额外的规则、命名约定和其他限制。假设读者熟悉 ECSchemas。

以下概念（写作 `{ClassName}`）在"BisCore" domain schema 中定义为 ECClasses。

## Elements

`Element` 是数字世界中表示现实世界中某个 entity 的对象，例如泵、梁、合同、公司等。Elements 包含在 Models 中。Elements 通过 ECProperties 定义。Elements 是 BIS 中可以被单独识别和锁定 finest-grained 对象。

有关更详细的讨论，请参见 Element Fundamentals。

## ElementAspects

`ElementAspect` 是一组"属于"特定 Element 的 ECProperties，但具有独立的生命周期（它们可以在 Element 的生命周期内来去）。ElementAspect 实例由单个 Element _拥有_；ElementAspects 永远不会被多个 Element 共享。ElementAspect 被视为 Element 的一部分，因此不能成为任何"传入" relationships 的目标（除了来自拥有它的单个 Element）。有 ElementUniqueAspects（每个 Element 最多一个实例）和 ElementMultiAspects（每个 Element 可能有多个实例）。

有关 ElementAspects 的更详细讨论，请参见 ElementAspect Fundamentals。

## Models

`Model` 是 Elements 的 _容器_，为包含的 Elements 提供上下文（和 Modeling Perspective）。

有关 Models 的更详细讨论，请参见 Model Fundamentals。

## Relationships

BisCore 中定义了各种 ECRelationship classes 来关联 Models、Elements 和 ElementAspects。有关 Relationships 的更详细讨论，请参见 Relationship Fundamentals。

## No other Data Types（没有其他数据类型）

所有 BIS 信息都使用 `Element`、`ElementAspect`、`Model` classes 或使用 relationships 定义。BIS domain schemas（除了 `BisCore`）只能定义（直接或间接）继承 `BisCore` domain 中定义的 classes 的 classes。

---

| 下一步：Element Fundamentals
|:---

最后更新：2025年6月11日