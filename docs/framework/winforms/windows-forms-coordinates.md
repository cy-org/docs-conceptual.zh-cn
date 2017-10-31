---
title: "Windows 窗体坐标 | Microsoft Docs"
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
  - "工作区坐标"
  - "坐标, Windows 窗体"
  - "屏幕坐标"
  - "Windows 窗体坐标"
ms.assetid: cc06e61f-43b6-4408-a676-2542dcfcd96e
caps.latest.revision: 5
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 5
---
# Windows 窗体坐标
Windows 窗体的坐标系基于设备坐标，在 Windows 窗体中绘制时的基本量度单位是设备单位（通常为像素）。  屏幕上的点通过 x 和 y 坐标对描述，x 坐标向右递增，y 坐标从上往下递增。  原点相对于屏幕的位置因指定的是屏幕坐标还是工作区坐标而异。  
  
## 屏幕坐标  
 Windows 窗体应用程序用屏幕坐标指定窗口在屏幕上的位置。  对于屏幕坐标而言，原点是屏幕的左上角。  窗口的完整位置通常用 <xref:System.Drawing.Rectangle> 结构来描述，该结构包含定义窗口的左上角和右下角的两个点的屏幕坐标。  
  
## 工作区坐标  
 Windows 窗体应用程序使用工作区坐标指定窗体或控件中的点的位置。  工作区坐标的原点是控件或窗体的工作区的左上角。  工作区坐标确保了无论窗体或控件在屏幕上的位置如何，应用程序在窗体或控件中绘制期间都可以使用一致的坐标值。  
  
 工作区的尺寸也用 <xref:System.Drawing.Rectangle> 结构来描述，该结构包含该区域的工作区坐标。  在所有情况下，矩形的左上角坐标都包含在工作区中，而右下角坐标则排除在工作区之外。  图形操作不包括工作区的右边缘和下边缘。  例如，<xref:System.Drawing.Graphics.FillRectangle%2A> 方法将一直填充到指定矩形的右边缘和下边缘，但是不包括这两条边。  
  
## 从一类坐标映射到另一类坐标  
 您可能偶尔需要从屏幕坐标映射到工作区坐标。  通过使用 <xref:System.Windows.Forms.Control> 类中的 <xref:System.Windows.Forms.Control.PointToClient%2A> 和 <xref:System.Windows.Forms.Control.PointToScreen%2A> 方法，可以轻松实现这一映射。  例如，<xref:System.Windows.Forms.Control> 的 <xref:System.Windows.Forms.Control.MousePosition%2A> 属性用屏幕坐标报告，但是您可能想将它们转换成工作区坐标。  
  
## 请参阅  
 <xref:System.Windows.Forms.Control.PointToClient%2A>   
 <xref:System.Windows.Forms.Control.PointToScreen%2A>