---
title: "如何：实现 CopyToDataTable&lt;T&gt;，其中泛型类型 T 不是 DataRow | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: b27b52cf-6172-485f-a75c-70ff9c5a2bd4
caps.latest.revision: 2
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 2
---
# 如何：实现 CopyToDataTable&lt;T&gt;，其中泛型类型 T 不是 DataRow
<xref:System.Data.DataTable> 对象通常用于数据绑定。  <xref:System.Data.DataTableExtensions.CopyToDataTable%2A> 方法接收查询结果并将数据复制到 <xref:System.Data.DataTable> 中，后者随后会使用该数据进行数据绑定。  但是，只在 <xref:System.Collections.Generic.IEnumerable%601> 源上执行 <xref:System.Data.DataTableExtensions.CopyToDataTable%2A> 方法，其中泛型参数 `T` 的类型为 <xref:System.Data.DataRow>。  虽然这十分有用，但是它并不允许从标量类型的序列、投影匿名类型的查询或执行表联接的查询创建表。  
  
 此主题描述如何实现两个自定义的 `CopyToDataTable<T>` 扩展方法，其接受类型不是 <xref:System.Data.DataRow> 的泛型参数 `T`。  从 <xref:System.Collections.Generic.IEnumerable%601> 源创建 <xref:System.Data.DataTable> 的逻辑包含在 `ObjectShredder<T>` 类中，该类稍后被包装在两个重载的 `CopyToDataTable<T>` 扩展方法中。  `ObjectShredder<T>` 类的 `Shred` 方法返回填充的 <xref:System.Data.DataTable> 并接受三个输入参数：一个 <xref:System.Collections.Generic.IEnumerable%601> 源、一个 <xref:System.Data.DataTable> 和一个 <xref:System.Data.LoadOption> 枚举。  返回的 <xref:System.Data.DataTable> 的初始架构是以类型为 `T` 的架构为基础的。  如果现有表作为输入提供，则该架构必须与类型为 `T` 的架构一致。  每个公共属性和类型为 `T` 的字段将转换为返回的表中的 <xref:System.Data.DataColumn>。  如果源序列包含从 `T` 派生的类型，则为任何其他公共属性或字段扩展返回的表的架构。  
  
 有关使用自定义的 `CopyToDataTable<T>` 方法的示例，请参见[通过查询创建数据表](../../../../docs/framework/data/adonet/creating-a-datatable-from-a-query-linq-to-dataset.md)。  
  
### 在应用程序中实现自定义的 CopyToDataTable\<T\> 方法  
  
1.  实现 `ObjectShredder<T>` 类，以从下面的 <xref:System.Collections.Generic.IEnumerable%601> 源创建 <xref:System.Data.DataTable>：  
  
     [!code-csharp[DP Custom CopyToDataTable Examples#ObjectShredderClass](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DP Custom CopyToDataTable Examples/CS/Program.cs#objectshredderclass)]
     [!code-vb[DP Custom CopyToDataTable Examples#ObjectShredderClass](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DP Custom CopyToDataTable Examples/VB/Module1.vb#objectshredderclass)]  
  
2.  在下面类中实现自定义 `CopyToDataTable<T>` 扩展方法：  
  
     [!code-csharp[DP Custom CopyToDataTable Examples#CustomCopyToDataTableMethods](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DP Custom CopyToDataTable Examples/CS/Program.cs#customcopytodatatablemethods)]
     [!code-vb[DP Custom CopyToDataTable Examples#CustomCopyToDataTableMethods](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DP Custom CopyToDataTable Examples/VB/Module1.vb#customcopytodatatablemethods)]  
  
3.  在应用程序中添加 `ObjectShredder<T>` 类和 `CopyToDataTable<T>` 扩展方法。  
  
    ```vb  
    Module Module1  
        Sub Main()  
        ' Your application code using CopyToDataTable<T>.  
        End Sub  
    End Module  
  
    Public Module CustomLINQtoDataSetMethods  
    …  
    End Module  
  
    Public Class ObjectShredder(Of T)  
    …  
    End Class  
    ```  
  
4.  ```c#  
    class Program  
    {  
            static void Main(string[] args)  
            {  
               // Your application code using CopyToDataTable<T>.  
            }  
    }  
    public static class CustomLINQtoDataSetMethods  
    {  
    …  
    }  
    public class ObjectShredder<T>  
    {  
    …  
    }  
    ```  
  
## 请参阅  
 [通过查询创建数据表](../../../../docs/framework/data/adonet/creating-a-datatable-from-a-query-linq-to-dataset.md)   
 [编程指南](../../../../docs/framework/data/adonet/programming-guide-linq-to-dataset.md)