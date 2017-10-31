---
title: "如何：排列 MDI 子窗体 | Microsoft Docs"
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
  - "子窗体, 排列"
  - "MDI, 排列子窗体"
ms.assetid: a0786378-3206-4ccc-898e-7d3b38cc5089
caps.latest.revision: 11
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 11
---
# 如何：排列 MDI 子窗体
通常，应用程序会有用于操作（例如“平铺”、“级联”和“排列”）的菜单命令，这些命令会控制打开的 MDI 子窗体布局。  你可以使用 <xref:System.Windows.Forms.Form.LayoutMdi%2A> 方法和一个 <xref:System.Windows.Forms.MdiLayout> 枚举值来重排 MDI 父窗体中的子窗体。  
  
 <xref:System.Windows.Forms.MdiLayout> 枚举值将子窗体显示为水平或垂直平铺的级联或沿 MDI 窗体下部排列的子窗体图表。  这些值与 Windows 命令“级联窗口”、“并排显示窗口”、“显示堆栈窗口”和“显示桌面”具有相同的效果。  
  
 通常，这些方法用作菜单项 <xref:System.Windows.Forms.Control.Click> 事件调用的事件处理程序。  通过此方法，包含文本“级联窗口”的菜单项可实现对 MDI 子窗口的预期效果。  
  
### 要排列子窗体  
  
1.  在一个方法中，使用 <xref:System.Windows.Forms.Form.LayoutMdi%2A> 方法来设置 MDI 父窗体的 <xref:System.Windows.Forms.MdiLayout> 枚举。  下面的示例使用 MDI 父窗体的子窗口（`Form1`）的 <xref:System.Windows.Forms.MdiLayout?displayProperty=fullName> 枚举值。  在事件处理程序处理“级联窗口”菜单项 <xref:System.Windows.Forms.Control.Click> 事件期间，枚举用于代码中。  
  
    ```vb  
    Protected Sub CascadeWindows_Click(ByVal sender As System.Object, ByVal e As System.EventArgs)  
       Me.LayoutMdi(System.Windows.Forms.MdiLayout.Cascade)  
    End Sub  
  
    ```  
  
    ```csharp  
    protected void CascadeWindows_Click(object sender, System.EventArgs e){  
       this.LayoutMdi(System.Windows.Forms.MdiLayout.Cascade);  
    }  
    ```  
  
    > [!NOTE]
    >  你也可以通过更改使用的 <xref:System.Windows.Forms.MdiLayout> 枚举值来堆积窗口并以图标形式排列窗口。  
  
2.  如果你正在使用 Visual C\#，将以下代码放在窗体构造函数中以注册事件处理程序。  
  
    ```csharp  
    this.button1.Click += new System.EventHandler(this.button1_Click);  
    ```  
  
## 请参阅  
 [多文档界面 \(MDI\) 应用程序](../../../../docs/framework/winforms/advanced/multiple-document-interface-mdi-applications.md)   
 [如何：创建 MDI 父窗体](../../../../docs/framework/winforms/advanced/how-to-create-mdi-parent-forms.md)   
 [如何：创建 MDI 子窗体](../../../../docs/framework/winforms/advanced/how-to-create-mdi-child-forms.md)   
 [如何：确定活动的 MDI 子窗体](../../../../docs/framework/winforms/advanced/how-to-determine-the-active-mdi-child.md)   
 [如何：将数据发送到活动的 MDI 子窗体](../../../../docs/framework/winforms/advanced/how-to-send-data-to-the-active-mdi-child.md)