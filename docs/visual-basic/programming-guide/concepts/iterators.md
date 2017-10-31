---
title: "迭代器 (Visual Basic 中) |Microsoft 文档"
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
dev_langs:
- VB
ms.assetid: f26b5c1e-fe9d-4004-b287-da7919d717ae
caps.latest.revision: 3
author: dotnet-bot
ms.author: dotnetcontent
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 4ea1e21bd8cc392889c477e78338384ed05d4cbb
ms.lasthandoff: 03/13/2017

---
# <a name="iterators-visual-basic"></a>迭代器 (Visual Basic)
*迭代器*可用于单步执行集合如列出和数组。  
  
 迭代器方法或`get`访问器在集合上执行自定义的迭代。 迭代器方法使用[生成](../../../visual-basic/language-reference/statements/yield-statement.md)语句可一次返回每个元素。 当`Yield`到达语句，记住代码中的当前位置。 在下次调用迭代器函数将从该位置重新开始执行。  
  
 通过使用从客户端代码的迭代器[为每个...下一步](../../../visual-basic/language-reference/statements/for-each-next-statement.md)语句中，还是通过使用 LINQ 查询。  
  
 在下面的示例中，第一次迭代`For Each`循环会导致执行按部就班地进行`SomeNumbers`直到第一个迭代器方法`Yield`到达语句。 此迭代返回的值为 3，且不保留当前在迭代器方法的位置。 在循环的下一个迭代，迭代器方法中的执行将继续从何处中断，达到时再次停止`Yield`语句。 此迭代返回值为 5，并再次保留当前在迭代器方法的位置。 在循环完成时到达迭代器方法的末尾。  
  
```vb  
Sub Main()  
    For Each number As Integer In SomeNumbers()  
        Console.Write(number & " ")  
    Next  
    ' Output: 3 5 8  
    Console.ReadKey()  
End Sub  
  
Private Iterator Function SomeNumbers() As System.Collections.IEnumerable  
    Yield 3  
    Yield 5  
    Yield 8  
End Function  
```  
  
 迭代器方法的返回类型或`get`取值函数可以是<xref:System.Collections.IEnumerable>， <xref:System.Collections.Generic.IEnumerable%601>， <xref:System.Collections.IEnumerator>，或<xref:System.Collections.Generic.IEnumerator%601>.</xref:System.Collections.Generic.IEnumerator%601> </xref:System.Collections.IEnumerator> </xref:System.Collections.Generic.IEnumerable%601> </xref:System.Collections.IEnumerable>  
  
 您可以使用`Exit Function`或`Return`语句来终止迭代。  
  
 Visual Basic 迭代器函数或`get`取值函数声明中包括[迭代器](../../../visual-basic/language-reference/modifiers/iterator.md)修饰符。  
  
 在 Visual Studio 2012 中的 Visual Basic 中引入了迭代器。  
  
 **主题内容**  
  
-   [简单的迭代器](#BKMK_SimpleIterator)  
  
-   [创建集合类](#BKMK_CollectionClass)  
  
-   [Try 块](#BKMK_TryBlocks)  
  
-   [匿名方法](#BKMK_AnonymousMethods)  
  
-   [对泛型列表使用迭代器](#BKMK_GenericList)  
  
-   [语法信息](#BKMK_SyntaxInformation)  
  
-   [技术实现](#BKMK_Technical)  
  
-   [迭代器的使用](#BKMK_UseOfIterators)  
  
> [!NOTE]
>  除了简单的迭代器示例主题中的所有示例，包括[导入](../../../visual-basic/language-reference/statements/imports-statement-net-namespace-and-type.md)语句`System.Collections`和`System.Collections.Generic`命名空间。  
  
##  <a name="BKMK_SimpleIterator"></a>简单的迭代器  
 下面的示例都有一个`Yield`内的语句[为...下一步](../../../visual-basic/language-reference/statements/for-next-statement.md)循环。 在`Main`，每次迭代`For Each`语句体创建了迭代器函数，它将继续到下一个调用`Yield`语句。  
  
```vb  
Sub Main()  
    For Each number As Integer In EvenSequence(5, 18)  
        Console.Write(number & " ")  
    Next  
    ' Output: 6 8 10 12 14 16 18  
    Console.ReadKey()  
End Sub  
  
Private Iterator Function EvenSequence(  
ByVal firstNumber As Integer, ByVal lastNumber As Integer) _  
As System.Collections.Generic.IEnumerable(Of Integer)  
  
    ' Yield even numbers in the range.  
    For number As Integer = firstNumber To lastNumber  
        If number Mod 2 = 0 Then  
            Yield number  
        End If  
    Next  
End Function  
```  
  
##  <a name="BKMK_CollectionClass"></a>创建集合类  
 在下面的示例中，`DaysOfTheWeek`类实现<xref:System.Collections.IEnumerable>接口，它要求<xref:System.Collections.IEnumerable.GetEnumerator%2A>方法。</xref:System.Collections.IEnumerable.GetEnumerator%2A> </xref:System.Collections.IEnumerable> 编译器隐式调用`GetEnumerator`方法，它返回<xref:System.Collections.IEnumerator>。</xref:System.Collections.IEnumerator>  
  
 `GetEnumerator`方法通过使用一次返回每个字符串之一`Yield`语句中，和一个`Iterator`修饰符是函数声明中。  
  
```vb  
Sub Main()  
    Dim days As New DaysOfTheWeek()  
    For Each day As String In days  
        Console.Write(day & " ")  
    Next  
    ' Output: Sun Mon Tue Wed Thu Fri Sat  
    Console.ReadKey()  
End Sub  
  
Private Class DaysOfTheWeek  
    Implements IEnumerable  
  
    Public days =  
        New String() {"Sun", "Mon", "Tue", "Wed", "Thu", "Fri", "Sat"}  
  
    Public Iterator Function GetEnumerator() As IEnumerator _  
        Implements IEnumerable.GetEnumerator  
  
        ' Yield each day of the week.  
        For i As Integer = 0 To days.Length - 1  
            Yield days(i)  
        Next  
    End Function  
End Class  
```  
  
 下面的示例创建`Zoo`类，该类包含动物的集合。  
  
 `For Each`引用类实例的语句 (`theZoo`) 隐式调用`GetEnumerator`方法。 `For Each`语句，请参阅`Birds`和`Mammals`属性使用`AnimalsForType`名为迭代器方法。  
  
```vb  
Sub Main()  
    Dim theZoo As New Zoo()  
  
    theZoo.AddMammal("Whale")  
    theZoo.AddMammal("Rhinoceros")  
    theZoo.AddBird("Penguin")  
    theZoo.AddBird("Warbler")  
  
    For Each name As String In theZoo  
        Console.Write(name & " ")  
    Next  
    Console.WriteLine()  
    ' Output: Whale Rhinoceros Penguin Warbler  
  
    For Each name As String In theZoo.Birds  
        Console.Write(name & " ")  
    Next  
    Console.WriteLine()  
    ' Output: Penguin Warbler  
  
    For Each name As String In theZoo.Mammals  
        Console.Write(name & " ")  
    Next  
    Console.WriteLine()  
    ' Output: Whale Rhinoceros  
  
    Console.ReadKey()  
End Sub  
  
Public Class Zoo  
    Implements IEnumerable  
  
    ' Private members.  
    Private animals As New List(Of Animal)  
  
    ' Public methods.  
    Public Sub AddMammal(ByVal name As String)  
        animals.Add(New Animal With {.Name = name, .Type = Animal.TypeEnum.Mammal})  
    End Sub  
  
    Public Sub AddBird(ByVal name As String)  
        animals.Add(New Animal With {.Name = name, .Type = Animal.TypeEnum.Bird})  
    End Sub  
  
    Public Iterator Function GetEnumerator() As IEnumerator _  
        Implements IEnumerable.GetEnumerator  
  
        For Each theAnimal As Animal In animals  
            Yield theAnimal.Name  
        Next  
    End Function  
  
    ' Public members.  
    Public ReadOnly Property Mammals As IEnumerable  
        Get  
            Return AnimalsForType(Animal.TypeEnum.Mammal)  
        End Get  
    End Property  
  
    Public ReadOnly Property Birds As IEnumerable  
        Get  
            Return AnimalsForType(Animal.TypeEnum.Bird)  
        End Get  
    End Property  
  
    ' Private methods.  
    Private Iterator Function AnimalsForType( _  
    ByVal type As Animal.TypeEnum) As IEnumerable  
        For Each theAnimal As Animal In animals  
            If (theAnimal.Type = type) Then  
                Yield theAnimal.Name  
            End If  
        Next  
    End Function  
  
    ' Private class.  
    Private Class Animal  
        Public Enum TypeEnum  
            Bird  
            Mammal  
        End Enum  
  
        Public Property Name As String  
        Public Property Type As TypeEnum  
    End Class  
End Class  
```  
  
##  <a name="BKMK_TryBlocks"></a>Try 块  
 Visual Basic 将允许`Yield`中的语句`Try`块[重试...Catch...Finally 语句](../../../visual-basic/language-reference/statements/try-catch-finally-statement.md)。 一个`Try`具有的块`Yield`语句可以有`Catch`阻止，并且也能`Finally`块。  
  
 下面的示例包含`Try`， `Catch`，和`Finally`块在迭代器函数。 `Finally`之前执行的迭代器函数中的块`For Each`迭代完成。  
  
```vb  
Sub Main()  
    For Each number As Integer In Test()  
        Console.WriteLine(number)  
    Next  
    Console.WriteLine("For Each is done.")  
  
    ' Output:  
    '  3  
    '  4  
    '  Something happened. Yields are done.  
    '  Finally is called.  
    '  For Each is done.  
    Console.ReadKey()  
End Sub  
  
Private Iterator Function Test() As IEnumerable(Of Integer)  
    Try  
        Yield 3  
        Yield 4  
        Throw New Exception("Something happened. Yields are done.")  
        Yield 5  
        Yield 6  
    Catch ex As Exception  
        Console.WriteLine(ex.Message)  
    Finally  
        Console.WriteLine("Finally is called.")  
    End Try  
End Function  
```  
  
 一个`Yield`语句不能包含在内`Catch`块或`Finally`块。  
  
 如果`For Each`（而不是迭代器方法中） 的主体引发了异常，`Catch`未执行迭代器函数中的块，但`Finally`执行迭代器函数中的块。 一个`Catch`迭代器函数内部的块将捕获在迭代器函数内部发生的异常。  
  
##  <a name="BKMK_AnonymousMethods"></a>匿名方法  
 在 Visual Basic 中，一个匿名函数可以是一个迭代器函数。 下面的示例阐释了这一点。  
  
```vb  
Dim iterateSequence = Iterator Function() _  
                      As IEnumerable(Of Integer)  
                          Yield 1  
                          Yield 2  
                      End Function  
  
For Each number As Integer In iterateSequence()  
    Console.Write(number & " ")  
Next  
' Output: 1 2  
Console.ReadKey()  
```  
  
 下面的示例有一个对参数进行验证的非迭代器方法。 该方法返回一个匿名的迭代器，描述集合元素的结果。  
  
```vb  
Sub Main()  
    For Each number As Integer In GetSequence(5, 10)  
        Console.Write(number & " ")  
    Next  
    ' Output: 5 6 7 8 9 10  
    Console.ReadKey()  
End Sub  
  
Public Function GetSequence(ByVal low As Integer, ByVal high As Integer) _  
As IEnumerable  
    ' Validate the arguments.  
    If low < 1 Then  
        Throw New ArgumentException("low is too low")  
    End If  
    If high > 140 Then  
        Throw New ArgumentException("high is too high")  
    End If  
  
    ' Return an anonymous iterator function.  
    Dim iterateSequence = Iterator Function() As IEnumerable  
                              For index = low To high  
                                  Yield index  
                              Next  
                          End Function  
    Return iterateSequence()  
End Function  
```  
  
 如果验证改为在迭代器函数中，不能只有第一次迭代开始时才执行验证`For Each`正文。  
  
##  <a name="BKMK_GenericList"></a>对泛型列表使用迭代器  
 在下面的示例中，`Stack(Of T)`泛型类实现<xref:System.Collections.Generic.IEnumerable%601>泛型接口。</xref:System.Collections.Generic.IEnumerable%601> `Push`方法将值分配给类型的数组`T`。 <xref:System.Collections.Generic.IEnumerable%601.GetEnumerator%2A>方法通过使用返回的数组值`Yield`语句。</xref:System.Collections.Generic.IEnumerable%601.GetEnumerator%2A>  
  
 除了泛型<xref:System.Collections.Generic.IEnumerable%601.GetEnumerator%2A>方法时，非泛型<xref:System.Collections.IEnumerable.GetEnumerator%2A>还必须实现方法。</xref:System.Collections.IEnumerable.GetEnumerator%2A> </xref:System.Collections.Generic.IEnumerable%601.GetEnumerator%2A> 这是因为<xref:System.Collections.Generic.IEnumerable%601>从<xref:System.Collections.IEnumerable>。</xref:System.Collections.IEnumerable>继承</xref:System.Collections.Generic.IEnumerable%601> 非泛型实现服从的通用实现。  
  
 该示例使用命名的迭代器来支持循环访问同一数据集合的各种方法。 这两个命名的迭代器是`TopToBottom`和`BottomToTop`属性，与`TopN`方法。  
  
 `BottomToTop`属性声明包含`Iterator`关键字。  
  
```vb  
Sub Main()  
    Dim theStack As New Stack(Of Integer)  
  
    ' Add items to the stack.  
    For number As Integer = 0 To 9  
        theStack.Push(number)  
    Next  
  
    ' Retrieve items from the stack.  
    ' For Each is allowed because theStack implements  
    ' IEnumerable(Of Integer).  
    For Each number As Integer In theStack  
        Console.Write("{0} ", number)  
    Next  
    Console.WriteLine()  
    ' Output: 9 8 7 6 5 4 3 2 1 0  
  
    ' For Each is allowed, because theStack.TopToBottom  
    ' returns IEnumerable(Of Integer).  
    For Each number As Integer In theStack.TopToBottom  
        Console.Write("{0} ", number)  
    Next  
    Console.WriteLine()  
    ' Output: 9 8 7 6 5 4 3 2 1 0  
  
    For Each number As Integer In theStack.BottomToTop  
        Console.Write("{0} ", number)  
    Next  
    Console.WriteLine()  
    ' Output: 0 1 2 3 4 5 6 7 8 9   
  
    For Each number As Integer In theStack.TopN(7)  
        Console.Write("{0} ", number)  
    Next  
    Console.WriteLine()  
    ' Output: 9 8 7 6 5 4 3  
  
    Console.ReadKey()  
End Sub  
  
Public Class Stack(Of T)  
    Implements IEnumerable(Of T)  
  
    Private values As T() = New T(99) {}  
    Private top As Integer = 0  
  
    Public Sub Push(ByVal t As T)  
        values(top) = t  
        top = top + 1  
    End Sub  
  
    Public Function Pop() As T  
        top = top - 1  
        Return values(top)  
    End Function  
  
    ' This function implements the GetEnumerator method. It allows  
    ' an instance of the class to be used in a For Each statement.  
    Public Iterator Function GetEnumerator() As IEnumerator(Of T) _  
        Implements IEnumerable(Of T).GetEnumerator  
  
        For index As Integer = top - 1 To 0 Step -1  
            Yield values(index)  
        Next  
    End Function  
  
    Public Iterator Function GetEnumerator1() As IEnumerator _  
        Implements IEnumerable.GetEnumerator  
  
        Yield GetEnumerator()  
    End Function  
  
    Public ReadOnly Property TopToBottom() As IEnumerable(Of T)  
        Get  
            Return Me  
        End Get  
    End Property  
  
    Public ReadOnly Iterator Property BottomToTop As IEnumerable(Of T)  
        Get  
            For index As Integer = 0 To top - 1  
                Yield values(index)  
            Next  
        End Get  
    End Property  
  
    Public Iterator Function TopN(ByVal itemsFromTop As Integer) _  
        As IEnumerable(Of T)  
  
        ' Return less than itemsFromTop if necessary.  
        Dim startIndex As Integer =  
            If(itemsFromTop >= top, 0, top - itemsFromTop)  
  
        For index As Integer = top - 1 To startIndex Step -1  
            Yield values(index)  
        Next  
    End Function  
End Class  
  
```  
  
##  <a name="BKMK_SyntaxInformation"></a>语法信息  
 迭代器可作为一种方法或`get`取值函数。 迭代器在事件、 实例构造函数、 静态构造函数或静态析构函数不能出现。  
  
 中的表达式类型必须存在的隐式转换`Yield`语句将返回迭代器的类型。  
  
 在 Visual Basic 中，迭代器方法不能有任何`ByRef`参数。  
  
 在 Visual Basic 程序"让步"不是保留的字并且仅当使用中具有特殊含义`Iterator`方法或`get`取值函数。  
  
##  <a name="BKMK_Technical"></a>技术实现  
 尽管您编写的迭代器作为一种方法，编译器将它转换嵌套类，它是，实际上，状态机。 此类跟踪的迭代器作为多长时间的位置`For Each...Next`客户端代码中的循环继续进行。  
  
 若要查看的编译器会执行，可以使用 Ildasm.exe 工具查看为迭代器方法生成的 Microsoft 中间语言代码。  
  
 当您创建的迭代器的[类](../../../csharp/language-reference/keywords/class.md)或[结构](../../../csharp/language-reference/keywords/struct.md)，不需要实现整个<xref:System.Collections.IEnumerator>接口。</xref:System.Collections.IEnumerator> 当编译器检测到迭代器时，它自动生成`Current`， `MoveNext`，和`Dispose`方法<xref:System.Collections.IEnumerator>或<xref:System.Collections.Generic.IEnumerator%601>接口。</xref:System.Collections.Generic.IEnumerator%601> </xref:System.Collections.IEnumerator>  
  
 上的每次后续迭代`For Each…Next`循环 (或直接调用`IEnumerator.MoveNext`) 下, 一个迭代器代码主体将在上一个后恢复`Yield`语句。 然后继续下一个`Yield`语句之前已到达迭代器主体的结尾，或直到`Exit Function`或`Return`遇到语句。  
  
 不支持迭代器<xref:System.Collections.IEnumerator.Reset%2A?displayProperty=fullName>方法。</xref:System.Collections.IEnumerator.Reset%2A?displayProperty=fullName> 若要重新循环从一开始，你必须获取新的迭代器。  
  
 有关其他信息，请参阅[Visual Basic 语言规范](../../../visual-basic/reference/language-specification.md)。  
  
##  <a name="BKMK_UseOfIterators"></a>迭代器的使用  
 迭代器使您能够维护的简单性`For Each`时需要使用复杂的代码来填充列表序列循环。 当想要执行下列操作时，这很有用︰  
  
-   在第一个之后修改列表序列`For Each`循环迭代。  
  
-   避免完全加载之前的第一个迭代的大型列表`For Each`循环。 一个示例是分页的提取要加载一批表行。 另一个示例是<xref:System.IO.DirectoryInfo.EnumerateFiles%2A>方法，该实现在.NET Framework 中的迭代器方法。</xref:System.IO.DirectoryInfo.EnumerateFiles%2A>  
  
-   封装构建的列表中迭代器。 在迭代器方法中，可以生成该列表，并让行在循环中的每个结果。  
  
## <a name="see-also"></a>另请参阅  
 <xref:System.Collections.Generic></xref:System.Collections.Generic>   
 <xref:System.Collections.Generic.IEnumerable%601></xref:System.Collections.Generic.IEnumerable%601>   
 [每个...下一条语句](../../../visual-basic/language-reference/statements/for-each-next-statement.md)   
 [Yield 语句](../../../visual-basic/language-reference/statements/yield-statement.md)   
 [Iterator](../../../visual-basic/language-reference/modifiers/iterator.md)
