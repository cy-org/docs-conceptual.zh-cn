---
title: "如何︰ 捕捉分析错误 (Visual Basic 中) |Microsoft 文档"
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
ms.assetid: 22e9068e-ea58-447b-816e-cd1852c11787
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
ms.openlocfilehash: 0c4ba619d1f269352b3288f6cadf3b6f37a0dc2d
ms.lasthandoff: 03/13/2017

---
# <a name="how-to-catch-parsing-errors-visual-basic"></a>如何︰ 捕捉分析错误 (Visual Basic)
本主题演示如何检测格式不正确或无效的 XML。  
  
 [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)]使用<xref:System.Xml.XmlReader>。</xref:System.Xml.XmlReader>实现 如果不正确或无效的 XML 传递给[!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)]，基础<xref:System.Xml.XmlReader>类将引发异常。</xref:System.Xml.XmlReader> 分析 XML，如的各种方法<xref:System.Xml.Linq.XElement.Parse%2A?displayProperty=fullName>，不会捕捉异常; 然后可以通过您的应用程序捕捉异常。</xref:System.Xml.Linq.XElement.Parse%2A?displayProperty=fullName>  
  
 请注意，如果使用 XML 文本，则无法获取分析错误。 Visual Basic 编译器将捕捉格式不正确或无效的 XML 错误。  
  
## <a name="example"></a>示例  
 下面的代码尝试分析无效的 XML：  
  
```vb  
Try  
    Dim contacts As XElement = XElement.Parse("<Contacts>" & vbCrLf & _  
        "    <Contact>" & vbCrLf & _  
        "        <Name>Jim Wilson</Name>" & vbCrLf & _  
        "    </Contact>" & vbCrLf & _  
        "</Contcts>")  
  
    Console.WriteLine(contacts)  
Catch e As System.Xml.XmlException  
    Console.WriteLine(e.Message)  
End Try  
```  
  
 运行此代码时，会引发以下异常：  
  
```  
The 'Contacts' start tag on line 1 does not match the end tag of 'Contcts'. Line 5, position 13.  
```  
  
 您可以预计的异常的相关信息<xref:System.Xml.Linq.XElement.Parse%2A?displayProperty=fullName>， <xref:System.Xml.Linq.XDocument.Parse%2A?displayProperty=fullName>， <xref:System.Xml.Linq.XElement.Load%2A?displayProperty=fullName>，和<xref:System.Xml.Linq.XDocument.Load%2A?displayProperty=fullName>方法引发，请参阅<xref:System.Xml.XmlReader>文档。</xref:System.Xml.XmlReader> </xref:System.Xml.Linq.XDocument.Load%2A?displayProperty=fullName> </xref:System.Xml.Linq.XElement.Load%2A?displayProperty=fullName> </xref:System.Xml.Linq.XDocument.Parse%2A?displayProperty=fullName> </xref:System.Xml.Linq.XElement.Parse%2A?displayProperty=fullName>  
  
## <a name="see-also"></a>另请参阅  
 [分析 XML (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/parsing-xml.md)
