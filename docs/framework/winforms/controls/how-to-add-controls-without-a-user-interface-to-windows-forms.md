---
title: "如何：向 Windows 窗体添加无用户界面的控件 | Microsoft Docs"
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
  - "NonVisualSelection"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "控件 [Windows 窗体], 不可见"
  - "不可见的控件"
  - "不可见控件"
  - "Windows 窗体控件, 添加到窗体"
  - "Windows 窗体控件, 不可见"
ms.assetid: 52134d9c-cff6-4eed-8e2b-3d5eb3bd494e
caps.latest.revision: 12
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 12
---
# 如何：向 Windows 窗体添加无用户界面的控件
非可视控件（或组件）为应用程序提供功能。  与其他控件不同，组件不向用户提供用户界面，因此不需要在 Windows 窗体设计器图面上显示。  当组件添加到窗体时，Windows 窗体设计器在窗体的底部显示可调整大小的栏，所有组件都在此栏中显示。  将控件添加到组件栏后，选定该组件并设置其属性，其方法与设置窗体上的任何其他控件的方法相同。  
  
> [!NOTE]
>  显示的对话框和菜单命令可能会与“帮助”中的描述不同，具体取决于您现用的设置或版本。  若要更改设置，请在**“工具”**菜单上选择**“导入和导出设置”**。  有关更多信息，请参见 [Customizing Development Settings in Visual Studio](http://msdn.microsoft.com/zh-cn/22c4debb-4e31-47a8-8f19-16f328d7dcd3)。  
  
### 向 Windows 窗体添加组件  
  
1.  打开窗体。  有关详细信息，请参见 [How to: Display Windows Forms in the Designer](http://msdn.microsoft.com/zh-cn/bf3f1e5b-ea07-4529-85c6-6af3ded0cec5)。  
  
2.  在**“工具箱”**中单击某个组件并将其拖动到窗体上。  
  
     此组件出现在组件栏中。  
  
 此外，组件可在运行时添加到窗体中。  这是一个常见的方案，尤其因为组件不像控件一样有用户界面，它们没有直观的表达方式。  在以下示例中，<xref:System.Windows.Forms.Timer> 组件是运行时添加的。  （注意，[!INCLUDE[vsprvs](../../../../includes/vsprvs-md.md)] 包含许多不同的计时器；在这种情况下，请使用 Windows 窗体 <xref:System.Windows.Forms.Timer> 组件。  有关 [!INCLUDE[vsprvs](../../../../includes/vsprvs-md.md)] 中不同计时器的更多信息，请参见 [Introduction to Server\-Based Timers](http://msdn.microsoft.com/zh-cn/adc0bc0a-a519-4812-bafc-fb9d1a5801fc)。）  
  
> [!CAUTION]
>  组件通常具有一些控件特定的属性，要使该组件有效运行，必须为其设置这些属性。  对于下面的 <xref:System.Windows.Forms.Timer> 组件，请设置 `Interval` 属性。  当将组件添加到项目时，请确保设置该组件必需的属性。  
  
#### 以编程方式向 Windows 窗体添加组件  
  
1.  在代码中创建一个 <xref:System.Windows.Forms.Timer> 类的实例。  
  
2.  设置 `Interval` 属性，以确定计时器两个刻度之间的时间。  
  
3.  为您的组件配置任何其他必要的属性。  
  
     下面的代码演示如何创建设置了 `Interval` 属性的 <xref:System.Windows.Forms.Timer>。  
  
    ```vb  
    Public Sub CreateTimer()  
       Dim timerKeepTrack As New System.Windows.Forms.Timer  
       timerKeepTrack.Interval = 1000  
    End Sub  
  
    ```  
  
    ```csharp  
    public void createTimer()  
    {  
       System.Windows.Forms.Timer timerKeepTrack = new  
           System.Windows.Forms.Timer();  
       timerKeepTrack.Interval = 1000;  
    }  
  
    ```  
  
    ```cpp  
    public:  
       void createTimer()  
       {  
          System::Windows::Forms::Timer^ timerKeepTrack = gcnew  
             System::Windows::Forms::Timer();  
          timerKeepTrack->Interval = 1000;  
       }  
    ```  
  
    > [!IMPORTANT]
    >  如果您引用了恶意的 UserControl，就可能会使本地计算机的安全受到来自网络的威胁。  只有发生以下情况时，这才是需要注意的问题：一个恶意的用户创建了一个破坏性的自定义控件，然后您又错误地将该控件添加到您的项目中。  
  
## 请参阅  
 [Windows 窗体控件](../../../../docs/framework/winforms/controls/index.md)   
 [如何：向 Windows 窗体添加控件](../../../../docs/framework/winforms/controls/how-to-add-controls-to-windows-forms.md)   
 [如何：向 Windows 窗体添加 ActiveX 控件](../../../../docs/framework/winforms/controls/how-to-add-activex-controls-to-windows-forms.md)   
 [如何：在 Windows 窗体之间复制控件](../../../../docs/framework/winforms/controls/how-to-copy-controls-between-windows-forms.md)   
 [将控件放在 Windows 窗体上](../../../../docs/framework/winforms/controls/putting-controls-on-windows-forms.md)   
 [标记单个 Windows 窗体控件并提供它们的快捷方式](../../../../docs/framework/winforms/controls/labeling-individual-windows-forms-controls-and-providing-shortcuts-to-them.md)   
 [在 Windows 窗体上使用的控件](../../../../docs/framework/winforms/controls/controls-to-use-on-windows-forms.md)   
 [根据功能列出的 Windows 窗体控件](../../../../docs/framework/winforms/controls/windows-forms-controls-by-function.md)