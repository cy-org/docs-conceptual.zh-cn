---
title: "如何：更改 Windows 窗体的边框 | Microsoft Docs"
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
  - "Windows 窗体, 更改边框"
ms.assetid: b3d5fa56-80c6-4b10-b505-f9672307ed55
caps.latest.revision: 12
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 12
---
# 如何：更改 Windows 窗体的边框
当确定 Windows 窗体的外观和行为时，有几种边框样式可供选择。  通过更改 <xref:System.Windows.Forms.Form.FormBorderStyle%2A> 属性，可控制窗体调整大小的行为。  此外，设置 <xref:System.Windows.Forms.Form.FormBorderStyle%2A> 会影响标题栏的显示方式以及其上出现的按钮布局。  有关详细信息，请参阅<xref:System.Windows.Forms.FormBorderStyle>。  
  
 [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] 中对此任务提供广泛支持。  
  
 另请参阅[如何：使用设计器更改 Windows 窗体的边框](http://msdn.microsoft.com/library/yettzh3e%20\(v=vs.110\))。  
  
### 以编程方式设置 Windows 窗体的边框样式  
  
-   将 <xref:System.Windows.Forms.Form.FormBorderStyle%2A> 属性设置为所需的样式。  下面的代码示例将窗体 `DlgBx1`  的边框样式设置为 <xref:System.Windows.Forms.FormBorderStyle>。  
  
    ```vb  
    DlgBx1.FormBorderStyle = System.Windows.Forms.FormBorderStyle.FixedDialog  
    ```  
  
    ```csharp  
    DlgBx1.FormBorderStyle = System.Windows.Forms.FormBorderStyle.FixedDialog;  
    ```  
  
    ```cpp  
    DlgBx1->FormBorderStyle =  
       System::Windows::Forms::FormBorderStyle::FixedDialog;  
    ```  
  
     另请参阅[如何：在设计时创建对话框](http://msdn.microsoft.com/library/55cz5x2c\(v=vs.110\))。  
  
     此外，如果已为提供**最小化**和**最大化**可选按钮的窗体选择了边框样式，则可指定可使用其中一个按钮还是两个按钮均可使用。  当想要密切控制用户体验时，这些按钮会非常有用。  **最小化**和**最大化**按钮默认处于启用状态，而且可通过**属性**窗口操作其功能。  
  
## 请参阅  
 <xref:System.Windows.Forms.FormBorderStyle>   
 <xref:System.Windows.Forms.FormBorderStyle>   
 [Windows 窗体入门](../../../docs/framework/winforms/getting-started-with-windows-forms.md)