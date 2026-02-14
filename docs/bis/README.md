# BIS (Base Infrastructure Schemas) 中文文档

> 原文链接：https://www.itwinjs.org/bis/

缩写 "BIS" 代表 "Base Infrastructure Schema_s_"（基础架构 Schema 集合），但通常作为单数名词使用。发音为 "biz"。BIS 是用于基础设施工程（Infrastructure Engineering）的 Federated Digital Twins（联邦数字孪生）建模的模块化 Schema 家族。

## 文档目录

### Guide 指南

#### [Introduction 介绍](guide/introduction/overview.md)
- [Overview 概述](guide/introduction/overview.md)
- [Federated Digital Twins 联邦数字孪生](guide/introduction/federated-digital-twins.md)
- [Modeling with BIS 使用 BIS 建模](guide/introduction/modeling-with-bis.md)
- [Organization of BIS BIS 组织结构](guide/introduction/organization-of-bis.md)
- [Fabric of the Universe 宇宙结构](guide/introduction/fabric-of-the-universe.md)

#### [Fundamentals 基础](guide/fundamentals/)
- Element Fundamentals - 元素基础
- Codes - 代码
- FederationGuids - 联邦 GUID
- ElementAspect Fundamentals - 元素方面基础
- Mixins - 混入
- Model Fundamentals - 模型基础
- Relationship Fundamentals - 关系基础
- Schemas ("Domains") - Schema（领域）
- Classifying Elements - 元素分类
- Type Definitions - 类型定义
- Categories - 类别

#### [Data Organization 数据组织](guide/data-organization/)
- Information Hierarchy - 信息层次
- Modeling Perspectives - 建模视角
- Top of the World - 世界顶层
- Single Responsible-Party Principle - 单一责任方原则
- Organizing Models and Elements - 组织模型和元素
- Spatial Composition - 空间组合
- Modeling Systems - 建模系统
- Organizing Definition Elements - 组织定义元素

#### [Physical Modeling Perspective 物理建模视角](guide/physical-modeling/)
- 3D Guidance - 3D 指导
- PhysicalModel Hierarchy - PhysicalModel 层次结构
- Physical Models and Elements - 物理模型和元素
- Physical Materials - 物理材料
- Quantity Takeoffs: Guidelines - 工程量提取指南

#### [Other Modeling Perspectives 其他建模视角](guide/other-modeling/)
- Functional Models and Elements - 功能模型和元素
- Analysis Models and Elements - 分析模型和元素
- Information Models and Elements - 信息模型和元素

#### [Schema Evolution Schema 演进](guide/schema-evolution/)
- Schema Customization - Schema 定制
- Data Evolution Across Time - 数据随时间演进
- Schema Versioning - Schema 版本控制
- Schema Production Status - Schema 生产状态
- Schema Design Guidelines - Schema 设计指南

#### [BIS Naming Guidelines 命名指南](guide/naming-guidelines/)
- Rules and Recommendations - 规则和建议
- Special Terms - 特殊术语
- Summary of Exceptions - 例外总结
- Abbreviations and Acronyms - 缩写和首字母缩略词
- Relationship "Strengths" - 关系"强度"

#### [Other Topics 其他主题](guide/other-topics/)
- BIS Schema Units - BIS Schema 单位
- BIS Schema KindOfQuantities - BIS Schema 量类
- BIS Schema Validation - BIS Schema 验证

#### [References 参考资料](guide/references/)
- BIS Glossary - BIS 词汇表
- Class-diagram Conventions - 类图约定
- Instance-diagram Conventions - 实例图约定

### Domain Schemas 领域 Schema

#### [Core Domains 核心领域](domains/core/)
- Overview - 概述
- Analytical - 分析
- BisCore - BIS 核心
  - Drawings & Sheets - 图纸和表单
  - Provenance in BIS - BIS 中的来源
- Functional - 功能
- Generic - 通用
- PhysicalMaterial - 物理材料

#### [Common Domains 通用领域](domains/common/)
- Overview - 概述
- AECUnits - AEC 单位
- ClassificationSystems - 分类系统
- DistributionSystems - 配电系统
- DocumentMetadata - 文档元数据
- Linear Referencing - 线性参考
- Profiles - 轮廓
- SpatialComposition - 空间组合

#### [Discipline-Physical Domains 物理学科领域](domains/discipline-physical/)
- Overview - 概述
- Building domains - 建筑领域
- Civil domains - 土木领域
- Construction - 施工
- Earthwork - 土方
- Structural domains - 结构领域
- Terrain - 地形

#### [Discipline-Other Domains 其他学科领域](domains/discipline-other/)
- Overview - 概述
- Structural domains - 结构领域

#### [Standard Schemas 标准 Schema](domains/standard/)
- Overview - 概述
- BisCustomAttributes - BIS 自定义属性
- CoreCustomAttributes - 核心自定义属性
- ECDbMap - ECDb 映射
- Formats - 格式
- Units - 单位

### [Engineering Content (EC)](ec/)
- Overview - 概述
- ECSchema
- ECClass
- ECEntityClass
- ECMixinClass
- ECStructClass
- ECCustomAttributeClass
- ECRelationshipClass
- ECProperty
- ECCustomAttributes
- ECEnumeration
- KindOfQuantity
- PropertyCategory
- PrimitiveTypes
- CustomAttribute Container Types
- Unit
- Constant
- Phenomenon
- UnitSystem
- Format
- ECName
- Changes Between ECObjects 2 and 3

## 相关文档

- [BIS Schemas 仓库结构说明](../schemas/README.md)
