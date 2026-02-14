# ECCustomAttributes

应用于 schema 中其他项以添加新元数据属性的 [ECCustomAttributeClasses](./ec-custom-attribute-class.md) 实例。任何数量的自定义属性都可以应用于 schema 项，但每个类只能应用一个实例。

例如：

```xml
<ECProperty propertyName="LastMod" typeName="dateTime" displayLabel="Last Modified" description="The last modified time of the bis:Element.">
    <ECCustomAttributes>
        <DateTimeInfo xmlns="CoreCustomAttributes.1.0">
            <DateTimeKind>Utc</DateTimeKind>
        </DateTimeInfo>
        <HiddenProperty xmlns="CoreCustomAttributes.1.0"/>
    </ECCustomAttributes>
</ECProperty>
```

```json
{
    "name" : "LastMod",
    "description" : "The last modified time of the bis:Element.",
    "isReadOnly" : true,
    "label" : "Last Modified",
    "type" : "PrimitiveProperty",
    "typeName" : "dateTime",
    "customAttributes" : [
      {
          "DateTimeKind" : "Utc",
          "className" : "CoreCustomAttributes.DateTimeInfo"
      },
      {
          "className" : "CoreCustomAttributes.HiddenProperty"
      }
    ]
},
```

自定义属性概念允许应用任何自定义元数据，因为它们是使用特殊类型的 ECClass 定义的，有关更多详细信息，请参见 [ECCustomAttributeClass](./ec-custom-attribute-class.md)

注意：自定义属性在其父容器中的顺序不保证。我们的 API 将返回一致的顺序，但它可能不总是与它们在 schema 中定义的顺序相同。这应该不是问题，因为相同的自定义属性只能应用一次。
