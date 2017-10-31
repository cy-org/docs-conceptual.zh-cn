---
title: "如何：使用设计器添加或移除 ImageList 图像 | Microsoft Docs"
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
  - "ImageList 组件 [Windows 窗体], 添加图像"
  - "ImageList 组件 [Windows 窗体], 移除图像"
  - "图像 [Windows 窗体], 添加到 ImageList 组件"
ms.assetid: 5699b244-e37c-4d20-bc35-7441e55c1e3a
caps.latest.revision: 7
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 7
---
# 如何：使用设计器添加或移除 ImageList 图像
可以采用几种不同的方式向 <xref:System.Windows.Forms.ImageList> 组件添加图像。  您可以通过使用与 <xref:System.Windows.Forms.ImageList> 关联的智能标记快速添加图像，如果正在设置 <xref:System.Windows.Forms.ImageList> 的其他几个属性，您或许会发现通过“属性”窗口添加图像更方便。  还可以通过使用代码来添加图像。  有关如何通过代码添加图像的更多信息，请参见 [如何：使用 Windows 窗体 ImageList 组件添加或移除图像](../../../../docs/framework/winforms/controls/how-to-add-or-remove-images-with-the-windows-forms-imagelist-component.md)。  通常会在 <xref:System.Windows.Forms.ImageList> 组件与控件关联之前为该组件填充图像，但这不是必需的。  
  
> [!NOTE]
>  显示的对话框和菜单命令可能会与“帮助”中的描述不同，具体取决于您现用的设置或版本。  若要更改设置，请在**“工具”**菜单上选择**“导入和导出设置”**。  有关更多信息，请参见 [Customizing Development Settings in Visual Studio](http://msdn.microsoft.com/zh-cn/22c4debb-4e31-47a8-8f19-16f328d7dcd3)。  
  
### 使用“属性”窗口添加或移除图像  
  
1.  选择 <xref:System.Windows.Forms.ImageList> 组件，或向窗体添加一个。  
  
2.  在“属性”窗口中，单击 <xref:System.Windows.Forms.ImageList.Images%2A> 属性旁的省略号按钮 \(![VisualStudioEllipsesButton 屏幕快照](../../../../docs/framework/winforms/media/vbellipsesbutton.png "vbEllipsesButton")\)。  
  
3.  在**“Image 集合编辑器”**中，单击**“添加”**或**“移除”**来添加或从列表中移除图像。  
  
### 使用智能标记添加或移除图像  
  
1.  选择 <xref:System.Windows.Forms.ImageList> 组件，或向窗体添加一个。  
  
2.  单击智能标记标志符号 \(![智能标记标志符号](../../../../docs/framework/winforms/controls/media/vs-winformsmttagglyph.png "VS\_WinFormSmtTagGlyph")\)  
  
3.  在**“ImageList 任务”**对话框中，选择**“选择图像”**。  
  
4.  在**“Images 集合编辑器”**中，单击**“添加”**或**“移除”**来添加或从列表中移除图像。  
  
## 请参阅  
 [图像、位图和图元文件](../../../../docs/framework/winforms/advanced/images-bitmaps-and-metafiles.md)   
 [演练：使用 Windows 窗体控件上的智能标记执行常规任务](../../../../docs/framework/winforms/controls/performing-common-tasks-using-smart-tags-on-wf-controls.md)   
 [ImageList 组件](../../../../docs/framework/winforms/controls/imagelist-component-windows-forms.md)