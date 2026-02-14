# ECEntityClass

ECEntityClass 构成 schema 中的域模型，定义将创建并插入到仓库中的对象。除了通用属性集外，它还有额外的属性。

除了有一个基类外，实体类还可以应用任意数量的 [Mixins](./ec-mixin-class.md)。

## 自定义属性

ECEntity 类从其基类和应用的任何 mixins 继承自定义属性。首先遍历基类，然后是 mixins。当发现多个相同类的自定义属性时，第一个被发现的是返回的那个。

## 附加子元素

[ECNavigationProperty](./ec-property.md#ecnavigationproperty) _(0..*)_

## 示例

```xml
<ECEntityClass typeName="Door">
    <BaseClass>bis:PhysicalElement</BaseClass>
    <ECProperty propertyName="OverallHeight" typeName="double" kindOfQuantity="AECU:LENGTH_SHORT"/>
    <ECProperty propertyName="OverallWidth" typeName= "double" kindOfQuantity="AECU:LENGTH_SHORT"/>
    <ECProperty propertyName="Description" typeName="string"/>
</ECEntityClass>
```

```json
"Door": {
  "schemaItemType": "EntityClass",
  "baseClass": "BisCore.PhysicalElement",
  "properties": [
    {
      "name": "OverallHeight",
      "type": "PrimitiveProperty",
      "description": "Overall Height of the Door",
      "label": "Overall Height",
      "kindOfQuantity": "AecUnits.LENGTH_SHORT",
      "typeName": "double"
    },
    {
      "name": "OverallWidth",
      "type": "PrimitiveProperty",
      "description": "Overal1 Width of the Door",
      "label": "Overall Width",
      "kindOfQuantity": "AecUnits.LENGTH_SHORT",
      "typeName": "double"
    },
    {
      "name": "Description",
      "type": "PrimitiveProperty",
      "typeName": "string"
    }
  ]
},
```
