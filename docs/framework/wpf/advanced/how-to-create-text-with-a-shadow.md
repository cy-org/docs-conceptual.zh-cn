---
title: "如何：创建具有阴影的文本 | Microsoft Docs"
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
  - "文本中的阴影效果"
  - "文本, 带有阴影的"
  - "版式, 阴影效果"
ms.assetid: 6ab9c754-6001-4708-b479-5367f2fd1a35
caps.latest.revision: 22
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 19
---
# 如何：创建具有阴影的文本
本节中的示例演示如何为所显示的文本创建阴影效果。  
  
## 示例  
 使用 <xref:System.Windows.Media.Effects.DropShadowEffect> 对象，可以为 [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] 对象创建各种投影效果。  下面的示例演示应用于文本的投影效果。  在本例中，阴影是柔和阴影，这表示阴影的颜色发生模糊。  
  
 ![Softness 为 0.25 的文本阴影](../../../../docs/framework/wpf/advanced/media/shadowtext01.png "ShadowText01")  
具有柔和阴影的文本的示例  
  
 可以通过设置 <xref:System.Windows.Media.Effects.DropShadowEffect.ShadowDepth%2A> 属性来控制阴影的宽度。  值 `4.0` 指示阴影的宽度为 4 个像素。  可以通过修改 <xref:System.Windows.Media.Effects.DropShadowEffect.BlurRadius%2A> 属性来控制阴影的柔和程度或模糊程度。  值 `0.0` 指示无模糊。  下面的代码示例演示如何创建柔和阴影效果。  
  
 [!code-xml[TextShadowSnippets#TextShadowSnippet1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/TextShadowSnippets/CS/SingleShadows.xaml#textshadowsnippet1)]  
  
> [!NOTE]
>  这些柔和效果不通过 [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] 文本呈现管道。  因此，在使用这些效果时，ClearType 处于禁用状态。  
  
 下面的示例演示应用于文本的强烈投影效果。  在本例中，阴影不模糊。  
  
 ![Softness 为 0 的文本阴影](../../../../docs/framework/wpf/advanced/media/shadowtext02.png "ShadowText02")  
具有强烈阴影的文本的示例  
  
 可以通过将 <xref:System.Windows.Media.Effects.DropShadowEffect.BlurRadius%2A> 属性设置为 `0.0`（这表示不使用阴影）来创建强烈阴影效果。  可以通过修改 <xref:System.Windows.Media.Effects.DropShadowEffect.Direction%2A> 属性来控制阴影的方向。  将该属性的方向值设置为 `0` 和 `360` 之间的度数。  下图显示了 <xref:System.Windows.Media.Effects.DropShadowEffect.Direction%2A> 属性设置的方向值。  
  
 ![阴影的 DropShadow 程度设置](../../../../docs/framework/wpf/advanced/media/shadowtext08.png "ShadowText08")  
DropShadow 方向关系图  
  
 下面的代码示例演示如何创建强烈阴影效果。  
  
 [!code-xml[TextShadowSnippets#TextShadowSnippet2](../../../../samples/snippets/csharp/VS_Snippets_Wpf/TextShadowSnippets/CS/SingleShadows.xaml#textshadowsnippet2)]  
  
## 使用模糊效果  
 <xref:System.Windows.Media.Effects.BlurBitmapEffect> 可用于创建可放置在文本对象后面的类似于阴影的效果。  应用于文本的模糊位图效果会使文本在各个方向上均匀地产生模糊效果。  
  
 下面的示例演示应用于文本的模糊效果。  
  
 ![使用 BlurBitmapEffect 的文本阴影](../../../../docs/framework/wpf/advanced/media/shadowtext06.png "ShadowText06")  
具有模糊效果的文本的示例  
  
 下面的代码示例演示如何创建模糊效果。  
  
 [!code-xml[TextShadowSnippets#TextShadowSnippet6](../../../../samples/snippets/csharp/VS_Snippets_Wpf/TextShadowSnippets/CS/BlurShadows.xaml#textshadowsnippet6)]  
  
## 使用转换变换  
 <xref:System.Windows.Media.TranslateTransform> 可用来创建可放置在文本对象后面的类似于阴影的效果。  
  
 下面的代码示例使用 <xref:System.Windows.Media.TranslateTransform> 来偏移文本。  在本示例中，原始文本下方略微偏移的文本副本产生了阴影效果。  
  
 ![使用 TranslateTransform 的文本阴影](../../../../docs/framework/wpf/advanced/media/shadowtext07.png "ShadowText07")  
针对阴影效果使用转换功能的文本的示例  
  
 下面的代码示例演示如何为阴影效果创建转换。  
  
 [!code-xml[TextShadowSnippets#TextShadowSnippet7](../../../../samples/snippets/csharp/VS_Snippets_Wpf/TextShadowSnippets/CS/TransformShadows.xaml#textshadowsnippet7)]