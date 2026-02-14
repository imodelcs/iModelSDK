# BIS Schemas 仓库结构说明

> 本文档基于 `c:\dev\iModelSDK\source\bis-schemas` 目录分析生成

## 概述

BIS Schemas 是 Bentley Systems 的 **BIS (Base Infrastructure Schema)** ECSchemas 仓库，作为所有 BIS schemas 的唯一权威来源（single-source-of-truth）。

## 目录层级结构

```
bis-schemas/
├── .github/                    # GitHub 配置 (CODEOWNERS, workflows)
├── .vscode/                    # VS Code 配置
├── cmaps/                      # 概念图文件
├── docs/                       # 文档目录
├── Domains/                    # 领域 Schema 主目录
├── System/                     # 系统 Schema 目录
├── tools/                      # 工具脚本目录
├── ignoreSchemaList.json       # 忽略验证的 Schema 列表
├── LICENSE.md                  # MIT 许可证
├── package.json                # NPM 项目配置
├── SchemaInventory.json        # Schema 清单 (包含版本、SHA1、作者等元数据)
└── snapshotInformation.json    # 快照比较信息
```

## Domains 目录结构

Domains 目录按 **Schema Layer** (schema 层级) 组织，分为 5 个主要层级：

### 1. 0-Core 层 (核心层)

**路径**: `Domains/0-Core/`

| Schema 名称 | 描述 |
|------------|------|
| **BisCore** | BIS 核心 Schema，包含所有其他领域 Schema 扩展的基础类 |
| **Functional** | 功能建模 Schema |
| **Generic** | 通用元素 Schema |
| **Analytical** | 分析建模 Schema |
| **Asset** | 资产管理 Schema |
| **BisCoreViews** | BIS 核心视图 Schema |
| **Markup** | 标注 Schema |
| **PhysicalMaterial** | 物理材料 Schema |

### 2. 1-Common 层 (通用层)

**路径**: `Domains/1-Common/`

| 子目录 | Schema 名称 | 描述 |
|--------|------------|------|
| AecUnits | AecUnits | 建筑/工程/施工单位系统 |
| AecValueDefinitions | AecValueDefinitions | AEC 值定义 |
| ClassificationSystems | ClassificationSystems | 分类系统 |
| DistributionSystems | DistributionSystems | 配电/配电系统 |
| DocumentMetadata | DocumentMetadata | 文档元数据 |
| Grids | Grids | 网格系统 |
| LinearReferencing | LinearReferencing | 线性参考系统 |
| NetworkTopology | NetworkTopology | 网络拓扑 |
| Profiles | Profiles | 轮廓/剖面 |
| SpatialComposition | SpatialComposition | 空间组合 |

### 3. 2-DisciplinePhysical 层 (物理学科层)

**路径**: `Domains/2-DisciplinePhysical/`

| 子目录 | 主要 Schema | 描述 |
|--------|------------|------|
| **Building/** | | 建筑领域 |
| ├─ ArchitecturalPhysical | ArchitecturalPhysical | 建筑物理 |
| ├─ BuildingPhysical | BuildingPhysical | 建筑物理元素 |
| └─ BuildingSpatial | BuildingSpatial | 建筑空间 |
| **Civil/** | | 土木工程领域 |
| ├─ BridgePhysical | BridgePhysical | 桥梁物理 |
| ├─ BridgeStructuralPhysical | BridgeStructuralPhysical | 桥梁结构物理 |
| ├─ CivilPhysical | CivilPhysical | 土木物理 |
| ├─ CivilUnits | CivilUnits | 土木单位 |
| ├─ RoadRailAlignment | RoadRailAlignment | 道路铁路定线 |
| ├─ RoadRailPhysical | RoadRailPhysical, RailPhysical, RoadPhysical | 道路铁路物理 |
| ├─ RoadRailUnits | RoadRailUnits | 道路铁路单位 |
| ├─ StormSewerPhysical | StormSewerPhysical | 雨水排污物理 |
| └─ WaterDistributionPhysical | WaterDistributionPhysical | 给水分布物理 |
| **Construction/** | Construction | 施工 |
| **Earthwork/** | Earthwork | 土方工程 |
| **Fasteners/** | Fasteners | 紧固件 |
| **GeotechnicalExploration/** | GeotechnicalExploration | 岩土勘探 |
| **Piping/** | PipeworkPhysical | 管道物理 |
| **QuantityTakeoffsAspects/** | QuantityTakeoffsAspects | 工程量提取 |
| **Rebar/** | Rebar | 钢筋 |
| **StructuralMaterials/** | StructuralMaterials | 结构材料 |
| **StructuralPhysical/** | StructuralPhysical | 结构物理 |
| **Terrain/** | Terrain | 地形 |

### 4. 3-DisciplineOther 层 (其他学科层)

**路径**: `Domains/3-DisciplineOther/`

| 子目录 | Schema 名称 | 描述 |
|--------|------------|------|
| Building/ | MechanicalFunctional | 机械功能 |
| Civil/NetworkTopology/ | RailNetwork, RoadNetwork | 铁路/道路网络 |
| GeologicalModel/ | GeologicalModel | 地质模型 |
| Hydraulics/ | PipeNetworkHydraulicAnalysis, SewerHydraulicAnalysis | 管网/污水水力分析 |
| IoT/ | IoTDeviceFunctional | IoT 设备功能 |
| StructuralAnalysis/ | StructuralAnalysis | 结构分析 |

### 5. 4-Application 层 (应用层)

**路径**: `Domains/4-Application/`

| 子目录 | 描述 |
|--------|------|
| **BuildingSpacePlanning/** | 建筑空间规划 |
| **Connectors/CivilInfrastructureFramework/** | 民用基础设施框架连接器 |
| **DefaultTools/** | 默认工具 |
| **DrawingProduction/** | 图纸生产 |
| **Egress/** | 疏散 |
| **ISM/** | ISM 集成 |
| **OpenSite/** | 开放场地 |
| **Plant/** | 工厂 |
| **PresentationRules/** | 展示规则 |
| **RealityModeling/** | 实景建模 |
| **Simulation4DResults/** | 4D 模拟结果 |
| **SynchroModeler/** | Synchro 建模器 |

## System 目录结构

**路径**: `System/`

```
System/
├── BisCustomAttributes.ecschema.xml      # BIS 自定义属性
├── CoreCustomAttributes.ecschema.xml     # 核心自定义属性
├── ECv3ConversionAttributes.ecschema.xml # ECv3 转换属性
├── Formats.ecschema.xml                  # 格式定义
├── Units.ecschema.xml                    # 单位定义
├── ECDb/
│   ├── ECDbMap.remarks.md
│   ├── ECDbMeta.remarks.md
│   └── Released/                         # ECDb 相关已发布版本
├── json_schema/                          # JSON Schema 定义
│   ├── ec31/                             # EC 3.1 版本
│   └── ec32/                             # EC 3.2 版本
├── xsd/                                  # XSD 验证文件
│   ├── ECSchemaXML3.1.xsd
│   └── ECSchemaXML3.2.xsd
└── Released/                             # 已发布版本
```

## Schema 文件格式

### ECSchema XML 文件

**文件扩展名**: `.ecschema.xml`

**示例结构** (来自 BisCore.ecschema.xml):
```xml
<?xml version="1.0" encoding="UTF-8"?>
<ECSchema schemaName="BisCore" alias="bis" version="01.00.26"
          xmlns="http://www.bentley.com/schemas/Bentley.ECXML.3.2"
          displayLabel="BIS Core"
          description="The BIS core schema contains classes that all other domain schemas extend.">

    <ECSchemaReference name="CoreCustomAttributes" version="01.00.03" alias="CoreCA"/>
    <ECSchemaReference name="BisCustomAttributes" version="01.00.00" alias="bisCA"/>

    <ECCustomAttributeClass typeName="SchemaHasBehavior" appliesTo="Schema" ...>
        <ECArrayProperty propertyName="Restrictions" typeName="string" .../>
    </ECCustomAttributeClass>

    <ECEntityClass typeName="CodeSpec" modifier="Sealed" ...>
        <ECProperty propertyName="Name" typeName="string" .../>
    </ECEntityClass>
</ECSchema>
```

**主要元素类型**:
- `ECSchema` - 根元素，定义 Schema 名称、别名、版本
- `ECSchemaReference` - 引用其他 Schema
- `ECEntityClass` - 实体类
- `ECCustomAttributeClass` - 自定义属性类
- `ECProperty` - 属性定义
- `ECArrayProperty` - 数组属性
- `ECEnumeration` - 枚举类型
- `ECRelationshipClass` - 关系类

### 备注文档

文件格式: `.remarks.md`

用于补充 Schema 的详细说明，与主文档关联。

### 版本命名规则

已发布的 Schema 文件名格式: `{SchemaName}.{MM}.{mm}.{bb}.ecschema.xml`

- MM: 主版本 (Major)
- mm: 次版本 (Minor)
- bb: 构建号 (Build)

示例: `BisCore.01.00.25.ecschema.xml`

## tools 目录

**路径**: `tools/`

```
tools/
├── SchemaBuildReporter.py           # Schema 构建报告器
├── testRunner.yaml                  # 测试运行配置
├── MarkdownGeneration/              # Markdown 文档生成
├── packages/                        # NPM 包生成工具
│   ├── generatePackages.js
│   ├── getSchemaJsons.js
│   └── test/
├── SchemaDifference/                # Schema 差异比较
│   ├── compareSchemas.js
│   └── test/
├── SchemaInventory/                 # Schema 清单管理
│   ├── computeSchemaChecksum.js
│   ├── updateSchemaInventory.js
│   └── test/
├── SchemaValidation/                # Schema 验证
│   ├── iModelSchemaValidation.js
│   ├── SchemaValidationRunner.js
│   └── test/
└── utils/                           # 工具函数
```

## 常用 NPM 脚本

```bash
# 安装依赖
npm install

# 更新 Schema 清单
npm run updateSchemaInventory

# 验证 Schema (BIS 规则)
npm run validateSchemas

# Schema 差异比较
npm run compareSchemas

# iModel Schema 验证
npm run iModelSchemaValidation

# 生成 JSON Schema
npm run generateJsonSchemas

# 生成 NPM 包
npm run genPackages

# 测试
npm run testPkgGen
npm run testInvGen
npm run testSchemaDifference
npm run testSchemaUpgrade
```

## SchemaInventory.json 结构

Schema 清单文件包含每个 Schema 的元数据:

```json
{
  "CoreCustomAttributes": [
    {
      "name": "CoreCustomAttributes",
      "path": "System\\Released\\CoreCustomAttributes.01.00.00.ecschema.xml",
      "released": true,
      "version": "01.00.00",
      "verifier": "Colin.Kerr",
      "sha1": "7355fdfd4968415c3b954f8cb4a68967b79ced03",
      "verified": "Yes",
      "author": "Colin.Kerr",
      "date": "Unknown",
      "dynamic": "No",
      "approved": "Yes"
    }
  ]
}
```

## 架构总结

BIS Schemas 采用**分层架构**设计:

```
┌─────────────────────────────────────────┐
│           4-Application                 │  应用层
├─────────────────────────────────────────┤
│         3-DisciplineOther               │  其他学科层
├─────────────────────────────────────────┤
│        2-DisciplinePhysical             │  物理学科层
├─────────────────────────────────────────┤
│            1-Common                     │  通用层
├─────────────────────────────────────────┤
│             0-Core                      │  核心层 (BisCore)
└─────────────────────────────────────────┘
```

每一层都依赖于其下方的层，形成了清晰的数据模型继承关系。
