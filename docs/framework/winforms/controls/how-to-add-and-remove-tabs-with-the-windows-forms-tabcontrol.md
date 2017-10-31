---
title: "如何：使用 Windows 窗体 TabControl 添加和移除选项卡 | Microsoft Docs"
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
  - "选项卡页"
  - "TabControl 控件 [Windows 窗体], 添加和移除选项卡"
  - "TabPage 控件"
  - "选项卡, 添加到页"
  - "选项卡, 从页中移除"
ms.assetid: 66d4dfca-41e8-44e3-9c80-fb7ac4cb1619
caps.latest.revision: 16
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 16
---
# 如何：使用 Windows 窗体 TabControl 添加和移除选项卡
默认情况下，<xref:System.Windows.Forms.TabControl> 控件包含两个 <xref:System.Windows.Forms.TabPage> 控件。  可以通过 <xref:System.Windows.Forms.TabControl.TabPages%2A> 属性访问这些选项卡。  
  
### 以编程方式添加选项卡  
  
-   使用 <xref:System.Windows.Forms.TabControl.TabPages%2A> 属性的 <xref:System.Windows.Forms.TabControl.TabPageCollection.Add%2A> 方法。  
  
    ```vb  
    Dim myTabPage As New TabPage()  
    myTabPage.Text = "TabPage" & (TabControl1.TabPages.Count + 1)  
    TabControl1.TabPages.Add(myTabPage)  
  
    ```  
  
    ```csharp  
    string title = "TabPage " + (tabControl1.TabCount + 1).ToString();  
    TabPage myTabPage = new TabPage(title);  
    tabControl1.TabPages.Add(myTabPage);  
  
    ```  
  
    ```cpp  
    String^ title = String::Concat("TabPage ",  
       (tabControl1->TabCount + 1).ToString());  
    TabPage^ myTabPage = gcnew TabPage(title);  
    tabControl1->TabPages->Add(myTabPage);  
    ```  
  
### 以编程方式移除选项卡  
  
-   若要移除选定的选项卡，请使用 <xref:System.Windows.Forms.TabControl.TabPages%2A> 属性的 <xref:System.Windows.Forms.TabControl.TabPageCollection.Remove%2A> 方法。  
  
     \- 或 \-  
  
-   若要移除所有选项卡，请使用 <xref:System.Windows.Forms.TabControl.TabPages%2A> 属性的 <xref:System.Windows.Forms.TabControl.TabPageCollection.Clear%2A> 方法。  
  
    ```vb  
    ' Removes the selected tab:  
    TabControl1.TabPages.Remove(TabControl1.SelectedTab)  
    ' Removes all the tabs:  
    TabControl1.TabPages.Clear()  
  
    ```  
  
    ```csharp  
    // Removes the selected tab:  
    tabControl1.TabPages.Remove(tabControl1.SelectedTab);  
    // Removes all the tabs:  
    tabControl1.TabPages.Clear();  
  
    ```  
  
    ```cpp  
    // Removes the selected tab:  
    tabControl1->TabPages->Remove(tabControl1->SelectedTab);  
    // Removes all the tabs:  
    tabControl1->TabPages->Clear();  
    ```  
  
## 请参阅  
 [TabControl 控件概述](../../../../docs/framework/winforms/controls/tabcontrol-control-overview-windows-forms.md)   
 [如何：将控件添加到选项卡页](../../../../docs/framework/winforms/controls/how-to-add-a-control-to-a-tab-page.md)   
 [如何：禁用选项卡页](../../../../docs/framework/winforms/controls/how-to-disable-tab-pages.md)   
 [如何：更改 Windows 窗体 TabControl 的外观](../../../../docs/framework/winforms/controls/how-to-change-the-appearance-of-the-windows-forms-tabcontrol.md)