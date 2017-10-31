---
title: "检索段落及其样式 (Visual Basic 中) |Microsoft 文档"
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
ms.assetid: d9ed2238-d38e-4ad4-b88b-db7859df9bde
caps.latest.revision: 3
author: dotnet-bot
ms.author: dotnetcontent
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: bb6d68296a720a796a319502c4cb2f0319727459
ms.lasthandoff: 03/13/2017


---
# <a name="retrieving-the-paragraphs-and-their-styles-visual-basic"></a>检索段落及其样式 (Visual Basic)
在本示例中，我们编写一个从 WordprocessingML 文档检索段落节点的查询。 它还标识每个段落的样式。  
  
 此查询基于在上一示例中，查询[查找默认段落样式 (Visual Basic 中)](../../../../visual-basic/programming-guide/concepts/linq/finding-the-default-paragraph-style.md)，即从样式列表检索默认样式。 这些信息是必需的，以便查询能标识未显式设置样式的段落样式。 段落样式通过 `w:pPr` 元素来设置；如果段落未包含此元素，则它会使用默认样式的格式。  
  
 本主题解释某些查询的意义，然后作为一个完整工作示例的一部分来显示查询。  
  
## <a name="example"></a>示例  
 检索文档中所有段落及其样式的查询的源如下所示：  
  
```vb  
xDoc.Root.<w:body>...<w:p>  
```  
  
 此表达式是类似于在上一示例中，查询的源[查找默认段落样式 (Visual Basic 中)](../../../../visual-basic/programming-guide/concepts/linq/finding-the-default-paragraph-style.md)。 主要区别是它使用<xref:System.Xml.Linq.XContainer.Descendants%2A>轴而不是<xref:System.Xml.Linq.XContainer.Elements%2A>轴。</xref:System.Xml.Linq.XContainer.Elements%2A> </xref:System.Xml.Linq.XContainer.Descendants%2A> 该查询使用<xref:System.Xml.Linq.XContainer.Descendants%2A>轴因为文档中包含节中，段落将不是正文元素的直接子级; 而是，段落将两个级别之下的层次结构中。</xref:System.Xml.Linq.XContainer.Descendants%2A> 通过使用<xref:System.Xml.Linq.XContainer.Descendants%2A>轴，该代码仍有效的文档是否使用节。</xref:System.Xml.Linq.XContainer.Descendants%2A>  
  
## <a name="example"></a>示例  
 该查询使用 `Let` 子句来确定包含样式节点的元素。 如果没有任何元素，则将 `styleNode` 设置为 `Nothing`：  
  
```vb  
Let styleNode As XElement = para.<w:pPr>.<w:pStyle>.FirstOrDefault()  
```  
  
 `Let`子句首先使用<xref:System.Xml.Linq.XContainer.Elements%2A>轴，查找名为的所有元素`pPr`，然后使用<xref:System.Xml.Linq.Extensions.Elements%2A>扩展方法，都查找名为的所有子元素`pStyle`，最后使用<xref:System.Linq.Enumerable.FirstOrDefault%2A>标准查询运算符将集合转换为单一实例。</xref:System.Linq.Enumerable.FirstOrDefault%2A> </xref:System.Xml.Linq.Extensions.Elements%2A> </xref:System.Xml.Linq.XContainer.Elements%2A> 如果集合为空，则将 `styleNode` 设置为 `Nothing`。 这是一个用于查找 `pStyle` 子代节点的有用方法。 请注意，如果 `pPr` 子节点不存在，代码不会通过引发异常而运行失败；相反，它会将 `styleNode` 设置为 `Nothing`，这是此 `Let` 子句的期望行为。  
  
 该查询投影一个具有两个成员 `StyleName` 和 `ParagraphNode` 的匿名类型的集合。  
  
## <a name="example"></a>示例  
 本示例处理一个 WordprocessingML 文档，它从 WordprocessingML 文档中检索段落节点。 它还标识每个段落的样式。 本示例以本教程中前面的一些示例为基础构建。 下面代码中的注释标识出了这个新查询。  
  
 您可以找到用于创建在本示例的源文档的说明[创建源 Office Open XML 文档 (Visual Basic 中)](../../../../visual-basic/programming-guide/concepts/linq/creating-the-source-office-open-xml-document.md)。  
  
 本示例使用 WindowsBase 程序集中的类。 它使用中的类型<xref:System.IO.Packaging?displayProperty=fullName>命名空间。</xref:System.IO.Packaging?displayProperty=fullName>  
  
```vb  
Imports <xmlns:w="http://schemas.openxmlformats.org/wordprocessingml/2006/main">  
  
Module Module1  
    Private Function GetStyleOfParagraph(ByVal styleNode As XElement, ByVal defaultStyle As String) As String  
        If (styleNode Is Nothing) Then  
            Return defaultStyle  
        Else  
            Return styleNode.@w:val  
        End If  
    End Function  
  
    Sub Main()  
        Dim fileName = "SampleDoc.docx"  
  
        Dim documentRelationshipType = "http://schemas.openxmlformats.org/officeDocument/2006/relationships/officeDocument"  
        Dim stylesRelationshipType = "http://schemas.openxmlformats.org/officeDocument/2006/relationships/styles"  
        Dim wordmlNamespace = "http://schemas.openxmlformats.org/wordprocessingml/2006/main"  
  
        Dim xDoc As XDocument = Nothing  
        Dim styleDoc As XDocument = Nothing  
        Using wdPackage As Package = Package.Open(fileName, FileMode.Open, FileAccess.Read)  
            Dim docPackageRelationship As PackageRelationship = wdPackage.GetRelationshipsByType(documentRelationshipType).FirstOrDefault()  
            If (docPackageRelationship IsNot Nothing) Then  
                Dim documentUri As Uri = PackUriHelper.ResolvePartUri(New Uri("/", UriKind.Relative), docPackageRelationship.TargetUri)  
                Dim documentPart As PackagePart = wdPackage.GetPart(documentUri)  
  
                '  Load the document XML in the part into an XDocument instance.  
                xDoc = XDocument.Load(XmlReader.Create(documentPart.GetStream()))  
  
                '  Find the styles part. There will only be one.  
                Dim styleRelation As PackageRelationship = documentPart.GetRelationshipsByType(stylesRelationshipType).FirstOrDefault()  
                If (styleRelation IsNot Nothing) Then  
                    Dim styleUri As Uri = PackUriHelper.ResolvePartUri(documentUri, styleRelation.TargetUri)  
                    Dim stylePart As PackagePart = wdPackage.GetPart(styleUri)  
  
                    '  Load the style XML in the part into an XDocument instance.  
                    styleDoc = XDocument.Load(XmlReader.Create(stylePart.GetStream()))  
                End If  
            End If  
        End Using  
  
        Dim defaultStyle As String = _  
            ( _  
                From style In styleDoc.Root.<w:style> _  
                Where style.@w:type = "paragraph" And _  
                      style.@w:default = "1" _  
                Select style _  
            ).First().@w:styleId  
  
        ' Following is the new query that finds all paragraphs in the  
        ' document and their styles.  
        Dim paragraphs = _  
            From para In xDoc.Root.<w:body>...<w:p> _  
        Let styleNode As XElement = para.<w:pPr>.<w:pStyle>.FirstOrDefault() _  
        Select New With { _  
            .ParagraphNode = para, _  
            .StyleName = GetStyleOfParagraph(styleNode, defaultStyle) _  
        }  
  
        For Each p In paragraphs  
            Console.WriteLine("StyleName:{0}", p.StyleName)  
        Next  
  
    End Sub  
End Module  
```  
  
 该示例产生下面的输出应用于文档中所述[创建源 Office Open XML 文档 (Visual Basic 中)](../../../../visual-basic/programming-guide/concepts/linq/creating-the-source-office-open-xml-document.md)。  
  
```  
StyleName:Heading1  
StyleName:Normal  
StyleName:Normal  
StyleName:Normal  
StyleName:Code  
StyleName:Code  
StyleName:Code  
StyleName:Code  
StyleName:Code  
StyleName:Code  
StyleName:Code  
StyleName:Normal  
StyleName:Normal  
StyleName:Normal  
StyleName:Code  
```  
  
## <a name="next-steps"></a>后续步骤  
 在下一个主题中，[检索段落 (Visual Basic 中) 的文本](../../../../visual-basic/programming-guide/concepts/linq/retrieving-the-text-of-the-paragraphs.md)，您将创建一个查询来检索段落的文本。  
  
## <a name="see-also"></a>另请参阅  
 [教程︰ 操作 WordprocessingML 文档 (Visual Basic 中) 中的内容](../../../../visual-basic/programming-guide/concepts/linq/tutorial-manipulating-content-in-a-wordprocessingml-document.md)
