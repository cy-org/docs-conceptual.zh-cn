---
title: "组织项目以支持 .NET Framework 和 .NET Core"
description: "帮助希望针对 .NET Framework 和 .NET Core 并行编译解决方案的项目所有者。"
keywords: ".NET, .NET Core, .NET Framework, 项目布局, 多个框架"
author: conniey
ms.author: mairaw
ms.date: 04/06/2017
ms.topic: article
ms.prod: .net-core
ms.devlang: dotnet
ms.assetid: 3af62252-1dfa-4336-8d2f-5cfdb57d7724
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: 93bec65e3bbee93855d6f5bce5e2d6cea8bb9f3d
ms.contentlocale: zh-cn
ms.lasthandoff: 08/11/2017

---

# <a name="organizing-your-project-to-support-net-framework-and-net-core"></a>组织项目以支持 .NET Framework 和 .NET Core

本文旨在帮助希望针对 .NET Framework 和 .NET Core 并行编译解决方案的项目所有者。 它提供了多个可组织项目的选项以帮助开发人员实现此目标。 下列列表提供了一些在决定如何使用 .NET Core 设置项目时需考虑的典型方案。 此列表可能无法涵盖所有要求；这些方案的优先级具体取决于项目需求。

* [**将现有项目和 .NET Core 项目合并为单个项目**][option-csproj]

  *此方案的好处：*
  * 通过编译单个项目（而非多个项目）简化生成过程，每个项目针对不同的 .NET Framework 版本或平台。
  * 由于需要管理单个项目文件，因此简化了多目标项目的源文件管理。 添加/删除源文件时，需要手动将备用文件与其他项目进行同步。
  * 轻松生成可供使用的 NuGet 包。
  * 允许通过使用编译器指令为库中特定的 .NET Framework 版本编写代码。

  *不支持的方案：*
  * 要求开发者使用 Visual Studio 2017 来打开现有项目。 若要支持 Visual Studio 的早期版本，建议[将项目文件保存在不同的文件夹中](#support-vs)。

* <a name="support-vs"></a>[**将现有项目和新的 .NET Core 项目分离**][option-csproj-folder]

  *此方案的好处：*
  * 继续支持现有项目的开发，而无需为没有安装 Visual Studio 2017 的开发人员/参与者进行升级。
  * 减少现有项目中出现新 bug 的可能性，因为这些项目中不需要进行任何代码改动。

## <a name="example"></a>示例

请考虑以下存储库：

![现有项目][example-initial-project]

[**源代码**][example-initial-project-code]

根据现有项目的约束和复杂性，有几种不同的方法可为此存储库添加对 .NET Core 的支持，下面描述了这些方法。

## <a name="replace-existing-projects-with-a-multi-targeted-net-core-project"></a>将现有项目替换为多目标的 .NET Core 项目

重新组织存储库，以便删除任何现有的 \*.csproj 文件，并创建以多个框架为目标的单一 \*.csproj 文件。 这是一项不错的选择，因为单个项目可以编译不同的框架。 它还可以处理每个目标框架的不同编译选项和依赖项。

![创建以多个框架为目标的 csproj][example-csproj]

[**源代码**][example-csproj-code]

需注意的更改：
* 用新的 [.NET Core *\*.csproj*][example-csproj-netcore] 替换 packages.config 和 \*.csproj。 NuGet 包是使用 `<PackageReference> ItemGroup` 指定的。

## <a name="keep-existing-projects-and-create-a-net-core-project"></a>保留现有项目并创建 .NET Core 项目

如果存在以较旧框架为目标的现有项目，可能需要保留这些项目并将 .NET Core 项目用作将来框架的目标。

![不同文件夹中包含现有项目的 .NET Core 项目][example-csproj-different-folder]

[**源代码**][example-csproj-different-code]

需注意的更改：
* 将 .NET Core 项目和现有项目保存在不同的文件夹中。
    * 将项目保存在不同的文件夹中可以避免强制使用 Visual Studio 2017。 可以创建仅打开旧项目的单独解决方案。

## <a name="see-also"></a>另请参阅

有关迁移到 .NET Core 的详细指南，请参阅 [.NET Core 移植文档][porting-doc]。

[porting-doc]: index.md
[example-initial-project]: media/project-structure/project.png "现有项目"
[example-initial-project-code]: https://github.com/dotnet/docs/tree/master/samples/framework/libraries/migrate-library/

[example-csproj]: media/project-structure/project.csproj.png "创建以多个框架为目标的 csproj"
[example-csproj-code]: https://github.com/dotnet/docs/tree/master/samples/framework/libraries/migrate-library-csproj/
[example-csproj-netcore]: https://github.com/dotnet/docs/tree/master/samples/framework/libraries/migrate-library-csproj/src/Car/Car.csproj

[example-csproj-different-folder]: media/project-structure/project.csproj.different.png "不同文件夹中包含现有 PCL 的 .NET Core 项目"
[example-csproj-different-code]: https://github.com/dotnet/docs/tree/master/samples/framework/libraries/migrate-library-csproj-keep-existing/

[option-csproj]: #replace-existing-projects-with-a-multi-targeted-net-core-project
[option-csproj-folder]: #keep-existing-projects-and-create-a-net-core-project

