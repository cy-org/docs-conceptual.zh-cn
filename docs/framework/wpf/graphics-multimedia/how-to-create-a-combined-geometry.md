---
title: "如何：创建组合的几何图形 | Microsoft Docs"
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
  - "组合几何图形"
  - "几何图形, 组合"
  - "图形, 组合几何图形"
ms.assetid: 54c3277c-6b6e-4b25-91be-fda0bbc706b4
caps.latest.revision: 8
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 8
---
# 如何：创建组合的几何图形
此示例演示如何组合几何图形。  若要组合两个几何图形，请使用 <xref:System.Windows.Media.CombinedGeometry> 对象。  对要组合的两个几何图形，设置该对象的 <xref:System.Windows.Media.CombinedGeometry.Geometry1%2A> 和 <xref:System.Windows.Media.CombinedGeometry.Geometry2%2A> 属性，并将 <xref:System.Windows.Media.CombinedGeometry.GeometryCombineMode%2A> 属性（确定如何将这两个几何图形组合在一起）设置为 `Union`、`Intersect`、`Exclude` 或 `Xor`。  
  
 若要通过两个或两个以上的几何图形创建复合几何图形，可使用 <xref:System.Windows.Media.GeometryGroup>。  
  
## 示例  
 在下面的示例中，用 `Exclude` 几何图形组合模式定义了一个 <xref:System.Windows.Media.CombinedGeometry>。  <xref:System.Windows.Media.CombinedGeometry.Geometry1%2A> 和 <xref:System.Windows.Media.CombinedGeometry.Geometry2%2A> 定义为相同半径的圆，但是中心偏离 50。  
  
 [!code-xml[GeometrySample#21](../../../../samples/snippets/csharp/VS_Snippets_Wpf/GeometrySample/CS/combininggeometriesexample.xaml#21)]  
  
 ![“排除”组合模式的结果](../../../../docs/framework/wpf/graphics-multimedia/media/mil-task-combined-geometry-exclude.png "mil\_task\_combined\_geometry\_exclude")  
使用 Exclude 模式组合的几何图形  
  
 在下面的标记中，用 `Intersect` 组合模式定义了一个 <xref:System.Windows.Media.CombinedGeometry>。  <xref:System.Windows.Media.CombinedGeometry.Geometry1%2A> 和 <xref:System.Windows.Media.CombinedGeometry.Geometry2%2A> 定义为相同半径的圆，但是中心偏离 50。  
  
 [!code-xml[GeometrySample#22](../../../../samples/snippets/csharp/VS_Snippets_Wpf/GeometrySample/CS/combininggeometriesexample.xaml#22)]  
  
 ![“相交”组合模式的结果](../../../../docs/framework/wpf/graphics-multimedia/media/mil-task-combined-geometry-intersect.png "mil\_task\_combined\_geometry\_intersect")  
使用 Intersect 模式组合的几何图形  
  
 在下面的标记中，用 `Union` 组合模式定义了一个 <xref:System.Windows.Media.CombinedGeometry>。  <xref:System.Windows.Media.CombinedGeometry.Geometry1%2A> 和 <xref:System.Windows.Media.CombinedGeometry.Geometry2%2A> 定义为相同半径的圆，但是中心偏离 50。  
  
 [!code-xml[GeometrySample#23](../../../../samples/snippets/csharp/VS_Snippets_Wpf/GeometrySample/CS/combininggeometriesexample.xaml#23)]  
  
 ![“联合”组合模式的结果](../../../../docs/framework/wpf/graphics-multimedia/media/mil-task-combined-geometry-union.png "mil\_task\_combined\_geometry\_union")  
使用 Union 模式组合的几何图形  
  
 在下面的标记中，用 `Xor` 组合模式定义了一个 <xref:System.Windows.Media.CombinedGeometry>。  <xref:System.Windows.Media.CombinedGeometry.Geometry1%2A> 和 <xref:System.Windows.Media.CombinedGeometry.Geometry2%2A> 定义为相同半径的圆，但是中心偏离 50。  
  
 [!code-xml[GeometrySample#24](../../../../samples/snippets/csharp/VS_Snippets_Wpf/GeometrySample/CS/combininggeometriesexample.xaml#24)]  
  
 ![Xor 组合模式的结果](../../../../docs/framework/wpf/graphics-multimedia/media/mil-task-combined-geometry-xor.png "mil\_task\_combined\_geometry\_xor")  
使用 Xor 模式组合的几何图形