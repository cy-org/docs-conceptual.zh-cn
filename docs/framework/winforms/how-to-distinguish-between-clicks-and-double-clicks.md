---
title: "如何：区分单击和双击 | Microsoft Docs"
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
  - "鼠标点击, 单击与双击"
  - "鼠标, 单击"
  - "鼠标, 双击"
ms.assetid: d836ac8c-85bc-4f3a-a761-8aee03dc682c
caps.latest.revision: 13
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 13
---
# 如何：区分单击和双击
通常情况下，一次*单击*会启动一个用户界面 \(UI\) 操作，而一次*双击*则会扩展该操作。  例如，一次单击通常可选择一个项，而双击则可编辑所选的项。  但是，Windows 窗体 Click 事件无法轻松应用于单击和双击执行多个不兼容操作的方案，因为绑定到 <xref:System.Windows.Forms.Control.Click> 或 <xref:System.Windows.Forms.Control.MouseClick> 事件的操作会在操作绑定到 <xref:System.Windows.Forms.Control.DoubleClick> 或 <xref:System.Windows.Forms.Control.MouseDoubleClick> 事件之前执行。  本主题演示此问题的两种解决方案。  一种解决方案是处理双击事件，并回滚单击事件处理过程中的操作。  在极少数情况下，可能需要通过处理 <xref:System.Windows.Forms.Control.MouseDown> 事件并使用 <xref:System.Windows.Forms.SystemInformation> 类的 <xref:System.Windows.Forms.SystemInformation.DoubleClickTime%2A> 和 <xref:System.Windows.Forms.SystemInformation.DoubleClickSize%2A> 属性来模拟单击和双击行为。  度量点击之间的时间，如果在达到 <xref:System.Windows.Forms.SystemInformation.DoubleClickTime%2A> 值之前发生第二次单击，并且单击发生在由 <xref:System.Windows.Forms.SystemInformation.DoubleClickSize%2A> 定义的矩形范围内，请执行双击操作；否则，请执行单击操作。  
  
### 回滚单击操作  
  
-   请确保你正在使用的控件具有标准双击行为。  如果不具有标准双击行为，请启用具有 <xref:System.Windows.Forms.Control.SetStyle%2A> 方法的控件。  处理双击事件，并回滚单击操作以及双击操作。  下面的代码示例演示了如何在启用了双击的情况下创建自定义按钮，以及如何回滚双击事件处理代码中的单击操作。  
  
     [!code-csharp[System.Windows.Forms.ButtonDoubleClick#1](../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.ButtonDoubleClick/CS/Form1.cs#1)]
     [!code-vb[System.Windows.Forms.ButtonDoubleClick#1](../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.ButtonDoubleClick/VB/Form1.vb#1)]  
  
### 区分 MouseDown 事件中的点击  
  
-   请使用适当的 <xref:System.Windows.Forms.SystemInformation> 属性和 <xref:System.Windows.Forms.Timer> 组件来处理 <xref:System.Windows.Forms.Control.MouseDown> 事件和确定点击之间的位置和时间跨度。  根据是否发生单击或双击执行相应的操作。  下面的代码示例演示如何实现这一点。  
  
     [!code-cpp[System.Windows.Forms.SingleVersusDoubleClick#0](../../../samples/snippets/cpp/VS_Snippets_Winforms/System.Windows.Forms.SingleVersusDoubleClick/cpp/form1.cpp#0)]
     [!code-csharp[System.Windows.Forms.SingleVersusDoubleClick#0](../../../samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.SingleVersusDoubleClick/CS/form1.cs#0)]
     [!code-vb[System.Windows.Forms.SingleVersusDoubleClick#0](../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.SingleVersusDoubleClick/VB/form1.vb#0)]  
  
## 编译代码  
 这些示例需要：  
  
-   对 System、System.Drawing 和 System.Windows.Forms 程序集的引用。  
  
 有关从 [!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)] 或 [!INCLUDE[csprcs](../../../includes/csprcs-md.md)] 的命令行生成这些示例的信息，请参阅[从命令行生成](../Topic/Building%20from%20the%20Command%20Line%20\(Visual%20Basic\).md) 或[在命令行上使用 csc.exe 生成](../../../ocs/csharp/language-reference/compiler-options/command-line-building-with-csc-exe.md)。  还可通过将代码粘贴到新项目，在 [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] 中生成此示例。  另请参阅[如何：使用 Visual Studio 编译和运行完整的 Windows 窗体代码示例](http://msdn.microsoft.com/library/Bb129228\(v=vs.110\))。  
  
## 请参阅  
 [Windows 窗体应用程序中的鼠标输入](../../../docs/framework/winforms/mouse-input-in-a-windows-forms-application.md)