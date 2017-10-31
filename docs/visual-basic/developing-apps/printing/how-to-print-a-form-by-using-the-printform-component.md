---
title: "如何：使用 PrintForm 组件打印窗体 (Visual Basic) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "窗体, 打印"
ms.assetid: df963bf6-3ee1-49f4-8b2e-1d95d1beb0be
caps.latest.revision: 19
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 19
---
# 如何：使用 PrintForm 组件打印窗体 (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

通过 <xref:Microsoft.VisualBasic.PowerPacks.Printing.PrintForm> 组件，可以在不使用 <xref:System.Drawing.Printing.PrintDocument> 组件的情况下如实快速打印窗体的图像。 以下过程介绍如何将窗体打印到打印机、打印预览窗口和封装的 PostScript 文件。  
  
 Visual Studio 中不再包含 PowerPack 控件，但你可以从[下载中心](http://www.microsoft.com/en-us/download/details.aspx?id=25169)下载它们。  
  
### 将窗体打印到默认打印机  
  
1.  在“工具箱”中，单击“Visual Basic PowerPacks”选项卡，然后将 <xref:Microsoft.VisualBasic.PowerPacks.Printing.PrintForm> 组件拖动到窗体上。  
  
     <xref:Microsoft.VisualBasic.PowerPacks.Printing.PrintForm> 组件被添加到组件栏。  
  
2.  在“属性”窗口中，将 <xref:Microsoft.VisualBasic.PowerPacks.Printing.PrintForm.PrintAction%2A> 属性设置为 <xref:System.Drawing.Printing.PrintAction>。  
  
3.  在相应的事件处理程序中（例如在“打印”`Button`的 `Click` 事件处理程序中）添加以下代码。  
  
    ```  
    PrintForm1.Print()  
    ```  
  
### 在打印预览窗口中显示窗体  
  
1.  在“工具箱”中，单击“Visual Basic PowerPacks”选项卡，然后将 <xref:Microsoft.VisualBasic.PowerPacks.Printing.PrintForm> 组件拖动到窗体上。  
  
     <xref:Microsoft.VisualBasic.PowerPacks.Printing.PrintForm> 组件被添加到组件栏。  
  
2.  在“属性”窗口中，将 <xref:Microsoft.VisualBasic.PowerPacks.Printing.PrintForm.PrintAction%2A> 属性设置为 <xref:System.Drawing.Printing.PrintAction>。  
  
3.  在相应的事件处理程序中（例如在“打印”`Button`的 `Click` 事件处理程序中）添加以下代码。  
  
    ```  
    PrintForm1.Print()  
    ```  
  
### 将窗体打印到文件  
  
1.  在“工具箱”中，单击“Visual Basic PowerPacks”选项卡，然后将 <xref:Microsoft.VisualBasic.PowerPacks.Printing.PrintForm> 组件拖动到窗体上。  
  
     <xref:Microsoft.VisualBasic.PowerPacks.Printing.PrintForm> 组件被添加到组件栏。  
  
2.  在“属性”窗口中，将 <xref:Microsoft.VisualBasic.PowerPacks.Printing.PrintForm.PrintAction%2A> 属性设置为 <xref:System.Drawing.Printing.PrintAction>。  
  
3.  （可选）选择 <xref:Microsoft.VisualBasic.PowerPacks.Printing.PrintForm.PrintFileName%2A> 属性，并键入目标文件的完整路径和文件名称。  
  
     如果跳过此步骤，将在运行时提示用户输入文件名。  
  
4.  在相应的事件处理程序中（例如在“打印”`Button`的 `Click` 事件处理程序中）添加以下代码。  
  
    ```  
    PrintForm1.Print()  
    ```  
  
## 请参阅  
 <xref:Microsoft.VisualBasic.PowerPacks.Printing.PrintForm.PrintAction%2A>   
 <xref:Microsoft.VisualBasic.PowerPacks.Printing.PrintForm.PrintFileName%2A>   
 [如何：打印窗体的工作区](../../../visual-basic/developing-apps/printing/how-to-print-the-client-area-of-a-form.md)   
 [如何：打印窗体的工作区和非工作区](../../../visual-basic/developing-apps/printing/how-to-print-client-and-non-client-areas-of-a-form.md)   
 [如何：打印可滚动的窗体](../../../visual-basic/developing-apps/printing/how-to-print-a-scrollable-form.md)   
 [PrintForm Component](../../../visual-basic/developing-apps/printing/printform-component.md)