---
title: "如何：向墨迹数据添加自定义数据 | Microsoft Docs"
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
  - "墨迹数据, 添加自定义数据"
  - "InkCanvas, 显示"
ms.assetid: f02aac6f-3436-4f7c-b6ea-0452cba5332c
caps.latest.revision: 5
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 5
---
# 如何：向墨迹数据添加自定义数据
您可以向墨迹添加自定义数据，在将墨迹另存为墨迹序列化格式 \(ISF\) 时将保存自定义数据。  您可以将自定义数据保存到 <xref:System.Windows.Ink.DrawingAttributes>、<xref:System.Windows.Ink.StrokeCollection> 或 <xref:System.Windows.Ink.Stroke> 中。  由于能够在三个对象上保存自定义数据，因此，您可以决定保存数据的最佳位置。  所有这三个类均使用类似的方法来存储和访问自定义数据。  
  
 只有以下类型的数据可以另存为自定义数据：  
  
-   <xref:System.Boolean>  
  
-   <xref:System.Boolean>\[\]  
  
-   <xref:System.Byte>  
  
-   <xref:System.Byte>\[\]  
  
-   <xref:System.Char>  
  
-   <xref:System.Char>\[\]  
  
-   <xref:System.DateTime>  
  
-   <xref:System.DateTime>\[\]  
  
-   <xref:System.Decimal>  
  
-   <xref:System.Decimal>\[\]  
  
-   <xref:System.Double>  
  
-   <xref:System.Double>\[\]  
  
-   <xref:System.Int16>  
  
-   <xref:System.Int16>\[\]  
  
-   <xref:System.Int32>  
  
-   <xref:System.Int32>\[\]  
  
-   <xref:System.Int64>  
  
-   <xref:System.Int64>\[\]  
  
-   <xref:System.Single>  
  
-   <xref:System.Single>\[\]  
  
-   <xref:System.String>  
  
-   <xref:System.UInt16>  
  
-   <xref:System.UInt16>\[\]  
  
-   <xref:System.UInt32>  
  
-   <xref:System.UInt32>\[\]  
  
-   <xref:System.UInt64>  
  
-   <xref:System.UInt64>\[\]  
  
## 示例  
 下面的示例演示如何添加和检索 <xref:System.Windows.Ink.StrokeCollection> 中的自定义数据。  
  
 [!code-csharp[HowToAddCustomDataToInk#1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/HowToAddCustomDataToInk/CSharp/Window1.xaml.cs#1)]  
  
 下面的示例创建了一个显示 <xref:System.Windows.Controls.InkCanvas> 和两个按钮的应用程序。  `switchAuthor` 按钮使两个不同的作者能够各用一枝笔。  `changePenColors` 按钮可以按作者来更改 <xref:System.Windows.Controls.InkCanvas> 上每个笔画的颜色。  此应用程序定义了两个 <xref:System.Windows.Ink.DrawingAttributes> 对象，并向每个对象添加了一个自定义属性以指明是哪个作者绘制了 <xref:System.Windows.Ink.Stroke>。  当用户单击 `changePenColors` 时，应用程序将按照自定义属性的值来更改笔画的外观。  
  
 [!code-xml[HowToAddCustomDataToInk#2](../../../../samples/snippets/csharp/VS_Snippets_Wpf/HowToAddCustomDataToInk/CSharp/Window1.xaml#2)]  
  
 [!code-csharp[HowToAddCustomDataToInk#3](../../../../samples/snippets/csharp/VS_Snippets_Wpf/HowToAddCustomDataToInk/CSharp/Window1.xaml.cs#3)]