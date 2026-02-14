# ECMixinClass

Mixin 是一种特殊类型的抽象类，可以向实体类添加属性和次要继承层次结构。Mixin 类定义了跨越主要实体继承层次结构的概念。它们可以保存公共属性定义并用作关系端点。Mixin 类除了标准实体类规则外，还遵循几个旨在避免多继承引起的问题的规则：

1. Mixin 可以有 0 或 1 个基类。
2. Mixin 只能将另一个 mixin 作为基类
3. Mixin 不得覆盖继承的属性
4. Mixin 必须定义一个实体类，限制可以应用它的实体类

实体类可以实现多个 mixin，但只能有一个实体基类。包含 mixin 的类也必须遵循严格的规则：

1. 只有当实体类派生自 mixin 定义中指定的"applies to"类时，实体类才能从 mixin 继承
2. 实体类不得从主要层次结构和 mixin 层次结构继承同名属性
3. 实体类不得覆盖从 mixin 继承的属性
4. 实体类必须首先放置其实体基类，然后在 xml 中放置 mixin

Mixin 可以用作关系端点，规则与任何抽象实体类相同。

## 示例

### Mixin 类定义

```xml
<ECEntityClass typeName="ISubModeledElement" modifier="Abstract" displayLabel="Sub-Modeled Element">
    <ECCustomAttributes>
        <IsMixin xmlns="CoreCustomAttributes.01.00.03">
            <AppliesToEntityClass>Element</AppliesToEntityClass>
        </IsMixin>
    </ECCustomAttributes>
</ECEntityClass>
```

> 在 xml 中，mixin 被表示为具有特殊自定义属性的 Entity Class

```json
"ISubModeledElement": {
  "schemaItemType": "Mixin",
  "label": "Sub-Modeled Element",
  "appliesTo": "BisCore.Element"
},
```

> 在 json 中，mixin 被表示为具有一等 schema 项类型。

### Mixin 应用于类定义

```xml
<ECEntityClass typeName="Drawing" description="A bis:Drawing is a bis:Document of a 2D drawing.">
    <BaseClass>Document</BaseClass>
    <BaseClass>ISubModeledElement</BaseClass>
</ECEntityClass>
```

> 在 xml 中，mixin 必须放在单个实体基类之后（如果存在）。代码中的验证逻辑不允许使用多个实体基类。

```json
"Drawing": {
  "schemaItemType": "EntityClass",
  "description": "A bis:Drawing is a bis:Document of a 2D drawing.",
  "baseClass": "BisCore.Document",
  "mixins": [
    "BisCore.ISubModeledElement"
  ]
},
```

> 在 json 中，mixin 被输入到它们自己的数组中，基类存储为字符串，因此格式本身不允许使用多个基类。
