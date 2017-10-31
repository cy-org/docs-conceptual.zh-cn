---
title: "使用 ShouldSerialize 和 Reset 方法定义默认值 | Microsoft Docs"
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
  - "自定义控件 [Windows 窗体], 属性方法"
  - "Reset 方法"
  - "ShouldPersist 方法"
ms.assetid: 7b6c5e00-3771-46b4-9142-5a80d5864a5e
caps.latest.revision: 11
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 11
---
# 使用 ShouldSerialize 和 Reset 方法定义默认值
如果属性不具有简单的默认值，则可以为属性提供可选方法 `ShouldSerialize` 和 `Reset`。  如果属性具有简单的默认值，则应用 <xref:System.ComponentModel.DefaultValueAttribute> 并将默认值提供给特性类构造函数。  上述机制中的任何一种都可以在设计器中启用下列功能：  
  
-   该属性在修改了其默认值的情况下，在属性浏览器中提供可视化表示。  
  
-   用户可以右击该属性并选择**“重置”**将该属性还原为其默认值。  
  
-   该设计器生成更为有效的代码。  
  
    > [!NOTE]
    >  可以应用 <xref:System.ComponentModel.DefaultValueAttribute> 或提供 `Reset`*属性名* 和 `ShouldSerialize`*属性名* 方法。  但两者不能同时使用。  
  
 `Reset` *属性名* 方法将属性设置为其默认值，如以下代码片段所示。  
  
```vb  
Public Sub ResetMyFont()  
   MyFont = Nothing  
End Sub  
```  
  
```csharp  
public void ResetMyFont() {  
   MyFont = null;  
}  
```  
  
> [!NOTE]
>  如果属性没有 `Reset` 方法，未用 <xref:System.ComponentModel.DefaultValueAttribute> 进行标记，而且在其声明中不提供默认值，那么该属性的 `Reset` 选项将在 [!INCLUDE[vsprvs](../../../../includes/vsprvs-md.md)] 的 Windows 窗体设计器**“属性”**窗口的快捷菜单中被禁用。  
  
 诸如 [!INCLUDE[vsprvs](../../../../includes/vsprvs-md.md)] 之类的设计器可使用 `ShouldSerialize`*属性名* 方法来检查属性是否已不再使用其默认值，并仅在属性发生改变的情况下将代码写入窗体中，从而更有效地生成代码。  例如：  
  
```vb  
'Returns true if the font has changed; otherwise, returns false.  
' The designer writes code to the form only if true is returned.  
Public Function ShouldSerializeMyFont() As Boolean  
   Return Not (thefont Is Nothing)  
End Function  
```  
  
```csharp  
// Returns true if the font has changed; otherwise, returns false.  
// The designer writes code to the form only if true is returned.  
public bool ShouldSerializeMyFont() {  
   return thefont != null;  
}  
```  
  
 完整的代码示例如下。  
  
```vb  
Option Explicit  
Option Strict  
  
Imports System  
Imports System.Windows.Forms  
Imports System.Drawing  
  
Public Class MyControl  
   Inherits Control  
  
   ' Declare an instance of the Font class  
   ' and set its default value to Nothing.  
   Private thefont As Font = Nothing  
  
   ' The MyFont property.   
   Public Property MyFont() As Font  
      ' Note that the Font property never  
      ' returns null.  
      Get  
         If Not (thefont Is Nothing) Then  
            Return thefont  
         End If  
         If Not (Parent Is Nothing) Then  
            Return Parent.Font  
         End If  
         Return Control.DefaultFont  
      End Get  
      Set  
         thefont = value  
      End Set  
   End Property  
  
   Public Function ShouldSerializeMyFont() As Boolean  
      Return Not (thefont Is Nothing)  
   End Function  
  
   Public Sub ResetMyFont()  
      MyFont = Nothing  
   End Sub  
End Class  
```  
  
```csharp  
using System;  
using System.Windows.Forms;  
using System.Drawing;  
  
public class MyControl : Control {  
   // Declare an instance of the Font class  
   // and set its default value to null.  
   private Font thefont = null;  
  
   // The MyFont property.      
   public Font MyFont {  
      // Note that the MyFont property never  
      // returns null.  
      get {  
         if (thefont != null) return thefont;  
         if (Parent != null) return Parent.Font;  
         return Control.DefaultFont;  
      }  
      set {  
         thefont = value;  
      }  
   }  
  
   public bool ShouldSerializeMyFont() {  
      return thefont != null;  
   }  
  
   public void ResetMyFont() {  
      MyFont = null;  
   }  
}  
```  
  
 在本例中，即使由 `MyFont` 属性访问的私有变量的值为 `null`，属性浏览器也不会显示 `null`，它显示的是父级的 <xref:System.Windows.Forms.Control.Font%2A> 属性（如果该属性不为 `null`），或者是在 <xref:System.Windows.Forms.Control> 中定义的 <xref:System.Windows.Forms.Control.Font%2A> 的默认值。  这样就不能简单地设置 `MyFont`  的默认值，并且不能对该属性应用 <xref:System.ComponentModel.DefaultValueAttribute>，  而是必须为 `MyFont` 属性实现 `ShouldSerialize` 和 `Reset` 方法。  
  
## 请参阅  
 [Windows 窗体控件中的属性](../../../../docs/framework/winforms/controls/properties-in-windows-forms-controls.md)   
 [定义属性](../../../../docs/framework/winforms/controls/defining-a-property-in-windows-forms-controls.md)   
 [属性更改事件](../../../../docs/framework/winforms/controls/property-changed-events.md)