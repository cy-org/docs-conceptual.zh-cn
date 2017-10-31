---
title: "使用双缓冲 | Microsoft Docs"
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
  - "缓冲, 双缓冲"
  - "双缓冲"
  - "闪烁, 在 Windows 窗体中减少"
  - "图形, 双缓冲"
ms.assetid: dc484e33-7101-4e4b-ada5-d3c96155fbcd
caps.latest.revision: 6
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 6
---
# 使用双缓冲
可以在包含复杂绘制操作的应用程序中使用双缓冲图形减少闪烁。  .NET Framework 包含对双缓冲的内置支持，或是您可以手动管理和呈现图形。  
  
## 本节内容  
 [双缓冲图形](../../../../docs/framework/winforms/advanced/double-buffered-graphics.md)  
 介绍双缓冲概念并概述 .NET Framework 支持。  
  
 [如何：通过对窗体和控件使用双缓冲来减少图形闪烁](../../../../docs/framework/winforms/advanced/how-to-reduce-graphics-flicker-with-double-buffering-for-forms-and-controls.md)  
 演示如何使用 .NET Framework 中的默认双缓冲支持。  
  
 [如何：手动管理缓冲图形](../../../../docs/framework/winforms/advanced/how-to-manually-manage-buffered-graphics.md)  
 演示如何在应用程序中管理双缓冲。  
  
 [如何：手动呈现缓冲图形](../../../../docs/framework/winforms/advanced/how-to-manually-render-buffered-graphics.md)  
 演示如何呈现双缓冲图形。  
  
## 参考  
 <xref:System.Windows.Forms.Control.SetStyle%2A> ,  
 用于启用双缓冲的控制方法。  
  
 <xref:System.Drawing.BufferedGraphicsContext> ,  
 提供创建图形缓冲的方法。  
  
 <xref:System.Drawing.BufferedGraphicsManager>  
 提供对应用程序域的缓冲图形上下文的访问。