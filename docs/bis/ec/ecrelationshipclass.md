# ECRelationshipClass

这种 ECClass 的特化具有与 ECClass 相同的子元素和属性，以及额外的子元素来描述类之间的关系。ECObjects 中的关系遵循关系范式而非 OO 范式，即它们不仅仅是简单的对象引用，如 C++ 或 .NET 类型系统中的那样。ECRelationshipClass 表示两个业务对象实例之间关系的实例的可能性（和约束）。参见 [ECRelationships](./ec-relationships.md)。

关系继承在概念上类似于常规 ECClass 继承，但有额外的限制。派生关系类表示基本关系的特化，而不是新的和不同的关系。因此，派生关系的范围必须等于或更严格于基本关系。

关系类规则：

- 每个关系必须完全定义，即使是抽象的
  - 要完全定义，source 和 target 端点必须指定：
    - 允许的 ECEntityClass
    - 多重性
    - 角色标签
    - 多态标志
    - 抽象约束 ECClass。只有在有多个约束类时才需要。

关系继承规则：

- 关系仅支持单继承
- 派生关系缩小其父关系的约束
  - 约束类必须等于或更派生于基类中定义的类
  - 多重性必须等于或更严格于基类中定义的
    - 所需端点的最小数量可以增加但不能减少
    - 所需端点的最大数量可以减少但不能增加
  - 多态标志可以保持不变或从 true 更改为 false，但不能从 false 更改为 true
    - **注意**：如果抽象关系类的多态标志设置为 false，则所有派生关系只能应用于抽象关系约束中指定的类。

- 角色标签可以在派生关系中无限制地自定义。
- 派生关系中定义的抽象约束类必须等于或派生于基本抽象约束类
- 只有基本关系可以被 Navigation 属性引用
- 只有基本关系可以设置 order by 属性

## 附加属性

**strength** 标识 source 和 target 对象的生命周期如何关联。

**strengthDirection** 指示 source 是父级还是反之亦然...
- Forward 表示 source 是"持有者"、"嵌入者"或"引用者"。"Forward"是默认值。Backward 表示 target 是持有者/嵌入者/引用者。

## 附加子元素

BaseClass _(0..1)_

[Source](#source-and-target) _(1..1)_

[Target](#source-and-target) _(1..1)_

## Source 和 Target 约束

关系的 Source 和 Target 定义端点类及其约束。每个端点必须至少定义一个 ECEntityClass、多重性、端点是否多态，如果定义了多个约束类，还需要一个抽象约束。

## 属性

**isPolymorphic** 如果此端还可以与特定类的子类实例相关联，则为 true。

**roleLabel** 从此端读取的关系标签。

- 这是此端关系处 ECClass 角色的标签，例如，在 DocumentCreatedByUser 关系中，Document 作为 source，User 作为 target，source 的 roleLabel 是从 Document 角度看的 source 类（Document）的角色："created by User"。target 端的 roleLabel 是从 User 角度看的关系："created Document"。这些应该包含对另一端 ECClass 的提及，以便可以国际化这些（可能需要更改词序）。

**multiplicity** 此端关系的多重性。使用 UML 格式 (x..y) 指定，其中 x >= 0 且 (y >= 1 或 y == "\*") 且 x <= y。如果没有限制，通常设置为 (1..1) 或 (0..\*)。

**abstractConstraint** 此端关系的所有约束类必须等于或派生自的 ECClass。如果此端关系有多个约束类，则在基本关系类中是必需的，否则是可选的。

## 自定义属性

关系约束可以应用 [Custom Attributes](./ec-custom-attributes.md)，但不从基本关系的约束继承自定义属性。

## 子元素

[ECCustomAttributes](./ec-custom-attributes.md) _(0..1)_

[Class](./ec-class.md) _(1..*)_

- 此端关系的 ECClass

## 示例

```xml
    <ECRelationshipClass typeName="ElementOwnsChildElements" strength="embedding" modifier="None" >
        <Source multiplicity="(0..1)" roleLabel="owns child" polymorphic="true">
            <Class class="Element"/>
        </Source>
        <Target multiplicity="(0..*)" roleLabel="is owned by parent" polymorphic="true">
            <Class class="Element"/>
        </Target>
    </ECRelationshipClass>
```

```json
"ElementOwnsChildElements": {
  "schemaItemType": "RelationshipClass",
  "modifier": "None",
  "strength": "Embedding",
  "strengthDirection": "Forward",
  "source": {
    "multiplicity": "(0..1)",
    "roleLabel": "owns child",
    "polymorphic": true,
    "constraintClasses": [
      "BisCore.Element"
    ]
  },
  "target": {
    "multiplicity": "(0..*)",
    "roleLabel": "is owned by parent",
    "polymorphic": true,
    "constraintClasses": [
      "BisCore.Element"
    ]
  }
},
```
