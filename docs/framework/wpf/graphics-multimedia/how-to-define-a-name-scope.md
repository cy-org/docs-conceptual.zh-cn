---
title: "如何：定义名称范围 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-wpf"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "动画, 情节提要, 在程序代码中"
  - "名称范围, 定义"
  - "情节提要, 在程序代码中进行动画处理"
ms.assetid: 4f361925-6a08-40dc-8231-a61111c6b28b
caps.latest.revision: 6
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 6
---
# 如何：定义名称范围
若要在代码中使用 <xref:System.Windows.Media.Animation.Storyboard> 进行动画处理，必须创建一个 <xref:System.Windows.NameScope>，并将目标对象的名称注册到拥有该名称范围的元素。  在下面的示例中，为 `myMainPanel` 创建 <xref:System.Windows.NameScope>。  将 `button1` 和 `button2` 两个按钮添加到面板中并注册其名称。  创建多个动画和一个 <xref:System.Windows.Media.Animation.Storyboard>。  使用此演示图板的 <xref:System.Windows.Media.Animation.Storyboard.Begin%2A> 方法来启动动画。  
  
 由于 `button1`、`button2` 和 `myMainPanel` 都共享同一个名称范围，因此可以将其中的任何一个与 <xref:System.Windows.Media.Animation.Storyboard> <xref:System.Windows.Media.Animation.Storyboard.Begin%2A> 方法结合使用来启动动画。  
  
## 示例  
 [!code-csharp[StoryboardBeginAnimation_procedural_snip#NameScopeExample](../../../../samples/snippets/csharp/VS_Snippets_Wpf/StoryboardBeginAnimation_procedural_snip/CSharp/ScopeExample.cs#namescopeexample)]
 [!code-vb[StoryboardBeginAnimation_procedural_snip#NameScopeExample](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/StoryboardBeginAnimation_procedural_snip/visualbasic/scopeexample.vb#namescopeexample)]  
  
## 请参阅  
 [使用演示图板对属性进行动画处理](../../../../docs/framework/wpf/graphics-multimedia/how-to-animate-a-property-by-using-a-storyboard.md)   
 [动画概述](../../../../docs/framework/wpf/graphics-multimedia/animation-overview.md)