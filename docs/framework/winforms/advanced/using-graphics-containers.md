---
title: "使用图形容器 | Microsoft Docs"
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
  - "示例 [Windows 窗体], 图形容器"
  - "图形容器"
  - "图形, 使用容器"
ms.assetid: 74632f91-cefa-4f51-ab7c-f9ac91942caf
caps.latest.revision: 9
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 9
---
# 使用图形容器
<xref:System.Drawing.Graphics> 对象提供了诸如 <xref:System.Drawing.Graphics.DrawLine%2A>、<xref:System.Drawing.Graphics.DrawImage%2A> 和 <xref:System.Drawing.Graphics.DrawString%2A> 之类的显示矢量图像、光栅图像和文本的方法。  <xref:System.Drawing.Graphics> 对象还具有几个影响所绘制项的质量和方向的属性。  例如，平滑模式属性确定是否对直线和曲线应用 Antialias，世界变换属性影响所绘制项目的位置和旋转。  
  
 <xref:System.Drawing.Graphics> 对象与特定的显示设备相关联。  使用 <xref:System.Drawing.Graphics> 对象在窗口中绘图时，<xref:System.Drawing.Graphics> 对象还与该特定的窗口相关联。  
  
 <xref:System.Drawing.Graphics> 对象可被视为容器，因为它包含一组影响绘图的属性并且与设备特定的信息相链接。  通过调用该 <xref:System.Drawing.Graphics> 对象的 <xref:System.Drawing.Graphics.BeginContainer%2A> 方法可以在现有的 <xref:System.Drawing.Graphics> 对象中创建一个辅助容器。  
  
## 本节内容  
 [管理 Graphics 对象的状态](../../../../docs/framework/winforms/advanced/managing-the-state-of-a-graphics-object.md)  
 描述如何管理 <xref:System.Drawing.Graphics> 对象的质量设置、剪辑区域和变形。  
  
 [使用嵌套的 Graphics 容器](../../../../docs/framework/winforms/advanced/using-nested-graphics-containers.md)  
 演示如何使用容器控制 <xref:System.Drawing.Graphics> 对象的状态。