---
title: "dotnet migrate 命令 - .NET Core CLI"
description: "dotnet migrate 命令可迁移项目及其所有依赖项。"
author: mairaw
ms.author: mairaw
ms.date: 08/14/2017
ms.topic: article
ms.prod: .net-core
ms.technology: dotnet-cli
ms.translationtype: HT
ms.sourcegitcommit: a19ab54a6cc44bd7acd1e40a4ca94da52bf14297
ms.openlocfilehash: 674b19f9fc546e057c7b7fa4b024a0b013eda7e5
ms.contentlocale: zh-cn
ms.lasthandoff: 08/14/2017

---
# <a name="dotnet-migrate"></a>dotnet migrate

[!INCLUDE [topic-appliesto-net-core-all](../../../includes/topic-appliesto-net-core-all.md)]

## <a name="name"></a>名称

`dotnet migrate` - 将预览版 2 .NET Core 项目迁移到 .NET Core SDK 1.0 项目。

## <a name="synopsis"></a>摘要

`dotnet migrate [<SOLUTION_FILE|PROJECT_DIR>] [-t|--template-file] [-v|--sdk-package-version] [-x|--xproj-file] [-s|--skip-project-references] [-r|--report-file] [--format-report-file-json] [--skip-backup] [-h|--help]`

## <a name="description"></a>描述

`dotnet migrate` 命令将有效的基于预览版 2 *project.json* 的项目迁移到有效的 .NET Core SDK 1.0 *csproj* 项目。 

默认情况下，命令迁移根项目和根项目包含的任何项目引用。 在运行时使用 `--skip-project-references` 选项禁用此行为。 

在以下情况下执行迁移：

* 通过指定 *project.json* 文件进行迁移的单个项目。
* 通过将路径传递到 *global.json* 文件在 *global.json* 文件中指定的所有目录。
* 一个 *solution.sln* 文件，它迁移在解决方案中引用的项目。
* 以递归方式迁移给定目录的所有子目录。

`dotnet migrate` 命令将迁移的 *project.json* 文件保存在 `backup` 目录中，如果该目录不存在，将创建一个。 使用 `--skip-backup` 选项重写此行为。

默认情况下，迁移操作会将迁移过程的状态输出到标准输出 (STDOUT)。 如果使用 `--report-file <REPORT_FILE>` 选项，输出将保存到指定的文件中。 

`dotnet migrate` 命令仅支持有效的预览版 2 基于 *project.json* 的项目。 这意味着，不能使用它将 DNX 或预览版 1 基于 *project.json* 的项目直接迁移到 MSBuild/csproj 项目。 首先需要将项目手动迁移到预览版 2 基于 *project.json* 的项目，然后使用 `dotnet migrate` 命令迁移该项目。

## <a name="arguments"></a>参数

`PROJECT_JSON/GLOBAL_JSON/SOLUTION_FILE/PROJECT_DIR`

下列路径之一：

* 要迁移的 *project.json* 文件。
* *global.json*文件，用于迁移 *global.json* 中指定的文件夹。
* *solution.sln* 文件，它将迁移解决方案中引用的项目。
* 要迁移的目录，它将以递归方式搜索要迁移的 *project.json* 文件。

如未指定，则默认为当前目录。

## <a name="options"></a>选项

`-h|--help`

打印出有关命令的简短帮助。

`-t|--template-file <TEMPLATE_FILE>`

用于迁移的模板 csproj 文件。 默认情况下，使用与被 `dotnet new console` 删除的模板相同的模板。

`-v|--sdk-package-version <VERSION>`

在已迁移应用中将被引用的 sdk 包的版本。 默认为 `dotnet new` 中 SDK 的版本。

`-x|--xproj-file <FILE>`

要使用的 xproj 文件的路径。 当项目目录中有多个 xproj 时需要。

`-s|--skip-project-references [Debug|Release]`

跳过迁移项目引用。 默认情况下，以递归方式迁移项目引用。

`-r|--report-file <REPORT_FILE>`

除控制台外，还将迁移报告输出到文件。

`--format-report-file-json <REPORT_FILE>`

将迁移报告文件（而非用户消息）作为 JSON 输出。

`--skip-backup`

在成功迁移后，跳过将 *project.json*、*global.json* 和 *\*.xproj* 移动到 `backup` 目录的步骤。

## <a name="examples"></a>示例

将当前目录中的项目及其所有项目迁移到项目依赖项：

`dotnet migrate`

迁移 *global.json* 文件所包含的所有项目：

`dotnet migrate path/to/global.json`

仅迁移当前项目，不迁移项目到项目 (P2P) 的依赖项。 此外，使用特定的 SDK 版本：

`dotnet migrate -s -v 1.0.0-preview4`
