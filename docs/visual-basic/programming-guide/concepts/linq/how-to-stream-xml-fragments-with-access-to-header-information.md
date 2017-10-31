---
title: "如何︰ 访问标头信息 (Visual Basic 中) 的 XML 片段进行流式处理 |Microsoft 文档"
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
ms.assetid: effd10df-87c4-4d7a-8a9a-1434d829dca5
caps.latest.revision: 3
author: dotnet-bot
ms.author: dotnetcontent
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
ms.translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 299a938cd4b10dbca308685e389fab76656ac20b
ms.contentlocale: zh-cn
ms.lasthandoff: 03/13/2017

---
# <a name="how-to-stream-xml-fragments-with-access-to-header-information-visual-basic"></a>如何︰ 访问标头信息 (Visual Basic 中) 的 XML 片段进行流式处理
有时，您必须读取任意大的 XML 文件并在编写您的应用程序时可以预测应用程序的内存需求量。 如果您试图用大 XML 文件填充 XML 树，则内存占用量将与文件大小成正比，也就是说会占用过多内存。 因此，您应改用流处理技术。  
  
 一种方法是编写使用<xref:System.Xml.XmlReader>。</xref:System.Xml.XmlReader>对应用程序 但您可能需要使用 [!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq_md.md)] 来查询 XML 树。 在这种情况下，您可以编写自己的自定义轴方法。 有关详细信息，请参阅[如何︰ 编写 LINQ to XML 轴方法 (Visual Basic 中)](../../../../visual-basic/programming-guide/concepts/linq/how-to-write-a-linq-to-xml-axis-method.md)。  
  
 若要编写您自己的轴方法，您编写一个小的方法使用<xref:System.Xml.XmlReader>来读取各个节点，直到它达到您感兴趣的节点之一。</xref:System.Xml.XmlReader> 该方法随后调用<xref:System.Xml.Linq.XNode.ReadFrom%2A>，从其读取<xref:System.Xml.XmlReader>并实例化 XML 片段。</xref:System.Xml.XmlReader> </xref:System.Xml.Linq.XNode.ReadFrom%2A> 然后，您可以对自定义轴方法编写 LINQ 查询。  
  
 流处理技术最适合只需处理一次源文档的情况，您可以按文档顺序处理各个元素。 某些标准查询运算符，如<xref:System.Linq.Enumerable.OrderBy%2A>、 循环访问其源、 收集的所有数据、 进行排序，以及最后生成序列中的第一项。</xref:System.Linq.Enumerable.OrderBy%2A> 请注意，如果使用可在生成第一项之前具体化源的查询运算符，则不会保持小的内存需求量。  
  
## <a name="example"></a>示例  
 有时，问题会变得更有意思。 在下面的 XML 文档中，自定义轴方法的使用方也必须知道每一项所属的使用方名称。  
  
```xml  
<?xml version="1.0" encoding="utf-8" ?>  
<Root>  
  <Customer>  
    <Name>A. Datum Corporation</Name>  
    <Item>  
      <Key>0001</Key>  
    </Item>  
    <Item>  
      <Key>0002</Key>  
    </Item>  
    <Item>  
      <Key>0003</Key>  
    </Item>  
    <Item>  
      <Key>0004</Key>  
    </Item>  
  </Customer>  
  <Customer>  
    <Name>Fabrikam, Inc.</Name>  
    <Item>  
      <Key>0005</Key>  
    </Item>  
    <Item>  
      <Key>0006</Key>  
    </Item>  
    <Item>  
      <Key>0007</Key>  
    </Item>  
    <Item>  
      <Key>0008</Key>  
    </Item>  
  </Customer>  
  <Customer>  
    <Name>Southridge Video</Name>  
    <Item>  
      <Key>0009</Key>  
    </Item>  
    <Item>  
      <Key>0010</Key>  
    </Item>  
  </Customer>  
</Root>  
```  
  
 本示例采用的方法还将监视此标头信息、保存标头信息，然后生成包含标头信息和所要枚举的详细信息的小型 XML 树。 该轴方法然后生成这个新的小型 XML 树。 之后，查询将可以访问标头信息以及详细信息。  
  
 此方法具有小的内存需求量。 由于生成了所有的详细 XML 片段，不再需要保留对前一个片段的引用，因此，此方法可用于垃圾回收。 请注意，此技术会在堆上创建许多短生存期的对象。  
  
 下面的示例演示如何实现和使用可流处理由 URI 指定的文件中的 XML 片段的自定义轴方法。 此自定义轴经过专门编写，可以处理具有 `Customer`、`Name` 和 `Item` 元素，并且这些元素按上述 `Source.xml` 文档排列的文档。 这是一个过于简单的实现。 将会准备一个更可靠的实现以分析无效文档。  
  
```vb  
Module Module1  
  
    Sub Main()  
        Dim xmlTree = <Root>  
                          <%=  
                              From el In New StreamCustomerItem("Source.xml")  
                              Let itemKey = CInt(el.<Key>.Value)  
                              Where itemKey >= 3 AndAlso itemKey <= 7  
                              Select <Item>  
                                         <Customer><%= el.Parent.<Name>.Value %></Customer>  
                                         <%= el.<Key> %>  
                                     </Item>  
                          %>  
                      </Root>  
  
        Console.WriteLine(xmlTree)  
    End Sub  
  
End Module  
  
Public Class StreamCustomerItem  
    Implements IEnumerable(Of XElement)  
  
    Private _uri As String  
  
    Public Sub New(ByVal uri As String)  
        _uri = uri  
    End Sub  
  
    Public Function GetEnumerator() As IEnumerator(Of XElement) Implements IEnumerable(Of XElement).GetEnumerator  
        Return New StreamCustomerItemEnumerator(_uri)  
    End Function  
  
    Public Function GetEnumerator1() As IEnumerator Implements IEnumerable.GetEnumerator  
        Return Me.GetEnumerator()  
    End Function  
End Class  
  
Public Class StreamCustomerItemEnumerator  
    Implements IEnumerator(Of XElement)  
  
    Private _current As XElement  
    Private _customerName As String  
    Private _reader As Xml.XmlReader  
    Private _uri As String  
  
    Public Sub New(ByVal uri As String)  
        _uri = uri  
        _reader = Xml.XmlReader.Create(_uri)  
        _reader.MoveToContent()  
    End Sub  
  
    Public ReadOnly Property Current As XElement Implements IEnumerator(Of XElement).Current  
        Get  
            Return _current  
        End Get  
    End Property  
  
    Public ReadOnly Property Current1 As Object Implements IEnumerator.Current  
        Get  
            Return Me.Current  
        End Get  
    End Property  
  
    Public Function MoveNext() As Boolean Implements IEnumerator.MoveNext  
        Dim item As XElement  
        Dim name As XElement  
  
        ' Parse the file, save header information when encountered, and return the  
        ' current Item XElement.  
  
        ' loop through Customer elements  
        While _reader.Read()  
            If _reader.NodeType = Xml.XmlNodeType.Element Then  
                Select Case _reader.Name  
                    Case "Customer"  
                        ' move to Name element  
                        While _reader.Read()  
  
                            If _reader.NodeType = Xml.XmlNodeType.Element AndAlso  
                                _reader.Name = "Name" Then  
  
                                name = TryCast(XElement.ReadFrom(_reader), XElement)  
                                _customerName = If(name IsNot Nothing, name.Value, "")  
                                Exit While  
                            End If  
  
                        End While  
                    Case "Item"  
                        item = TryCast(XElement.ReadFrom(_reader), XElement)  
                        Dim tempRoot = <Root>  
                                           <Name><%= _customerName %></Name>  
                                           <%= item %>  
                                       </Root>  
                        _current = item  
                        Return True  
                End Select  
            End If  
        End While  
  
        Return False  
    End Function  
  
    Public Sub Reset() Implements IEnumerator.Reset  
        _reader = Xml.XmlReader.Create(_uri)  
        _reader.MoveToContent()  
    End Sub  
  
#Region "IDisposable Support"  
    Private disposedValue As Boolean ' To detect redundant calls  
  
    ' IDisposable  
    Protected Overridable Sub Dispose(ByVal disposing As Boolean)  
        If Not Me.disposedValue Then  
            If disposing Then  
                _reader.Close()  
            End If  
        End If  
        Me.disposedValue = True  
    End Sub  
  
    Public Sub Dispose() Implements IDisposable.Dispose  
        Dispose(True)  
        GC.SuppressFinalize(Me)  
    End Sub  
#End Region  
  
End Class  
```  
  
 此代码生成以下输出：  
  
```xml  
<Root>  
  <Item>  
    <Customer>A. Datum Corporation</Customer>  
    <Key>0003</Key>  
  </Item>  
  <Item>  
    <Customer>A. Datum Corporation</Customer>  
    <Key>0004</Key>  
  </Item>  
  <Item>  
    <Customer>Fabrikam, Inc.</Customer>  
    <Key>0005</Key>  
  </Item>  
  <Item>  
    <Customer>Fabrikam, Inc.</Customer>  
    <Key>0006</Key>  
  </Item>  
  <Item>  
    <Customer>Fabrikam, Inc.</Customer>  
    <Key>0007</Key>  
  </Item>  
</Root>  
```  
  
## <a name="see-also"></a>另请参阅  
 [高级的 LINQ to XML 编程 (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/advanced-linq-to-xml-programming.md)

