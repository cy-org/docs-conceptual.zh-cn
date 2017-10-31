---
title: "&lt;proceduresignature1&gt;因为它重载不符合 cls 的&lt;proceduresignature2&gt;与它不同的只能通过数组参数类型的数组或通过数组参数类型的秩方面 |Microsoft 文档"
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
f1_keywords:
- vbc40035
- bc40035
dev_langs:
- VB
helpviewer_keywords:
- BC40035
ms.assetid: 50a66dbe-2c1e-41bf-96bc-369301c891ac
caps.latest.revision: 11
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
ms.openlocfilehash: 984c04a107444036b980439b231d27a8a81656c1
ms.lasthandoff: 03/13/2017

---
# <a name="ltproceduresignature1gt-is-not-cls-compliant-because-it-overloads-ltproceduresignature2gt-which-differs-from-it-only-by-array-of-array-parameter-types-or-by-the-rank-of-the-array-parameter-types"></a>&lt;proceduresignature1&gt;因为它重载不符合 cls 的&lt;proceduresignature2&gt;与它不同的只能通过数组参数类型的数组或通过数组参数类型的秩方面
过程或属性被标记为`<CLSCompliant(True)>`时它会替代另一个过程或属性以及它们的参数列表的唯一区别是交错数组的嵌套级别还是数组的秩。  
  
 在下面的声明中，在第二个和第三个声明生成此错误。  
  
 `Overloads Sub processArray(ByVal arrayParam() As Integer)`  
  
 `Overloads Sub processArray(ByVal arrayParam()() As Integer)`  
  
 `Overloads Sub processArray(ByVal arrayParam(,) As Integer)`  
  
 第二个声明更改原始的一维参数`arrayParam`到数组的数组。 第三个声明的更改`arrayParam`为二维数组 （级别 2）。 尽管 Visual Basic 允许重载，可只是某项更改不同，这种过载不符合[语言独立性和与语言无关的组件](https://msdn.microsoft.com/library/12a7a7h3)(CLS)。  
  
 当您将应用<xref:System.CLSCompliantAttribute>编程元素中，设置该属性的`isCompliant`至任一参数`True`或`False`来指示符合或不符合性。</xref:System.CLSCompliantAttribute> 此参数没有默认值，必须为其提供一个值。  
  
 如果不适用<xref:System.CLSCompliantAttribute>到元素，它被视为不符合要求。</xref:System.CLSCompliantAttribute>  
  
 默认情况下，此消息是一个警告。 有关隐藏警告或将警告视为错误的信息，请参见 [Configuring Warnings in Visual Basic](https://docs.microsoft.com/visualstudio/ide/configuring-warnings-in-visual-basic)。  
  
 **错误 ID:** BC40035  
  
## <a name="to-correct-this-error"></a>更正此错误  
  
-   如果您需要 CLS 遵从性，对重载进行定义在比仅引用此帮助页上的更改的更多方面不同于彼此。  
  
-   如果你需要重载的区别仅由所做的更改引用此帮助页上，删除<xref:System.CLSCompliantAttribute>于它们的定义或将其标记为`<CLSCompliant(False)>`。</xref:System.CLSCompliantAttribute>  
  
## <a name="see-also"></a>另请参阅  
 [\<PAVE 通过&1;> 编写符合 Cls 的代码](http://msdn.microsoft.com/en-us/4c705105-69a2-4e5e-b24e-0633bc32c7f3)   
 [过程重载](../../../visual-basic/programming-guide/language-features/procedures/procedure-overloading.md)   
 [重载](../../../visual-basic/language-reference/modifiers/overloads.md)
