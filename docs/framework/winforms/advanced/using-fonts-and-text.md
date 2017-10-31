---
title: "使用字体和文本 | Microsoft Docs"
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
  - "示例 [Windows 窗体], 字体和文本"
  - "字体, 在 Windows 窗体中使用"
  - "GDI, 绘制文本 [Windows 窗体]"
  - "字符串 [Windows 窗体], 在 Windows 窗体中绘制"
  - "文本 [Windows 窗体], 在 Windows 窗体中绘制"
ms.assetid: d43640f3-da94-4df2-a29d-a9d021a1c069
caps.latest.revision: 16
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 16
---
# 使用字体和文本
[!INCLUDE[ndptecgdiplus](../../../../includes/ndptecgdiplus-md.md)] 和 [!INCLUDE[ndptecgdi](../../../../includes/ndptecgdi-md.md)] 提供了多个类用于在 Windows 窗体上绘制文本。  [!INCLUDE[ndptecgdiplus](../../../../includes/ndptecgdiplus-md.md)] <xref:System.Drawing.Graphics> 类有多个可用于指定文本的各种特征（如位置、边框、字体和格式）的 <xref:System.Drawing.Graphics.DrawString%2A> 方法。  此外，通过 [!INCLUDE[ndptecgdi](../../../../includes/ndptecgdi-md.md)]，可以使用 `TextRenderer` 类提供的 <xref:System.Windows.Forms.TextRenderer.DrawText%2A> 和 <xref:System.Windows.Forms.TextRenderer.MeasureText%2A> 静态方法绘制和测量文本。  [!INCLUDE[ndptecgdi](../../../../includes/ndptecgdi-md.md)] 方法还允许您指定位置、字体和格式。  可以选择 [!INCLUDE[ndptecgdi](../../../../includes/ndptecgdi-md.md)] 或 [!INCLUDE[ndptecgdiplus](../../../../includes/ndptecgdiplus-md.md)] 来进行文本呈现；但是 [!INCLUDE[ndptecgdi](../../../../includes/ndptecgdi-md.md)] 通常能够提供更好的性能和更精确的文本测量。  涉及文本呈现的其他类包括 `FontFamily`、`Font`、<xref:System.Drawing.StringFormat> 和 `TextFormatFlags`。  
  
## 本节内容  
 [如何：构造字体系列和字体](../../../../docs/framework/winforms/advanced/how-to-construct-font-families-and-fonts.md)  
 演示如何创建 `Font` 和 `FontFamily` 对象。  
  
 [如何：在指定位置绘制文本](../../../../docs/framework/winforms/advanced/how-to-draw-text-at-a-specified-location.md)  
 描述如何使用 [!INCLUDE[ndptecgdiplus](../../../../includes/ndptecgdiplus-md.md)] 和 [!INCLUDE[ndptecgdi](../../../../includes/ndptecgdi-md.md)] 在特定位置上绘制文本。  
  
 [如何：在矩形中绘制换行文本](../../../../docs/framework/winforms/advanced/how-to-draw-wrapped-text-in-a-rectangle.md)  
 说明如何使用 [!INCLUDE[ndptecgdiplus](../../../../includes/ndptecgdiplus-md.md)] 和 [!INCLUDE[ndptecgdi](../../../../includes/ndptecgdi-md.md)] 在矩形中绘制文本。  
  
 [如何：用 GDI 绘制文本](../../../../docs/framework/winforms/advanced/how-to-draw-text-with-gdi.md)  
 演示如何使用 [!INCLUDE[ndptecgdi](../../../../includes/ndptecgdi-md.md)] 绘制文本。  
  
 [如何：对齐绘制的文本](../../../../docs/framework/winforms/advanced/how-to-align-drawn-text.md)  
 演示如何设置 [!INCLUDE[ndptecgdiplus](../../../../includes/ndptecgdiplus-md.md)] 和 [!INCLUDE[ndptecgdi](../../../../includes/ndptecgdi-md.md)] 文本的格式。  
  
 [如何：创建垂直文本](../../../../docs/framework/winforms/advanced/how-to-create-vertical-text.md)  
 描述如何使用 [!INCLUDE[ndptecgdiplus](../../../../includes/ndptecgdiplus-md.md)] 绘制垂直对齐的文本。  
  
 [如何：在绘制的文本中设置制表位](../../../../docs/framework/winforms/advanced/how-to-set-tab-stops-in-drawn-text.md)  
 演示如何使用 [!INCLUDE[ndptecgdiplus](../../../../includes/ndptecgdiplus-md.md)] 绘制包含制表位的文本。  
  
 [如何：枚举已安装的字体](../../../../docs/framework/winforms/advanced/how-to-enumerate-installed-fonts.md)  
 说明如何列出已安装的字体的名称。  
  
 [如何：创建专用的字体集合](../../../../docs/framework/winforms/advanced/how-to-create-a-private-font-collection.md)  
 描述如何创建 <xref:System.Drawing.Text.PrivateFontCollection> 对象。  
  
 [如何：获取字体规格](../../../../docs/framework/winforms/advanced/how-to-obtain-font-metrics.md)  
 演示如何获取字体规格，如单元格的升高值与降低值。  
  
 [如何：对文本使用抗锯齿效果](../../../../docs/framework/winforms/advanced/how-to-use-antialiasing-with-text.md)  
 说明如何在绘制文本时使用抗锯齿。  
  
## 参考  
 <xref:System.Drawing.Font>  
 描述此类并包含指向其所有成员的链接。  
  
 <xref:System.Drawing.FontFamily>  
 描述此类并包含指向其所有成员的链接。  
  
 <xref:System.Drawing.Text.PrivateFontCollection>  
 描述此类并包含指向其所有成员的链接。  
  
 <xref:System.Windows.Forms.TextRenderer>  
 描述此类并包含指向其所有成员的链接。  
  
 <xref:System.Windows.Forms.TextFormatFlags>  
 描述此类并包含指向其所有成员的链接。