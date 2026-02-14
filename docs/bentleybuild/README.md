# BentleyBuild 构建系统文档

> 基于 imodel-native 项目分析生成

## 1. 概述

BentleyBuild 是 Bentley Systems 开发的自定义构建系统，基于 **bmake**（类 make 构建工具）。该系统使用 PartFile XML 定义、.mke makefile 和 .mki 包含文件的层次结构来管理跨平台 C++ 编译。

### 1.1 核心组件

| 组件 | 文件类型 | 用途 |
|------|----------|------|
| PartFile | `.PartFile.xml` | 定义构建组件的逻辑结构和依赖关系 |
| Makefile | `.mke` | 定义编译规则和目标 |
| Include | `.mki` | 可重用的构建配置片段 |

### 1.2 支持的平台

| 平台 | 架构 | 编译器 | 库类型 |
|------|------|--------|--------|
| **Windows** | x64 | Visual Studio 2019 | 动态库 (DLL) |
| **Linux** | x64 | Clang 7 | 静态库 (.a) |
| **macOS** | x64, ARM64 | Xcode Clang | 静态库 (.a) |
| **iOS** | ARM64, Simulator | Xcode Clang | 静态库 (.a) |
| **Android** | ARM64, ARM7A, x64 | Android NDK Clang | 静态库 (.a) |

---

## 2. PartFile.xml 结构

### 2.1 根元素

```xml
<BuildContext xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
              xsi:noNamespaceSchemaLocation="../../../bentleybuild/PartFile.xsd">
    <!-- 构建组件定义 -->
</BuildContext>
```

### 2.2 核心元素

#### `<Part>` - 构建组件定义

定义一个逻辑构建组件及其依赖和构建指令。

**关键属性：**

| 属性 | 用途 |
|------|------|
| `Name` | 组件唯一标识符 |
| `BentleyBuildMakeFile` | 构建此组件的 .mke 文件路径 |
| `BentleyBuildMakeOptions` | 额外的 make 选项/标志 |
| `DeferType` | 构建阶段（如 `BuildUnitTests`, `RunUnitTests`） |
| `OnlyPlatforms` | 限制特定平台 |
| `ExcludePlatforms` | 排除特定平台 |
| `LibType` | 库类型：`Static` 或 `Dynamic` |

**示例：**

```xml
<Part Name="ECObjectsNative" BentleyBuildMakeFile="src/ecobjects.mke">
    <SubPart PartName="PublicAPI" />
    <SubPart PartName="BentleyDll" PartFile="iModelCore/Bentley/Bentley" />
    <Bindings>
        <Libs>Delivery/$(libprefix)iTwinECObjects$(libext)</Libs>
        <Assemblies>Delivery/$(shlibprefix)iTwinECObjects$(shlibext)</Assemblies>
    </Bindings>
</Part>
```

#### `<SubPart>` - 依赖引用

引用同一文件中的其他 Part 或外部 PartFile。

| 属性 | 用途 |
|------|------|
| `PartName` | 依赖组件名称 |
| `PartFile` | 外部 PartFile 路径（不含 .PartFile.xml 扩展名） |
| `LibType` | 覆盖库类型 |
| `Repository` | 外部仓库 |

#### `<Bindings>` - 输出产物

定义组件产生的文件。

- `<Libs>` - 静态/导入库文件
- `<Assemblies>` - 共享库/DLL 文件
- `<PublicAPI>` - 公共头文件
- `<VendorAPI>` - 第三方 API 头文件

**路径变量：**

| 变量 | 说明 |
|------|------|
| `$(libprefix)` | 库前缀（Unix 上为 `lib`） |
| `$(libext)` | 库扩展名（如 `.lib`） |
| `$(shlibprefix)` | 共享库前缀 |
| `$(shlibext)` | 共享库扩展名（如 `.dll`, `.so`, `.dylib`） |
| `$(stlibprefix)` | 静态库前缀 |
| `$(stlibext)` | 静态库扩展名 |

---

## 3. MKE 文件（Makefile）

### 3.1 基本结构

```makefile
#---------------------------------------------------------------------------------------------
#  Copyright (c) Bentley Systems, Incorporated. All rights reserved.
#  See LICENSE.md in the repository root for full copyright notice.
#---------------------------------------------------------------------------------------------

%include mdl.mki                    # 核心构建系统定义
%include $(_MakeFilePath)../mki/ECObjects.mki   # 模块特定包含

# 变量定义
baseDir             = $(_MakeFilePath)
programName         = ECObjects
o                   = $(PartBuildDir)   # 输出目录

# 编译器标志
BUILD_WITH_C20=1    # 启用 C++20

# 预处理器定义
nameToDefine        = __BENTLEYDLL_BUILD__
%include cdefapnd.mki

# 包含目录
dirToSearch         = $(BuildContext)VendorAPI/icu4c/
%include cincapnd.mki
```

### 3.2 预编译头

```makefile
PchCompiland        = $(baseDir)ECObjectsPch.cpp
PchOutputDir        = $(o)
%include $(SharedMki)PreCompileHeader.mki

CCPchOpts           = $(UsePrecompiledHeaderOptions)
CPchOpts            = $(UsePrecompiledHeaderOptions)
```

### 3.3 库定义和链接

```makefile
# 库配置
DLM_NAME            = iTwinECObjects
DLM_DEST            = $(o)
DLM_OBJECT_DEST     = $(o)
DLM_OBJECT_FILES    = $(cppObjects)
DLM_NOINITFUNC      = 1
DLM_NOENTRY         = 1
DLM_NO_BENTLEY_LIB  = 1

# 链接器依赖
LINKER_LIBRARIES    = $(BuildContext)SubParts/Libs/$(libprefix)iTwinBentley$(libext)

# 输出位置
DLM_CONTEXT_LOCATION        = $(BuildContext)Delivery/
DLM_LIB_CONTEXT_LOCATION    = $(BuildContext)Delivery/

# 包含库链接规则
%include $(sharedMki)linkLibrary.mki
```

### 3.4 DLM 变量说明

| 变量 | 用途 |
|------|------|
| `DLM_NAME` | 库/DLL 名称 |
| `DLM_DEST` | 输出目标目录 |
| `DLM_OBJECT_FILES` | 包含的对象文件列表 |
| `DLM_OBJECT_DEST` | 对象文件目标 |
| `DLM_NOINITFUNC` | 无初始化函数 |
| `DLM_NOENTRY` | 无入口点 |
| `DLM_NO_BENTLEY_LIB` | 不自动链接 Bentley 库 |

---

## 4. MKI 文件（包含文件）

### 4.1 包含保护模式

```makefile
%if defined (__ECObjects_mki__)
    %return
%endif

__ECObjects_mki__ = 1
```

### 4.2 目录和路径定义

```makefile
# 构建目录
OutECObjects        = $(OutBuildDir)ECObjects/
buildDir            = $(OutECObjects)
o                   = $(PartBuildDir)

# 源代码目录
ecobjectsSrc        =% $(_CurrentFilePath)../
ecPublicAPISrc      = $(ecobjectsSrc)PublicApi/
```

### 4.3 库名称定义

```makefile
BeSQLiteLib         = $(libprefix)iTwinSQLite$(libext)
ECNativeObjectsLib  = $(libprefix)iTwinECObjects$(libext)
UnitsLib            = $(libprefix)iTwinUnits$(libext)
BentleyGeomLib      = $(libprefix)iTwinGeom$(libext)
```

### 4.4 常用 MKI 文件

| 文件 | 用途 |
|------|------|
| `mdl.mki` | 核心构建系统（外部） |
| `cdefapnd.mki` | 添加预处理器定义 |
| `cincapnd.mki` | 添加包含目录 |
| `linkLibrary.mki` | 库链接规则 |
| `PreCompileHeader.mki` | PCH 支持 |
| `MultiCppCompileRule.mki` | 多文件编译设置 |

---

## 5. 依赖管理

### 5.1 依赖流程（自底向上）

```
第三方库（静态）
    ↓
Bentley（基础工具库）
    ↓
Units, Geom, Xml, Json
    ↓
ECObjects, BeSQLite
    ↓
ECDb, GeoCoord
    ↓
iModelPlatform
    ↓
ECPresentation
    ↓
iModelJsNodeAddon
```

### 5.2 PartFile 中的依赖声明

```xml
<Part Name="iModelPlatformDLL" BentleyBuildMakeFile="iModelPlatform.mke">
    <SubPart PartName="BentleyDll" PartFile="iModelCore/Bentley/Bentley" />
    <SubPart PartName="ECDbLibrary" PartFile="iModelCore/ECDb/ECDb" />
    <SubPart PartName="GeomDlls" PartFile="iModelCore/GeomLibs/geomlibs" />
    <SubPart PartName="ECObjects" PartFile="iModelCore/ecobjects/ECObjects" />
</Part>
```

---

## 6. 目标命名约定

库遵循模式：`iTwin<模块名>`

| 库名 | 说明 |
|------|------|
| `iTwinBentley` | 基础 Bentley 库 |
| `iTwinECObjects` | EC Objects 库 |
| `iTwinPlatform` | iModel 平台库 |
| `iTwinSQLite` | SQLite 包装器 |
| `iTwinGeom` | 几何库 |
| `iTwinCurl` | cURL 包装器 |

---

## 7. 平台条件编译

```makefile
%if $(TARGET_PLATFORM)=="Windows"
    LINKER_LIBRARIES + iphlpapi.lib
    LINKER_LIBRARIES + winhttp.lib
%endif

%if $(TARGET_PLATFORM)!="Android" && $(TARGET_PLATFORM)!="Linux"
    BeSQLiteRequiredLibs + $(ContextSubPartsStaticLibs)$(stlibprefix)proxyres$(stlibext)
%endif
```

---

## 8. 关键构建变量

| 变量 | 说明 |
|------|------|
| `$(_MakeFilePath)` | 当前 makefile 的目录 |
| `$(_MakeFileSpec)` | 当前 makefile 的完整路径 |
| `$(PartBuildDir)` | 当前组件的输出目录 |
| `$(BuildContext)` | 构建上下文根目录 |
| `$(SrcRoot)` | 源代码根目录 |
| `$(SharedMki)` | 共享 mki 文件路径 |
| `$(o)` | 对象输出目录 |
| `$(oext)` | 对象文件扩展名（.obj 或 .o） |

---

## 9. Python 要求

BentleyBuild 需要：
- Python 3.5+（仅限 64 位）
- 必需包：`lxml` (3.0+)、`xxhash` (1.0+)

---

## 10. 构建命令

### Windows
```cmd
cd imodel-native
build\buildwin.bat
```

### Linux
```bash
cd imodel-native
build/buildlinux.sh
```

### macOS
```bash
cd imodel-native
build/buildmac.sh
```

### 构建选项
- `debug=1` - 调试构建
- `PRG=1` - 生产发布（无断言）
- `-a x64` - 指定架构

---

## 11. 总结

BentleyBuild 的主要特点：

1. **关注点分离** - PartFiles 定义结构/依赖，MKE 文件定义编译规则，MKI 文件提供可重用配置

2. **多平台支持** - Windows、Linux、macOS、iOS、Android，每种平台有适当的库类型

3. **复杂依赖管理** - 从基础库到最终产品的清晰依赖链

4. **测试基础设施** - 集成 GTest、JUnit、XCTest 支持

5. **分发支持** - 内置 NuGet 和 UPack 包生成

6. **预编译头** - 提高编译性能

7. **多文件编译** - 并行编译多个源文件
