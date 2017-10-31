---
title: "在 Windows 窗体控件中定义属性 | Microsoft Docs"
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
  - "自定义控件 [Windows 窗体], 在代码中定义属性"
  - "属性 [Windows 窗体], 在代码中定义"
ms.assetid: c2eb8277-a842-4d99-89a9-647b901a0434
caps.latest.revision: 13
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 13
---
# 在 Windows 窗体控件中定义属性
有关属性的概述，请参见 [属性概述](../Topic/Properties%20Overview.md)。  定义属性时需考虑以下重要的注意事项：  
  
-   必须将特性应用于定义的属性。  特性用来指定设计器显示属性的方式。  有关详细信息，请参见[组件的设计时特性\)](../Topic/Design-Time%20Attributes%20for%20Components.md)。  
  
-   如果更改属性会影响到控件的视觉显示，请从 `set` 访问器中调用 <xref:System.Windows.Forms.Control.Invalidate%2A> 方法，此方法是控件从 <xref:System.Windows.Forms.Control> 继承的。  而 <xref:System.Windows.Forms.Control.Invalidate%2A> 又会调用 <xref:System.Windows.Forms.Control.OnPaint%2A> 方法来重绘控件。  为提高效率起见，对 <xref:System.Windows.Forms.Control.Invalidate%2A> 的多次调用将产生对 <xref:System.Windows.Forms.Control.OnPaint%2A> 的一次调用。  
  
-   .NET Framework 类库为常见数据类型（如整数、小数、布尔值和其他数据）提供了类型转换器。  类型转换器的目的通常是用来提供字符串到数值的转换（从字符串数据转换为其他数据类型）。  常见数据类型与默认类型转换器（将数值转换为字符串，并将字符串转换为相应数据类型）相关联。  如果定义了自定义（即非标准）数据类型的属性，则应用的特性必须将类型转换器指定为与该属性相关联。  还可以使用特性使自定义 UI 类型编辑器与某个属性相关联。  UI 类型编辑器提供了一个用来编辑属性或数据类型的用户界面。  颜色选择器是 UI 类型编辑器的一个示例。  在本主题的最后给出了特性的示例。  
  
    > [!NOTE]
    >  如果没有类型转换器或 UI 类型编辑器可供自定义属性使用，则可按 [Extending Design\-Time Support](../Topic/Extending%20Design-Time%20Support.md) 中描述的方法来实现一个。  
  
 以下代码片段为自定义控件 `FlashTrackBar` 定义了一个名为 `EndColor` 的自定义属性。  
  
```vb  
Public Class FlashTrackBar  
   Inherits Control  
   ...  
   ' Private data member that backs the EndColor property.  
   Private _endColor As Color = Color.LimeGreen  
  
   ' The Category attribute tells the designer to display  
   ' it in the Flash grouping.   
   ' The Description attribute provides a description of  
   ' the property.   
   <Category("Flash"), _  
   Description("The ending color of the bar.")>  _  
   Public Property EndColor() As Color  
      ' The public property EndColor accesses _endColor.  
      Get  
         Return _endColor  
      End Get  
      Set  
         _endColor = value  
         If Not (baseBackground Is Nothing) And showGradient Then  
            baseBackground.Dispose()  
            baseBackground = Nothing  
         End If  
         ' The Invalidate method calls the OnPaint method, which redraws    
         ' the control.  
         Invalidate()  
      End Set  
   End Property  
   ...  
End Class  
  
```  
  
```csharp  
public class FlashTrackBar : Control {  
   ...  
   // Private data member that backs the EndColor property.  
   private Color endColor = Color.LimeGreen;  
   // The Category attribute tells the designer to display  
   // it in the Flash grouping.   
   // The Description attribute provides a description of  
   // the property.   
   [  
   Category("Flash"),  
   Description("The ending color of the bar.")  
   ]  
   // The public property EndColor accesses endColor.  
   public Color EndColor {  
      get {  
         return endColor;  
      }  
      set {  
         endColor = value;  
         if (baseBackground != null && showGradient) {  
            baseBackground.Dispose();  
            baseBackground = null;  
         }  
         // The Invalidate method calls the OnPaint method, which redraws   
         // the control.  
         Invalidate();  
      }  
   }  
   ...  
}  
```  
  
 以下代码片段将类型转换器和 UI 类型编辑器与属性 `Value` 相关联。  在这种情况下，`Value` 是一个整数，且具有默认的类型转换器，但 <xref:System.ComponentModel.TypeConverterAttribute> 特性应用一个自定义类型转换器 \(`FlashTrackBarValueConverter`\)，该类型转换器允许设计器按百分比形式显示该值。  UI 类型编辑器 `FlashTrackBarValueEditor` 允许以可视化的方式显示百分比。  此示例还演示了由 <xref:System.ComponentModel.TypeConverterAttribute> 或 <xref:System.ComponentModel.EditorAttribute> 特性指定的类型转换器或编辑器如何重写默认的转换器。  
  
```vb  
<Category("Flash"), _  
TypeConverter(GetType(FlashTrackBarValueConverter)), _  
Editor(GetType(FlashTrackBarValueEditor), _  
GetType(UITypeEditor)), _  
Description("The current value of the track bar.  You can enter an actual value or a percentage.")>  _  
Public ReadOnly Property Value() As Integer  
...  
End Property  
  
```  
  
```csharp  
[  
Category("Flash"),   
TypeConverter(typeof(FlashTrackBarValueConverter)),  
Editor(typeof(FlashTrackBarValueEditor), typeof(UITypeEditor)),  
Description("The current value of the track bar.  You can enter an actual value or a percentage.")  
]  
public int Value {  
...  
}  
```  
  
## 请参阅  
 [Windows 窗体控件中的属性](../../../../docs/framework/winforms/controls/properties-in-windows-forms-controls.md)   
 [使用 ShouldSerialize 和 Reset 方法定义默认值](../../../../docs/framework/winforms/controls/defining-default-values-with-the-shouldserialize-and-reset-methods.md)   
 [属性更改事件](../../../../docs/framework/winforms/controls/property-changed-events.md)   
 [Windows 窗体控件中的特性](../../../../docs/framework/winforms/controls/attributes-in-windows-forms-controls.md)