# Data Evolution Across Time（跨时间的数据演进）

## 介绍

BIS 需要支持随时间演进的基础设施建模。演进可能像定义几个新属性那样简单，也可能像详细描述一个项目那样复杂。BIS 支持这整个范围。

在本附录中，将以楼梯为例说明随时间的演进。Stair class 的设计者将无法预测将来可能需要与楼梯关联的所有可能信息，或需要多么复杂的 Stair 定义。

## 从简单开始

最好以尽可能少的假设和要求开始。Stair class 设计者确定 Stair 是一个 PhysicalElement，并给它一个定义，如"*A vertical passageway allowing occupants to walk (step) from one floor level to another floor level at a different elevation. It may include a landing as an intermediate floor slab.*"（复制自 IAI）。Stair class 不需要其他复杂性即可发挥作用。

### 简单 Stair 继承图

![Image 1: Start Simple](https://www.itwinjs.org/media/start-simple.png)

### 简单 Stair 实例图

![Image 2: Stair](https://www.itwinjs.org/media/stair.png)

Stair 实例可以纯粹由实例内的 GeometryStream EC Property（从 GeometricElement3d 继承）定义。像这样建模的 Stair 可能是通过从 IFC 导入创建的。在 iModel 应用程序中原生设计的 Stair 不太可能以这种方式定义。

## 使用 Types

使用 Types 可以更简单、更清晰地定义 Stair。由于 Stair 是 PhysicalElement，它具有 PhysicalElementIsOfType relationship，因此实例可以通过其与 Type 的关系来定义。为了清晰起见，schema 设计者可能会添加一个 StairType class 和自定义 relationship：

### 使用 Types 的 Stair 继承图

![Image 3: Using Types](https://www.itwinjs.org/media/using-types.png)

### 使用 Types 的 Stair 实例图

![Image 4: Stair Inheritance](https://www.itwinjs.org/media/stair-inheritance.png)

这种 Type 建模可能会在初步设计和设计阶段广泛使用。

## 使用 Child Elements

使用 Type 或 FormAspect 的 Stairs 最终可能需要详细说明（详细建模也可以从一开始就进行）。这种详细说明使用 child Elements 实现。为了支持这一点，Stair class 设计者将添加 mixin class IParentElement 作为 Stair 的 superclass（表明此 Stair 可以通过其 children 定义，但不能通过 sub-Model 定义）。为了进一步清晰，Stair class 设计者将创建 PhysicalElementAssemblesChildElements 的 subclass...

这种建模允许楼梯由任何 PhysicalElement 定义；Stair class 设计者提供了极大的灵活性，但"编译时类型检查"较弱。这种妥协在 BIS 中很常见。

### 使用 Children 的 Stair 继承图

![Image 5: Stair defined by Physical Element](https://www.itwinjs.org/media/stair-physical-element.png)

### 使用 Children 的 Stair 实例图

![Image 6: Stair Inheritance defined by Child Element](https://www.itwinjs.org/media/stair-inheritance-child-defined.png)

所有这些建模方法都将通过 schema 可用，但永远不会被同一个实例同时使用。

## 简单数据添加 - Aspects & Relationships

其他 schema 设计者可以创建可以附加到 Stair 或其 superclasses 之一的 Aspects。Stair class 设计者不需要预测将来可能需要与 Stair 关联的所有 Aspects。用户可以随时利用这些 Aspects。

Relationships（如 Aspects）可以为 Stair class（及其 superclasses）定义，而 Stair class 设计者无需任何了解。用户可以随时利用这些与其他 Elements 的 Relationships。

---

| 下一篇：Schema Versioning
|:---|
