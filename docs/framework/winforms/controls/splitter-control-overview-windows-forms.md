---
title: "Splitter 控件概述（Windows 窗体） | Microsoft Docs"
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
  - "Splitter"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "Splitter 控件 [Windows 窗体], 关于 Splitter 控件"
ms.assetid: e2b6ab83-dfdd-40ec-9762-850702c82dcb
caps.latest.revision: 12
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 12
---
# Splitter 控件概述（Windows 窗体）
> [!IMPORTANT]
>  尽管 <xref:System.Windows.Forms.SplitContainer> 替换了早期版本的 <xref:System.Windows.Forms.Splitter> 控件并添加了功能；但是也可选择保留 <xref:System.Windows.Forms.Splitter> 以备向后兼容和将来使用。  
  
 Windows 窗体 <xref:System.Windows.Forms.Splitter> 控件用于在运行时调整停靠控件的大小。  <xref:System.Windows.Forms.Splitter> 控件常用于一类窗体，这类窗体上的控件所显示的数据长度可变，如 Windows 资源管理器，它的数据窗格所包含的信息在不同的时间有不同的宽度。  
  
## 使用 Splitter 控件  
 如果一个控件可由 splitter 控件调整其大小，则当用户将鼠标指针指向该控件的未停靠的边缘时，鼠标指针将更改外观，指示该控件的大小是可以调整的。  使用 splitter 控件，用户可以调整该控件紧前面的停靠控件的大小。  因此，为使用户能够在运行时调整停靠控件的大小，请将要调整大小的控件停靠在容器的一条边缘上，然后将拆分控件停靠在该容器的同一侧。  
  
## 请参阅  
 <xref:System.Windows.Forms.SplitContainer>   
 [如何：在 Windows 窗体上停靠控件](../../../../docs/framework/winforms/controls/how-to-dock-controls-on-windows-forms.md)   
 [在 Windows 窗体上使用的控件](../../../../docs/framework/winforms/controls/controls-to-use-on-windows-forms.md)