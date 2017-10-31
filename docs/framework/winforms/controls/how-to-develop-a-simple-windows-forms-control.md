---
title: "如何：开发简单的 Windows 窗体控件 | Microsoft Docs"
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
  - "Control 类, Windows 窗体"
  - "控件 [Windows 窗体]"
  - "自定义控件 [Windows 窗体], 使用代码创建简单控件"
ms.assetid: 86cbe435-45b7-4cb4-9b5a-47418369758d
caps.latest.revision: 17
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 17
---
# 如何：开发简单的 Windows 窗体控件
本节将带您步入创作自定义 Windows 窗体控件的关键步骤。  在此演练中开发的简单控件允许更改其 <xref:System.Windows.Forms.Control.Text%2A> 属性的对齐方式。  它不会引发或处理事件。  
  
### 创建简单的自定义控件  
  
1.  定义一个从 <xref:System.Windows.Forms.Control?displayProperty=fullName> 派生的类。  
  
    ```vb  
    Public Class FirstControl  
       Inherits Control  
  
    End Class  
    ```  
  
    ```csharp  
    public class FirstControl:Control{}  
    ```  
  
2.  定义属性。  （不要求您定义属性，因为控件从 <xref:System.Windows.Forms.Control> 类继承了许多属性，但大多数自定义控件通常需要定义附加属性。）以下代码片段定义名为 `TextAlignment`  的属性，`FirstControl`  使用该属性来设置从 <xref:System.Windows.Forms.Control> 继承的 <xref:System.Windows.Forms.Control.Text%2A> 属性的显示格式。  有关定义属性的更多信息，请参见 [属性概述](../Topic/Properties%20Overview.md)。  
  
     [!code-csharp[System.Windows.Forms.FirstControl#3](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.FirstControl/CS/FirstControl.cs#3)]
     [!code-vb[System.Windows.Forms.FirstControl#3](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.FirstControl/VB/FirstControl.vb#3)]  
  
     在设置更改控件的视觉显示的属性时，必须调用 <xref:System.Windows.Forms.Control.Invalidate%2A> 方法来重新绘制该控件。  <xref:System.Windows.Forms.Control.Invalidate%2A> 是在基类 <xref:System.Windows.Forms.Control> 中定义的。  
  
3.  重写从 <xref:System.Windows.Forms.Control> 继承的受保护的 <xref:System.Windows.Forms.Control.OnPaint%2A> 方法，以便为控件提供呈现逻辑。  如果不改写 <xref:System.Windows.Forms.Control.OnPaint%2A>，您的控件将无法自行绘制。  在下面的代码片段中，<xref:System.Windows.Forms.Control.OnPaint%2A> 方法显示从 <xref:System.Windows.Forms.Control> 继承的 <xref:System.Windows.Forms.Control.Text%2A> 属性，并使用 `alignmentValue` 字段指定的对齐方式。  
  
     [!code-csharp[System.Windows.Forms.FirstControl#4](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.FirstControl/CS/FirstControl.cs#4)]
     [!code-vb[System.Windows.Forms.FirstControl#4](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.FirstControl/VB/FirstControl.vb#4)]  
  
4.  提供控件特性。  特性可使可视化设计器在设计时适当地显示控件及其属性和事件。  以下代码片段将特性应用于 `TextAlignment` 属性。  在 Visual Studio 这样的设计器中，<xref:System.ComponentModel.CategoryAttribute.Category%2A> 特性（如代码片段所示）使该属性显示在逻辑类别中。  在选择 `TextAlignment` 属性时，<xref:System.ComponentModel.DescriptionAttribute.Description%2A> 特性使说明字符串显示在**“属性”**窗口的底部。  有关特性的更多信息，请参见 [组件的设计时特性\)](../Topic/Design-Time%20Attributes%20for%20Components.md)。  
  
     [!code-csharp[System.Windows.Forms.FirstControl#5](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.FirstControl/CS/FirstControl.cs#5)]
     [!code-vb[System.Windows.Forms.FirstControl#5](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.FirstControl/VB/FirstControl.vb#5)]  
  
5.  （可选）提供控件资源。  通过使用编辑器选项（C\# 中为 `/res`），可以为控件提供诸如位图之类的资源，从而将资源与控件打包。  运行时，可以使用 <xref:System.Resources.ResourceManager> 类的方法检索资源。  有关创建和使用资源的更多信息，请参见 [桌面应用程序中的资源](../../../../docs/framework/resources/index.md)。  
  
6.  编译和部署控件。  要编译和部署 `FirstControl,`，请执行以下步骤：  
  
    1.  将下列示例中的代码保存到源文件（如 FirstControl.cs 或 FirstControl.vb）。  
  
    2.  将源代码编译成程序集，并将其保存到应用程序的目录中。  为了实现这一目的，需在包含源文件的目录中执行以下命令。  
  
        ```vb  
        vbc /t:library /out:[path to your application's directory]/CustomWinControls.dll /r:System.dll /r:System.Windows.Forms.dll /r:System.Drawing.dll FirstControl.vb  
        ```  
  
        ```csharp  
        csc /t:library /out:[path to your application's directory]/CustomWinControls.dll /r:System.dll /r:System.Windows.Forms.dll /r:System.Drawing.dll FirstControl.cs  
        ```  
  
         `/t:library` 编译器选项告诉编译器正在创建的程序集是一个库（而不是一个可执行文件）。  `/out` 选项用来指定程序集的路径和名称。  `/r` 选项提供代码所引用的程序集的名称。  在本示例中，创建了一个仅供您自己的应用程序使用的专用程序集。  因此，您必须将其保存到您的应用程序的目录中。  有关打包和部署控件以进行分发的更多信息，请参见 [部署](../../../../docs/framework/deployment/net-framework-and-applications.md)。  
  
 下面的示例显示了 `FirstControl` 的代码。  该控件包含在命名空间 `CustomWinControls` 中。  命名空间提供了相关类型的逻辑分组。  可以在新命名空间或现有的命名空间中创建控件。  在 C\# 中，`using` 声明（在 Visual Basic 中，`Imports`）允许从命名空间访问类型，而无须使用完全限定的类型名称。  在下面的示例中，`using` 声明允许代码仅以 <xref:System.Windows.Forms.Control> 来访问 <xref:System.Windows.Forms?displayProperty=fullName> 中的 <xref:System.Windows.Forms.Control> 类，而无需使用完全限定名称 <xref:System.Windows.Forms.Control?displayProperty=fullName>。  
  
 [!code-csharp[System.Windows.Forms.FirstControl#1](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.FirstControl/CS/FirstControl.cs#1)]
 [!code-vb[System.Windows.Forms.FirstControl#1](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.FirstControl/VB/FirstControl.vb#1)]  
  
## 在窗体上使用自定义控件  
 下面的示例说明了一个使用 `FirstControl` 的简单窗体。  它创建了三个 `FirstControl` 实例，每个实例都有不同的 `TextAlignment` 属性值。  
  
#### 编译和运行该示例  
  
1.  将下列示例中的代码保存到源文件（SimpleForm.cs 或 SimpleForms.vb）。  
  
2.  通过从包含该源文件的目录中执行以下命令，将源代码编译成可执行的程序集。  
  
    ```vb  
    vbc /r:CustomWinControls.dll /r:System.dll /r:System.Windows.Forms.dll /r:System.Drawing.dll SimpleForm.vb  
    ```  
  
    ```csharp  
    csc /r:CustomWinControls.dll /r:System.dll /r:System.Windows.Forms.dll /r:System.Drawing.dll SimpleForm.cs  
    ```  
  
     CustomWinControls.dll 是包含类 `FirstControl` 的程序集。  该程序集必须与存取它的窗体源文件位于同一目录中（SimpleForm.cs 或 SimpleForms.vb）。  
  
3.  使用下列命令执行 SimpleForm.exe。  
  
    ```  
    SimpleForm  
    ```  
  
 [!code-csharp[System.Windows.Forms.FirstControl#10](../../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.FirstControl/CS/SimpleForm.cs#10)]
 [!code-vb[System.Windows.Forms.FirstControl#10](../../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.FirstControl/VB/SimpleForm.vb#10)]  
  
## 请参阅  
 [Windows 窗体控件中的属性](../../../../docs/framework/winforms/controls/properties-in-windows-forms-controls.md)   
 [Windows 窗体控件中的事件](../../../../docs/framework/winforms/controls/events-in-windows-forms-controls.md)