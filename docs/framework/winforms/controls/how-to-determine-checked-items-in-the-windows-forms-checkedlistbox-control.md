---
title: "如何：确定 Windows 窗体 CheckedListBox 控件中的选定项 | Microsoft Docs"
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
  - "复选框, 确定选中状态"
  - "CheckedListBox 控件 [Windows 窗体], 确定选中状态"
ms.assetid: 178b477d-27c9-489c-8914-44a9623a4d41
caps.latest.revision: 14
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 14
---
# 如何：确定 Windows 窗体 CheckedListBox 控件中的选定项
当显示 Windows 窗体 <xref:System.Windows.Forms.CheckedListBox> 控件中的数据时，可以循环访问 <xref:System.Windows.Forms.CheckedListBox.CheckedItems%2A> 属性中存储的集合，或者使用 <xref:System.Windows.Forms.CheckedListBox.GetItemChecked%2A> 方法逐句通过列表来确定选中的项。  <xref:System.Windows.Forms.CheckedListBox.GetItemChecked%2A> 方法接受一个项索引号作为参数，并返回 `true` 或 `false`。  可能与您期望的相反，<xref:System.Windows.Forms.ListBox.SelectedItems%2A> 和 <xref:System.Windows.Forms.ListBox.SelectedIndices%2A> 属性并不确定哪些项已选中；它们确定哪些项为突出显示。  
  
### 确定 CheckedListBox 控件中的已选中项  
  
1.  因为 <xref:System.Windows.Forms.CheckedListBox.CheckedItems%2A> 集合是从零开始的，所以请从 0 开始循环访问该集合。  注意，此方法将向您提供项在已选中项列表而不是整个列表中的编号。  因此，如果未选中列表中的第一项而选中了第二项，则下面的代码显示的文本将类似于“Checked Item 1 \= MyListItem2”（选中的第 1 项 \= MyListItem2）。  
  
    ```vb  
    ' Determine if there are any items checked.  
    If CheckedListBox1.CheckedItems.Count <> 0 Then  
       ' If so, loop through all checked items and print results.  
       Dim x As Integer  
       Dim s As String = ""  
       For x = 0 To CheckedListBox1.CheckedItems.Count - 1  
          s = s & "Checked Item " & (x + 1).ToString & " = " & CheckedListBox1.CheckedItems(x).ToString & ControlChars.CrLf  
       Next x  
       MessageBox.Show(s)  
    End If  
  
    ```  
  
    ```csharp  
    // Determine if there are any items checked.  
    if(checkedListBox1.CheckedItems.Count != 0)  
    {  
       // If so, loop through all checked items and print results.  
       string s = "";  
       for(int x = 0; x <= checkedListBox1.CheckedItems.Count - 1 ; x++)  
       {  
          s = s + "Checked Item " + (x+1).ToString() + " = " + checkedListBox1.CheckedItems[x].ToString() + "\n";  
       }  
    MessageBox.Show (s);  
    }  
  
    ```  
  
    ```cpp  
    // Determine if there are any items checked.  
    if(checkedListBox1->CheckedItems->Count != 0)  
    {  
       // If so, loop through all checked items and print results.  
       String ^ s = "";  
       for(int x = 0; x <= checkedListBox1->CheckedItems->Count - 1; x++)  
       {  
          s = String::Concat(s, "Checked Item ", (x+1).ToString(),  
             " = ", checkedListBox1->CheckedItems[x]->ToString(),  
             "\n");  
       }  
       MessageBox::Show(s);  
    }  
    ```  
  
     \- 或 \-  
  
2.  因为 <xref:System.Windows.Forms.CheckedListBox.Items%2A> 集合是从零开始的，所以请从 0 开始逐句通过该集合，并对每个项调用 <xref:System.Windows.Forms.CheckedListBox.GetItemChecked%2A> 方法。  请注意，此方法将为您提供总体列表中的项号，因此如果未选中该列表中的第一个项，而选中了第二个项，则显示的内容类似“Item 2 \= MyListItem2”。  
  
    ```vb  
    Dim i As Integer  
    Dim s As String  
    s = "Checked Items:" & ControlChars.CrLf  
    For i = 0 To (CheckedListBox1.Items.Count - 1)  
       If CheckedListBox1.GetItemChecked(i) = True Then  
          s = s & "Item " & (i + 1).ToString & " = " & CheckedListBox1.Items(i).ToString & ControlChars.CrLf  
       End If  
    Next  
    MessageBox.Show(s)  
  
    ```  
  
    ```csharp  
    int i;  
    string s;   
    s = "Checked items:\n" ;  
    for (i = 0; i <= (checkedListBox1.Items.Count-1); i++)  
    {  
       if (checkedListBox1.GetItemChecked(i))  
       {  
          s = s + "Item " + (i+1).ToString() + " = " + checkedListBox1.Items[i].ToString() + "\n";  
       }  
    }  
    MessageBox.Show (s);  
  
    ```  
  
    ```cpp  
    int i;  
    String ^ s;   
    s = "Checked items:\n" ;  
    for (i = 0; i <= (checkedListBox1->Items->Count-1); i++)  
    {  
       if (checkedListBox1->GetItemChecked(i))  
       {  
          s = String::Concat(s, "Item ", (i+1).ToString(), " = ",  
             checkedListBox1->Item[i]->ToString(), "\n");  
       }  
    }  
    MessageBox::Show(s);  
    ```  
  
## 请参阅  
 [用于列出选项的 Windows 窗体控件](../../../../docs/framework/winforms/controls/windows-forms-controls-used-to-list-options.md)