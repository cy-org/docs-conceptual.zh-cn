---
title: "数学函数 (Visual Basic) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "数学函数, Visual Basic"
  - "算术运算, 数学函数"
  - "数学例程"
  - "Atn 函数"
ms.assetid: 4d2d82e7-6924-42fe-a4a7-b4dd5bebbd0c
caps.latest.revision: 23
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 23
---
# 数学函数 (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

<xref:System.Math?displayProperty=fullName> 选件类的方法提供三角形，对数和其他常见的算术函数。  
  
## 备注  
 下表列出了 <xref:System.Math?displayProperty=fullName> 选件类的方法。  在 Visual Basic 程序可以使用它们。  
  
|.NET Framework 方法|描述|  
|-----------------------|--------|  
|<xref:System.Math.Abs%2A>|返回数字的绝对值。|  
|<xref:System.Math.Acos%2A>|返回余弦值为指定数字的角度。|  
|<xref:System.Math.Asin%2A>|返回正弦值为指定数字的角度。|  
|<xref:System.Math.Atan%2A>|返回正切值为指定数字的角度。|  
|<xref:System.Math.Atan2%2A>|返回正切值为两个指定数字的商的角度。|  
|<xref:System.Math.BigMul%2A>|返回两个 32 位数完整的产品。|  
|<xref:System.Math.Ceiling%2A>|返回大于或等于指定的 `Decimal` 或 `Double`的最小整数值。|  
|<xref:System.Math.Cos%2A>|返回指定角度的余弦值。|  
|<xref:System.Math.Cosh%2A>|返回指定角度的双曲余弦值。|  
|<xref:System.Math.DivRem%2A>|返回两个 32 位或 64 位带符号整数控件，并返回该输出参数的其余部分。|  
|<xref:System.Math.Exp%2A>|返回 e \(自然对数的底\) 引发到指定的幂次。|  
|<xref:System.Math.Floor%2A>|返回小于或等于指定的 `Decimal` 或 `Double` 数字的最大的整数。|  
|<xref:System.Math.IEEERemainder%2A>|返回余数会将一个指定数目的部门的结果是由另一个指定数目。|  
|<xref:System.Math.Log%2A>|返回指定数量的自然对数 e\(基\) 或一个指定数量的对数在指定的基础。|  
|<xref:System.Math.Log10%2A>|返回指定数字以 10 为底的对数。|  
|<xref:System.Math.Max%2A>|返回大两个数字。|  
|<xref:System.Math.Min%2A>|返回两个数字中较小的一个。|  
|<xref:System.Math.Pow%2A>|返回指定数字的指定次幂。|  
|<xref:System.Math.Round%2A>|返回 `Decimal` 或 `Double` 值四舍五入到最新的整数值或对小数位指定数目的。|  
|<xref:System.Math.Sign%2A>|返回表示数字符号的 `Integer` 值。|  
|<xref:System.Math.Sin%2A>|返回指定角度的正弦值。|  
|<xref:System.Math.Sinh%2A>|返回指定角度的双曲正弦值。|  
|<xref:System.Math.Sqrt%2A>|返回指定数字的平方根。|  
|<xref:System.Math.Tan%2A>|返回指定角度的正切值。|  
|<xref:System.Math.Tanh%2A>|返回指定角度的双曲正切值。|  
|<xref:System.Math.Truncate%2A>|计算一个指定的 `Decimal` 或 `Double` 数字组成部分。|  
  
 若要使用这些功能，无需限定，则应导入命名空间 <xref:System.Math?displayProperty=fullName> 到可通过将以下代码添加到源文件顶部：  
  
```  
Imports System.Math  
```  
  
## 示例  
 本示例使用 <xref:System.Math> 类的 <xref:System.Math.Abs%2A> 方法来计算一个数字的绝对值。  
  
```  
' Returns 50.3.  
Dim MyNumber1 As Double = Math.Abs(50.3)  
' Returns 50.3.  
Dim MyNumber2 As Double = Math.Abs(-50.3)  
```  
  
## 示例  
 本示例使用 <xref:System.Math> 类的 <xref:System.Math.Atan%2A> 方法计算 pi 的值。  
  
```  
Public Function GetPi() As Double  
    ' Calculate the value of pi.  
    Return 4.0 * Math.Atan(1.0)  
End Function  
```  
  
## 示例  
 本示例使用 <xref:System.Math> 类的 <xref:System.Math.Cos%2A> 方法返回角度的余弦值。  
  
```  
Public Function Sec(ByVal angle As Double) As Double  
    ' Calculate the secant of angle, in radians.  
    Return 1.0 / Math.Cos(angle)  
End Function  
```  
  
## 示例  
 本示例使用 <xref:System.Math> 类的 <xref:System.Math.Exp%2A> 方法返回以 e 为底的幂。  
  
```  
Public Function Sinh(ByVal angle As Double) As Double  
    ' Calculate hyperbolic sine of an angle, in radians.  
    Return (Math.Exp(angle) - Math.Exp(-angle)) / 2.0  
End Function  
```  
  
## 示例  
 本示例使用 <xref:System.Math> 类的 <xref:System.Math.Log%2A> 方法返回数字的自然对数。  
  
```  
Public Function Asinh(ByVal value As Double) As Double  
    ' Calculate inverse hyperbolic sine, in radians.  
    Return Math.Log(value + Math.Sqrt(value * value + 1.0))  
End Function  
```  
  
## 示例  
 本示例使用 <xref:System.Math> 类的 <xref:System.Math.Round%2A> 方法将数字舍入为最接近的整数。  
  
```  
' Returns 3.  
Dim MyVar2 As Double = Math.Round(2.8)  
```  
  
## 示例  
 本示例使用 <xref:System.Math> 类的 <xref:System.Math.Sign%2A> 方法确定数字的符号。  
  
```  
' Returns 1.  
Dim MySign1 As Integer = Math.Sign(12)  
' Returns -1.  
Dim MySign2 As Integer = Math.Sign(-2.4)  
' Returns 0.  
Dim MySign3 As Integer = Math.Sign(0)  
```  
  
## 示例  
 本示例使用 <xref:System.Math> 类的 <xref:System.Math.Sin%2A> 方法返回角度的正弦值。  
  
```  
Public Function Csc(ByVal angle As Double) As Double  
    ' Calculate cosecant of an angle, in radians.  
    Return 1.0 / Math.Sin(angle)  
End Function  
```  
  
## 示例  
 本示例使用 <xref:System.Math> 类的 <xref:System.Math.Sqrt%2A> 方法计算数字的平方根。  
  
```  
' Returns 2.  
Dim MySqr1 As Double = Math.Sqrt(4)  
' Returns 4.79583152331272.  
Dim MySqr2 As Double = Math.Sqrt(23)  
' Returns 0.  
Dim MySqr3 As Double = Math.Sqrt(0)  
' Returns NaN (not a number).  
Dim MySqr4 As Double = Math.Sqrt(-4)  
```  
  
## 示例  
 本示例使用 <xref:System.Math> 类的 <xref:System.Math.Tan%2A> 方法返回角度的正切值。  
  
```  
Public Function Ctan(ByVal angle As Double) As Double  
    ' Calculate cotangent of an angle, in radians.  
    Return 1.0 / Math.Tan(angle)  
End Function  
```  
  
## 要求  
 **类：** <xref:System.Math>  
  
 **命名空间：** <xref:System>  
  
 **程序集：**mscorlib（位于 mscorlib.dll 中）  
  
## 请参阅  
 <xref:Microsoft.VisualBasic.VBMath.Rnd%2A>   
 <xref:Microsoft.VisualBasic.VBMath.Randomize%2A>   
 <xref:System.Double.NaN>   
 [派生的数学函数](../../../visual-basic/language-reference/keywords/derived-math-functions.md)   
 [算术运算符](../../../visual-basic/language-reference/operators/arithmetic-operators.md)