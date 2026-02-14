# BIS 中的特殊术语

本节包含与 BIS 上层本体中的特殊术语相关的规则和建议 [rec.]。

## Model

|  | 描述 | 备注 |
| --- | --- | --- |
| 规则 | Model Class 必须始终以 Model 为后缀 | 例如 `FunctionalModel`、`PhysicalModel`。例外：`GeometricModel2d`、`GeometricModel3d` |

## Element

|  | 描述 | 备注 |
| --- | --- | --- |
| 规则 | 抽象术语应仅出现在继承层次结构中高于具体术语的位置 | 例如，术语 `Element` 用于为某些抽象 Class 添加后缀。一旦从名称中删除了 `Element`（因为 Class 是具体的），它就永远不会回来。面向用户的 Class 通常是具体的，我们尤其不想向这些 Class 添加多余的术语。 |
| 建议 | 面向用户的 Class 不应以抽象术语表示 | 例如，当可以使用 `Document` 时，不要使用 `InformationContentElement` |

## RoleElement

|  | 描述 | 备注 |
| --- | --- | --- |
| 建议 | 不要以 `Role` 为后缀 | 例如，使用 `Resource`、`Asset` 而不是 `ResourceRole` 或 `AssetRole` |

## Aspect

|  | 描述 | 备注 |
| --- | --- | --- |
| 建议 | 以 `Aspect` 为后缀 |  |

## Type

|  | 描述 | 备注 |
| --- | --- | --- |
| 建议 | 对现实世界类型使用术语 `Type`，而不是 Class 或 Kind | 例如，使用 `FunctionalType` 而不是 `FunctionalClass` 或 `FunctionalKind` |

---

**原文**: [Special Terms in BIS](https://www.itwinjs.org/bis/guide/naming-guidelines/special-terms/)

**最后更新**: 2025年6月11日
