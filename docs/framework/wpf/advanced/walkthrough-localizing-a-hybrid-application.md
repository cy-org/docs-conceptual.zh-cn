---
title: "演练：本地化混合应用程序 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-wpf"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "混合应用程序 [WPF 互操作性]"
  - "本地化 [WPF 互操作性]"
ms.assetid: fbc0c54e-930a-4c13-8e9c-27b83665010a
caps.latest.revision: 17
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 14
---
# 演练：本地化混合应用程序
本演练演示如何在基于 [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)]的混合应用程序中本地化 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 元素。  
  
 本演练涉及以下任务：  
  
-   创建 [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)]宿主项目。  
  
-   添加可本地化的内容。  
  
-   启用本地化。  
  
-   分配资源标识符。  
  
-   使用 LocBaml 工具生成附属程序集。  
  
 有关本演练中所阐释任务的完整代码清单，请参见 [Localizing a Hybrid Application Sample](http://go.microsoft.com/fwlink/?LinkID=160015)（本地化混合应用程序示例）。  
  
 在完成本演练后，您将具有一个本地化的混合应用程序。  
  
## 系统必备  
 您需要以下组件来完成本演练：  
  
-   [!INCLUDE[vs_orcas_long](../../../../includes/vs-orcas-long-md.md)].  
  
## 创建 Windows 窗体宿主项目  
 第一步是创建 [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)]应用程序项目并添加一个包含要本地化的内容的 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 元素。  
  
#### 创建宿主项目  
  
1.  创建一个名为 `LocalizingWpfInWf` 的 WPF 应用程序项目。  有关更多信息，请参见[How to: Create a Windows Application Project](http://msdn.microsoft.com/zh-cn/b2f93fed-c635-4705-8d0e-cf079a264efa)。  
  
2.  向该项目添加一个名为 `SimpleControl` 的 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] <xref:System.Windows.Controls.UserControl> 元素。  
  
3.  使用 <xref:System.Windows.Forms.Integration.ElementHost> 控件在窗体上放置一个 `SimpleControl` 元素。  有关更多信息，请参见[演练：在 Windows 窗体中承载 3\-D WPF 复合控件](../../../../docs/framework/wpf/advanced/walkthrough-hosting-a-3-d-wpf-composite-control-in-windows-forms.md)。  
  
## 添加可本地化的内容  
 下一步，您将添加一个 [!INCLUDE[TLA#tla_winforms](../../../../includes/tlasharptla-winforms-md.md)]标签控件，并将 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 元素的内容设置为可本地化的字符串。  
  
#### 添加可本地化的内容  
  
1.  在解决方案资源管理器中双击**“SimpleControl.xaml”**，以便在 [!INCLUDE[wpfdesigner_current_short](../../../../includes/wpfdesigner-current-short-md.md)]中将其打开。  
  
2.  使用以下代码示设置 <xref:System.Windows.Controls.Button> 控件的内容。  
  
     [!code-xml[LocalizingWpfInWf#10](../../../../samples/snippets/csharp/VS_Snippets_Wpf/LocalizingWpfInWf/CSharp/SimpleControl0.xaml#10)]  
  
3.  在解决方案资源管理器中，双击**“Form1”**在 Windows 窗体设计器中打开它。  
  
4.  打开工具箱，并双击**“标签”**向窗体中添加一个标签控件。  将其 <xref:System.Windows.Forms.Control.Text%2A> 属性的值设置为 `"Hello"`。  
  
5.  按 F5 生成并运行该应用程序。  
  
     `SimpleControl` 元素和该标签控件都会显示文本 **"Hello"**。  
  
## 启用本地化  
 Windows 窗体设计器提供了用于在附属程序集中启用本地化的设置。  
  
#### 启用本地化  
  
1.  在解决方案资源管理器中，双击**“Form1.cs”**在 Windows 窗体设计器中打开它。  
  
2.  在“属性”窗口中，将该窗体的**“Localizable”**属性值设置为 `true`。  
  
3.  在“属性”窗口中，将**“Language”**属性的值设置为**“西班牙语\(西班牙\)”**。  
  
4.  在 Windows 窗体设计器中，选择该标签控件。  
  
5.  在“属性”窗口中，将 <xref:System.Windows.Forms.Control.Text%2A> 属性的值设置为 `"Hola"`。  
  
     此时，名为“Form1.es\-ES.resx”的新资源会添加到该项目中。  
  
6.  在解决方案资源管理器中，右击**“Form1.cs”**，然后单击**“查看代码”**在代码编辑器中打开它。  
  
7.  将下面的代码复制到 `Form1` 构造函数，然后调用 `InitializeComponent`。  
  
     [!code-csharp[LocalizingWpfInWf#2](../../../../samples/snippets/csharp/VS_Snippets_Wpf/LocalizingWpfInWf/CSharp/Form1.cs#2)]  
  
8.  在解决方案资源管理器中，右击**“LocalizingWpfInWf”**，然后单击**“卸载项目”**。  
  
     此时，该项目名称会被标记为**“\(不可用\)”**。  
  
9. 右击**“LocalizingWpfInWf”**，然后单击**“编辑 LocalizingWpfInWf.csproj”**。  
  
     此时，该项目文件会在代码编辑器中打开。  
  
10. 将下面一行复制到该项目文件中的第一个 `PropertyGroup`。  
  
    ```  
    <UICulture>en-US</UICulture>   
    ```  
  
11. 保存该项目文件，然后将其关闭。  
  
12. 在解决方案资源管理器中，右击**“LocalizingWpfInWf”**，然后单击**“重新加载项目”**。  
  
## 分配资源标识符  
 您可以使用资源标识符将可本地化的内容映射到资源程序集。  当指定 `updateuid` 选项时，MsBuild.exe 应用程序会自动分配资源标识符。  
  
#### 分配资源标识符  
  
1.  从“开始”菜单中打开 [!INCLUDE[vsprvs](../../../../includes/vsprvs-md.md)] 命令提示窗口。  
  
2.  使用以下命令将资源标识符分配给可本地化的内容。  
  
    ```  
    msbuild /t:updateuid LocalizingWpfInWf.csproj  
    ```  
  
3.  在解决方案资源管理器中，双击**“SimpleControl.xaml”**在代码编辑器中打开它。  此时，您会看到 `msbuild` 命令已将 `Uid` 特性添加到所有元素中。  这通过分配资源标识符，简化了本地化操作。  
  
     [!code-xml[LocalizingWpfInWf#20](../../../../samples/snippets/csharp/VS_Snippets_Wpf/LocalizingWpfInWf/CSharp/SimpleControl.xaml#20)]  
  
4.  按 F6 键生成解决方案。  
  
## 使用 LocBaml 工具生成附属程序集  
 本地化内容存储在一个纯资源附属程序集中。  使用命令行工具 LocBaml.exe 为 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 内容生成本地化程序集。  
  
#### 生成附属程序集  
  
1.  将 LocBaml.exe 复制到您项目的 obj\\Debug 文件夹中。  有关更多信息，请参见[对应用程序进行本地化](../../../../docs/framework/wpf/advanced/how-to-localize-an-application.md)。  
  
2.  在命令提示窗口中，使用以下命令将资源字符串提取到一个临时文件中。  
  
    ```  
    LocBaml /parse LocalizingWpfInWf.g.en-US.resources /out:temp.csv  
    ```  
  
3.  使用 [!INCLUDE[vsprvs](../../../../includes/vsprvs-md.md)] 或其他文本编辑器打开 temp.csv 文件。  将字符串 `"Hello"` 替换为其西班牙语的翻译 `"Hola"`。  
  
4.  保存 temp.csv 文件。  
  
5.  使用以下命令生成本地化资源文件。  
  
    ```  
    LocBaml /generate /trans:temp.csv LocalizingWpfInWf.g.en-US.resources /out:. /cul:es-ES  
    ```  
  
     在 obj\\Debug 文件夹中创建 LocalizingWpfInWf.g.es\-ES.resources 文件。  
  
6.  使用以下命令生成本地化附属程序集。  
  
    ```  
    Al.exe /out:LocalizingWpfInWf.resources.dll /culture:es-ES /embed:LocalizingWpfInWf.Form1.es-ES.resources /embed:LocalizingWpfInWf.g.es-ES.resources  
    ```  
  
     在 obj\\Debug 文件夹中创建 LocalizingWpfInWf.resources.dll 文件。  
  
7.  将 LocalizingWpfInWf.resources.dll 文件复制到该项目的 bin\\Debug\\es\-ES 文件夹中。  替换现有文件。  
  
8.  运行 LocalizingWpfInWf.exe，该文件位于该项目的 bin\\Debug 文件夹中。  不要重新生成将被覆盖的应用程序或附属程序集。  
  
     此时，应用程序会显示本地化字符串，而不是英语字符串。  
  
## 请参阅  
 <xref:System.Windows.Forms.Integration.ElementHost>   
 <xref:System.Windows.Forms.Integration.WindowsFormsHost>   
 [对应用程序进行本地化](../../../../docs/framework/wpf/advanced/how-to-localize-an-application.md)   
 [Walkthrough: Localizing Windows Forms](http://msdn.microsoft.com/zh-cn/9a96220d-a19b-4de0-9f48-01e5d82679e5)   
 [WPF 设计器](http://msdn.microsoft.com/zh-cn/c6c65214-8411-4e16-b254-163ed4099c26)