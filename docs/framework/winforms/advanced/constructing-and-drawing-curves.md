---
title: "构造并绘制曲线 | Microsoft Docs"
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
  - "曲线, 绘图"
  - "绘图, 曲线"
  - "示例 [Windows 窗体], 绘制曲线"
ms.assetid: 76e92623-4130-4644-b867-faca58bdb3a2
caps.latest.revision: 14
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 14
---
# 构造并绘制曲线
[!INCLUDE[ndptecgdiplus](../../../../includes/ndptecgdiplus-md.md)] 支持多种类型的曲线：椭圆、弧形、基数样条和贝塞尔样条。  椭圆是由其边框定义的；弧是椭圆的一部分，由一个起始角和一个扫描角定义。  基数样条由一系列点和张力参数定义，即曲线平滑地通过系列中的每个点，张力参数影响曲线的弯曲方式。  贝塞尔样条由两个端点和两个控制点定义，即该曲线不通过控制点，但是控制点影响曲线从一个端点到另一个端点时的方向和弯曲程度。  
  
## 本节内容  
 [如何：绘制基数样条曲线](../../../../docs/framework/winforms/advanced/how-to-draw-cardinal-splines.md)  
 描述基数样条以及如何绘制基数样条。  
  
 [如何：绘制单个贝塞尔样条](../../../../docs/framework/winforms/advanced/how-to-draw-a-single-bezier-spline.md)  
 描述贝塞尔样条以及如何绘制贝塞尔样条。  
  
 [如何：绘制贝塞尔样条序列](../../../../docs/framework/winforms/advanced/how-to-draw-a-sequence-of-bezier-splines.md)  
 解释如何按顺序绘制贝塞尔样条。