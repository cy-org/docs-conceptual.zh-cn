---
title: "如何：在 Windows 窗体中为 ToolStrip 控件创建和设置自定义呈现器 | Microsoft Docs"
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
  - "示例 [Windows 窗体], 工具栏"
  - "工具栏 [Windows 窗体], 呈现"
  - "ToolStrip 控件 [Windows 窗体], 自定义呈现"
  - "ToolStrip 控件 [Windows 窗体], 呈现"
ms.assetid: 88a804ba-679f-4ba3-938a-0dc396199c5b
caps.latest.revision: 16
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 16
---
# 如何：在 Windows 窗体中为 ToolStrip 控件创建和设置自定义呈现器
<xref:System.Windows.Forms.ToolStrip> 控件提供了针对主题和样式的简易支持。  通过将 <xref:System.Windows.Forms.ToolStrip.Renderer%2A?displayProperty=fullName> 属性或 <xref:System.Windows.Forms.ToolStripManager.Renderer%2A?displayProperty=fullName> 属性设置为自定义呈现器，可以完全实现自定义的外观和行为（观感）。  
  
 您可以为每个 <xref:System.Windows.Forms.ToolStrip>、<xref:System.Windows.Forms.MenuStrip>、<xref:System.Windows.Forms.ContextMenuStrip> 或 <xref:System.Windows.Forms.StatusStrip> 控件分配呈现器，也可以通过将 <xref:System.Windows.Forms.ToolStrip.RenderMode%2A?displayProperty=fullName> 属性设置为 <xref:System.Windows.Forms.ToolStripRenderMode?displayProperty=fullName> 来使用 <xref:System.Windows.Forms.ToolStripManager.Renderer%2A> 属性影响所有对象。  
  
> [!NOTE]
>  只有当 <xref:System.Windows.Forms.ToolStrip.Renderer%2A?displayProperty=fullName> 的值不是 `null` 时，<xref:System.Windows.Forms.ToolStrip.RenderMode%2A> 才会返回 <xref:System.Windows.Forms.ToolStripRenderMode>。  
  
### 创建自定义呈现器  
  
1.  扩展 <xref:System.Windows.Forms.ToolStripRenderer> 类。  
  
2.  通过重写适当的 *On…* 成员来实现所需的自定义呈现。  
  
    ```vb  
    Public Class RedTextRenderer  
        Inherits System.Windows.Forms.ToolStripRenderer  
        Protected Overrides Sub OnRenderItemText(ByVal e As _  
            ToolStripItemTextRenderEventArgs)   
            e.TextColor = Color.Red  
            e.TextFont = New Font("Helvetica", 7, FontStyle.Bold)  
            MyBase.OnRenderItemText(e)  
        End Sub  
    End Class  
  
    ```  
  
     \[C\#\]  
  
    ```  
    public class RedTextRenderer : _  
        System.Windows.Forms.ToolStripRenderer  
    {  
        protected override void _  
            OnRenderItemText(ToolStripItemTextRenderEventArgs e)  
        {  
            e.TextColor = Color.Red;  
            e.TextFont = new Font("Helvetica", 7, FontStyle.Bold);  
           base.OnRenderItemText(e);  
        }  
    }  
  
    ```  
  
### 将自定义体现程序设置为当前呈现器  
  
1.  若要为一个 <xref:System.Windows.Forms.ToolStrip> 设置自定义呈现器，请将 <xref:System.Windows.Forms.ToolStrip.Renderer%2A?displayProperty=fullName> 属性设置为自定义呈现器。  
  
    ```vb  
    toolStrip1.Renderer = New RedTextRenderer()  
  
    ```  
  
     \[C\#\]  
  
    ```  
    toolStrip1.Renderer = new RedTextRenderer();  
  
    ```  
  
2.  或者，若要为应用程序中包含的所有 <xref:System.Windows.Forms.ToolStrip> 类设置自定义呈现器，请将 <xref:System.Windows.Forms.ToolStripManager.Renderer%2A?displayProperty=fullName> 属性设置为自定义呈现器并将 <xref:System.Windows.Forms.ToolStrip.RenderMode%2A> 属性设置为 <xref:System.Windows.Forms.ToolStripRenderMode>。  
  
    ```vb  
    toolStrip1.RenderMode = ToolStripRenderMode.ManagerRenderMode  
    ToolStripManager.Renderer = New RedTextRenderer()  
  
    ```  
  
     \[C\#\]  
  
    ```  
    toolStrip1.RenderMode = ToolStripRenderMode.ManagerRenderMode;  
    ToolStripManager.Renderer = new RedTextRenderer();  
  
    ```  
  
## 请参阅  
 <xref:System.Windows.Forms.ToolStripManager.Renderer%2A>   
 <xref:System.Windows.Forms.ToolStripRenderer>   
 <xref:System.Windows.Forms.ToolStrip.RenderMode%2A>   
 [ToolStrip 控件概述](../../../../docs/framework/winforms/controls/toolstrip-control-overview-windows-forms.md)   
 [ToolStrip 控件体系结构](../../../../docs/framework/winforms/controls/toolstrip-control-architecture.md)   
 [ToolStrip 技术摘要](../../../../docs/framework/winforms/controls/toolstrip-technology-summary.md)