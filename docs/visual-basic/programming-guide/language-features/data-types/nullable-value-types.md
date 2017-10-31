---
title: "可以为 null 的值类型 (Visual Basic 中) |Microsoft 文档"
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
f1_keywords:
- vb.Nullable
dev_langs:
- VB
helpviewer_keywords:
- nullable types [Visual Basic]
- '? [Visual Basic]'
- types [Visual Basic], nullable
- nullable types
- data types [Visual Basic], nullable
ms.assetid: 9ac3b602-6f96-4e6d-96f7-cd4e81c468a6
caps.latest.revision: 23
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
ms.openlocfilehash: 9cdf1864fe955a082936596821ee84c831b86444
ms.lasthandoff: 03/13/2017

---
# <a name="nullable-value-types-visual-basic"></a>可以为 Null 的值类型 (Visual Basic)
有时，您将使用的值类型，在某些情况下没有已定义的值。 例如，数据库中的字段可能需要区分具有分配的值有意义，而不让分配的值。 可以扩展值类型，以使其正常值或 null 值。 调用此类扩展*可空类型*。  
  
 每个可以为 null 的类型从泛型构造<xref:System.Nullable%601>结构。</xref:System.Nullable%601> 请考虑用于跟踪与工作相关的活动数据库。 下面的示例构造一个可以为 null`Boolean`类型，并声明该类型的变量。 你可以以下三种方式来编写声明︰  
  
 [!code-vb[VbVbalrNullableValue #&1;](../../../../visual-basic/programming-guide/language-features/data-types/codesnippet/VisualBasic/nullable-value-types_1.vb)]  
  
 该变量`ridesBusToWork`可以包含的值`True`，值为`False`，或者根本没有值。 它的初始默认值根本没有值，它在这种情况下可能意味着，信息具有尚未获得此人。 与此相反，`False`可能是获取的信息，而此人未乘坐公共汽车去上班。  
  
 可以使用可以为 null 的类型来声明变量和属性，而您可以声明具有可以为 null 的类型的元素的数组。 可以使用作为参数，可以为 null 的类型来声明过程，并可以返回 null 的类型从`Function`过程。  
  
 无法构造上如数组、 引用类型的可以为 null 类型`String`，或类。 基础类型必须是值类型。 有关详细信息，请参阅[值类型和引用类型](../../../../visual-basic/programming-guide/language-features/data-types/value-types-and-reference-types.md)。  
  
## <a name="using-a-nullable-type-variable"></a>使用可以为 Null 的类型变量  
 可以为 null 的类型的最重要的成员是其<xref:System.Nullable%601.HasValue%2A>和<xref:System.Nullable%601.Value%2A>属性。</xref:System.Nullable%601.Value%2A> </xref:System.Nullable%601.HasValue%2A> 对于可空类型的变量<xref:System.Nullable%601.HasValue%2A>告诉您此变量是否包含已定义的值。</xref:System.Nullable%601.HasValue%2A> 如果<xref:System.Nullable%601.HasValue%2A>是`True`，你可以读取的值从<xref:System.Nullable%601.Value%2A>。</xref:System.Nullable%601.Value%2A> </xref:System.Nullable%601.HasValue%2A> 请注意，这两<xref:System.Nullable%601.HasValue%2A>和<xref:System.Nullable%601.Value%2A>是`ReadOnly`属性。</xref:System.Nullable%601.Value%2A> </xref:System.Nullable%601.HasValue%2A>  
  
### <a name="default-values"></a>默认值  
 在与 null 的类型，声明一个变量时其<xref:System.Nullable%601.HasValue%2A>属性具有默认值为`False`。</xref:System.Nullable%601.HasValue%2A> 这意味着默认情况下该变量具有未定义的值，而不是其基础值类型的默认值。 在下面的示例中，该变量`numberOfChildren`最初具有未定义的值，即使默认值的`Integer`类型为 0。  
  
 [!code-vb[VbVbalrNullableValue #&2;](../../../../visual-basic/programming-guide/language-features/data-types/codesnippet/VisualBasic/nullable-value-types_2.vb)]  
  
 空值可用于指示未定义的或未知的值。 如果`numberOfChildren`已声明为`Integer`，不会有任何值，则表明，信息当前不可用。  
  
### <a name="storing-values"></a>将值存储  
 典型方式，可以在变量或可以为 null 的类型的属性中存储一个值。 下面的示例将值赋给变量`numberOfChildren`在前面的示例中声明。  
  
 [!code-vb[VbVbalrNullableValue #&3;](../../../../visual-basic/programming-guide/language-features/data-types/codesnippet/VisualBasic/nullable-value-types_3.vb)]  
  
 如果变量或可以为 null 的类型的属性中包含已定义的值，则可以使此恢复到其初始状态，即未获分配的值。 执行此操作通过设置该变量或属性设置为`Nothing`，如下面的示例所示。  
  
 [!code-vb[VbVbalrNullableValue #&4;](../../../../visual-basic/programming-guide/language-features/data-types/codesnippet/VisualBasic/nullable-value-types_4.vb)]  
  
> [!NOTE]
>  虽然您可分配`Nothing`给可以为 null 的类型的变量，不能测试它以`Nothing`使用等号。 比较过程中使用等号`someVar = Nothing`，计算结果始终为`Nothing`。 您可以测试该变量<xref:System.Nullable%601.HasValue%2A>属性`False`，或通过使用测试`Is`或`IsNot`运算符。</xref:System.Nullable%601.HasValue%2A>  
  
### <a name="retrieving-values"></a>检索值  
 若要检索的值可以为 null 的类型的变量，应该首先测试其<xref:System.Nullable%601.HasValue%2A>属性，以确认它具有值。</xref:System.Nullable%601.HasValue%2A> 如果您尝试读取值时<xref:System.Nullable%601.HasValue%2A>是`False`，[!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]引发<xref:System.InvalidOperationException>异常。</xref:System.InvalidOperationException> </xref:System.Nullable%601.HasValue%2A> 下面的示例演示读取该变量的推荐的方式`numberOfChildren`的前面的示例。  
  
 [!code-vb[VbVbalrNullableValue #&5;](../../../../visual-basic/programming-guide/language-features/data-types/codesnippet/VisualBasic/nullable-value-types_5.vb)]  
  
## <a name="comparing-nullable-types"></a>比较 Null 的类型  
 可以为 null 时`Boolean`在布尔表达式中使用变量，结果可能`True`， `False`，或`Nothing`。 下面是真值表`And`和`Or`。 因为`b1`和`b2`现在具有三个可能值有九种组合来评估。  
  
|b1|b2|b1 和 b2|b1 或 b2|  
|--------|--------|---------------|--------------|  
|`Nothing`|`Nothing`|`Nothing`|`Nothing`|  
|`Nothing`|`True`|`Nothing`|`True`|  
|`Nothing`|`False`|`False`|`Nothing`|  
|`True`|`Nothing`|`Nothing`|`True`|  
|`True`|`True`|`True`|`True`|  
|`True`|`False`|`False`|`True`|  
|`False`|`Nothing`|`False`|`Nothing`|  
|`False`|`True`|`False`|`True`|  
|`False`|`False`|`False`|`False`|  
  
 一个布尔型变量或表达式的值时`Nothing`，它既不是`true`也`false`。 请看下面的示例。  
  
 [!code-vb[VbVbalrNullableValue #&6;](../../../../visual-basic/programming-guide/language-features/data-types/codesnippet/VisualBasic/nullable-value-types_6.vb)]  
  
 在此示例中，`b1 And b2`的计算结果为`Nothing`。 因此，`Else`子句执行在每个`If`语句，并输出如下所述︰  
  
 `Expression is not true`  
  
 `Expression is not false`  
  
> [!NOTE]
>  `AndAlso`和`OrElse`，可使用该技术短路计算，必须评估其第二个操作数，当第一个计算结果为`Nothing`。  
  
## <a name="propagation"></a>传播  
 如果一个或两个操作数的算术、 比较、 shift 键或类型运算可以为空，操作的结果也是可以为 null。 如果这两个操作数的值不是`Nothing`，如同它们都不是，对底层的操作数，值执行此操作可以为 null 的类型。 在下面的示例中，变量`compare1`和`sum1`隐式类型化。 如果将鼠标指针停留在其上时，您将看到编译器将为 null 的类型推断为它们两个。  
  
 [!code-vb[VbVbalrNullableValue #&7;](../../../../visual-basic/programming-guide/language-features/data-types/codesnippet/VisualBasic/nullable-value-types_7.vb)]  
  
 如果一个或两个操作数都具有值为`Nothing`，结果将是`Nothing`。  
  
 [!code-vb[VbVbalrNullableValue #&8;](../../../../visual-basic/programming-guide/language-features/data-types/codesnippet/VisualBasic/nullable-value-types_8.vb)]  
  
## <a name="using-nullable-types-with-data"></a>数据中使用可以为 Null 的类型  
 数据库是一个最重要的地方使用可以为 null 的类型。 并非所有数据库对象当前都支持可以为 null 的类型，但设计器生成的表适配器。 请参阅中的"为 Null 的类型的 TableAdapter 支持" [TableAdapter 概述](https://docs.microsoft.com/visualstudio/data-tools/tableadapter-overview)。  
  
## <a name="see-also"></a>另请参阅  
 <xref:System.InvalidOperationException></xref:System.InvalidOperationException>   
 <xref:System.Nullable%601.HasValue%2A></xref:System.Nullable%601.HasValue%2A>   
 [使用可以为 null 的类型](../../../../csharp/programming-guide/nullable-types/using-nullable-types.md)   
 [数据类型](../../../../visual-basic/programming-guide/language-features/data-types/index.md)   
 [值类型和引用类型](../../../../visual-basic/programming-guide/language-features/data-types/value-types-and-reference-types.md)   
 [数据类型疑难解答](../../../../visual-basic/programming-guide/language-features/data-types/troubleshooting-data-types.md)   
 [TableAdapter 概述](https://docs.microsoft.com/visualstudio/data-tools/tableadapter-overview)   
 [如果运算符](../../../../visual-basic/language-reference/operators/if-operator.md)   
 [局部类型推理](../../../../visual-basic/programming-guide/language-features/variables/local-type-inference.md)   
 [Is 运算符](../../../../visual-basic/language-reference/operators/is-operator.md)   
 [IsNot 运算符](../../../../visual-basic/language-reference/operators/isnot-operator.md)
