---
title: "集合 (Visual Basic 中) |Microsoft 文档"
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: get-started-article
dev_langs:
- VB
ms.assetid: 5f7749f3-aaf2-4319-b63c-bfa72e1e2b7a
caps.latest.revision: 6
author: stevehoag
ms.author: shoag
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: b3c8de3e22075d576f86bcd4eb599946740ebe16
ms.lasthandoff: 03/13/2017

---
# <a name="collections-visual-basic"></a>集合 (Visual Basic)
对于许多应用程序，你会想要创建和管理相关对象的组。 有两种方法对对象进行分组：通过创建对象的数组，以及通过创建对象的集合。  
  
 数组最适用于创建和使用固定数量的强类型化对象。 有关数组的信息，请参阅[数组](../../../visual-basic/programming-guide/language-features/arrays/index.md)。  
  
 集合提供更灵活的方式来使用对象组。 与数组不同，你使用的对象组随着应用程序更改的需要动态地放大和缩小。 对于某些集合，你可以为放入集合中的任何对象分配一个密钥，这样你便可以使用该密钥快速检索此对象。  
  
 集合是一个类，因此必须在向该集合添加元素之前，声明类的实例。  
  
 如果集合包含一种数据类型的元素，您可以使用中的类之一<xref:System.Collections.Generic?displayProperty=fullName>命名空间。</xref:System.Collections.Generic?displayProperty=fullName> 泛型集合强制类型安全，因此无法向其添加任何其他数据类型。 当你从泛型集合检索元素时，你无需确定其数据类型或对其进行转换。  
  
> [!NOTE]
>  对于本主题中的示例中，包括[导入](../../../visual-basic/language-reference/statements/imports-statement-net-namespace-and-type.md)语句`System.Collections.Generic`和`System.Linq`命名空间。  
  
 **主题内容**  
  
-   [使用简单集合](#BKMK_SimpleCollection)  
  
-   [类型的集合](#BKMK_KindsOfCollections)  
  
    -   [System.Collections.Generic 类](#BKMK_Generic)  
  
    -   [System.Collections.Concurrent 类](#BKMK_Concurrent)  
  
    -   [System.Collections 类](#BKMK_Collections)  
  
    -   [Visual Basic 集合类](#BKMK_VisualBasic)  
  
-   [实现键/值对的集合](#BKMK_KeyValuePairs)  
  
-   [使用 LINQ 访问集合](#BKMK_LINQ)  
  
-   [对集合排序](#BKMK_Sorting)  
  
-   [定义自定义集合](#BKMK_CustomCollection)  
  
-   [迭代器](#BKMK_Iterators)  
  
<a name="BKMK_SimpleCollection"></a>
## <a name="using-a-simple-collection"></a>使用简单集合  
 本部分中的示例使用泛型<xref:System.Collections.Generic.List%601>类，它使您能够使用对象的强类型列表。</xref:System.Collections.Generic.List%601>  
  
 下面的示例创建一个字符串列表，然后循环通过字符串使用[为每个...下一步](../../../visual-basic/language-reference/statements/for-each-next-statement.md)语句。  
  
```vb  
' Create a list of strings.  
Dim salmons As New List(Of String)  
salmons.Add("chinook")  
salmons.Add("coho")  
salmons.Add("pink")  
salmons.Add("sockeye")  
  
' Iterate through the list.  
For Each salmon As String In salmons  
    Console.Write(salmon & " ")  
Next  
'Output: chinook coho pink sockeye  
```  
  
 如果提前知道集合中的内容，则可以使用*集合初始值设定项*来初始化集合。 有关详细信息，请参阅[集合初始值设定项](../../../visual-basic/programming-guide/language-features/collection-initializers/index.md)。  
  
 以下示例与上一示例相同，除了有一个集合初始值设定项用于将元素添加到集合。  
  
```vb  
' Create a list of strings by using a  
' collection initializer.  
Dim salmons As New List(Of String) From  
    {"chinook", "coho", "pink", "sockeye"}  
  
For Each salmon As String In salmons  
    Console.Write(salmon & " ")  
Next  
'Output: chinook coho pink sockeye  
```  
  
 您可以使用[为...下一步](../../../visual-basic/language-reference/statements/for-next-statement.md)语句而不是`For Each`语句循环访问集合。 通过按索引位置访问集合元素实现此目的。 元素的索引开始于 0，结束于元素计数减 1。  
  
 下面的示例循环访问集合中的元素使用`For…Next`而不是`For Each`。  
  
```vb  
Dim salmons As New List(Of String) From  
    {"chinook", "coho", "pink", "sockeye"}  
  
For index = 0 To salmons.Count - 1  
    Console.Write(salmons(index) & " ")  
Next  
'Output: chinook coho pink sockeye  
```  
  
 以下示例通过指定要删除的对象，从集合中删除一个元素。  
  
```vb  
' Create a list of strings by using a  
' collection initializer.  
Dim salmons As New List(Of String) From  
    {"chinook", "coho", "pink", "sockeye"}  
  
' Remove an element in the list by specifying  
' the object.  
salmons.Remove("coho")  
  
For Each salmon As String In salmons  
    Console.Write(salmon & " ")  
Next  
'Output: chinook pink sockeye  
```  
  
 以下示例从一个泛型列表中删除元素。 而不是`For Each`语句，[为...下一步](../../../visual-basic/language-reference/statements/for-next-statement.md)使用按降序顺序循环的语句。 这是因为<xref:System.Collections.Generic.List%601.RemoveAt%2A>方法将导致触发 after 具有较低的索引值的已移除元素的元素。</xref:System.Collections.Generic.List%601.RemoveAt%2A>  
  
```vb  
Dim numbers As New List(Of Integer) From  
    {0, 1, 2, 3, 4, 5, 6, 7, 8, 9}  
  
' Remove odd numbers.  
For index As Integer = numbers.Count - 1 To 0 Step -1  
    If numbers(index) Mod 2 = 1 Then  
        ' Remove the element by specifying  
        ' the zero-based index in the list.  
        numbers.RemoveAt(index)  
    End If  
Next  
  
' Iterate through the list.  
' A lambda expression is placed in the ForEach method  
' of the List(T) object.  
numbers.ForEach(  
    Sub(number) Console.Write(number & " "))  
' Output: 0 2 4 6 8  
```  
  
 类型的元素中<xref:System.Collections.Generic.List%601>，您还可以定义您自己的类。</xref:System.Collections.Generic.List%601> 在下面的示例中，`Galaxy`类，用于通过<xref:System.Collections.Generic.List%601>代码中定义。</xref:System.Collections.Generic.List%601>  
  
```vb  
Private Sub IterateThroughList()  
    Dim theGalaxies As New List(Of Galaxy) From  
        {  
            New Galaxy With {.Name = "Tadpole", .MegaLightYears = 400},  
            New Galaxy With {.Name = "Pinwheel", .MegaLightYears = 25},  
            New Galaxy With {.Name = "Milky Way", .MegaLightYears = 0},  
            New Galaxy With {.Name = "Andromeda", .MegaLightYears = 3}  
        }  
  
    For Each theGalaxy In theGalaxies  
        With theGalaxy  
            Console.WriteLine(.Name & "  " & .MegaLightYears)  
        End With  
    Next  
  
    ' Output:  
    '  Tadpole  400  
    '  Pinwheel  25  
    '  Milky Way  0  
    '  Andromeda  3  
End Sub  
  
Public Class Galaxy  
    Public Property Name As String  
    Public Property MegaLightYears As Integer  
End Class  
```  
  
<a name="BKMK_KindsOfCollections"></a>
## <a name="kinds-of-collections"></a>集合的类型   
 许多通用集合由 .NET Framework 提供。 每种类型的集合用于特定的用途。  
  
 本部分介绍了一些通用集合类：  
  
-   @System.Collections.Generic类  
  
-   @System.Collections.Concurrent类  
  
-   @System.Collections类  
  
-   Visual Basic`Collection`类  
  
<a name="BKMK_Generic"></a>
### <a name="systemcollectionsgeneric-classes"></a>System.Collections.Generic 类  

 可以使用的某个类中创建的泛型集合<xref:System.Collections.Generic>命名空间。</xref:System.Collections.Generic> 当集合中的所有项都具有相同的数据类型时，泛型集合会非常有用。 泛型集合通过仅允许添加所需的数据类型，强制实施强类型化。  
  
 下表列出了一些经常使用的类的<xref:System.Collections.Generic?displayProperty=fullName>命名空间︰</xref:System.Collections.Generic?displayProperty=fullName>  
  
|类|说明|  
|---|---|  
|<xref:System.Collections.Generic.Dictionary%602></xref:System.Collections.Generic.Dictionary%602>|表示基于键进行组织的键/值对的集合。|  
|<xref:System.Collections.Generic.List%601></xref:System.Collections.Generic.List%601>|表示可按索引访问的对象的列表。 提供用于对列表进行搜索、排序和修改的方法。|  
|<xref:System.Collections.Generic.Queue%601></xref:System.Collections.Generic.Queue%601>|表示对象的先进先出 (FIFO) 集合。|  
|<xref:System.Collections.Generic.SortedList%602></xref:System.Collections.Generic.SortedList%602>|表示基于相关的按键进行排序的键/值对的集合<xref:System.Collections.Generic.IComparer%601>实现。</xref:System.Collections.Generic.IComparer%601>|  
|<xref:System.Collections.Generic.Stack%601></xref:System.Collections.Generic.Stack%601>|表示对象的后进先出 (LIFO) 集合。|  
  
 有关其他信息，请参阅[常用集合类型](http://msdn.microsoft.com/library/f5d4c6a4-0d7b-4944-a9fb-3b12d9ebfd55)，[选择集合类](../../../standard/collections/selecting-a-collection-class.md)，和<xref:System.Collections.Generic?displayProperty=fullName>。</xref:System.Collections.Generic?displayProperty=fullName>  
  
<a name="BKMK_Concurrent"></a>
### <a name="systemcollectionsconcurrent-classes"></a>System.Collections.Concurrent 类   
 在.NET Framework 4 或更高版本，在集合<xref:System.Collections.Concurrent>命名空间提供高效的线程安全操作，以便从多个线程访问集合项。</xref:System.Collections.Concurrent>  
  
 中的类<xref:System.Collections.Concurrent>应使用命名空间而不是中的对应类型<xref:System.Collections.Generic?displayProperty=fullName>和<xref:System.Collections?displayProperty=fullName>命名空间，当有多个线程并发访问集合时。</xref:System.Collections?displayProperty=fullName> </xref:System.Collections.Generic?displayProperty=fullName> </xref:System.Collections.Concurrent> 有关详细信息，请参阅[线程安全集合](../../../standard/collections/threadsafe/index.md)和<xref:System.Collections.Concurrent>。</xref:System.Collections.Concurrent>  
  
 中包含一些类<xref:System.Collections.Concurrent>命名空间是<xref:System.Collections.Concurrent.BlockingCollection%601>， <xref:System.Collections.Concurrent.ConcurrentDictionary%602>， <xref:System.Collections.Concurrent.ConcurrentQueue%601>，和<xref:System.Collections.Concurrent.ConcurrentStack%601>。</xref:System.Collections.Concurrent.ConcurrentStack%601> </xref:System.Collections.Concurrent.ConcurrentQueue%601> </xref:System.Collections.Concurrent.ConcurrentDictionary%602> </xref:System.Collections.Concurrent.BlockingCollection%601> </xref:System.Collections.Concurrent>  
  
<a name="BKMK_Collections"></a>
### <a name="systemcollections-classes"></a>System.Collections 类    
 中的类<xref:System.Collections?displayProperty=fullName>命名空间作为指定类型的对象，而是作为类型的对象不存储元素`Object`。</xref:System.Collections?displayProperty=fullName>  
  
 只要有可能，应使用中的泛型集合<xref:System.Collections.Generic?displayProperty=fullName>命名空间或<xref:System.Collections.Concurrent>而不是中的旧类型的命名空间`System.Collections`命名空间。</xref:System.Collections.Concurrent> </xref:System.Collections.Generic?displayProperty=fullName>  
  
 下表列出了一些中的常用类`System.Collections`命名空间︰  
  
|类|描述|  
|---|---|  
|<xref:System.Collections.ArrayList></xref:System.Collections.ArrayList>|表示对象的数组，这些对象的大小会根据需要动态增加。|  
|<xref:System.Collections.Hashtable></xref:System.Collections.Hashtable>|表示根据键的哈希代码进行组织的键/值对的集合。|  
|<xref:System.Collections.Queue></xref:System.Collections.Queue>|表示对象的先进先出 (FIFO) 集合。|  
|<xref:System.Collections.Stack></xref:System.Collections.Stack>|表示对象的后进先出 (LIFO) 集合。|  
  
 <xref:System.Collections.Specialized>命名空间提供了专用的强类型集合类，如仅包含字符串的集合和链接列表和混合字典。</xref:System.Collections.Specialized>  

<a name="BKMK_VisualBasic"></a> 
###  <a name="visual-basic-collection-class"></a>Visual Basic 集合类  
 可以使用 Visual Basic<xref:Microsoft.VisualBasic.Collection>类以访问集合项使用数字索引或`String`密钥。</xref:Microsoft.VisualBasic.Collection> 你可以向集合对象中添加一个已经或还未指定键的项。 如果你添加了不带有键的项，必须使用其数字索引来访问它。  
  
 Visual Basic`Collection`类作为类型存储它的所有元素`Object`，因此您可以添加任何数据类型的项。 没有任何保护措施来防止添加不适当的数据类型。  
  
 当您使用 Visual Basic`Collection`类中，集合中的第一项的索引为 1。 这不同于 .NET Framework 集合类，其起始索引为 0。  
  
 只要有可能，应使用中的泛型集合<xref:System.Collections.Generic?displayProperty=fullName>命名空间或<xref:System.Collections.Concurrent>命名空间而不是 Visual Basic`Collection`类</xref:System.Collections.Concurrent></xref:System.Collections.Generic?displayProperty=fullName>  
  
 有关详细信息，请参阅<xref:Microsoft.VisualBasic.Collection>。</xref:Microsoft.VisualBasic.Collection>  
  
<a name="BKMK_KeyValuePairs"></a>
## <a name="implementing-a-collection-of-keyvalue-pairs"></a>实现键/值对集合   
 <xref:System.Collections.Generic.Dictionary%602>泛型集合使您可以通过使用每个元素的键访问集合中的元素。</xref:System.Collections.Generic.Dictionary%602> 每次对字典的添加都包含一个值和与其关联的键。 快，因为通过它的键来检索一个值是`Dictionary`类实现作为哈希表。  
  
 下面的示例创建`Dictionary`集合并通过循环访问字典`For Each`语句。  
  
```vb  
Private Sub IterateThroughDictionary()  
    Dim elements As Dictionary(Of String, Element) = BuildDictionary()  
  
    For Each kvp As KeyValuePair(Of String, Element) In elements  
        Dim theElement As Element = kvp.Value  
  
        Console.WriteLine("key: " & kvp.Key)  
        With theElement  
            Console.WriteLine("values: " & .Symbol & " " &  
                .Name & " " & .AtomicNumber)  
        End With  
    Next  
End Sub  
  
Private Function BuildDictionary() As Dictionary(Of String, Element)  
    Dim elements As New Dictionary(Of String, Element)  
  
    AddToDictionary(elements, "K", "Potassium", 19)  
    AddToDictionary(elements, "Ca", "Calcium", 20)  
    AddToDictionary(elements, "Sc", "Scandium", 21)  
    AddToDictionary(elements, "Ti", "Titanium", 22)  
  
    Return elements  
End Function  
  
Private Sub AddToDictionary(ByVal elements As Dictionary(Of String, Element),  
ByVal symbol As String, ByVal name As String, ByVal atomicNumber As Integer)  
    Dim theElement As New Element  
  
    theElement.Symbol = symbol  
    theElement.Name = name  
    theElement.AtomicNumber = atomicNumber  
  
    elements.Add(Key:=theElement.Symbol, value:=theElement)  
End Sub  
  
Public Class Element  
    Public Property Symbol As String  
    Public Property Name As String  
    Public Property AtomicNumber As Integer  
End Class  
```  
  
 而是使用集合初始值设定项来生成`Dictionary`集合中，您可以替换`BuildDictionary`和`AddToDictionary`方法替换为以下方法。  
  
```vb  
Private Function BuildDictionary2() As Dictionary(Of String, Element)  
    Return New Dictionary(Of String, Element) From  
        {  
            {"K", New Element With  
                {.Symbol = "K", .Name = "Potassium", .AtomicNumber = 19}},  
            {"Ca", New Element With  
                {.Symbol = "Ca", .Name = "Calcium", .AtomicNumber = 20}},  
            {"Sc", New Element With  
                {.Symbol = "Sc", .Name = "Scandium", .AtomicNumber = 21}},  
            {"Ti", New Element With  
                {.Symbol = "Ti", .Name = "Titanium", .AtomicNumber = 22}}  
        }  
End Function  
```  
  
 下面的示例使用<xref:System.Collections.Generic.Dictionary%602.ContainsKey%2A>方法和<xref:System.Collections.Generic.Dictionary%602.Item%2A>属性`Dictionary`以快速查找按的键的项。</xref:System.Collections.Generic.Dictionary%602.Item%2A> </xref:System.Collections.Generic.Dictionary%602.ContainsKey%2A> `Item`属性使您能够访问中的项`elements`集合使用`elements(symbol)`在 Visual Basic 中的代码。  
  
```vb  
Private Sub FindInDictionary(ByVal symbol As String)  
    Dim elements As Dictionary(Of String, Element) = BuildDictionary()  
  
    If elements.ContainsKey(symbol) = False Then  
        Console.WriteLine(symbol & " not found")  
    Else  
        Dim theElement = elements(symbol)  
        Console.WriteLine("found: " & theElement.Name)  
    End If  
End Sub  
```  
  
 下面的示例改为使用<xref:System.Collections.Generic.Dictionary%602.TryGetValue%2A>方法快速查找项目，请按的键。</xref:System.Collections.Generic.Dictionary%602.TryGetValue%2A>  
  
```vb  
Private Sub FindInDictionary2(ByVal symbol As String)  
    Dim elements As Dictionary(Of String, Element) = BuildDictionary()  
  
    Dim theElement As Element = Nothing  
    If elements.TryGetValue(symbol, theElement) = False Then  
        Console.WriteLine(symbol & " not found")  
    Else  
        Console.WriteLine("found: " & theElement.Name)  
    End If  
End Sub  
```  
  
<a name="BKMK_LINQ"></a> 
##  <a name="using-linq-to-access-a-collection"></a>使用 LINQ 访问集合  
 可以使用 LINQ（语言集成查询）来访问集合。 LINQ 查询提供筛选、排序和分组功能。 有关详细信息，请参阅[在 Visual Basic 中的 LINQ 入门](../../../visual-basic/programming-guide/concepts/linq/getting-started-with-linq.md)。  
  
 下面的示例对泛型运行 LINQ 查询`List`。 LINQ 查询返回一个包含结果的不同集合。  
  
```vb  
Private Sub ShowLINQ()  
    Dim elements As List(Of Element) = BuildList()  
  
    ' LINQ Query.  
    Dim subset = From theElement In elements  
                  Where theElement.AtomicNumber < 22  
                  Order By theElement.Name  
  
    For Each theElement In subset  
        Console.WriteLine(theElement.Name & " " & theElement.AtomicNumber)  
    Next  
  
    ' Output:  
    '  Calcium 20  
    '  Potassium 19  
    '  Scandium 21  
End Sub  
  
Private Function BuildList() As List(Of Element)  
    Return New List(Of Element) From  
        {  
            {New Element With  
                {.Symbol = "K", .Name = "Potassium", .AtomicNumber = 19}},  
            {New Element With  
                {.Symbol = "Ca", .Name = "Calcium", .AtomicNumber = 20}},  
            {New Element With  
                {.Symbol = "Sc", .Name = "Scandium", .AtomicNumber = 21}},  
            {New Element With  
                {.Symbol = "Ti", .Name = "Titanium", .AtomicNumber = 22}}  
        }  
End Function  
  
Public Class Element  
    Public Property Symbol As String  
    Public Property Name As String  
    Public Property AtomicNumber As Integer  
End Class  
```  
  
 <a name="BKMK_Sorting"></a> 
## <a name="sorting-a-collection"></a>对集合排序  
 以下示例阐释了对集合排序的过程。 该示例进行排序的实例`Car` <xref:System.Collections.Generic.List%601>。</xref:System.Collections.Generic.List%601>中存储的类 `Car`类实现<xref:System.IComparable%601>接口，此操作需要<xref:System.IComparable%601.CompareTo%2A>方法来实现。</xref:System.IComparable%601.CompareTo%2A> </xref:System.IComparable%601>  
  
 每次调用<xref:System.IComparable%601.CompareTo%2A>方法可用于排序的一个比较。</xref:System.IComparable%601.CompareTo%2A> 用户编写的代码中`CompareTo`方法返回当前对象与另一个对象的每个比较的值。 如果当前对象小于另一个对象，则返回的值小于零；如果当前对象大于另一个对象，则返回的值大于零；如果当前对象等于另一个对象，则返回的值等于零。 这使你可以在代码中定义大于、小于和等于条件。  
  
 在`ListCars`方法，`cars.Sort()`语句对列表进行排序。 此调用<xref:System.Collections.Generic.List%601.Sort%2A>方法<xref:System.Collections.Generic.List%601>导致`CompareTo`方法来对自动调用`Car`中的对象`List`。</xref:System.Collections.Generic.List%601> </xref:System.Collections.Generic.List%601.Sort%2A>  
  
```vb  
Public Sub ListCars()  
  
    ' Create some new cars.  
    Dim cars As New List(Of Car) From  
    {  
        New Car With {.Name = "car1", .Color = "blue", .Speed = 20},  
        New Car With {.Name = "car2", .Color = "red", .Speed = 50},  
        New Car With {.Name = "car3", .Color = "green", .Speed = 10},  
        New Car With {.Name = "car4", .Color = "blue", .Speed = 50},  
        New Car With {.Name = "car5", .Color = "blue", .Speed = 30},  
        New Car With {.Name = "car6", .Color = "red", .Speed = 60},  
        New Car With {.Name = "car7", .Color = "green", .Speed = 50}  
    }  
  
    ' Sort the cars by color alphabetically, and then by speed  
    ' in descending order.  
    cars.Sort()  
  
    ' View all of the cars.  
    For Each thisCar As Car In cars  
        Console.Write(thisCar.Color.PadRight(5) & " ")  
        Console.Write(thisCar.Speed.ToString & " ")  
        Console.Write(thisCar.Name)  
        Console.WriteLine()  
    Next  
  
    ' Output:  
    '  blue  50 car4  
    '  blue  30 car5  
    '  blue  20 car1  
    '  green 50 car7  
    '  green 10 car3  
    '  red   60 car6  
    '  red   50 car2  
End Sub  
  
Public Class Car  
    Implements IComparable(Of Car)  
  
    Public Property Name As String  
    Public Property Speed As Integer  
    Public Property Color As String  
  
    Public Function CompareTo(ByVal other As Car) As Integer _  
        Implements System.IComparable(Of Car).CompareTo  
        ' A call to this method makes a single comparison that is  
        ' used for sorting.  
  
        ' Determine the relative order of the objects being compared.  
        ' Sort by color alphabetically, and then by speed in  
        ' descending order.  
  
        ' Compare the colors.  
        Dim compare As Integer  
        compare = String.Compare(Me.Color, other.Color, True)  
  
        ' If the colors are the same, compare the speeds.  
        If compare = 0 Then  
            compare = Me.Speed.CompareTo(other.Speed)  
  
            ' Use descending order for speed.  
            compare = -compare  
        End If  
  
        Return compare  
    End Function  
End Class  
```  
  
<a name="BKMK_CustomCollection"></a> 
## <a name="defining-a-custom-collection"></a>定义自定义集合  
 可以通过实现定义集合，<xref:System.Collections.Generic.IEnumerable%601>或<xref:System.Collections.IEnumerable>接口。</xref:System.Collections.IEnumerable> </xref:System.Collections.Generic.IEnumerable%601> 有关其他信息，请参阅[对集合进行枚举](http://msdn.microsoft.com/en-us/71807ea7-9180-48a6-916f-35a5251d477f)。  
  
 尽管您可以定义自定义集合，则通常最好改为使用.NET Framework 中，这一点在说明中包含的集合[集合类型](http://msdn.microsoft.com/library/e76533a9-5033-4a0b-b003-9c2be60d185b)本主题前面的。  
  
 下面的示例定义一个名为的自定义集合类`AllColors`。 此类实现<xref:System.Collections.IEnumerable>接口，此操作需要<xref:System.Collections.IEnumerable.GetEnumerator%2A>方法来实现。</xref:System.Collections.IEnumerable.GetEnumerator%2A> </xref:System.Collections.IEnumerable>  
  
 `GetEnumerator`方法返回的一个实例`ColorEnumerator`类。 `ColorEnumerator`实现<xref:System.Collections.IEnumerator>接口，此操作需要<xref:System.Collections.IEnumerator.Current%2A>属性，<xref:System.Collections.IEnumerator.MoveNext%2A>方法，和<xref:System.Collections.IEnumerator.Reset%2A>方法来实现。</xref:System.Collections.IEnumerator.Reset%2A> </xref:System.Collections.IEnumerator.MoveNext%2A> </xref:System.Collections.IEnumerator.Current%2A> </xref:System.Collections.IEnumerator>  
  
```vb  
Public Sub ListColors()  
    Dim colors As New AllColors()  
  
    For Each theColor As Color In colors  
        Console.Write(theColor.Name & " ")  
    Next  
    Console.WriteLine()  
    ' Output: red blue green  
End Sub  
  
' Collection class.  
Public Class AllColors  
    Implements System.Collections.IEnumerable  
  
    Private _colors() As Color =  
    {  
        New Color With {.Name = "red"},  
        New Color With {.Name = "blue"},  
        New Color With {.Name = "green"}  
    }  
  
    Public Function GetEnumerator() As System.Collections.IEnumerator _  
        Implements System.Collections.IEnumerable.GetEnumerator  
  
        Return New ColorEnumerator(_colors)  
  
        ' Instead of creating a custom enumerator, you could  
        ' use the GetEnumerator of the array.  
        'Return _colors.GetEnumerator  
    End Function  
  
    ' Custom enumerator.  
    Private Class ColorEnumerator  
        Implements System.Collections.IEnumerator  
  
        Private _colors() As Color  
        Private _position As Integer = -1  
  
        Public Sub New(ByVal colors() As Color)  
            _colors = colors  
        End Sub  
  
        Public ReadOnly Property Current() As Object _  
            Implements System.Collections.IEnumerator.Current  
            Get  
                Return _colors(_position)  
            End Get  
        End Property  
  
        Public Function MoveNext() As Boolean _  
            Implements System.Collections.IEnumerator.MoveNext  
            _position += 1  
            Return (_position < _colors.Length)  
        End Function  
  
        Public Sub Reset() Implements System.Collections.IEnumerator.Reset  
            _position = -1  
        End Sub  
    End Class  
End Class  
  
' Element class.  
Public Class Color  
    Public Property Name As String  
End Class  
```  
  
<a name="BKMK_Iterators"></a>
##  <a name="iterators"></a>迭代器  
 *迭代器*用于在集合上执行自定义的迭代。 一个迭代器，可以是一种方法或`get`取值函数。 迭代器使用[产生](../../../visual-basic/language-reference/statements/yield-statement.md)语句可返回一次该集合的每个元素。  
  
 通过使用调用迭代器[为每个...下一步](../../../visual-basic/language-reference/statements/for-each-next-statement.md)语句。 每次迭代`For Each`循环就会调用迭代器。 当`Yield`语句访问中迭代器，则返回表达式，并且保留当前在代码的位置。 下次调用迭代器时，将从该位置重新开始执行。  
  
 有关详细信息，请参阅[迭代器 (Visual Basic 中)](../../../visual-basic/programming-guide/concepts/iterators.md)。  
  
 下面的示例使用迭代器方法。 迭代器方法具有`Yield`内的语句[为...下一步](../../../visual-basic/language-reference/statements/for-next-statement.md)循环。 在`ListEvenNumbers`方法时，每次迭代`For Each`语句体创建迭代器方法，将继续到下一个调用`Yield`语句。  
  
```vb  
Public Sub ListEvenNumbers()  
    For Each number As Integer In EvenSequence(5, 18)  
        Console.Write(number & " ")  
    Next  
    Console.WriteLine()  
    ' Output: 6 8 10 12 14 16 18  
End Sub  
  
Private Iterator Function EvenSequence(  
ByVal firstNumber As Integer, ByVal lastNumber As Integer) _  
As IEnumerable(Of Integer)  
  
' Yield even numbers in the range.  
    For number = firstNumber To lastNumber  
        If number Mod 2 = 0 Then  
            Yield number  
        End If  
    Next  
End Function  
```  
  
## <a name="see-also"></a>另请参阅  
 [集合初始值设定项](../../../visual-basic/programming-guide/language-features/collection-initializers/index.md)   
 [编程概念 (Visual Basic)](../../../visual-basic/programming-guide/concepts/index.md)   
 [Option Strict 语句](../../../visual-basic/language-reference/statements/option-strict-statement.md)   
 [LINQ to Objects (Visual Basic)](../../../visual-basic/programming-guide/concepts/linq/linq-to-objects.md)   
 [并行 LINQ (PLINQ)](http://msdn.microsoft.com/library/3d4d0cd3-bde4-490b-99e7-f4e41be96455)   
 [集合和数据结构](../../../standard/collections/index.md)   
 [创建和操作集合](http://msdn.microsoft.com/en-us/2065398e-eb1a-4821-9188-75f16e42e069)   
 [选择集合类](../../../standard/collections/selecting-a-collection-class.md)   
 [集合中比较和排序](../../../standard/collections/comparisons-and-sorts-within-collections.md)   
 [何时使用泛型集合](../../../standard/collections/when-to-use-generic-collections.md)
