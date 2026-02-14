# 组织 Definition Elements

DefinitionElement 的实例保存旨在被引用和共享的配置相关信息。它们预期被包含在 `DefinitionModel`s 中，如 Model Fundamentals 中所解释的。

`DefinitionElement`s 的示例包括以下实例：

- `Category` 和 `Subcategory`
- `TypeDefinitionElement`
- `RenderMaterial`
- `PhysicalMaterial`
- `LineStyle`
- 等

## Definition Rank

一些 `DefinitionElement` 实例是为了标准化而引入 iModel 的。这是在 BIS 生态系统的各个级别完成的。在本讨论中要记住的级别是：

- Core: 在 BIS schema 层次结构的"Core"和"Common"层语义上的标准化定义。实际上目前还没有这些的示例。
- Discipline: 在 BIS schema 层次结构的"Discipline-Physical"或"Discipline-Other"层的标准化定义。
- Application: 应用程序特定的定义。注意，应用程序和连接器应该努力定义和使用标准化领域，所以这并不意味着"连接器写入的任何定义"。
- User: 大多数定义，是用户特定的或项目特定的。

## Definition scope

仓库中的 `Subject` 层次结构本质上定义了各种范围级别。Root `Subject` 是"全局"范围，所有其他 `Subjects` 定义更窄的范围。

每个 `Subject` 可以有 0 或 1 个子 `DefinitionPartition` 元素，该元素被子 `DefinitionModel` 建模。

### DictionaryModel（用于全局范围的定义）

Root `Subject` 的 `DefinitionPartion` 总是有一个 "BisCore.DictionaryModel" 的 `CodeValue`。其子模型称为"DictionaryModel"。DictionaryModel 是 `DefinitionElement` 实例的单例容器。它_直接_持有 User 级别的定义，并在 `DefinitionContainer`s 下持有 Core、Discipline 和 Application 标准化定义。

- 对于 Discipline 级别的定义，应该有一个 `DefinitionContainer`，其 `CodeValue` 为 _"{domain alias}:DomainDefinitions"_（其中 {domain alias} 是进行标准化的领域的 schema alias - 这_可能与_定义特定 `DefinitionElement` 子类的 schema _不同_）- 以及一个 `CodeScope`，它是包含它的 `DefinitionModel` 的 ElementId。领域标准化定义应该放在该 `DefinitionContainer` 的子模型中。
- 对于标准化的 Application 级别定义，应该有一个 `DefinitionContainer`，其 `CodeValue` 为 _"{application name}:ApplicationDefinitions"_ 以及一个 `CodeScope`，它是包含它的 `DefinitionModel` 的 Id。应用程序标准化定义应该放在该 `DefinitionContainer` 的子模型中。
- 对于 Core 级别的定义，应该有一个 `DefinitionContainer`，其 `CodeValue` 为 _"bis:CoreDefinitions"_ 以及一个 `CodeScope`，它是包含它的 `DefinitionModel` 的 Id。BIS 标准化定义应该放在该 `DefinitionContainer` 的子模型中。

所有全局范围的 Core 级别、Discipline 级别和 Application 级别定义应该组织在 DictionaryModel 下。

作为领域级别定义的示例，"Terrain" 领域（前缀"trrn"）定义了一组标准 `Category` 元素，"Earthworks" 领域（前缀"ew"）定义了一些标准的 `PhysicalType` 元素，用于支持该领域的 Connectors 和 Applications。请参阅下图。

### Subject 特定的定义

只有 User 级别的定义应该放在 Subject 特定的 `DictionaryModel`s 中，这些通常由 iModel Connectors 创建。在这种情况下，Subject 特定定义的 `DefinitionPartion` 应该有一个 "Definitions" 的 `CodeValue` 和其父 `Subject` 的 `CodeScope`。

### 定义的组织示例

下面的实例图描述了各种级别和范围的定义元素的组织。有关所用约定的详细信息，请参阅实例图约定。

![Repository-Global DefinitionElements](https://www.itwinjs.org/media/repository-global-definitions.png)

---

| 下一篇：3D Guidance
|:---

最后更新：2025年6月11日
