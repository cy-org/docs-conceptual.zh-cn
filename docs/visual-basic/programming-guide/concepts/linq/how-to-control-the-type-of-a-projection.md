---
title: "如何︰ 控制投影 (Visual Basic 中) 的类型 |Microsoft 文档"
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
ms.assetid: a0171276-0b46-4817-aee5-a8d5191b12fe
caps.latest.revision: 3
author: dotnet-bot
ms.author: dotnetcontent
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 1dd461b51c661121497f9c641d64124f8aee44cb
ms.lasthandoff: 03/13/2017


---
# <a name="how-to-control-the-type-of-a-projection-visual-basic"></a>如何︰ 控制投影 (Visual Basic 中) 的类型
投影是一个过程，这一过程包括：获取一组数据，筛选这些数据，更改数据形状，甚至更改数据的类型。 大多数查询表达式都可执行投影。 大部分此节中所示的查询表达式的计算结果为<xref:System.Collections.Generic.IEnumerable%601>的<xref:System.Xml.Linq.XElement>，但您可以控制投影来创建其他类型的集合的类型。</xref:System.Xml.Linq.XElement> </xref:System.Collections.Generic.IEnumerable%601> 本主题演示如何执行此操作。  
  
## <a name="example"></a>示例  
 下面的示例定义一个新类型 `Customer`。 然后，查询表达式在 `Customer` 子句中实例化新的 `Select` 对象。 这将导致要的查询表达式的类型<xref:System.Collections.Generic.IEnumerable%601>的`Customer`。</xref:System.Collections.Generic.IEnumerable%601>  
  
 此示例使用下面的 XML 文档︰[示例 XML 文件︰ 客户和订单 (LINQ to XML)](../../../../visual-basic/programming-guide/concepts/linq/sample-xml-file-customers-and-orders-linq-to-xml.md)。  
  
```vb  
Public Class Customer  
    Private customerIDValue As String  
    Public Property CustomerID() As String  
        Get  
            Return customerIDValue  
        End Get  
        Set(ByVal value As String)  
            customerIDValue = value  
        End Set  
    End Property  
  
    Private companyNameValue As String  
    Public Property CompanyName() As String  
        Get  
            Return companyNameValue  
        End Get  
        Set(ByVal value As String)  
            companyNameValue = value  
        End Set  
    End Property  
  
    Private contactNameValue As String  
    Public Property ContactName() As String  
        Get  
            Return contactNameValue  
        End Get  
        Set(ByVal value As String)  
            contactNameValue = value  
        End Set  
    End Property  
  
    Public Sub New(ByVal customerID As String, _  
                   ByVal companyName As String, _  
                   ByVal contactName As String)  
        CustomerIDValue = customerID  
        CompanyNameValue = companyName  
        ContactNameValue = contactName  
    End Sub  
  
    Public Overrides Function ToString() As String  
        Return String.Format("{0}:{1}:{2}", Me.CustomerID, Me.CompanyName, Me.ContactName)  
    End Function  
End Class  
  
Sub Main()  
    Dim custOrd As XElement = XElement.Load("CustomersOrders.xml")  
    Dim custList As IEnumerable(Of Customer) = _  
        From el In custOrd.<Customers>.<Customer> _  
        Select New Customer( _  
            el.@<CustomerID>, _  
            el.<CompanyName>.Value, _  
            el.<ContactName>.Value _  
        )  
    For Each cust In custList  
        Console.WriteLine(cust)  
    Next  
End Sub  
  
```  
  
 此代码生成以下输出：  
  
```  
GREAL:Great Lakes Food Market:Howard Snyder  
HUNGC:Hungry Coyote Import Store:Yoshi Latimer  
LAZYK:Lazy K Kountry Store:John Steel  
LETSS:Let's Stop N Shop:Jaime Yorres  
```  
  
## <a name="see-also"></a>另请参阅  
 <xref:System.Linq.Enumerable.Select%2A></xref:System.Linq.Enumerable.Select%2A>   
 [投影和转换 (LINQ to XML) (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/projections-and-transformations-linq-to-xml.md)
