---
title: "如何：访问 Windows 窗体 ComboBox 控件、ListBox 控件或 CheckedListBox 控件中的特定项 | Microsoft Docs"
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
  - "CheckedListBox 控件 [Windows 窗体], 访问项"
  - "组合框, 访问项"
  - "ComboBox 控件 [Windows 窗体], 访问项"
  - "列表框, 访问项"
  - "ListBox 控件 [Windows 窗体], 访问项"
  - "ListBox 控件 [Windows 窗体], 返回项信息"
ms.assetid: 1216742f-bcf9-4ff8-8a62-d7c9053c2b96
caps.latest.revision: 13
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 13
---
# 如何：访问 Windows 窗体 ComboBox 控件、ListBox 控件或 CheckedListBox 控件中的特定项
访问 Windows 窗体组合框、列表框或复选列表框中的特定项是一项基本任务。  它使您可以编程方式确定列表中任意给定位置处的内容。  
  
### 访问特定项  
  
1.  使用指定项的索引查询 `Items`  集合：  
  
    ```vb  
    Private Function GetItemText(i As Integer) As String  
       ' Return the text of the item using the index:  
       Return ComboBox1.Items(i).ToString  
    End Function  
  
    ```  
  
    ```csharp  
    private string GetItemText(int i)  
    {  
       // Return the text of the item using the index:  
       return (comboBox1.Items[i].ToString());  
    }  
  
    ```  
  
    ```cpp  
    private:  
       String^ GetItemText(int i)  
       {  
          // Return the text of the item using the index:  
          return (comboBox1->Items->Item[i]->ToString());  
       }  
    ```  
  
## 请参阅  
 <xref:System.Windows.Forms.ComboBox>   
 <xref:System.Windows.Forms.ListBox>   
 <xref:System.Windows.Forms.CheckedListBox>   
 [用于列出选项的 Windows 窗体控件](../../../../docs/framework/winforms/controls/windows-forms-controls-used-to-list-options.md)