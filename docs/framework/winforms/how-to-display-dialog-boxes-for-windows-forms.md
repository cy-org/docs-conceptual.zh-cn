---
title: "如何：显示 Windows 窗体的对话框 | Microsoft Docs"
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
  - "对话框, 为 Windows 窗体显示"
  - "Windows 窗体对话框, 显示"
  - "Windows 窗体, 从一个窗体调用另一个窗体"
  - "Windows 窗体, 显示"
ms.assetid: aaac1b38-c651-495a-8d3d-5a9bfb32fee3
caps.latest.revision: 10
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 10
---
# 如何：显示 Windows 窗体的对话框
显示对话框的方法与在应用程序中显示任何其他窗体的方法一样。  当运行应用程序时，自动加载启动窗体。  若要使第二个窗体或对话框出现在应用程序中，请编写加载并显示它的代码。  同样，若要使窗体或对话框消失，可编写卸载或隐藏它的代码。  
  
### 显示对话框  
  
1.  定位到要用其打开对话框的事件处理程序。  它可发生在选中菜单命令时、单击按钮时或发生任何其他事件时。  
  
2.  在事件处理程序中，添加打开对话框的代码。  在下列示例中，单击按钮事件用于显示对话框：  
  
    ```vb  
    Private Sub Button1_Click(ByVal sender As System.Object, ByVal e As System.EventArgs) Handles Button1.Click  
       Dim dlg1 as new Form()  
       dlg1.ShowDialog()  
    End Sub  
  
    ```  
  
    ```csharp  
    private void button1_Click(object sender, System.EventArgs e)   
    {  
       Form dlg1 = new Form();  
       dlg1.ShowDialog();  
    }  
  
    ```  
  
    ```cpp  
    private:   
      void button1_Click(System::Object ^ sender,  
        System::EventArgs ^ e)  
      {  
        Form ^ dlg1 = gcnew Form();  
        dlg1->ShowDialog();  
      }  
    ```