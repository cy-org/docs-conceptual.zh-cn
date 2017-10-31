---
title: "Windows 窗体可视化继承 | Microsoft Docs"
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
  - "基窗体"
  - "窗体继承"
  - "继承"
  - "继承, 窗体"
  - "继承的窗体"
  - "继承的窗体, Windows 窗体"
  - "Windows 窗体, 继承"
ms.assetid: 857eb737-3602-4d49-bd8b-f70d33ace345
caps.latest.revision: 9
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 9
---
# Windows 窗体可视化继承
有时，您的项目可能需要一个与在以前的项目中创建的窗体类似的窗体。  或者，您可能希望创建一个基本窗体，其中含有您随后将在项目中再次使用的水印或某种控件布局之类的设置，每次重复使用时，都会对该原始窗体模板进行修改。  窗体继承使您得以创建基窗体，然后从其继承并进行修改，同时保留任何需要的原始设置。  
  
 可以编程方式或使用可视化继承选择器创建派生类窗体。  
  
## 本节内容  
 [如何：继承 Windows 窗体](../../../../docs/framework/winforms/advanced/how-to-inherit-windows-forms.md)  
 给出在代码中创建继承的窗体的说明。  
  
 [如何：使用“继承选择器”对话框继承窗体](../../../../docs/framework/winforms/advanced/how-to-inherit-forms-using-the-inheritance-picker-dialog-box.md)  
 给出用继承选择器创建继承的窗体的说明。  
  
 [修改基窗体的外观的效果](../../../../docs/framework/winforms/advanced/effects-of-modifying-base-form-appearance.md)  
 给出更改基窗体的控件及其属性的说明。  
  
 [演练：演示可视化继承](../../../../docs/framework/winforms/advanced/walkthrough-demonstrating-visual-inheritance.md)  
 描述如何创建基 Windows 窗体并将其编译为类库。  可将此类库导入另一个项目中，并创建一个从该基窗体继承的新窗体。  
  
 [如何：使用 Modifiers 和 GenerateMember 属性](../../../../docs/framework/winforms/advanced/how-to-use-the-modifiers-and-generatemember-properties.md)  
 提供有关如何使用 `GenerateMember` 和 `Modifiers` 属性的说明，当 Windows 窗体设计器为组件生成成员变量时会涉及这些属性。  
  
## 相关章节  
 [NOT IN BUILD: Inheritance in Visual Basic](http://msdn.microsoft.com/zh-cn/e5e6e240-ed31-4657-820c-079b7c79313c)  
 描述如何定义作为其他类的基础的 Visual Basic 类。  
  
 [类](../Topic/class%20\(C%23%20Reference\).md)  
 描述类的 C\# 方法，在此方法中允许单个继承。  
  
 [有关 Visual Basic 中继承的事件处理程序的疑难解答](../Topic/Troubleshooting%20Inherited%20Event%20Handlers%20in%20Visual%20Basic.md)  
 列出了由继承的组件中的事件处理程序引发的常见问题