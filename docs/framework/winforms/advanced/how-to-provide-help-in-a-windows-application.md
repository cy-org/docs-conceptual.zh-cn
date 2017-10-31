---
title: "如何：在 Windows 应用程序中提供帮助 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-winforms"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "窗体, 提供帮助"
  - "帮助, Windows 应用程序"
  - "HelpProvider 组件 [Windows 窗体]"
  - "HTML 帮助, Windows 窗体"
  - "Windows 应用程序, 提供帮助"
ms.assetid: 7c4e5cec-2bd2-4f0b-8d75-c2b88929bd61
caps.latest.revision: 10
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 9
---
# 如何：在 Windows 应用程序中提供帮助
使用 <xref:System.Windows.Forms.HelpProvider> 组件，可以将帮助文件中的帮助主题附加到 Windows 窗体的特定控件。  帮助文件可以是 HTML、HTMLHelp 1.x 或更高版本的格式。  
  
> [!NOTE]
>  显示的对话框和菜单命令可能会与“帮助”中的描述不同，具体取决于您现用的设置或版本。  若要更改设置，请在**“工具”**菜单上选择**“导入和导出设置”**。  有关更多信息，请参见 [Customizing Development Settings in Visual Studio](http://msdn.microsoft.com/zh-cn/22c4debb-4e31-47a8-8f19-16f328d7dcd3)。  
  
### 提供帮助  
  
1.  将 <xref:System.Windows.Forms.HelpProvider> 组件从**“工具箱”**拖到窗体上。  
  
     该组件将位于 Windows 窗体设计器底部的栏中。  
  
2.  在**“属性”**窗口中，将 <xref:System.Windows.Forms.HelpProvider.HelpNamespace%2A> 属性设置为 .chm、.col 或 .htm 帮助文件。  
  
3.  选择窗体上的另一个控件，在**“属性”**窗口中设置 [HelpKeyword](frlrfSystemWindowsFormsHelpProviderClassSetHelpKeywordTopic) 属性。  
  
     这是通过 <xref:System.Windows.Forms.HelpProvider> 组件传递给帮助文件的字符串，用于请求相应的“帮助”主题。  
  
4.  在**“属性”**窗口中，将 [HelpNavigator](frlrfSystemWindowsFormsHelpProviderClassSetHelpNavigatorTopic) 属性设置为 <xref:System.Windows.Forms.HelpNavigator> 枚举的值。  
  
     这将确定以何种方式将 **HelpKeyword** 属性传递给帮助系统。  下表显示可能的设置及其说明。  
  
    |成员名称|说明|  
    |----------|--------|  
    |AssociateIndex|指定在指定 URL 中执行指定主题的索引。|  
    |查找|指定显示指定 URL 的搜索页。|  
    |索引|指定显示指定 URL 的索引。|  
    |KeywordIndex|指定要搜索的关键字和要在指定 URL 中采取的操作。|  
    |TableOfContents|指定显示 HTML 1.0 帮助文件的目录。|  
    |主题|指定显示指定 URL 引用的主题。|  
  
 在运行时，如果当已设置 **HelpKeyword** 和 **HelpNavigator** 属性的控件具有焦点时按 F1 键，将打开与 <xref:System.Windows.Forms.HelpProvider> 组件关联的帮助文件。  
  
 目前，**HelpNamespace** 属性支持下列三种格式的帮助文件：HTMLHelp 1.x、HTMLHelp 2.0 和 HTML。  因此，可以将 **HelpNamespace** 属性设置为 http:\/\/ 地址（如网页）。  如果此操作已完成，将打开默认浏览器，并显示作为定位点的**“HelpKeyword”**属性中指定的字符串所对应的网页。  定位点用于跳转到 HTML 页的特定部分。  
  
> [!IMPORTANT]
>  一定要先仔细检查从客户端发来的所有信息，再在应用程序中使用这些信息。  恶意用户可能会尝试发送或注入可执行脚本、SQL 语句或其他代码。  显示用户的输入、将其存储在数据库中或使用它之前，请确定它没有包含可能的不安全信息。  通常的检查方法是在收到某个用户发来的输入后，使用正则表达式查找关键字，如“SCRIPT”。  
  
 还可使用 <xref:System.Windows.Forms.HelpProvider> 组件显示弹出帮助（即使已经将其配置为显示 Windows 窗体上控件的帮助文件）。  有关更多信息，请参见 [如何：显示弹出帮助](../../../../docs/framework/winforms/advanced/how-to-display-pop-up-help.md)。  
  
## 请参阅  
 [如何：显示弹出帮助](../../../../docs/framework/winforms/advanced/how-to-display-pop-up-help.md)   
 [使用工具提示的控件帮助](../../../../docs/framework/winforms/advanced/control-help-using-tooltips.md)   
 [在 Windows 窗体中集成用户帮助](../../../../docs/framework/winforms/advanced/integrating-user-help-in-windows-forms.md)   
 [Windows 窗体](../../../../docs/framework/winforms/index.md)