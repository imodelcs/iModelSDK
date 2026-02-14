# ECStructClass

ECStructClass 定义复杂类型，可以用作 ECStructProperty 的类型。结构体不能在包含实例的上下文之外实例化，也不能在实例之间共享。结构体可以包含结构体属性，但不能创建无限递归的结构。

## 示例

```xml
<ECStructClass typeName="DistanceExpression" description="Core structure carrying linearly-referenced information.">
    <ECProperty propertyName="DistanceAlongFromStart" typeName="double" kindOfQuantity="LENGTH"/>
    <ECProperty propertyName="LateralOffsetFromILinearElement" typeName="double" kindOfQuantity="LENGTH"/>
    <ECProperty propertyName="VerticalOffsetFromILinearElement" typeName="double" kindOfQuantity="LENGTH"/>
    <ECProperty propertyName="DistanceAlongFromReferent" typeName="double" kindOfQuantity="LENGTH"/>
</ECStructClass>
```

```json
"DistanceExpression": {
  "schemaItemType": "StructClass",
  "description": "Core structure carrying linearly-referenced information.",
  "properties": [
    {
      "name": "DistanceAlongFromStart",
      "type": "PrimitiveProperty",
      "label": "Distance-along",
      "kindOfQuantity": "LinearReferencing.LENGTH",
      "typeName": "double"
    },
    {
      "name": "LateralOffsetFromILinearElement",
      "type": "PrimitiveProperty",
      "label": "Lateral offset",
      "kindOfQuantity": "LinearReferencing.LENGTH",
      "typeName": "double"
    },
    {
      "name": "VerticalOffsetFromILinearElement",
      "type": "PrimitiveProperty",
      "label": "Vertical offset",
      "kindOfQuantity": "LinearReferencing.LENGTH",
      "typeName": "double"
    },
    {
      "name": "DistanceAlongFromReferent",
      "type": "PrimitiveProperty",
      "label": "Distance-along from Referent",
      "kindOfQuantity": "LinearReferencing.LENGTH",
      "typeName": "double"
    }
  ]
},
```
