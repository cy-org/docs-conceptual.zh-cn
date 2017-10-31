---
title: "构成控件 | Microsoft Docs"
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
  - "构成控件"
  - "自定义控件 [Windows 窗体], 构成控件"
  - "用户控件 [Windows 窗体], 构成控件"
  - "UserControl 类"
ms.assetid: 5565e720-198b-4bbd-a2bd-c447ba641798
caps.latest.revision: 16
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 15
---
# 构成控件
组成用户控件的控件（也称作*“构成控件”*）在自定义图形呈现时的灵活性相对较差。  所有 Windows 窗体控件都通过各自的 <xref:System.Windows.Forms.Control.OnPaint%2A> 方法处理自己的呈现。  由于这种方法是受保护的，开发人员无法访问它，因此在绘制控件时必定会执行。  然而，这并不意味着不能添加影响构成控件外观的代码。  附加呈现可以通过添加事件处理程序来完成。  例如，假设正在创作一个 <xref:System.Windows.Forms.UserControl> 控件，该控件有一个名为 `MyButton` 的按钮。  如果想要获取 [Button 类](frlrfSystemWebUIWebControlsButtonClassTopic)无法提供的附加呈现，则要将类似于以下内容的代码添加到用户控件中：  
  
```vb  
Public Sub MyPaint(ByVal sender as Object, e as PaintEventArgs) Handles _  
   MyButton.Paint  
   'Additional rendering code goes here  
End Sub  
  
```  
  
```csharp  
// Add the event handler to the button's Paint event.  
MyButton.Paint +=   
   new System.Windows.Forms.PaintEventHandler (this.MyPaint);  
// Create the custom painting method.  
protected void MyPaint (object sender,   
System.Windows.Forms.PaintEventArgs e)  
{  
   // Additional rendering code goes here.  
}  
```  
  
> [!NOTE]
>  某些 Windows 窗体控件（如 <xref:System.Windows.Forms.TextBox>）是由 Windows 直接绘制的。  在这些情况中，永远不调用 <xref:System.Windows.Forms.Control.OnPaint%2A> 方法，因此永远不会调用上面的示例。  
  
 上例创建一个在每次执行 `MyButton.Paint` 事件时执行的方法，用于将附加的图形化表示形式添加到控件中。  请注意，这并不妨碍 `MyButton.OnPaint` 的执行，因此，除了自定义绘制外，仍将执行通常由某个按钮执行的所有绘制操作。  有关 GDI\+ 技术和自定义呈现的详细信息，请参见[用 GDI\+ 创建图形图像](../../../../docs/framework/winforms/advanced/how-to-create-graphics-objects-for-drawing.md)。  如果想要控件具有唯一的表示形式，则最好创建一个继承的控件，为它编写自定义呈现代码。  有关详细信息，请参见[用户描述的控件](../../../../docs/framework/winforms/controls/user-drawn-controls.md)。  
  
## 请参阅  
 <xref:System.Windows.Forms.UserControl>   
 <xref:System.Windows.Forms.Control.OnPaint%2A>   
 [用户描述的控件](../../../../docs/framework/winforms/controls/user-drawn-controls.md)   
 [如何：创建用于绘制的 Graphics 对象](../../../../docs/framework/winforms/advanced/how-to-create-graphics-objects-for-drawing.md)   
 [各种自定义控件](../../../../docs/framework/winforms/controls/varieties-of-custom-controls.md)