# ECCustomAttributeClass

ECCustomAttributeClass 定义自定义元数据，可以应用于任何允许 ECCustomAttributes 的 schema 项。有关可以应用自定义属性的 schema 项列表，请参见 [CustomAttribute Container Types](./customattribute-container-types.md)。有关应用于 schema 项的自定义属性示例，请参见 [ECCustom Attributes](./ec-custom-attributes.md)。

## 附加属性

**appliesTo** [CustomAttribute Container Types](./customattribute-container-types.md) 定义 ECCustomAttributeClass 的 ECInstance 可以应用于哪些 ECSchema 项。可以使用逗号分隔的字符串指定多个容器类型，例如 `Schema, EntityClass, StructClass`。

## 示例

```xml
<ECCustomAttributeClass typeName="HiddenProperty" appliesTo="AnyProperty" modifier="Sealed" >
    <ECProperty propertyName="Show" typeName="boolean" />
</ECCustomAttributeClass>

<ECCustomAttributeClass typeName="DateTimeInfo" description="Optional additional meta data for ECProperties of type DateTime." appliesTo="PrimitiveProperty, ArrayProperty" modifier="Sealed">
    <ECProperty propertyName="DateTimeKind" typeName="DateTimeKind" description="Either Utc, Local or Unspecified. Default: Unspecified."/>
    <ECProperty propertyName="DateTimeComponent" typeName="DateTimeComponent" description="Either DateTime or Date. Default: DateTime."/>
</ECCustomAttributeClass>
<ECEnumeration typeName="DateTimeKind" backingTypeName="string" isStrict="true">
    <ECEnumerator value="Unspecified" name="Unspecified"/>
    <ECEnumerator value="Utc" name="Utc"/>
    <ECEnumerator value="Local" name="Local"/>
</ECEnumeration>
<ECEnumeration typeName="DateTimeComponent" backingTypeName="string" isStrict="true">
    <ECEnumerator value="DateTime" name="DateTime"/>
    <ECEnumerator value="Date" name="Date"/>
    <ECEnumerator value="TimeOfDay" name="TimeOfDay"/>
</ECEnumeration>
```

```json
"HiddenProperty": {
  "schemaItemType": "CustomAttributeClass",
  "modifier": "Sealed",
  "properties": [
    {
      "name": "Show",
      "type": "PrimitiveProperty",
      "typeName": "boolean"
    }
  ],
  "appliesTo": "AnyProperty"
},

"DateTimeInfo": {
  "schemaItemType": "CustomAttributeClass",
  "description": "Optional additional meta data for ECProperties of type DateTime.",
  "modifier": "Sealed",
  "properties": [
    {
      "name": "DateTimeKind",
      "type": "PrimitiveProperty",
      "description": "Either Utc, Local or Unspecified. Default: Unspecified.",
      "typeName": "CoreCustomAttributes.DateTimeKind"
    },
    {
      "name": "DateTimeComponent",
      "type": "PrimitiveProperty",
      "description": "Either DateTime or Date. Default: DateTime.",
      "typeName": "CoreCustomAttributes.DateTimeComponent"
    }
  ],
  "appliesTo": "PrimitiveProperty, ArrayProperty"
},
"DateTimeKind": {
  "schemaItemType": "Enumeration",
  "type": "string",
  "isStrict": true,
  "enumerators": [
    { "name": "Unspecified", "value": "Unspecified" },
    { "name": "Utc", "value": "Utc" },
    { "name": "Local", "value": "Local" }
  ]
},
"DateTimeComponent": {
  "schemaItemType": "Enumeration",
  "type": "string",
  "isStrict": true,
  "enumerators": [
    { "name": "DateTime", "value": "DateTime" },
    { "name": "Date", "value": "Date" },
    { "name": "TimeOfDay", "value": "TimeOfDay" }
  ]
},
```
