---
title: "自定义控件中的方法实现 | Microsoft Docs"
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
  - "方法实现的用户控件 [Windows 窗体]"
  - "重载方法的自定义控件 [Windows 窗体]"
  - "方法实现的自定义控件 [Windows 窗体]"
  - "方法 [Windows 窗体]"
  - "自定义控件的方法 [Windows 窗体]"
ms.assetid: 35d14fca-4bb4-4a27-8211-1f7a98ea27de
caps.latest.revision: 11
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 11
---
# 自定义控件中的方法实现
控件中方法的实现与任何其他组件中方法的实现方式相同。  
  
 在 Visual Basic 中，如果要求方法返回一个值，则方法以 `Public Function` 形式实现。 如果不返回值，则方法以 `Public Sub` 形式实现。 使用以下语法声明方法：  
  
```vb  
Public Function ConvertMatterToEnergy(Matter as Integer) As Integer  
   ' Conversion code goes here.  
End Function  
```  
  
 由于函数返回一个值，所以这些数必须指定返回类型（例如整型、字符串型、对象等等）。 可能的话，还须指定 `Function` 或 `Sub` 过程所使用的参数。  
  
 C# 与 Visual Basic 一样，不区分函数和过程。 方法返回值或返回 `void`。 声明 C# 公共方法的语法是：  
  
```csharp  
public int ConvertMatterToEnergy(int matter)  
{  
   // Conversion code goes here.  
}  
```  
  
 在声明方法时，应尽可能将它的所有参数都声明为显式数据类型。 接受对象引用的参数应被声明为特定的类类型，例如 `As Widget` 而不是 `As Object`。 在 Visual Basic 中，默认设置 `Option Strict` 将自动执行此规则。  
  
 键入的参数允许编译器捕获由开发人员犯的很多错误，而不是在运行时才捕获。 编译器总是捕获错误，而运行时测试只相当于测试套件。  
  
## <a name="overloaded-methods"></a>重载方法  
 如果想允许控件的用户为某个方法提供参数的不同组合，则应使用显式数据类型提供该方法的多个重载。 应避免创建声明 `As Object` 的参数，这样声明的参数可以包含任何数据类型，从而会产生测试时无法捕获的错误。  
  
> [!NOTE]
>  公共语言运行时中的通用数据类型是 `Object` 而不是 `Variant`。 `Variant` 已从该语言中移除。  
  
 例如，有一个假想的 `Spin` 控件，其 `Widget` 方法可能允许直接指定旋转方向和速度，或者允许指定另一个 `Widget` 对象作为角动力的来源：  
  
```vb  
Overloads Public Sub Spin( _  
   ByVal SpinDirection As SpinDirectionsEnum, _  
   ByVal RevolutionsPerSecond As Double)  
   ' Implementation code here.  
End Sub  
Overloads Public Sub Spin(ByVal Driver As Widget) _  
   ' Implementation code here.  
End Sub  
```  
  
```csharp  
public void Spin(SpinDirectionsEnum spinDirection, double revolutionsPerSecond)  
{  
   // Implementation code here.  
}  
  
public void Spin(Widget driver)  
{  
   // Implementation code here.  
}  
```  
  
## <a name="see-also"></a>另请参阅  
 [事件](../../../../docs/standard/events/index.md)   
 [Windows 窗体控件中的属性](../../../../docs/framework/winforms/controls/properties-in-windows-forms-controls.md)