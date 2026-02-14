# Top of the World（世界之巅）

BIS 仓库具有严格的层次结构组织。本页描述该层次结构的顶部及其如何作为整个仓库的_目录_功能。这个_目录_由以下组成：

- `RepositoryModel`
- `Subject`s
- `InformationPartitionElement`s

下图显示了一个简单的层次结构顶部示例。有关所用约定的详细信息，请参阅实例图约定。

![Top of the world](https://www.itwinjs.org/media/top-of-the-world.png)

## RepositoryModel

每个 BIS 仓库都恰好有一个 `RepositoryModel`，它定义了层次结构的顶部。`Element`s 可以插入到 `RepositoryModel` 中或在其中更新，但 `RepositoryModel` 本身不能被删除。`RepositoryModel` 对 BIS 仓库的根 `Subject` 进行子建模。

_RepositoryModel 是 BIS 仓库中唯一对自己包含的 Element（根 `Subject`）进行子建模的 Model。由于实现细节，这比 RepositoryModel 不对任何 Element 进行子建模更容易。_

## Subjects

`Subject`s 是用于标识仓库_关于_什么的 `Element`s。`Subject` 类不能被特化（子类化）。`Subject` 最重要的能力是：

- 它可以有一个 UserLabel（从 Element 继承）
- 它可以有一个 Description
- 它可以有子 `Subject`s
- 它可以有子 `InformationPartitionElement`s

`Subject`s 只存在于 `RepositoryModel` 中。

每个 BIS 仓库都恰好有一个_根_ `Subject`，它描述整个仓库关于什么。

- 根 `Subject` - 像所有 `Subject`s 一样 - 被 `RepositoryModel` 包含。
- 根 `Subject` 没有父元素，因为它是 `Subject` 层次结构的顶部。
- 根 `Subject` 可以被更新，但不能被删除。
- 根 `Subject` 被 `RepositoryModel` 子建模。

可以引入子 `Subject`s 来进一步组织仓库的内容。

- 子 `Subject`s - 像所有 `Subject`s 一样 - 被 `RepositoryModel` 包含。
- 子 `Subject`s 有另一个 `Subject` 作为父级。
- 子 `Subject` 可以被标识为_编辑通道的根_。

## Editing Channels

`Editing Channel` 是一个 _Channel Root_ `Subject` 元素下面的 models 和 elements 树。`Editing Channel`s 将 BIS 仓库的内容分成_部分_，以提供对哪些应用程序可以更改哪些数据的访问控制。有关此主题的更多信息，请参阅 Editing Channels。

## InformationPartitionElements

正如 Modeling Perspectives 中所讨论的，`Subject`s 可以从多个建模视角（物理、功能、分析等）进行查看和建模。`InformationPartitionElement`s 用于将 `Subject` "分区"成不同的建模视角。

当确定要从特定建模视角对 `Subject` 进行建模时，将适当建模视角的 `InformationPartitionElement` 添加为 `Subject` 的子级。该 InformationPartitionElement 是代表建模视角的 Model 层次结构的开始。`InformationPartitionElement` 被具有相同建模视角的 `Model` 子建模。

总之，`Subject`s 捕获 BIS 仓库关于什么的_人类可理解的_层次分解，根据创建其数据的应用程序的设计，按照 BIS 仓库中的 `Editing Channels` 组织。此外，`InformationPartitionElement` 主要向任何为了不同目的消费 BIS 仓库中数据的_软件_声明关于其父 `Subject` 在其子模型下开始进行的数据建模类型 - 建模视角。

由于 `InformationPartitionElement` 的"_Name_"（例如 Code 和 UserLabel 属性）在业务上下文中通常没有意义，通常被认为是 Partition 的子模型"_Name_"的是其父 `Subject` 的_Code_。由于这个原因，通常预期 `Subject` 对于给定的建模视角只有一个 `InformationPartitionElement` 实例，但这不被强制执行。当出现这种需求时，通常最好通过子 `Subjects` 来解决，每个拥有相同建模视角的不同 `InformationPartitionElement` 实例。

`InformationPartitionElement`s 总是有父 `Subject`，并且永远不会在 `RepositoryModel` 之外使用。

---

| 下一篇：Single Responsible-Party Principle
|:---
