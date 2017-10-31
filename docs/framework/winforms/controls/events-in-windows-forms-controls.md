---
title: "Windows 窗体控件中的事件 | Microsoft Docs"
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
  - "自定义控件 [Windows 窗体], 事件概述（使用代码）"
  - "事件 [Windows 窗体], 自定义控件（使用代码）"
ms.assetid: 7e3d1379-87aa-437c-afce-c99454eff30e
caps.latest.revision: 8
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 8
---
# Windows 窗体控件中的事件
Windows 窗体控件从 <xref:System.Windows.Forms.Control?displayProperty=fullName> 继承了六十多个事件。  其中包括 <xref:System.Windows.Forms.Control.Paint> 事件（将引起控件的绘制）、与显示窗口相关的事件（如 <xref:System.Windows.Forms.Control.Resize> 和 <xref:System.Windows.Forms.Control.Layout> 事件）以及低级别的鼠标和键盘事件。  某些低级别事件通过 <xref:System.Windows.Forms.Control> 合成为语义事件（如 <xref:System.Windows.Forms.Control.Click> 和 <xref:System.Windows.Forms.Control.DoubleClick>）。  有关继承的事件的详细信息，请参见 <xref:System.Windows.Forms.Control>。  
  
 如果您的自定义控件需要重写所继承的事件功能，则将重写所继承的 `On`*事件名称* 方法，而不是附加委派。  如果不熟悉 .NET Framework 中的事件模型，请参见 [从组件引发事件](../Topic/Raising%20Events%20from%20a%20Component.md)。  
  
## 请参阅  
 [重写 OnPaint 方法](../../../../docs/framework/winforms/controls/overriding-the-onpaint-method.md)   
 [处理用户输入](../../../../docs/framework/winforms/controls/handling-user-input.md)   
 [定义事件](../../../../docs/framework/winforms/controls/defining-an-event-in-windows-forms-controls.md)   
 [事件](../../../../docs/standard/events/index.md)