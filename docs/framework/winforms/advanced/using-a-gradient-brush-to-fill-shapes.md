---
title: "使用渐变画笔填充形状 | Microsoft Docs"
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
  - "画笔, 渐变画刷"
  - "示例 [Windows 窗体], 渐变画刷"
  - "渐变画刷"
ms.assetid: 2c6037b9-05bd-44c0-a22a-19584b722524
caps.latest.revision: 11
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 11
---
# 使用渐变画笔填充形状
可借助渐变画笔用渐变的颜色填充形状。  例如，可借助水平渐变画笔，从形状的左边缘到右边缘用逐渐变化的颜色来填充形状。  设想这样一个矩形：它的左边缘为黑色（红色、绿色和蓝色分量均为 0）；右边为红色（这三个分量分别为 255，0，0）。  如果矩形的宽度为 256 个像素，则给定像素的红色分量将多于其左侧的像素的红色分量。  在一行中，最左边像素的颜色分量为 \(0, 0, 0\)；第二个像素的分量为 \(1, 0, 0\)；第三个为 \(2, 0, 0\)，依此类推，直到到达最右边的像素，它的分量为 \(255, 0, 0\)。  这些插值颜色的值构成了颜色渐变。  
  
 当水平地、垂直地或平行一指定的斜线移动到时，线性渐变改变颜色。  当在轨迹的内部和边界来回移动时，轨迹渐变改变颜色。  可自定义轨迹渐变以获得多种效果。  
  
 下面的插图显示用线性渐变画笔填充矩形，用路径渐变画笔填充椭圆。  
  
 ![渐变](../../../../docs/framework/winforms/advanced/media/gradient2.png "gradient2")  
  
## 本节内容  
 [如何：创建线性渐变](../../../../docs/framework/winforms/advanced/how-to-create-a-linear-gradient.md)  
 演示如何使用 <xref:System.Drawing.Drawing2D.LinearGradientBrush> 类创建线性渐变。  
  
 [如何：创建路径渐变](../../../../docs/framework/winforms/advanced/how-to-create-a-path-gradient.md)  
 描述如何使用 <xref:System.Drawing.Drawing2D.PathGradientBrush> 类创建路径渐变。  
  
 [如何：对渐变应用灰度校正](../../../../docs/framework/winforms/advanced/how-to-apply-gamma-correction-to-a-gradient.md)  
 解释如何将灰度校正用于渐变画笔。  
  
## 参考  
 <xref:System.Drawing.Drawing2D.LinearGradientBrush?displayProperty=fullName>  
 包含此类的说明和指向其所有成员的链接。  
  
 <xref:System.Drawing.Drawing2D.PathGradientBrush?displayProperty=fullName>  
 包含此类的说明和指向其所有成员的链接。