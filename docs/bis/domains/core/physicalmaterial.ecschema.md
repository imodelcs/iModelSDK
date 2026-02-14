# PhysicalMaterial Schema

**Alias:** physMat

**Version:** 1.0.2

## 目录

- Entity Classes
  - Aggregate
  - Aluminum
  - Asphalt
  - Concrete
  - Steel

## Entity Classes

### __Aggregate__ (Aggregate) _Sealed_ EntityClass

Aggregate 是一个 bis:PhysicalMaterial，表示一类粗到中等颗粒的颗粒状材料，通常用于建筑以及作为基础、道路和铁路下方的基底材料。

**Base Class:** BisCore:PhysicalMaterial

继承属性

| Name | Description | Type | Extended Type |
| --- | --- | --- | --- |
| Model | 包含此 bis:Element 的 bis:Model。 | navigation |  |
| LastMod | bis:Element 的最后修改时间。此属性由核心框架维护，应用程序不应直接设置。 | dateTime |  |
| CodeSpec | CodeSpec 属性标识用于生成和验证此 bis:Element 代码值的 bis:CodeSpec。CodeSpec、CodeScope 和 CodeValue 属性的组合对每个 bis:Element 实例必须是唯一的。 | navigation |  |
| CodeScope | CodeScope 属性标识为代码值提供唯一性范围的 bis:Element。CodeSpec、CodeScope 和 CodeValue 属性的组合对每个 bis:Element 实例必须是唯一的。 | navigation |  |
| CodeValue | 可空字符串属性，保存 Element 的 Code 的实际文本。CodeSpec、CodeScope 和 CodeValue 属性的组合对每个 bis:Element 实例必须是唯一的。 | string |  |
| UserLabel | 用户给出的可选友好名称（与存储在 CodeValue 属性中的正式名称相对）。 | string |  |
| Parent | 拥有此 bis:Element 的父 bis:Element。 | navigation |  |
| FederationGuid | 用于在存储库之间联合此 bis:Element 的 GUID。 | binary | BeGuid |
| JsonProperties | 用户和/或应用程序可用于持久化临时 JSON 值的字符串属性。 | string | Json |
| IsPrivate | 如果为 true，则此 bis:DefinitionElement 不应在 GUI 中显示。 | boolean |  |
| Density |  | double |  |
| RenderMaterial | 可选地引用用于显示 bis:PhysicalMaterial 的 bis:RenderMaterial。 | navigation |  |

### __Aluminum__ (Aluminum) _Sealed_ EntityClass

Aluminum 是一个 bis:PhysicalMaterial，表示铝（原子符号 Al）或其合金之一。

**Base Class:** BisCore:PhysicalMaterial

继承属性

| Name | Description | Type | Extended Type |
| --- | --- | --- | --- |
| Model | 包含此 bis:Element 的 bis:Model。 | navigation |  |
| LastMod | bis:Element 的最后修改时间。此属性由核心框架维护，应用程序不应直接设置。 | dateTime |  |
| CodeSpec | CodeSpec 属性标识用于生成和验证此 bis:Element 代码值的 bis:CodeSpec。CodeSpec、CodeScope 和 CodeValue 属性的组合对每个 bis:Element 实例必须是唯一的。 | navigation |  |
| CodeScope | CodeScope 属性标识为代码值提供唯一性范围的 bis:Element。CodeSpec、CodeScope 和 CodeValue 属性的组合对每个 bis:Element 实例必须是唯一的。 | navigation |  |
| CodeValue | 可空字符串属性，保存 Element 的 Code 的实际文本。CodeSpec、CodeScope 和 CodeValue 属性的组合对每个 bis:Element 实例必须是唯一的。 | string |  |
| UserLabel | 用户给出的可选友好名称（与存储在 CodeValue 属性中的正式名称相对）。 | string |  |
| Parent | 拥有此 bis:Element 的父 bis:Element。 | navigation |  |
| FederationGuid | 用于在存储库之间联合此 bis:Element 的 GUID。 | binary | BeGuid |
| JsonProperties | 用户和/或应用程序可用于持久化临时 JSON 值的字符串属性。 | string | Json |
| IsPrivate | 如果为 true，则此 bis:DefinitionElement 不应在 GUI 中显示。 | boolean |  |
| Density |  | double |  |
| RenderMaterial | 可选地引用用于显示 bis:PhysicalMaterial 的 bis:RenderMaterial。 | navigation |  |

### __Asphalt__ (Asphalt) _Sealed_ EntityClass

Asphalt 是一个 bis:PhysicalMaterial，表示沥青粘结剂和集料的混合物。Asphalt 通常用于道路铺装。

**Base Class:** BisCore:PhysicalMaterial

继承属性

| Name | Description | Type | Extended Type |
| --- | --- | --- | --- |
| Model | 包含此 bis:Element 的 bis:Model。 | navigation |  |
| LastMod | bis:Element 的最后修改时间。此属性由核心框架维护，应用程序不应直接设置。 | dateTime |  |
| CodeSpec | CodeSpec 属性标识用于生成和验证此 bis:Element 代码值的 bis:CodeSpec。CodeSpec、CodeScope 和 CodeValue 属性的组合对每个 bis:Element 实例必须是唯一的。 | navigation |  |
| CodeScope | CodeScope 属性标识为代码值提供唯一性范围的 bis:Element。CodeSpec、CodeScope 和 CodeValue 属性的组合对每个 bis:Element 实例必须是唯一的。 | navigation |  |
| CodeValue | 可空字符串属性，保存 Element 的 Code 的实际文本。CodeSpec、CodeScope 和 CodeValue 属性的组合对每个 bis:Element 实例必须是唯一的。 | string |  |
| UserLabel | 用户给出的可选友好名称（与存储在 CodeValue 属性中的正式名称相对）。 | string |  |
| Parent | 拥有此 bis:Element 的父 bis:Element。 | navigation |  |
| FederationGuid | 用于在存储库之间联合此 bis:Element 的 GUID。 | binary | BeGuid |
| JsonProperties | 用户和/或应用程序可用于持久化临时 JSON 值的字符串属性。 | string | Json |
| IsPrivate | 如果为 true，则此 bis:DefinitionElement 不应在 GUI 中显示。 | boolean |  |
| Density |  | double |  |
| RenderMaterial | 可选地引用用于显示 bis:PhysicalMaterial 的 bis:RenderMaterial。 | navigation |  |

### __Concrete__ (Concrete) _Sealed_ EntityClass

Concrete 是一个 bis:PhysicalMaterial，表示水硬性水泥、集料、水和可选其他材料的混合物。

**Base Class:** BisCore:PhysicalMaterial

继承属性

| Name | Description | Type | Extended Type |
| --- | --- | --- | --- |
| Model | 包含此 bis:Element 的 bis:Model。 | navigation |  |
| LastMod | bis:Element 的最后修改时间。此属性由核心框架维护，应用程序不应直接设置。 | dateTime |  |
| CodeSpec | CodeSpec 属性标识用于生成和验证此 bis:Element 代码值的 bis:CodeSpec。CodeSpec、CodeScope 和 CodeValue 属性的组合对每个 bis:Element 实例必须是唯一的。 | navigation |  |
| CodeScope | CodeScope 属性标识为代码值提供唯一性范围的 bis:Element。CodeSpec、CodeScope 和 CodeValue 属性的组合对每个 bis:Element 实例必须是唯一的。 | navigation |  |
| CodeValue | 可空字符串属性，保存 Element 的 Code 的实际文本。CodeSpec、CodeScope 和 CodeValue 属性的组合对每个 bis:Element 实例必须是唯一的。 | string |  |
| UserLabel | 用户给出的可选友好名称（与存储在 CodeValue 属性中的正式名称相对）。 | string |  |
| Parent | 拥有此 bis:Element 的父 bis:Element。 | navigation |  |
| FederationGuid | 用于在存储库之间联合此 bis:Element 的 GUID。 | binary | BeGuid |
| JsonProperties | 用户和/或应用程序可用于持久化临时 JSON 值的字符串属性。 | string | Json |
| IsPrivate | 如果为 true，则此 bis:DefinitionElement 不应在 GUI 中显示。 | boolean |  |
| Density |  | double |  |
| RenderMaterial | 可选地引用用于显示 bis:PhysicalMaterial 的 bis:RenderMaterial。 | navigation |  |

### __Steel__ (Steel) _Sealed_ EntityClass

Steel 是一个 bis:PhysicalMaterial，表示铁、碳和其他元素的合金。

**Base Class:** BisCore:PhysicalMaterial

继承属性

| Name | Description | Type | Extended Type |
| --- | --- | --- | --- |
| Model | 包含此 bis:Element 的 bis:Model。 | navigation |  |
| LastMod | bis:Element 的最后修改时间。此属性由核心框架维护，应用程序不应直接设置。 | dateTime |  |
| CodeSpec | CodeSpec 属性标识用于生成和验证此 bis:Element 代码值的 bis:CodeSpec。CodeSpec、CodeScope 和 CodeValue 属性的组合对每个 bis:Element 实例必须是唯一的。 | navigation |  |
| CodeScope | CodeScope 属性标识为代码值提供唯一性范围的 bis:Element。CodeSpec、CodeScope 和 CodeValue 属性的组合对每个 bis:Element 实例必须是唯一的。 | navigation |  |
| CodeValue | 可空字符串属性，保存 Element 的 Code 的实际文本。CodeSpec、CodeScope 和 CodeValue 属性的组合对每个 bis:Element 实例必须是唯一的。 | string |  |
| UserLabel | 用户给出的可选友好名称（与存储在 CodeValue 属性中的正式名称相对）。 | string |  |
| Parent | 拥有此 bis:Element 的父 bis:Element。 | navigation |  |
| FederationGuid | 用于在存储库之间联合此 bis:Element 的 GUID。 | binary | BeGuid |
| JsonProperties | 用户和/或应用程序可用于持久化临时 JSON 值的字符串属性。 | string | Json |
| IsPrivate | 如果为 true，则此 bis:DefinitionElement 不应在 GUI 中显示。 | boolean |  |
| Density |  | double |  |
| RenderMaterial | 可选地引用用于显示 bis:PhysicalMaterial 的 bis:RenderMaterial。 | navigation |  |

---

*最后更新: 2025年6月11日*

---

**源文档:** [https://www.itwinjs.org/bis/domains/physicalmaterial.ecschema/](https://www.itwinjs.org/bis/domains/physicalmaterial.ecschema/)
