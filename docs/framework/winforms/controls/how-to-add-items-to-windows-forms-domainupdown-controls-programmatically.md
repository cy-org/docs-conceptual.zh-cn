---
title: "如何：以编程方式向 Windows 窗体 DomainUpDown 控件添加项 | Microsoft Docs"
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
  - "DomainUpDown 控件 [Windows 窗体], 添加项"
  - "数值调节钮控件, 添加项"
ms.assetid: fd31d314-33eb-4181-90f8-d32ed0c4e072
caps.latest.revision: 14
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 14
---
# 如何：以编程方式向 Windows 窗体 DomainUpDown 控件添加项
可以用代码向 Windows 窗体 <xref:System.Windows.Forms.DomainUpDown> 控件添加项。  调用 <xref:System.Windows.Forms.DomainUpDown.DomainUpDownItemCollection> 类的 <xref:System.Windows.Forms.DomainUpDown.DomainUpDownItemCollection.Add%2A> 或 <xref:System.Windows.Forms.DomainUpDown.DomainUpDownItemCollection.Insert%2A> 方法以向控件的 <xref:System.Windows.Forms.DomainUpDown.Items%2A> 属性添加项。  <xref:System.Windows.Forms.DomainUpDown.DomainUpDownItemCollection.Add%2A> 方法将项添加到集合的末尾，而 <xref:System.Windows.Forms.DomainUpDown.DomainUpDownItemCollection.Insert%2A> 方法则将项添加到指定的位置。  
  
### 添加新项  
  
1.  使用 <xref:System.Windows.Forms.DomainUpDown.DomainUpDownItemCollection.Add%2A> 方法将项添加到项列表的末尾。  
  
    ```vb  
    DomainUpDown1.Items.Add("noodles")  
  
    ```  
  
    ```csharp  
    domainUpDown1.Items.Add("noodles");  
  
    ```  
  
    ```cpp  
    domainUpDown1->Items->Add("noodles");  
    ```  
  
     \- 或 \-  
  
2.  使用 <xref:System.Windows.Forms.DomainUpDown.DomainUpDownItemCollection.Insert%2A> 方法将项插入到列表中的指定位置。  
  
    ```vb  
    ' Inserts an item at the third position in the list  
    DomainUpDown1.Items.Insert(2, "rice")  
  
    ```  
  
    ```csharp  
    // Inserts an item at the third position in the list  
    domainUpDown1.Items.Insert(2, "rice");  
  
    ```  
  
    ```cpp  
    // Inserts an item at the third position in the list  
    domainUpDown1->Items->Insert(2, "rice");  
    ```  
  
## 请参阅  
 <xref:System.Windows.Forms.DomainUpDown>   
 <xref:System.Windows.Forms.DomainUpDown.DomainUpDownItemCollection.Add%2A?displayProperty=fullName>   
 <xref:System.Collections.ArrayList.Insert%2A?displayProperty=fullName>   
 [DomainUpDown 控件](../../../../docs/framework/winforms/controls/domainupdown-control-windows-forms.md)   
 [DomainUpDown 控件概述](../../../../docs/framework/winforms/controls/domainupdown-control-overview-windows-forms.md)