---
title: "如何︰ 查询一组文件夹 (LINQ) (Visual Basic 中) 中的字节总数 |Microsoft 文档"
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
ms.assetid: bfe85ed2-44dc-4ef1-aac7-241622b80a69
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
ms.openlocfilehash: 668a8a4d89f7b81c3aef9b4e1a46ad749c4a8341
ms.lasthandoff: 03/13/2017

---
# <a name="how-to-query-for-the-total-number-of-bytes-in-a-set-of-folders-linq-visual-basic"></a>如何︰ 查询一组文件夹 (LINQ) (Visual Basic 中) 中的字节总数
此示例演示如何检索由指定的文件夹中的所有文件和所有子文件夹所用的字节总数。  
  
## <a name="example"></a>示例  
 <xref:System.Linq.Enumerable.Sum%2A>方法中所选的所有项的值相加时`select`子句。</xref:System.Linq.Enumerable.Sum%2A> 您可以轻松地修改此查询以检索在指定的目录树中的最大或最小文件通过调用<xref:System.Linq.Enumerable.Min%2A>或<xref:System.Linq.Enumerable.Max%2A>而不是<xref:System.Linq.Enumerable.Sum%2A>。</xref:System.Linq.Enumerable.Sum%2A>方法</xref:System.Linq.Enumerable.Max%2A></xref:System.Linq.Enumerable.Min%2A>  
  
```vb  
Module QueryTotalBytes  
    Sub Main()  
  
        ' Change the drive\path if necessary.  
        Dim root As String = "C:\Program Files\Microsoft Visual Studio 9.0\VB"  
  
        'Take a snapshot of the folder contents.  
        ' This method assumes that the application has discovery permissions  
        ' for all folders under the specified path.  
        Dim fileList = My.Computer.FileSystem.GetFiles _  
                  (root, FileIO.SearchOption.SearchAllSubDirectories, "*.*")  
  
        Dim fileQuery = From file In fileList _  
                        Select GetFileLength(file)  
  
        ' Force execution and cache the results to avoid multiple trips to the file system.  
        Dim fileLengths = fileQuery.ToArray()  
  
        ' Find the largest file  
        Dim maxSize = Aggregate aFile In fileLengths Into Max()  
  
        ' Find the total number of bytes  
        Dim totalBytes = Aggregate aFile In fileLengths Into Sum()  
  
        Console.WriteLine("The largest file is " & maxSize & " bytes")  
        Console.WriteLine("There are " & totalBytes & " total bytes in " & _  
                          fileList.Count & " files under " & root)  
  
        ' Keep the console window open in debug mode  
        Console.WriteLine("Press any key to exit.")  
        Console.ReadKey()  
    End Sub  
  
    ' This method is used to catch the possible exception  
    ' that can be raised when accessing the FileInfo.Length property.  
    Function GetFileLength(ByVal filename As String) As Long  
        Dim retval As Long  
        Try  
            Dim fi As New System.IO.FileInfo(filename)  
            retval = fi.Length  
        Catch ex As System.IO.FileNotFoundException  
            ' If a file is no longer present,  
            ' just return zero bytes.   
            retval = 0  
        End Try  
  
        Return retval  
    End Function  
End Module  
```  
  
 如果只需要计算指定的目录树中的字节数，可以执行此操作而无需创建一个 LINQ 查询，因此这样会导致创建列表集合作为数据源的系统开销的效率。 随着查询变得更加复杂，或者在您需要对同一数据源运行多个查询时，会增加 LINQ 方法的实用性。  
  
 查询调用到一个单独的方法来获取文件长度。 这是为了使用可能的异常︰ 如果在另一个线程后删除了该文件将会引发<xref:System.IO.FileInfo>对的调用中创建对象`GetFiles`。</xref:System.IO.FileInfo> 即使<xref:System.IO.FileInfo>对象已创建，会发生异常因为<xref:System.IO.FileInfo>对象将尝试刷新其<xref:System.IO.FileInfo.Length%2A>属性与第一次访问此属性的最新长度。</xref:System.IO.FileInfo.Length%2A> </xref:System.IO.FileInfo> </xref:System.IO.FileInfo> 通过将此操作放在查询外的一个 try catch 块中，该代码遵循避免在可能会导致的副作用的查询操作的规则。 一般情况下，当使用例外，以确保应用程序不会保留处于未知状态时，必须格外谨慎。  
  
## <a name="compiling-the-code"></a>编译代码  
 创建一个面向.NET Framework 版本 3.5 或更高版本对 System.Core.dll 的引用与项目和一个`Imports`System.Linq 命名空间的语句。  
  
## <a name="see-also"></a>另请参阅  
 [LINQ to Objects (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/linq-to-objects.md)   
 [LINQ 和文件目录 (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/linq-and-file-directories.md)
