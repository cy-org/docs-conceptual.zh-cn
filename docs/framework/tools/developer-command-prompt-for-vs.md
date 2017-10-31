---
title: "Visual Studio 开发人员命令提示"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology:
- dotnet-clr
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- command prompt, Windows SDK
- Visual Studio command prompt
- command prompt, Visual Studio
- SDK command prompt
- tools [.NET Framework], setting environment variables
- environment variables, setting for tools
- developer command prompt
ms.assetid: 94fcf524-9045-4993-bfb2-e2d8bad44219
caps.latest.revision: 45
author: mairaw
ms.author: mairaw
manager: wpickett
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: 0287c3f250a57f7a685191702be3ad5cc28fbec6
ms.contentlocale: zh-cn
ms.lasthandoff: 07/28/2017

---
# <a name="developer-command-prompt-for-visual-studio"></a>Visual Studio 开发人员命令提示
Visual Studio 开发人员命令提示会自动设置环境变量，这些变量使你能够轻松使用 .NET Framework 工具。 安装完整版或社区版 Visual Studio 时会安装开发人员命令提示。 安装 Express 版 Visual Studio 时不会安装。  
  
<a name="find"></a>   
## <a name="searching-for-the-command-prompt-on-your-machine"></a>在计算机中搜索命令提示  
 你可能会看到多个命令提示，具体取决于你安装的 Visual Studio 及其他任何 SDK 的版本。 例如，Visual Studio 的 64 位版本同时提供 32 位和 64 位命令提示。 （大多数工具的 32 位和 64 位版本都相同；但少数工具针对具体的 32 位和 64 位环境做了一些改变。）如果以下步骤不起作用，可以尝试[在计算机中手动查找文件](#alternative)或[从 Visual Studio 内部运行命令提示](#visualstudio)。  
  
 **在 Windows 10 中**  
  
1.  通过按键盘上的 Windows 徽标键 ![Windows 徽标](../../../docs/framework/get-started/media/windowskeyboardlogo.png "Windowskeyboardlogo")（举例说明），打开“开始”菜单。  
  
2.  在“开始”菜单上，输入 `dev`。 此时将显示一个列表，其中包含与搜索模式匹配的已安装应用程序。 如果要查找不同的命令提示，请尝试输入不同的搜索词，例如 `prompt`。  
  
3.  选择“开发人员命令提示”（或者你想使用的命令提示）。  
  
 **在 Windows 8.1 中**  
  
1.  通过按键盘上的 Windows 徽标键 ![Windows 徽标](../../../docs/framework/get-started/media/windowskeyboardlogo.png "Windowskeyboardlogo")（举例说明），转到“开始”屏幕。  
  
2.  在“开始”屏幕上，按 `CTRL + TAB` 打开“应用”列表，然后输入 `V`。 此时将显示一个列表，其中包含所有已安装的 Visual Studio 命令提示。  
  
3.  选择“开发人员命令提示”（或者你想使用的命令提示）。  
  
 **在 Windows 8 中**  
  
1.  通过按键盘上的 Windows 徽标键 ![Windows 徽标](../../../docs/framework/get-started/media/windowskeyboardlogo.png "Windowskeyboardlogo")（举例说明），转到“开始”屏幕。  
  
2.  在“开始”屏幕上，按 Windows 徽标键 ![Windows 徽标](../../../docs/framework/get-started/media/windowskeyboardlogo.png "Windowskeyboardlogo") `+ Z`。  
  
3.  选择屏幕底部的“应用视图”图标，然后输入 `V`。 此时将显示一个列表，其中包含所有已安装的 Visual Studio 命令提示。  
  
4.  选择“开发人员命令提示”（或者你想使用的命令提示）。  
  
 **在 Windows 7 中**  
  
1.  选择“开始”，展开“所有程序”，然后展开“Microsoft Visual Studio”。  
  
2.  根据已安装的 Visual Studio 版本，选择“Visual Studio Tools”、“Visual Studio 命令提示”或你想使用的命令提示。  
  
 如果安装了 [Windows SDK](http://msdn.microsoft.com/windows/desktop/aa904949) 或 [Windows Phone SDK](https://dev.windowsphone.com/downloadsdk)，则可能会看到 ARM、x86 或 x64 体系结构的其他命令提示。 查看单个工具的文档，以确定应使用哪个版本的命令提示。  
  
<a name="alternative"></a>   
## <a name="manually-locating-the-files-on-your-machine"></a>在计算机中手动查找文件  
  已安装的命令提示的快捷方式通常放在 Visual Studio 的“Start Menu”文件夹中，例如 C:\ProgramData\Microsoft\Windows\Start Menu\Programs\Visual Studio 2015\Visual Studio Tools。    但是如果出于某种原因，搜索命令提示未产生预期的效果，你可以尝试在计算机中手动查找快捷方式，以便使用该快捷方式。   请尝试搜索命令提示文件的名称，例如 VsDevCmd.bat，或者转到 Tools 文件夹，例如 C:\Program Files (x86)\Microsoft Visual Studio 14.0\Common7\Tools（该路径将根据你的 Visual Studio 版本和安装位置而变化）。  
  
<a name="visualstudio"></a>   
## <a name="running-command-prompt-from-inside-visual-studio"></a>从 Visual Studio 内部运行命令提示  
 为便于访问，你可以将 Visual Studio 开发人员命令提示或其他任何命令提示添加到 Visual Studio 的“工具”菜单中，方法是将其添加到外部工具列表中。 下面说明了如何实现此操作：  
  
1.  打开 Visual Studio。  
  
2.  选择“工具”菜单并选择“外部工具...”。  
  
3.  在“外部工具”对话框中，选择“添加”按钮。 随即出现一个新项  
  
4.  为新菜单项输入“标题”，例如 `Command Prompt`。  
  
5.  在“命令”字段中，指定要启动的文件，例如 `%comspec%` 或 `C:\Windows\System32\cmd.exe`。  
  
6.  在“参数”字段中，指定可在其中找到要使用的特定命令提示的位置，例如 `/k "C:\Program Files (x86)\Microsoft Visual Studio 14.0\Common7\Tools\VsDevCmd.bat"`（这将启动随 [!INCLUDE[vs_dev14](../../../includes/vs-dev14-md.md)] 一起安装的开发人员命令提示）。 此值需根据 Visual Studio 版本和安装位置进行更改。  
  
7.  为“初始目录”字段选择一个值，例如“项目目录”。  
  
8.  选择“确定”  按钮。  
  
 完成这些步骤后，系统会添加新的菜单项，你可以从“工具”菜单访问命令提示。  
  
## <a name="see-also"></a>另请参阅  
 [工具](../../../docs/framework/tools/index.md)   
 [管理外部工具](/visualstudio/ide/managing-external-tools)

