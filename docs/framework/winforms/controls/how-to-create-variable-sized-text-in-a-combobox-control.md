---
title: "如何：在 ComboBox 控件中创建大小可变的文本 | Microsoft Docs"
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
  - "组合框, 绘制文本"
  - "ComboBox 控件 [Windows 窗体], 绘制自定义文本"
  - "ComboBox 控件 [Windows 窗体], 示例 [C#]"
  - "示例 [Windows 窗体], ComboBox 控件"
  - "文本, 在组合框中绘制"
ms.assetid: ce39b9ea-e626-49fe-bd5a-f567f6d157df
caps.latest.revision: 9
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 9
---
# 如何：在 ComboBox 控件中创建大小可变的文本
此示例演示如何在 <xref:System.Windows.Forms.ComboBox> 控件中自定义文本绘制。  当项满足特定条件时，就会以较大的字体绘制并变为红色。  
  
## 示例  
  
```vb  
Private Sub ComboBox1_MeasureItem(ByVal sender As Object, ByVal e As _  
System.Windows.Forms.MeasureItemEventArgs) Handles ComboBox1.MeasureItem  
    Dim bFont As New Font("Arial", 8, FontStyle.Bold)  
    Dim lFont As New Font("Arial", 12, FontStyle.Bold)  
    Dim siText As SizeF  
  
    If ComboBox1.Items().Item(e.Index) = "Two" Then  
        siText = e.Graphics.MeasureString(ComboBox1.Items().Item(e.Index), _  
lFont)  
    Else  
        siText = e.Graphics.MeasureString(ComboBox1.Items().Item(e.Index), bFont)  
    End If  
  
    e.ItemHeight = siText.Height  
    e.ItemWidth = siText.Width  
End Sub  
  
Private Sub ComboBox1_DrawItem(ByVal sender As Object, ByVal e As _  
System.Windows.Forms.DrawItemEventArgs) Handles ComboBox1.DrawItem  
    Dim g As Graphics = e.Graphics  
    Dim bFont As New Font("Arial", 8, FontStyle.Bold)  
    Dim lFont As New Font("Arial", 12, FontStyle.Bold)  
  
    If ComboBox1.Items().Item(e.Index) = "Two" Then  
        g.DrawString(ComboBox1.Items.Item(e.Index), lfont, Brushes.Red, _  
e.Bounds.X, e.Bounds.Y)  
    Else  
        g.DrawString(ComboBox1.Items.Item(e.Index), bFont, Brushes.Black, e.Bounds.X, e.Bounds.Y)  
    End If  
End Sub  
```  
  
## 编译代码  
 此示例需要：  
  
-   一个 Windows 窗体。  
  
-   一个名为  `ListBox1`  的 <xref:System.Windows.Forms.ComboBox> 控件，其 <xref:System.Windows.Forms.ComboBox.Items%2A> 属性中包含三项。  在此示例中，这三个项名为  `"One", Two", and Three"`。   `ComboBox1`  的 <xref:System.Windows.Forms.ComboBox.DrawMode%2A> 属性必须设置为 <xref:System.Windows.Forms.DrawMode>。  
  
    > [!NOTE]
    >  这种方法也适用于 <xref:System.Windows.Forms.ListBox> 控件 \-\- 您可以用 <xref:System.Windows.Forms.ListBox> 替换 <xref:System.Windows.Forms.ComboBox>。  
  
-   对 <xref:System.Windows.Forms?displayProperty=fullName> 和 <xref:System.Drawing?displayProperty=fullName> 命名空间的引用。  
  
## 请参阅  
 <xref:System.Windows.Forms.ComboBox.DrawItem>   
 <xref:System.Windows.Forms.DrawItemEventArgs>   
 <xref:System.Windows.Forms.ComboBox.MeasureItem>   
 [具有内置所有者描述支持的控件](../../../../docs/framework/winforms/controls/controls-with-built-in-owner-drawing-support.md)   
 [ListBox 控件](../../../../docs/framework/winforms/controls/listbox-control-windows-forms.md)   
 [ComboBox 控件](../../../../docs/framework/winforms/controls/combobox-control-windows-forms.md)