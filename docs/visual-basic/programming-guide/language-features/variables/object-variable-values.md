---
title: "对象变量值 (Visual Basic 中) |Microsoft 文档"
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- VB
helpviewer_keywords:
- object variables, values
- values, of object variables
- data types [Visual Basic], object variable
- variables [Visual Basic], object
ms.assetid: 31555704-58a3-49f1-9a0a-6421f605664f
caps.latest.revision: 18
author: dotnet-bot
ms.author: dotnetcontent
translation.priority.ht:
- cs-cz
- de-de
- es-es
- fr-fr
- it-it
- ja-jp
- ko-kr
- pl-pl
- pt-br
- ru-ru
- tr-tr
- zh-cn
- zh-tw
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: ff219571de9c76802d3f8d3046cf6b6f9d5be9d5
ms.lasthandoff: 03/13/2017

---
# <a name="object-variable-values-visual-basic"></a>对象变量值 (Visual Basic)
变量[Object 数据类型](../../../../visual-basic/language-reference/data-types/object-data-type.md)可以引用任何类型的数据。 在中存储的值`Object`变量被保存别处在内存中，而变量本身保存到数据指针。  
  
## <a name="object-classifier-functions"></a>对象分类器函数  
 [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]提供的函数可返回有关新增功能的信息`Object`变量所引用下, 表中所示。  
  
|函数|如果对象变量引用的则返回 True|  
|--------------|---------------------------------------------------|  
|<xref:Microsoft.VisualBasic.Information.IsArray%2A></xref:Microsoft.VisualBasic.Information.IsArray%2A>|一个值，而不是单个值的数组|  
|<xref:Microsoft.VisualBasic.Information.IsDate%2A></xref:Microsoft.VisualBasic.Information.IsDate%2A>|一个[Date 数据类型](../../../../visual-basic/language-reference/data-types/date-data-type.md)值或可以解释为日期和时间值的字符串|  
|<xref:Microsoft.VisualBasic.Information.IsDBNull%2A></xref:Microsoft.VisualBasic.Information.IsDBNull%2A>|一个对象类型<xref:System.DBNull>，这表示缺少或不存在的数据</xref:System.DBNull>|  
|<xref:Microsoft.VisualBasic.Information.IsError%2A></xref:Microsoft.VisualBasic.Information.IsError%2A>|一个异常对象，它派生自<xref:System.Exception></xref:System.Exception>|  
|<xref:Microsoft.VisualBasic.Information.IsNothing%2A></xref:Microsoft.VisualBasic.Information.IsNothing%2A>|[执行任何操作](../../../../visual-basic/language-reference/nothing.md)，也就是说，没有任何对象当前分配给该变量|  
|<xref:Microsoft.VisualBasic.Information.IsNumeric%2A></xref:Microsoft.VisualBasic.Information.IsNumeric%2A>|一个数字或可以解释为数字的字符串|  
|<xref:Microsoft.VisualBasic.Information.IsReference%2A></xref:Microsoft.VisualBasic.Information.IsReference%2A>|引用类型 （如字符串、 数组、 委托或类类型）|  
  
 可以使用这些函数可以避免提交至某项操作或过程的无效值。  
  
## <a name="typeof-operator"></a>TypeOf 运算符  
 您还可以使用[TypeOf 运算符](../../../../visual-basic/language-reference/operators/typeof-operator.md)来确定对象变量当前是指特定的数据类型。 The `TypeOf`...`Is`表达式计算结果为`True`如果操作数的运行时类型派生自或实现指定的类型。  
  
 下面的示例使用`TypeOf`值和引用类型引用的对象变量上。  
  
```  
' The following statement puts a value type (Integer) in an Object variable.  
Dim num As Object = 10  
' The following statement puts a reference type (Form) in an Object variable.  
Dim frm As Object = New Form()  
If TypeOf num Is Long Then Debug.WriteLine("num is Long")  
If TypeOf num Is Integer Then Debug.WriteLine("num is Integer")  
If TypeOf num Is Short Then Debug.WriteLine("num is Short")  
If TypeOf num Is Object Then Debug.WriteLine("num is Object")  
If TypeOf frm Is Form Then Debug.WriteLine("frm is Form")  
If TypeOf frm Is Label Then Debug.WriteLine("frm is Label")  
If TypeOf frm Is Object Then Debug.WriteLine("frm is Object")  
```  
  
 前面的示例将以下行**调试**窗口︰  
  
 `num is Integer`  
  
 `num is Object`  
  
 `frm is Form`  
  
 `frm is Object`  
  
 对象变量`num`类型的数据是指`Integer`，和`frm`指的是类<xref:System.Windows.Forms.Form>。</xref:System.Windows.Forms.Form>的对象  
  
## <a name="object-arrays"></a>对象数组  
 您可以声明和使用的数组`Object`变量。 当您需要处理各种数据类型和对象类时，这非常有用。 为数组中的所有元素必须都具有相同的声明的数据类型。 声明此数据类型为`Object`可以用于存储对象和类实例及其他数组中的数据类型。  
  
## <a name="see-also"></a>另请参阅  
 [对象变量](../../../../visual-basic/programming-guide/language-features/variables/object-variables.md)   
 [对象变量声明](../../../../visual-basic/programming-guide/language-features/variables/object-variable-declaration.md)   
 [对象变量赋值](../../../../visual-basic/programming-guide/language-features/variables/object-variable-assignment.md)   
 [如何︰ 引用对象的当前实例](../../../../visual-basic/programming-guide/language-features/variables/how-to-refer-to-the-current-instance-of-an-object.md)   
 [如何︰ 确定对象变量引用的类型](../../../../visual-basic/programming-guide/language-features/variables/how-to-determine-what-type-an-object-variable-refers-to.md)   
 [如何︰ 确定两个对象是否相关](../../../../visual-basic/programming-guide/language-features/variables/how-to-determine-whether-two-objects-are-related.md)   
 [如何︰ 确定两个对象是否相同](../../../../visual-basic/programming-guide/language-features/variables/how-to-determine-whether-two-objects-are-identical.md)   
 [数据类型](../../../../visual-basic/programming-guide/language-features/data-types/index.md)
