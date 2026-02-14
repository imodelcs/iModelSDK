# Overview

> 原文链接：https://www.itwinjs.org/bis/guide/intro/overview/

缩写 "BIS" 代表 "Base Infrastructure Schema_s_"（基础架构 Schema 集合），但通常作为单数名词使用。发音为 "biz"。BIS 是用于基础设施工程（Infrastructure Engineering）的 Federated Digital Twins（联邦数字孪生）建模的模块化 Schema 家族。

BIS 是一个"概念 Schema"，用于表达现实世界实体（Entity）建模的分类法、数据结构和关系。它使用 Bentley 开放的 "EC" 语言进行实体-关系建模。

## 开放与可扩展

BIS 是一个"开放"且可扩展的 Schema 家族。它被模块化为多个 Domain（领域）。"BIS Core" Domain 表达了基本的建模概念。每个 Domain 作为一个独立的 ECSchema 表达。任何人都可以按照本文档中的规则和指南编写新的 Domain Schema。用户还可以通过添加自定义类（class）、属性（property）和关系（relationship）来扩展 Domain Schema。

## BIS Repository

BIS 是 iModels 的概念 Schema，而 iModels 是 Federated Digital Twins 的关键组成部分。iModels 将 BIS 映射到低级数据库 Schema，并支持 ECSQL 查询语言，该语言被翻译成低级 SQL 查询执行。

BIS 也可以用作 Federated Digital Twin 中其他 Repository 的数据抽象层的概念 Schema。这些 Repository 具有特定的机制，将 BIS 的部分映射到特定 Repository 的技术和信息内容。

"BIS Repository" 指的是使用 BIS 概念 Schema 暴露给 Federated Digital Twins 的 iModels 和其他 Repository。

任何给定的 BIS Repository 都将包含 "BIS Core" Domain 和一个或多个直接或间接依赖于 "BIS Core" 的额外 Domain。没有单个 "BIS Repository" 可能使用 BIS 家族中的**所有** Domain Schema。

## 范围

为了支持基础设施工程的 Federated Digital Twins，BIS 用于建模：

- 物理空间中的物理基础设施
- 由物理基础设施实现的功能系统（工艺工厂）
- 与物理基础设施相关的非物理（但空间上的）实体（边界线、网格线等）
- 物理基础设施的数学分析和仿真模型
- 基础设施工作流中涉及的业务概念和流程（项目、企业、阶段、检查、移交等）
- 与基础设施和业务工作流相关的信息（文档、图纸、合同、规范、报告、RFI、问题、交付物、版本等）

> 下一篇：[Federated Digital Twins](federated-digital-twins.md)

---
*最后更新：2025年6月11日*
