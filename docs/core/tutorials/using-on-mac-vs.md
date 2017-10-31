---
title: "借助 Visual Studio for Mac 在 macOS 上开始使用.NET Core"
description: "本主题将指导你使用 Visual Studio for Mac 和 .NET Core 来构建简单的控制台应用程序。"
keywords: .NET, .NET Core, macOS, Mac
author: guardrex
ms.author: mairaw
ms.date: 06/12/2017
ms.topic: get-started-article
ms.prod: .net-core
ms.devlang: dotnet
ms.assetid: 8902e849-dd17-42c0-8264-cc7ae3927a0c
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: e11515031716a66ead866e52504137cb4e1df137
ms.contentlocale: zh-cn
ms.lasthandoff: 07/28/2017

---

# <a name="getting-started-with-net-core-on-macos-using-visual-studio-for-mac"></a>借助 Visual Studio for Mac 在 macOS 上开始使用.NET Core

Visual Studio for Mac 提供用于开发 .NET Core 应用程序的功能全面的集成开发环境 (IDE)。 本主题将指导你使用 Visual Studio for Mac 和 .NET Core 来构建简单的控制台应用程序。

> [!NOTE]
> 你的反馈非常有价值。 有两种方法可以向开发团队提供有关 Visual Studio for Mac 的反馈：
> * 在 Visual Studio for Mac 中，从菜单中选择“帮助” > “报告问题”，或从欢迎屏幕中选择“报告问题”，将打开一个窗口，以供填写 bug 报告。 可在[开发人员社区](https://developercommunity.visualstudio.com/spaces/8/index.html)门户中跟踪自己的反馈。
> * 若要提出建议，从菜单中选择“帮助” > “提供建议”，或从欢迎屏幕中选择“提供建议”，转到 [Visual Studio for Mac UserVoice 网页](https://visualstudio.uservoice.com/forums/563332-visual-studio-for-mac)。

## <a name="prerequisites"></a>先决条件

请参阅 [Mac 上 .NET Core 的先决条件](../../core/macos-prerequisites.md)主题。

## <a name="getting-started"></a>入门

如果已安装先决条件和 Visual Studio for Mac，请跳过此部分，并继续[创建项目](#creating-a-project)。 请按照以下步骤安装先决条件和 Visual Studio for Mac：

下载 [Visual Studio for Mac 安装程序](https://www.visualstudio.com/vs/visual-studio-mac/)。 运行安装程序。 阅读并同意许可协议。 在安装过程中，为你提供安装 Xamarin（一个跨平台移动应用开发技术）的机会。 安装 Xamarin 及其相关组件对于 .NET Core 开发而言是可选项。 有关 Visual Studio for Mac 安装过程的分步介绍，请参阅 [Visual Studio for Mac 简介](https://developer.xamarin.com/guides/cross-platform/visual-studio-mac/)。 安装完成后，启动 Visual Studio for Mac IDE。

## <a name="creating-a-project"></a>创建项目

1. 选择欢迎屏幕上的“新建项目”。

   ![Visual Studio for Mac 欢迎屏幕上的新建项目按钮](./media/using-on-mac-vs/vsmac1.png)

1. 在“新建项目”对话框中，选择“.NET Core”节点下的“应用”。 单击“下一步”，然后选择“控制台应用程序”模板。

   ![新项目模板列表](./media/using-on-mac-vs/vsmac2.png)

1. 为“项目名称”键入“HelloWorld”。 选择“创建”。

   ![配置新的控制台应用程序对话框](./media/using-on-mac-vs/vsmac3.png)

1. 等待还原项目的依赖项。 该项目包含一个 C# 文件 *Program.cs*，其中包含具有 `Main` 方法的 `Program` 类。 运行应用时，`Console.WriteLine` 语句将“Hello World!” 输出至控制台。

   ![打开 Program.cs 文件的主窗口](./media/using-on-mac-vs/vsmac4.png)

## <a name="run-the-application"></a>运行此应用程序

使用 <kbd>F5</kbd> 在调试模式下运行此应用，或使用 <kbd>Ctrl</kbd>+<kbd>F5</kbd> 在发布模式下运行此应用。

![应用程序输出窗格显示 Hello World!](./media/using-on-mac-vs/vsmac5.png)

## <a name="next-step"></a>下一步

[使用 Visual Studio for Mac 在 macOS 上构建完整的 .NET Core 解决方案](using-on-mac-vs-full-solution.md)主题为你演示如何构建包含可重用的库和单元测试的完整的 .NET Core 解决方案。

