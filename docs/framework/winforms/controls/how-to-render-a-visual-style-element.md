---
title: "如何：呈现视觉样式元素 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-winforms"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "专业外观, 应用于 Windows 窗体应用程序的元素"
  - "视觉样式, 呈现“Windows 窗体”控件"
  - "直观主题, 应用于 Windows 窗体应用程序的元素"
ms.assetid: a207781b-1baa-4ce9-b788-1e951bd4b5df
caps.latest.revision: 9
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 9
---
# 如何：呈现视觉样式元素
<xref:System.Windows.Forms.VisualStyles?displayProperty=fullName> 命名空间公开了表示由视觉样式支持的 Windows 用户界面 \(UI\) 元素的 <xref:System.Windows.Forms.VisualStyles.VisualStyleElement> 对象。  本主题演示如何使用 <xref:System.Windows.Forms.VisualStyles.VisualStyleRenderer> 类呈现表示“开始”菜单中的**“注销”**和**“关机”**按钮的 <xref:System.Windows.Forms.VisualStyles.VisualStyleElement>。  
  
### 呈现视觉样式元素  
  
1.  创建一个 <xref:System.Windows.Forms.VisualStyles.VisualStyleRenderer> 并将其设置为您想绘制的元素。  请注意 <xref:System.Windows.Forms.Application.RenderWithVisualStyles%2A?displayProperty=fullName> 属性和 <xref:System.Windows.Forms.VisualStyles.VisualStyleRenderer.IsElementDefined%2A?displayProperty=fullName> 方法的使用；如果视觉样式被禁用或某个元素未定义，则 <xref:System.Windows.Forms.VisualStyles.VisualStyleRenderer.%23ctor%2A> 构造函数将引发异常。  
  
     [!code-cpp[System.Windows.Forms.VisualStyles.VisualStyleRenderer_Simple#4](../../../../samples/snippets/cpp/VS_Snippets_Winforms/System.Windows.Forms.VisualStyles.VisualStyleRenderer_Simple/cpp/form1.cpp#4)]
     [!code-csharp[System.Windows.Forms.VisualStyles.VisualStyleRenderer_Simple#4](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.VisualStyles.VisualStyleRenderer_Simple/CS/form1.cs#4)]
     [!code-vb[System.Windows.Forms.VisualStyles.VisualStyleRenderer_Simple#4](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.VisualStyles.VisualStyleRenderer_Simple/VB/form1.vb#4)]  
  
2.  调用 <xref:System.Windows.Forms.VisualStyles.VisualStyleRenderer.DrawBackground%2A> 方法呈现 <xref:System.Windows.Forms.VisualStyles.VisualStyleRenderer> 当前所表示的元素。  
  
     [!code-cpp[System.Windows.Forms.VisualStyles.VisualStyleRenderer_Simple#6](../../../../samples/snippets/cpp/VS_Snippets_Winforms/System.Windows.Forms.VisualStyles.VisualStyleRenderer_Simple/cpp/form1.cpp#6)]
     [!code-csharp[System.Windows.Forms.VisualStyles.VisualStyleRenderer_Simple#6](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.VisualStyles.VisualStyleRenderer_Simple/CS/form1.cs#6)]
     [!code-vb[System.Windows.Forms.VisualStyles.VisualStyleRenderer_Simple#6](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.VisualStyles.VisualStyleRenderer_Simple/VB/form1.vb#6)]  
  
## 编译代码  
 此示例需要：  
  
-   派生自 <xref:System.Windows.Forms.Control> 类的自定义控件。  
  
-   承载该自定义控件的 <xref:System.Windows.Forms.Form>。  
  
-   对 <xref:System?displayProperty=fullName>、<xref:System.Drawing?displayProperty=fullName>、<xref:System.Windows.Forms?displayProperty=fullName> 和 <xref:System.Windows.Forms.VisualStyles?displayProperty=fullName> 命名空间的引用。  
  
## 请参阅  
 [使用视觉样式呈现控件](../../../../docs/framework/winforms/controls/rendering-controls-with-visual-styles.md)