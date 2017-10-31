---
title: "如何︰ 将对象数据写入到 XML 文件 (Visual Basic 中) |Microsoft 文档"
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
ms.assetid: f7966480-5ed2-43ac-9894-33427436de2a
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
ms.openlocfilehash: 146ccb7b1999049106d5f0be1ce78e740dfcf060
ms.lasthandoff: 03/13/2017

---
# <a name="how-to-write-object-data-to-an-xml-file-visual-basic"></a>如何︰ 将对象数据写入到 XML 文件 (Visual Basic)
该示例将对象从类写入到 XML 文件使用<xref:System.Xml.Serialization.XmlSerializer>类。</xref:System.Xml.Serialization.XmlSerializer>  
  
## <a name="example"></a>示例  
  
```vb  
Public Module XMLWrite  
  
    Sub Main()  
        WriteXML()  
    End Sub  
  
    Public Class Book  
        Public Title As String  
    End Class  
  
    Public Sub WriteXML()  
        Dim overview As New Book  
        overview.Title = "Serialization Overview"  
        Dim writer As New System.Xml.Serialization.XmlSerializer(GetType(Book))  
        Dim file As New System.IO.StreamWriter(  
            "c:\temp\SerializationOverview.xml")  
        writer.Serialize(file, overview)  
        file.Close()  
    End Sub  
End Module  
```  
  
## <a name="compiling-the-code"></a>编译代码  
 此类必须具有不带参数的公共构造函数。  
  
## <a name="robust-programming"></a>可靠编程  
 以下情况可能会导致异常：  
  
-   正在序列化的类没有公共的无参数构造函数。  
  
-   文件存在并且是只读的 (<xref:System.IO.IOException>)。</xref:System.IO.IOException>  
  
-   路径过长 (<xref:System.IO.PathTooLongException>)。</xref:System.IO.PathTooLongException>  
  
-   磁盘已满 (<xref:System.IO.IOException>)。</xref:System.IO.IOException>  
  
## <a name="net-framework-security"></a>.NET Framework 安全性  
 此示例创建一个新文件，如果该文件不存在。 如果应用程序需要创建一个文件，该应用程序需要`Create`文件夹的访问。 如果该文件已存在，该应用程序仅需要`Write`访问，较弱的特权。 如有可能，会在部署期间，创建该文件，并仅授予更安全`Read`访问单个文件，而不是`Create`文件夹的访问。  
  
## <a name="see-also"></a>另请参阅  
 <xref:System.IO.StreamWriter></xref:System.IO.StreamWriter>   
 [如何︰ 从 XML 文件 (Visual Basic 中) 中读取对象数据](../../../../visual-basic/programming-guide/concepts/serialization/how-to-read-object-data-from-an-xml-file.md)   
 [序列化 (Visual Basic)](../../../../visual-basic/programming-guide/concepts/serialization/index.md)
