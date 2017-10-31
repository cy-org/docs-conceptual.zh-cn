---
title: "每个...下一条语句 (Visual Basic 中) |Microsoft 文档"
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
f1_keywords:
- vb.ForEach
- vb.ForEachNext
- vb.Each
- ForEachNext
dev_langs:
- VB
helpviewer_keywords:
- infinite loops
- Next statement, For Each...Next
- endless loops
- loop structures, For Each...Next
- loops, endless
- Each keyword
- instructions, repeating
- For Each statement
- collections, instruction repetition
- loops, infinite
- For Each...Next statements
- For keyword [Visual Basic], For Each...Next statements
- Exit statement, For Each...Next statements
- iteration
ms.assetid: ebce3120-95c3-42b1-b70b-fa7da40c75e2
caps.latest.revision: 56
author: stevehoag
ms.author: shoag
translation.priority.ht:
- de-de
- es-es
- fr-fr
- it-it
- ja-jp
- ko-kr
- ru-ru
- zh-cn
- zh-tw
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: e0173877fa4a57da76fd774d70ce63d2beda23ad
ms.lasthandoff: 03/13/2017

---
# <a name="for-eachnext-statement-visual-basic"></a>For Each...Next 语句 (Visual Basic)
集合中每个元素重复一的组语句。  
  
## <a name="syntax"></a>语法  
  
```  
For Each element [ As datatype ] In group  
    [ statements ]  
    [ Continue For ]  
    [ statements ]  
    [ Exit For ]  
    [ statements ]  
Next [ element ]  
```  
  
## <a name="parts"></a>部件  
  
|术语|定义|  
|---|---|  
|`element`|在所需`For Each`语句。 参数是可选的`Next`语句。 变量。 用于循环访问集合的元素。|  
|`datatype`|如果使用`element`不已声明。 数据类型的`element`。|  
|`group`|必需。 是集合类型或对象类型的变量。 引用的集合对其`statements`要重复。|  
|`statements`|可选。 之间的一个或多个语句`For Each`和`Next`中每一项上运行`group`。|  
|`Continue For`|可选。 将控制转移到的起始位置`For Each`循环。|  
|`Exit For`|可选。 传输控件外的`For Each`循环。|  
|`Next`|必需。 终止的定义`For Each`循环。|  
  
## <a name="simple-example"></a>简单的示例  
 Use a `For Each`...`Next`循环时想要为集合或数组的每个元素重复的一组语句。  
  
> [!TIP]
>  A [For...下一条语句](../../../visual-basic/language-reference/statements/for-next-statement.md)正常时，您可以将每个循环迭代与控制变量相关联，并确定该变量的初始值和最终值。 但是，当您正在同一个集合，初始和最终值的概念没有意义，并且您不必知道集合中存在的元素数量。 在这种情况下， `For Each`...`Next`循环通常是更好的选择。  
  
 在下面的示例中， `For Each`...`Next` 语句循环访问列表集合中的所有元素。  
  
 [!code-vb[VbVbalrStatements #&121;](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/for-each-next-statement_1.vb)]  
  
 有关更多示例，请参阅[集合](http://msdn.microsoft.com/library/e76533a9-5033-4a0b-b003-9c2be60d185b)和[数组](../../../visual-basic/programming-guide/language-features/arrays/index.md)。  
  
## <a name="nested-loops"></a>嵌套的循环  
 您可以嵌套`For Each`通过将另一个循环内的循环。  
  
 下面的示例演示嵌套`For Each`...`Next` 结构表示。  
  
 [!code-vb[VbVbalrStatements #&122;](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/for-each-next-statement_2.vb)]  
  
 每次循环时，则此嵌套循环必须具有一个唯一`element`变量。  
  
 此外可以嵌套不同类型的彼此内部控制结构。 有关详细信息，请参阅[嵌套的控制结构](../../../visual-basic/programming-guide/language-features/control-flow/nested-control-structures.md)。  
  
## <a name="exit-for-and-continue-for"></a>有关退出并继续  
 [Exit For](../../../visual-basic/language-reference/statements/exit-statement.md)语句会导致执行退出`For`...`Next` 为后面的语句的循环，并将控制权`Next`语句。  
  
 `Continue For`语句将控制权立即到循环的下一个迭代。 有关详细信息，请参阅[继续语句](../../../visual-basic/language-reference/statements/continue-statement.md)。  
  
 下面的示例演示如何使用`Continue For`和`Exit For`语句。  
  
 [!code-vb[VbVbalrStatements #&123;](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/for-each-next-statement_3.vb)]  
  
 你可以放置任意数量的`Exit For`中的语句`For Each`循环。 当使用内嵌套`For Each`循环，`Exit For`会导致执行到下一个较高级别的嵌套退出最里面的循环，并将控制权。  
  
 `Exit For`通常在某些条件的评估后使用，因为在`If`...`Then`...`Else`结构。 您可能想要使用`Exit For`针对下列条件︰  
  
-   继续循环不必要或不可能。 这可能引起错误的值或终止请求。  
  
-   中捕获到异常`Try`...`Catch`...`Finally`. 您可以使用`Exit For`末尾`Finally`块。  
  
-   存在无限循环，这是一个循环，无法运行大型或甚至无限数量的次数。 如果检测到此类情况，则可以使用`Exit For`来退出循环。 有关详细信息，请参阅[做...循环语句](../../../visual-basic/language-reference/statements/do-loop-statement.md)。  
  
## <a name="iterators"></a>迭代器  
 您使用*迭代器*要在集合上执行自定义的迭代。 一个迭代器，可以是函数或`Get`取值函数。 它使用`Yield`语句可返回一次该集合的每个元素。  
  
 通过使用调用迭代器`For Each...Next`语句。 每次迭代`For Each`循环就会调用迭代器。 当`Yield`中迭代器中的表达式到达语句`Yield`返回语句，且不保留代码中的当前位置。 下次调用迭代器时，将从该位置重新开始执行。  
  
 下面的示例使用迭代器函数。 迭代器函数具有`Yield`内的语句[为...下一步](../../../visual-basic/language-reference/statements/for-next-statement.md)循环。 在`ListEvenNumbers`方法时，每次迭代`For Each`语句体创建了迭代器函数，它将继续到下一个调用`Yield`语句。  
  
 [!code-vb[VbVbalrStatements #&127;](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/for-each-next-statement_4.vb)]  
  
 有关详细信息，请参阅[迭代器](http://msdn.microsoft.com/library/f45331db-d595-46ec-9142-551d3d1eb1a7)， [Yield 语句](../../../visual-basic/language-reference/statements/yield-statement.md)，和[迭代器](../../../visual-basic/language-reference/modifiers/iterator.md)。  
  
## <a name="technical-implementation"></a>技术实现  
 当`For Each`...`Next` 运行语句时，Visual Basic 集合只有一次，在循环开始之前进行评估。 如果更改了语句块`element`或`group`，这些更改不会影响循环的迭代。  
  
 当在集合中的所有元素已连续都分配给`element`、`For Each`循环停止并将控制权传递到后面的语句`Next`语句。  
  
 如果`element`尚未被外部声明该循环中，您必须将其声明中`For Each`语句。 您可以声明的类型`element`使用由显式`As`语句，或者您可以依赖类型推断为指定类型。 在任一情况下，范围`element`是循环的正文。 但是，不能声明`element`循环内外。  
  
 您可以选择指定`element`中`Next`语句。 这可以提高您的程序的可读性，尤其是在具有嵌套`For Each`循环。 你必须指定相同的变量作为出现在对应的那个`For Each`语句。  
  
 您可能想要避免更改的值`element`在一个循环内。 执行此操作可以导致更难以阅读和调试代码。 更改的值`group`不会影响该集合或它的元素，在第一次进入循环时已确定。  
  
 当在嵌套循环中，如果`Next`外部的嵌套级别语句遇到过`Next`作为内部级别的编译器会引发错误。 但是，编译器可检测到这仅在您指定重叠错误`element`中每个`Next`语句。  
  
 如果您的代码依赖于遍历以特定的顺序集合`For Each`...`Next`循环不是最佳选择，除非您知道的枚举器对象的特征，否则该集合公开。 遍历的顺序不由 Visual Basic 中，而是由确定<xref:System.Collections.IEnumerator.MoveNext%2A>的枚举数对象的方法。</xref:System.Collections.IEnumerator.MoveNext%2A> 因此，您可能无法预测集合中的哪个元素是在中返回的第一个`element`，或者它的下一个要返回给定元素的后面。 您可能会获得更可靠的结果使用其他循环结构，如`For`...`Next` or `Do`...`Loop`.  
  
 数据类型`element`这样的数据类型的元素必须是`group`可以转换为它。  
  
 数据类型`group`必须是指的是集合或数组，它是可枚举的引用类型。 通常这意味着`group`实现的对象是指<xref:System.Collections.IEnumerable>接口`System.Collections`命名空间或<xref:System.Collections.Generic.IEnumerable%601>接口`System.Collections.Generic`命名空间。</xref:System.Collections.Generic.IEnumerable%601> </xref:System.Collections.IEnumerable> `System.Collections.IEnumerable`定义<xref:System.Collections.IEnumerable.GetEnumerator%2A>方法，它返回集合的枚举器对象。</xref:System.Collections.IEnumerable.GetEnumerator%2A> 枚举数对象实现`System.Collections.IEnumerator`接口`System.Collections`命名空间，并公开<xref:System.Collections.IEnumerator.Current%2A>属性和<xref:System.Collections.IEnumerator.Reset%2A>和<xref:System.Collections.IEnumerator.MoveNext%2A>方法。</xref:System.Collections.IEnumerator.MoveNext%2A> </xref:System.Collections.IEnumerator.Reset%2A> </xref:System.Collections.IEnumerator.Current%2A> Visual Basic 使用这些来遍历该集合。  
  
### <a name="narrowing-conversions"></a>收缩转换  
 当`Option Strict`设置为`On`，收缩转换通常会导致编译器错误。 在`For Each`语句，但是，从中的元素的转换`group`到`element`进行求值和在运行时执行收缩转换所致的编译器错误将被抑制。  
  
 在下面的示例中，分配`m`的初始值为`n`时将不会编译`Option Strict`打开，因为转换`Long`到`Integer`是收缩转换。 在`For Each`语句，但是，没有编译器错误是，即使报告分配给`number`要求从同一转换`Long`到`Integer`。 在`For Each`语句中包含很多，运行时错误发生时<xref:Microsoft.VisualBasic.CompilerServices.Conversions.ToInteger%2A>应用于较大的数字。</xref:Microsoft.VisualBasic.CompilerServices.Conversions.ToInteger%2A>  
  
 [!code-vb[VbVbalrStatements #&89;](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/for-each-next-statement_5.vb)]  
  
### <a name="ienumerator-calls"></a>IEnumerator 调用  
 当执行`For Each`...`Next`循环启动时，Visual Basic 验证`group`指的是有效的集合对象。 如果没有，则它引发异常。 否则，它调用<xref:System.Collections.IEnumerator.MoveNext%2A>方法和<xref:System.Collections.IEnumerator.Current%2A>要返回的第一个元素的枚举数对象的属性。</xref:System.Collections.IEnumerator.Current%2A> </xref:System.Collections.IEnumerator.MoveNext%2A> 如果`MoveNext`指示是否有没有下一个元素，即如果该集合为空，`For Each`循环停止并将控制权传递到后面的语句`Next`语句。 否则，则 Visual Basic 设置`element`到第一个元素和运行此语句块。  
  
 每次 Visual Basic 遇到`Next`语句，它返回到`For Each`语句。 它将再次调用`MoveNext`和`Current`要返回的下一个元素，并再次运行块或停止根据结果的循环。 此过程将继续，直至`MoveNext`指示没有下一个元素或`Exit For`遇到语句。  
  
 **对集合进行修改。** 返回的枚举器对象<xref:System.Collections.IEnumerable.GetEnumerator%2A>通常不允许您通过添加、 删除、 替换或重新排列任何元素更改集合。</xref:System.Collections.IEnumerable.GetEnumerator%2A> 如果您已经启动后更改集合`For Each`...`Next`循环中，枚举器对象将变为无效，并访问的元素的下一步尝试导致<xref:System.InvalidOperationException>异常。</xref:System.InvalidOperationException>  
  
 但是，修改此阻止不由[!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]，而是通过实现<xref:System.Collections.IEnumerable>接口。</xref:System.Collections.IEnumerable> 它是可以实现`IEnumerable`允许在迭代期间修改的方式。 如果您正在考虑进行这种动态修改，请确保您了解的特征`IEnumerable`上正在使用的集合实现。  
  
 **修改集合元素。** <xref:System.Collections.IEnumerator.Current%2A>枚举器对象的属性是[ReadOnly](../../../visual-basic/language-reference/modifiers/readonly.md)，并返回集合中的每个元素的本地副本。</xref:System.Collections.IEnumerator.Current%2A> 这意味着您不能修改这些元素本身中`For Each`...`Next` loop. 您所做的任何修改会影响中的本地副本`Current`而不反映回基础集合。 但是，如果元素是引用类型，您可以修改它所指向的实例的成员。 下面的示例修改`BackColor`的每个成员`thisControl`元素。 但是，不能修改`thisControl`本身。  
  
<CodeContentPlaceHolder>1</CodeContentPlaceHolder>  
 前面的示例可以修改`BackColor`的每个成员`thisControl`元素，但是不能修改`thisControl`本身。  
  
 **遍历数组进行初始化。** 因为<xref:System.Array>类实现<xref:System.Collections.IEnumerable>接口，所有数组都公开<xref:System.Array.GetEnumerator%2A>方法。</xref:System.Array.GetEnumerator%2A> </xref:System.Collections.IEnumerable> </xref:System.Array> 这意味着您可以循环访问数组`For Each`...`Next` loop. 但是，只能读取数组元素。 你不能更改它们。  
  
## <a name="example"></a>示例  
 下面的示例列出在 C:\ 目录中的所有文件夹使用<xref:System.IO.DirectoryInfo>类。</xref:System.IO.DirectoryInfo>  
  
 [!code-vb[VbVbalrStatements #&124;](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/for-each-next-statement_6.vb)]  
  
## <a name="example"></a>示例  
 以下示例阐释了对集合排序的过程。 该示例进行排序的实例`Car` <xref:System.Collections.Generic.List%601>。</xref:System.Collections.Generic.List%601>中存储的类 `Car`类实现<xref:System.IComparable%601>接口，此操作需要<xref:System.IComparable%601.CompareTo%2A>方法来实现。</xref:System.IComparable%601.CompareTo%2A> </xref:System.IComparable%601>  
  
 每次调用<xref:System.IComparable%601.CompareTo%2A>方法可用于排序的一个比较。</xref:System.IComparable%601.CompareTo%2A> 用户编写的代码中`CompareTo`方法返回当前对象与另一个对象的每个比较的值。 如果当前对象小于另一个对象，则返回的值小于零；如果当前对象大于另一个对象，则返回的值大于零；如果当前对象等于另一个对象，则返回的值等于零。 这使你可以在代码中定义大于、小于和等于条件。  
  
 在`ListCars`方法，`cars.Sort()`语句对列表进行排序。 此调用<xref:System.Collections.Generic.List%601.Sort%2A>方法<xref:System.Collections.Generic.List%601>导致`CompareTo`方法来对自动调用`Car`中的对象`List`。</xref:System.Collections.Generic.List%601> </xref:System.Collections.Generic.List%601.Sort%2A>  
  
 [!code-vb[VbVbalrStatements #&125;](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/for-each-next-statement_7.vb)]  
  
## <a name="see-also"></a>另请参阅  
 [集合](http://msdn.microsoft.com/library/e76533a9-5033-4a0b-b003-9c2be60d185b)   
 [有关...下一条语句](../../../visual-basic/language-reference/statements/for-next-statement.md)   
 [循环结构](../../../visual-basic/programming-guide/language-features/control-flow/loop-structures.md)   
 [While...While 语句结束](../../../visual-basic/language-reference/statements/while-end-while-statement.md)   
 [执行操作...循环语句](../../../visual-basic/language-reference/statements/do-loop-statement.md)   
 [扩大转换和收缩转换](../../../visual-basic/programming-guide/language-features/data-types/widening-and-narrowing-conversions.md)   
 [对象初始值设定项︰ 命名类型和匿名类型](../../../visual-basic/programming-guide/language-features/objects-and-classes/object-initializers-named-and-anonymous-types.md)   
 [集合初始值设定项](../../../visual-basic/programming-guide/language-features/collection-initializers/index.md)   
 [阵列](../../../visual-basic/programming-guide/language-features/arrays/index.md)
