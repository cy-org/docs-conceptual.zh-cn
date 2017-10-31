---
title: "如何：通过 Windows 窗体 LinkLabel 控件显示网页 (Visual Basic) | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-winforms"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "LinkLabel1_LinkClicked"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "示例 [Windows 窗体], LinkLabel 控件"
  - "链接, 从窗体到网页"
  - "LinkLabel 控件 [Windows 窗体], 示例"
  - "网页, 显示"
  - "Windows 窗体, 链接到网页"
ms.assetid: 477a7398-5971-4de3-b24c-f49f32bdb28a
caps.latest.revision: 7
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 7
---
# 如何：通过 Windows 窗体 LinkLabel 控件显示网页 (Visual Basic)
本示例在用户单击 Windows 窗体 <xref:System.Windows.Forms.LinkLabel> 控件时在默认浏览器中显示网页。  
  
## 示例  
  
```vb  
Private Sub Form1_Load(ByVal sender As System.Object, ByVal e _  
As System.EventArgs) Handles MyBase.Load  
    LinkLabel1.Text = "Click here to get more info."  
    LinkLabel1.Links.Add(6, 4, "www.microsoft.com")  
End Sub  
Private Sub LinkLabel1_LinkClicked(ByVal sender As System.Object, ByVal _  
e As System.Windows.Forms.LinkLabelLinkClickedEventArgs) Handles _  
LinkLabel1.LinkClicked  
    System.Diagnostics.Process.Start(e.Link.LinkData.ToString())  
End Sub  
```  
  
## 编译代码  
 此示例需要：  
  
-   名为 `Form1` 的 Windows 窗体。  
  
-   名为 `LinkLabel1` 的 <xref:System.Windows.Forms.LinkLabel> 控件。  
  
-   活动 Internet 连接。  
  
## .NET Framework 安全性  
 对 <xref:System.Diagnostics.Process.Start%2A> 方法的调用要求完全信任。  有关更多信息，请参见 <xref:System.Security.SecurityException>。  
  
## 请参阅  
 <xref:System.Windows.Forms.LinkLabel>   
 [LinkLabel 控件](../../../../docs/framework/winforms/controls/linklabel-control-windows-forms.md)