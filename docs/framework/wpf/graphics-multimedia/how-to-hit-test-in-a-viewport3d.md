---
title: "如何：在 Viewport3D 中进行命中测试 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-wpf"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "三维可视化效果, 命中测试"
  - "命中测试, 对于三维可视化效果"
  - "Viewport3D"
ms.assetid: 42bfbd99-c7c6-43f1-940b-90448faa412e
caps.latest.revision: 11
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 11
---
# 如何：在 Viewport3D 中进行命中测试
此示例演示如何为 <xref:System.Windows.Controls.Viewport3D> 中的三维视觉效果进行命中测试。  
  
 由于 <xref:System.Windows.Media.VisualTreeHelper.HitTest%2A> 会返回二维和三维信息，所以通过循环访问测试结果以便仅读取三维结果是可能的。  
  
 [!code-csharp[HitTest3D#HitTest3D3DN4](../../../../samples/snippets/csharp/VS_Snippets_Wpf/HitTest3D/CSharp/Window1.xaml.cs#hittest3d3dn4)]
 [!code-vb[HitTest3D#HitTest3D3DN4](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/HitTest3D/visualbasic/window1.xaml.vb#hittest3d3dn4)]  
  
 以下代码中的 <xref:System.Windows.Media.HitTestResultBehavior> 确定如何处理命中测试结果。  `UpdateResultInfo` 和 `UpdateMaterial` 是本地定义的方法。  
  
 [!code-csharp[HitTest3D#HitTest3D3DN5](../../../../samples/snippets/csharp/VS_Snippets_Wpf/HitTest3D/CSharp/Window1.xaml.cs#hittest3d3dn5)]
 [!code-vb[HitTest3D#HitTest3D3DN5](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/HitTest3D/visualbasic/window1.xaml.vb#hittest3d3dn5)]  
  
## 请参阅  
 [3\-D Hit Testing Sample](http://go.microsoft.com/fwlink/?LinkID=159959)