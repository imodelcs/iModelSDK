# PhysicalModel 层级结构

> 原文: [PhysicalModel Hierarchy - iTwin.js](https://www.itwinjs.org/bis/guide/physical-perspective/physical-hierarchy-organization/)
>
> 最后更新: 2025年6月11日

BIS Repository 中的每个 Subject 都可以有一个 PhysicalPartition 子 Element，该 Element 将被一个"顶层" PhysicalModel 进行子建模（sub-model），如下图所示。

![PhysicalModel 层级结构顶部](https://www.itwinjs.org/media/physical-hierarchy-organization-top-of-the-world.png)

建立 Model 层级结构有两种方式：

- 通过 `Subject` 层级结构
- 通过子建模（sub-modeling）

## Subject 层级结构

通过在 Subject 之间建立父子关系来构建 Subject 层级结构，与这些 Subject 相关联的 PhysicalPartition 和 PhysicalModel 可以按层级方式组织。

iModel connectors 和遗留应用程序使用 Subject 层级结构方法，因为它更接近地映射到传统的建模方式。

> _理论上，子 Subject 可以与其父 Subject 的 PhysicalModel 中的某个 Element 建立关系，以表明子 Subject 的 PhysicalModel 正在对另一个 model 中的 Element 所表示的同一事物进行建模，尽管这在实践中尚未实现。这将是表达子 Subject 的 PhysicalModel 本质上是在对父 `Subject` 的 PhysicalModel 中的 Element 进行子建模的一种更灵活的方式，如下所述。_
>
> _通常，可以发明新的关系类来将特定的 Element 与特定的 Subject 关联起来，而不管它们的建模视角如何。这可以促进 Model/Element 的灵活重组，同时保持与 Subject 层级结构的语义连接。_

## 子建模（Sub-modeling）

子建模在 Model Hierarchy 中有描述，它可以更直接地建立 PhysicalModel 的层级结构。

![Element 和 Model 建模建筑](https://www.itwinjs.org/media/physical-hierarchy-organization-building-model.png)

通过子建模，"顶层" PhysicalModel 包含一些混入（mixin）ISubModeledElement 的 Element。这些 Element 将有一个 sub-PhysicalModel，该 Model 以更细的粒度表示与被子建模的 Element 相同的现实世界 Entity。某些基于 iModel 的创作应用程序采用这种方法来建立 PhysicalModel 的层级结构。

## 组织 PhysicalModel 的内容

没有严格的要求限制顶层 `PhysicalModel` 只能包含单个 `PhysicalElement`。如果最适合源数据的组织方式，从其他 repository 生成的 iModel 有时会有包含多个 `PhysicalElement` 的顶层 `PhysicalModel`。遗留数据也可能具有非标准的组织方式。

Sub-`Model` 在 BIS 中是弱类型的。要理解一个 `Model` 正在建模的现实世界 Entity，需要查看该 `Model` 正在子建模的 `Element`。

**注意：PhysicalModel 不应该被子类化。** 现有的少数 `PhysicalModel` 子类已被弃用，不应使用。当使用诸如"Site Model"这样的术语时，它表示"一个对 `Site` 进行子建模的 `Model`"，而不是表示一个强类型的 `SiteModel`。

## 组织 Element

可以使用 SpatialComposition schema 和 PhysicalSystem class 对 Element 应用额外的层级组织。

---

| 下一篇：Physical Models and Elements |
|:---|
