---
title: "Windows 窗体设计器中的设计时错误 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-winforms"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "DTELErrorList"
  - "WhyDTELPage"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "设计时错误 [Windows 窗体设计器]"
  - "错误 [Windows 窗体设计器]"
ms.assetid: ad408380-825a-46d8-9a4a-531b130b88ce
caps.latest.revision: 16
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 16
---
# Windows 窗体设计器中的设计时错误
本主题说明了在 Windows 窗体设计器无法加载时 Microsoft Visual Studio 中显示的设计时错误列表的含义和使用方法。  如果出现此错误列表，则不应将其理解为设计器中的 Bug，而应作为纠正代码中的错误的辅助手段。  
  
 下面提供了有关错误的详细信息和建议的可行解决方案，通过对此错误列表有一个基本的了解，将有助于您调试应用程序。  
  
## 设计时错误列表界面  
 如果 Windows 窗体设计器无法加载，则设计器中将显示一个错误列表。  错误按类别进行分组。  例如，如果具有四个未声明变量的实例，则这些实例将分组到同一错误类别中。  每个错误类别包含一个对错误进行概述的简短说明。  
  
 通过单击错误类别标题或单击展开\/折叠 V 形按钮，可以展开或折叠错误类别。  当展开错误类别时，将显示以下附加帮助：  
  
-   此错误的实例。  
  
-   有关此错误的帮助。  
  
-   有关此错误的论坛文章。  
  
### 此错误的实例  
 附加帮助列出了当前项目中错误的所有实例。  许多错误包含用以下格式表示的确切位置：*\[项目名称\]* *\[窗体名称\]* 行:*\[行号\]* 列:*\[列号\]*。  单击**“转至代码”**链接将跳转到代码中发生错误的位置。  
  
 如果调用堆栈与错误关联，则可单击**“显示调用堆栈”**链接，这将进一步扩展此错误以显示调用堆栈。  检查堆栈可提供有价值的调试信息。  例如，可以跟踪在错误发生之前调用过的函数。  调用堆栈是可选定的，因此您可以复制并保存它。  
  
> [!NOTE]
>  在 Visual Basic 中，虽然设计时错误列表不会显示多个错误，但它可以显示同一错误的多个实例。  在 Visual C\+\+ 中，错误没有“转至代码”链接\/“行号”链接。  
  
### 有关此错误的帮助  
 如果错误包含一个指向相关 MSDN 帮助主题的链接，则附加帮助将包含一个指向该帮助主题的链接。  当单击该链接时，Visual Studio 中将显示相关帮助主题。  
  
### 有关此错误的论坛文章  
 附加帮助将包含一个指向与该错误相关的 MSDN 论坛文章的链接。  可根据错误消息字符串搜索论坛。  您还可以尝试搜索以下论坛：  
  
-   [Windows Forms Designer Forum](http://go.microsoft.com/fwlink/?LinkId=203524)（Windows 窗体设计器论坛）  
  
-   [Windows Forms Forums](http://go.microsoft.com/fwlink/?LinkId=203523)（Windows 窗体论坛）  
  
### 忽略并继续  
 可以选择忽略错误条件并继续加载设计器。  选择此操作可能会导致意外行为。  例如，控件可能不会显示在设计图面上。  
  
## 请参阅  
 [Troubleshooting Design\-Time Development](../Topic/Troubleshooting%20Design-Time%20Development.md)   
 [控件和组件创作疑难解答](../../../../docs/framework/winforms/controls/troubleshooting-control-and-component-authoring.md)   
 [设计时开发 Windows 窗体控件](../../../../docs/framework/winforms/controls/developing-windows-forms-controls-at-design-time.md)   
 [Windows Forms Designer Error Messages](http://msdn.microsoft.com/zh-cn/cf610bf4-5fe4-471c-bce7-6a05ece07bd2)