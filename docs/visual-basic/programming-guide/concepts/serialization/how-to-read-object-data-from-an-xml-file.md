---
title: "如何︰ 从 XML 文件 (Visual Basic 中) 中读取对象数据 |Microsoft 文档"
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
ms.assetid: 1e1423bf-74a4-4dde-a3bb-ae1bfc0a68ed
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
ms.openlocfilehash: c448d79a88517925712f79ed061aa90933e3f6d1
ms.lasthandoff: 03/13/2017

---
# <a name="how-to-read-object-data-from-an-xml-file-visual-basic"></a>如何︰ 从 XML 文件 (Visual Basic 中) 中读取对象数据
以下示例将读取对象数据时，以前写入 XML 文件中使用<xref:System.Xml.Serialization.XmlSerializer>类。</xref:System.Xml.Serialization.XmlSerializer>  
  
## <a name="example"></a>示例  
  
```vb  
Public Class Book  
    Public Title As String  
End Class  
  
Public Sub ReadXML()  
    Dim reader As New System.Xml.Serialization.XmlSerializer(GetType(Book))  
    Dim file As New System.IO.StreamReader(  
        "c:\temp\SerializationOverview.xml")  
    Dim overview As Book  
    overview = CType(reader.Deserialize(file), Book)  
    Console.WriteLine(overview.Title)  
End Sub  
```  
  
## <a name="compiling-the-code"></a>编译代码  
 文件名称"c:\temp\SerializationOverview.xml"替换为包含序列化的数据的文件的名称。 有关序列化数据的详细信息，请参阅[如何︰ 将对象数据写入到 XML 文件 (Visual Basic 中)](../../../../visual-basic/programming-guide/concepts/serialization/how-to-write-object-data-to-an-xml-file.md)。  
  
 此类必须具有不带参数的公共构造函数。  
  
 只有公共属性和字段被反序列化。  
  
## <a name="robust-programming"></a>可靠编程  
 以下情况可能会导致异常：  
  
-   正在序列化的类没有公共的无参数构造函数。  
  
-   文件中的数据不表示从类要反序列化的数据。  
  
-   该文件不存在 (<xref:System.IO.IOException>)。</xref:System.IO.IOException>  
  
## <a name="net-framework-security"></a>.NET Framework 安全性  
 始终验证输入内容，并且永远不会反序列化来自不受信任源的数据。 重新创建的对象在反序列化其代码的权限的本地计算机上运行。 在应用程序中使用输入的数据之前，需验证所有的输入内容。  
  
## <a name="see-also"></a>另请参阅  
 <xref:System.IO.StreamWriter></xref:System.IO.StreamWriter>   
 [如何︰ 将对象数据写入到 XML 文件 (Visual Basic)](../../../../visual-basic/programming-guide/concepts/serialization/how-to-write-object-data-to-an-xml-file.md)   
 [序列化 (Visual Basic)](../../../../visual-basic/programming-guide/concepts/serialization/index.md)   
 [Visual Basic 编程指南](../../../../visual-basic/programming-guide/index.md)
