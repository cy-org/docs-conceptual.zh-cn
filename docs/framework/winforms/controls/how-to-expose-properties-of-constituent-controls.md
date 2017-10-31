---
title: "如何：公开构成控件的属性 | Microsoft Docs"
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
  - "控件 [Windows 窗体], 构成"
  - "自定义控件 [Windows 窗体], 公开属性"
  - "用户控件 [Windows 窗体], 公开构成控件"
ms.assetid: 5c1ec98b-aa48-4823-986e-4712551cfdf1
caps.latest.revision: 13
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 13
---
# 如何：公开构成控件的属性
组成复合控件的控件称为*“构成控件”*。  这些控件通常被声明为私有的，因此开发人员不能访问它们。  如果想要使将来的用户可以使用这些控件的属性，则必须将它们公开给用户。  通过在用户控件中创建一个属性，并使用该属性的 `get` 和 `set` 访问器完成对构成控件的私有属性的改变，就可以使构成控件的属性得以公开。  
  
 假设有一个用户控件，带有名为 `MyButton` 的构成按钮。  在本示例中，当用户请求 `ConstituentButtonBackColor` 属性时，将传递存储在 `MyButton` 的 <xref:System.Windows.Forms.Control.BackColor%2A> 属性中的值。  当用户为此属性赋值时，该值将自动传递给 `MyButton` 的 <xref:System.Windows.Forms.Control.BackColor%2A> 属性，`set` 代码将会执行以更改 `MyButton` 的颜色。  
  
 下面的示例显示了如何公开构成按钮的 <xref:System.Windows.Forms.Control.BackColor%2A> 属性：  
  
```vb  
Public Property ButtonColor() as System.Drawing.Color  
   Get  
      Return MyButton.BackColor  
   End Get  
   Set(Value as System.Drawing.Color)  
      MyButton.BackColor = Value  
   End Set  
End Property  
```  
  
```csharp  
public Color ButtonColor  
{  
   get  
   {  
      return(myButton.BackColor);  
   }  
   set  
   {  
      myButton.BackColor = value;  
   }  
}  
```  
  
### 公开构成控件的属性  
  
1.  创建用户控件的公共属性。  
  
2.  在此属性的 `get` 部分，编写用于检索要公开的属性值的代码。  
  
3.  在此属性的 `set` 部分，编写用于将此属性的值传递给构成控件的公开属性的代码。  
  
## 请参阅  
 <xref:System.Windows.Forms.UserControl>   
 [Windows 窗体控件中的属性](../../../../docs/framework/winforms/controls/properties-in-windows-forms-controls.md)   
 [各种自定义控件](../../../../docs/framework/winforms/controls/varieties-of-custom-controls.md)