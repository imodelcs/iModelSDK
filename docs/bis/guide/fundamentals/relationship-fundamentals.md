# Relationship 基础

## 简介

Relationships 是 BIS 的主要构建块之一。它们用于定义实体之间的关联。更具体地说，BIS 严重依赖 EC relationships 来定义其概念 schema。除了导航属性使用的关系外，BIS 中的所有关系都必须继承自核心中的某个关系。最常用的核心关系是：

- ElementOwnsChildElements
- ElementRefersToElements
- ElementOwnsUniqueAspect / ElementOwnsMultiAspects
- ModelContainsElements

## BIS 中的关系继承

BIS 支持关系继承，但受到严格限制。所有关系必须是抽象的、具体的或密封的：

- 抽象关系类永远不能实例化。`ElementRefersToElements` 是抽象关系的示例。它必须被子类化才能实例化。
- 具体关系类可以被继承并且可以被实例化。`ElementOwnsUniqueAspect` 是 Concrete 关系的示例。
- 密封关系类永远不能被继承。`ModelContainsElements` 是密封关系的示例。

此外，所有 BIS 关系，除了用于定义新导航属性的关系外，都必须（直接或间接）继承自 BIS 核心中的关系。

继承关系必须"收窄"关系：

- 相等或更具体的源和目标。
- 相等或更严格的多重性。
- 多态标志可以从 `true` 更改为 `false`，但不能从 `false` 更改为 `true`。
- 强度和方向必须相同。

## 关系强度

关系的强度定义其目标端对象的生存期，因此必须指定。BIS 中接受的两种强度是：

- Embedding：对象控制某些其他对象的生存期，被视为其子对象。也就是说，当删除父对象时，相关的子对象也会被删除。`ElementOwnsChildElements` 是嵌入关系的示例。
- Referencing：对象指向某些其他对象，而不控制其生存期。`ElementRefersToElements` 是引用关系的示例。

关系的强度方向指定解释强度的方向。也就是说，在 `Forward` 关系中，其强度从 Source 到 Target 强制执行。而在 `Backward` 关系中，其强度从 Target 到 Source 强制执行。如果关系没有指定强度方向，则默认假定 `Forward`。

`ElementOwnsChildElements` 是 `Forward` 关系的示例。`ModelModelsElement` 是 `Backward` 关系的示例，因为其嵌入强度从 Element 强制执行到其 Model。

在大多数情况下，关系的强度和方向已经由核心中定义的基关系定义。这些设置不能被子类修改或覆盖。

## 关系多重性

关系的每个端点必须定义多重性，它们共同定义关系的基数。多重性格式指定端点在此关系中可能使用的次数。它使用格式 `(<lower>..<upper>)` 定义。Lower 必须在 `0` 和 `*` 之间，upper 在 `1` 和 `*` 之间，其中 `*` 表示无界。

### 示例

```xml
<ECRelationshipClass typeName="ElementOwnsChildElements" strength="embedding" modifier="None">
  <Source multiplicity="(0..1)" roleLabel="owns child" polymorphic="true">
    <Class class="Element"/>
  </Source>
  <Target multiplicity="(0..*)" roleLabel="is owned by parent" polymorphic="true">
    <Class class="Element"/>
  </Target>
</ECRelationshipClass>
```

`ElementOwnsChildElements` 关系定义以下约束：

- 父 Element（Source）可以拥有由 Target 多重性确定的任意数量的子 Elements（Target）。
- 父 Element 控制子 Elements 的生存期，因此删除父级会删除子级。由关系强度确定。注意：假定方向是从 Source 到 Target，因为未指定。
- Element 只能有一个父级。由 Source 多重性确定。

从 `ElementOwnsChildElements` 派生的关系可以进行以下更改：

- 通过将目标多重性更改为 `(1..*)` 使关系对父级强制。
- 通过将源多重性更改为 `(1..1)` 使关系对子级强制。
- 通过将目标多重性更改为 `(0..1)` 将父级限制为只有一个子级。
- 通过将 Class 约束更改为从 Element 派生的实体类，将任一端点限制为比 Element 更具体的类。
- 通过将多态标志更改为 `false` 将任一端点限制为特定类。
- 通过将修饰符更改为 `Abstract` 或 `Sealed` 使关系抽象或密封。

## 支持的关系能力

BIS 中的关系比普通 EC 中的限制更多。

- 关系继承受到严格限制，如前所述。关系只能有一个基类。
- 关系端点必须是实体类或链接表关系。
- 关系端点必须有一个约束类。
- Aspects 只允许作为导航属性背后关系的源，或 element-owns-aspect 关系的目标。
- 普通 EC 支持 `Holding` 作为额外类型的关系强度，但 BIS 不支持它。

## 限制关系灵活性的实现细节

为了优化使用 iModel 技术的 BIS 应用程序的性能，并非在所有情况下都提供关系的全部功能。要了解这些限制，有助于了解 iModel 数据库中关系的两种实现。

### 关系继承的 iModel 特定含义

- 如果关系不是密封的（可以被子类化），则需要额外的数据库列来存储关系类 Id。这是 ElementOwnsChildElements 关系的情况，预期会被子类化。
- 没有基类且没有子类的密封关系不需要额外的列来存储关系类 Id。这是 ModelContainsElements 关系的情况，它被标记为没有基类的密封。

### 链接表

在 iModel 数据库中，有一个链接表（bis_ElementRefersToElements）支持具有以下任一要求的元素之间的所有关系：

- Source 和 target 都具有无约束的多重性 `(*..*)`
- 关系可以包含属性

具有这些要求之一的所有关系必须继承自 BIS Core schema 中的 ElementRefersToElements 关系。

请注意，Models 和 Aspects 都不能作为链接表中关系的源或目标，因此 Models 和 Aspects 不能参与具有属性或具有 `(*..*)` 多重性的关系。

存储在链接表中的关系示例是具有无约束多重性 `(*..*)` 的 ElementGroupsMembers 关系。

### 导航属性

导航属性类似于数据库中的外键，但作为 EC 属性和 EC 关系公开。作为 iModels 的实现细节，它们的关系存储（和呈现）策略通过指向它的对象中的被指向对象的外键进行访问。存储在外键中的关系端必须具有 `(0..1)` 或 `(1..1)` 的多重性。导航属性始终在基关系中定义，从不通过子类化。

对于密封的导航属性，使用单个外键数据库列来存储关系。密封关系使用导航属性的示例是 `ModelContainsElements` 关系。关系在源端具有 `(1..1)` 的多重性（每个 Element 必须在 Model 中），因此关系存储在目标 Element 的 Model 导航属性中。

关于可子类化的导航属性关系，可以查看 `ElementOwnsChildElements` 关系作为示例。此关系不是密封的（它可以并且经常被子类化），因此使用两个数据库列来存储它。关系在源端具有 `(0..1)` 的多重性（每个 Element 有 0 或 1 个父级），因此关系存储在目标的 Parent 导航属性中。

最后，也可以为链接表关系定义导航属性。在这种情况下，链接表关系被指定为导航属性关系的端点。

---

| 下一篇：Schemas
|:---
