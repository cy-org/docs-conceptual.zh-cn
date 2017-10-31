---
title: "如何：向 Windows 窗体添加 ActiveX 控件 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-winforms"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "ActiveX 控件 [Windows 窗体], 添加"
  - "窗体, 添加 ActiveX 控件"
  - "Windows 窗体控件, ActiveX 控件"
ms.assetid: 54a61e5b-555e-4887-b41e-6244fed271eb
caps.latest.revision: 10
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 10
---
# 如何：向 Windows 窗体添加 ActiveX 控件
虽然 Windows 窗体设计器是为了承载 Windows 窗体控件而优化，但您也可以将 ActiveX 控件放在 Windows 窗体上。  
  
> [!CAUTION]
>  将 ActiveX 控件添加到 Windows 窗体时，对于 Windows 窗体有一些性能限制。  
  
 在将 ActiveX 控件添加到窗体之前，必须将其添加到“工具箱”中。  有关更多信息，请参见[“自定义工具箱”对话框 \-\>“COM 组件”](http://msdn.microsoft.com/zh-cn/171333f3-f207-4e02-bbdc-17862556212c)。  
  
> [!NOTE]
>  显示的对话框和菜单命令可能会与“帮助”中的描述不同，具体取决于您现用的设置或版本。  若要更改设置，请单击**“工具”**菜单上的**“导入和导出设置”**。  有关更多信息，请参见 [Customizing Development Settings in Visual Studio](http://msdn.microsoft.com/zh-cn/22c4debb-4e31-47a8-8f19-16f328d7dcd3)。  
  
### 向 Windows 窗体添加 ActiveX 控件  
  
-   在“工具箱”上双击该控件。  
  
     [!INCLUDE[vsprvs](../../../../includes/vsprvs-md.md)] 将对该控件的所有引用都添加到项目中。  有关使用 Windows 窗体上的 ActiveX 控件时需要注意的事项的更多信息，请参见[在 Windows 窗体上承载 ActiveX 控件时的注意事项](../../../../docs/framework/winforms/controls/considerations-when-hosting-an-activex-control-on-a-windows-form.md)。  
  
    > [!NOTE]
    >  Windows 窗体 ActiveX 控件导入程序 \(AxImp.exe\) 创建的事件参数的类型不同于导入 ActiveX 动态链接库时所需的事件参数类型。  AxImp.exe 创建的参数类似于：`Invoke(object sender, DWebBrowserEvents2_ProgressChangeEvent e)`，而所需参数为 `Invoke(object sender, DWebBrowserEvents2_ProgressChangeEventArgs e)`。  注意，这种不正常情况并不影响代码的正常使用。  有关详细信息，请参见 [Windows 窗体 ActiveX 控件导入程序 \(Aximp.exe\)](../../../../docs/framework/tools/aximp-exe-windows-forms-activex-control-importer.md)。  
  
## 请参阅  
 [Windows 窗体控件](../../../../docs/framework/winforms/controls/index.md)   
 [Controls and Programmable Objects Compared in Various Languages and Libraries](http://msdn.microsoft.com/zh-cn/021f2a1b-8247-4348-a5ad-e1d9ab23004b)   
 [如何：向 Windows 窗体添加控件](../../../../docs/framework/winforms/controls/how-to-add-controls-to-windows-forms.md)   
 [排列 Windows 窗体上的控件](../../../../docs/framework/winforms/controls/arranging-controls-on-windows-forms.md)   
 [标记单个 Windows 窗体控件并提供它们的快捷方式](../../../../docs/framework/winforms/controls/labeling-individual-windows-forms-controls-and-providing-shortcuts-to-them.md)   
 [在 Windows 窗体上使用的控件](../../../../docs/framework/winforms/controls/controls-to-use-on-windows-forms.md)   
 [根据功能列出的 Windows 窗体控件](../../../../docs/framework/winforms/controls/windows-forms-controls-by-function.md)