---
title: "如何︰ 将 XML 转换通过使用 LINQ (Visual Basic 中) |Microsoft 文档"
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
helpviewer_keywords:
- XML [Visual Basic], transforming
- LINQ to XML [Visual Basic], transforming XML
ms.assetid: 815687f4-0bc2-4c0b-adc6-d78744aa356f
caps.latest.revision: 14
author: dotnet-bot
ms.author: dotnetcontent
translation.priority.ht:
- cs-cz
- de-de
- es-es
- fr-fr
- it-it
- ja-jp
- ko-kr
- pl-pl
- pt-br
- ru-ru
- tr-tr
- zh-cn
- zh-tw
ms.translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 9f97466727064ea275c051b5916b0fb297e9e23a
ms.contentlocale: zh-cn
ms.lasthandoff: 03/13/2017

---
# <a name="how-to-transform-xml-by-using-linq-visual-basic"></a>如何：使用 LINQ 转换 XML (Visual Basic)
[XML 文本](../../../../visual-basic/language-reference/xml-literals/index.md)方便地从一个源读取的 XML 并将其转换为新的 XML 格式。 您可以利用 LINQ 查询以检索要转换的内容或将现有的文档中的内容更改为新的 XML 格式。  
  
 本主题中的示例转换为 HTML，以在浏览器中查看 XML 源文档中的内容。  
  
[!INCLUDE[note_settings_general](~/includes/note-settings-general-md.md)]  
  
### <a name="to-transform-an-xml-document"></a>若要转换的 XML 文档  
  
1.  在 Visual Studio 中，创建新的 Visual Basic 项目中**控制台应用程序**项目模板。  
  
2.  双击要修改的 Visual Basic 代码的项目中创建的 Module1.vb 文件。 添加以下代码到`Sub Main`的`Module1`模块。 此代码将创建源 XML 文档作为<xref:System.Xml.Linq.XDocument>对象。</xref:System.Xml.Linq.XDocument>  
  
    ```vb  
    Dim catalog =   
      <?xml version="1.0"?>  
        <Catalog>  
          <Book id="bk101">  
            <Author>Garghentini, Davide</Author>  
            <Title>XML Developer's Guide</Title>  
            <Price>44.95</Price>  
            <Description>  
              An in-depth look at creating applications  
              with <technology>XML</technology>. For   
              <audience>beginners</audience> or   
              <audience>advanced</audience> developers.  
            </Description>  
          </Book>  
          <Book id="bk331">  
            <Author>Spencer, Phil</Author>  
            <Title>Developing Applications with Visual Basic .NET</Title>  
            <Price>45.95</Price>  
            <Description>  
              Get the expert insights, practical code samples,   
              and best practices you need   
              to advance your expertise with <technology>Visual   
              Basic .NET</technology>.   
              Learn how to create faster, more reliable applications  
              based on professional,   
              pragmatic guidance by today's top <audience>developers</audience>.  
            </Description>  
          </Book>  
        </Catalog>  
    ```  
  
     [如何︰ 从文件、 字符串或流加载 XML](../../../../visual-basic/programming-guide/language-features/xml/how-to-load-xml-from-a-file-string-or-stream.md)。  
  
3.  若要创建的源 XML 文档的代码，后面添加以下代码来检索所有\<簿&1;> 对象元素并将它们转换为 HTML 文档。 列表\<簿&1;> 使用返回的集合的 LINQ 查询来创建元素<xref:System.Xml.Linq.XElement>对象，其中包含转换后的 HTML。</xref:System.Xml.Linq.XElement> 可以使用嵌入式的表达式可以从新的 XML 格式中的源文档将的值。  
  
     生成的 HTML 文档使用写入到文件<xref:System.Xml.Linq.XElement.Save%2A>方法。</xref:System.Xml.Linq.XElement.Save%2A>  
  
    ```vb  
    Dim htmlOutput =   
      <html>  
        <body>  
          <%= From book In catalog.<Catalog>.<Book>   
              Select <div>  
                       <h1><%= book.<Title>.Value %></h1>  
                       <h3><%= "By " & book.<Author>.Value %></h3>  
                        <h3><%= "Price = " & book.<Price>.Value %></h3>  
                        <h2>Description</h2>  
                        <%= TransformDescription(book.<Description>(0)) %>  
                        <hr/>  
                      </div> %>  
        </body>  
      </html>  
  
    htmlOutput.Save("BookDescription.html")  
    ```  
  
4.  之后`Sub Main`的`Module1`，添加一个新方法 (`Sub`) 来转换\<说明&1;> 节点插入指定的 HTML 格式。 此方法称为由上一步中的代码，用于保留的格式\<说明&1;> 元素。  
  
     此方法将替换的子元素\<说明&1;> 与 HTML 元素。 `ReplaceWith`方法用来保留子元素的位置。 转换后的内容的\<说明&1;> 元素包含在一个 HTML 段落 (\<p&1;>) 元素。 <xref:System.Xml.Linq.XContainer.Nodes%2A>属性用于检索的转换的内容\<说明&1;> 元素。</xref:System.Xml.Linq.XContainer.Nodes%2A> 这可确保将在转换后的内容中包含的子元素。  
  
     添加下面的代码之后`Sub Main`的`Module1`。  
  
    ```vb  
    Public Function TransformDescription(ByVal desc As XElement) As XElement  
  
      ' Replace <technology> elements with <b>.  
      Dim content = (From element In desc...<technology>).ToList()  
  
      If content.Count > 0 Then  
        For i = 0 To content.Count - 1  
          content(i).ReplaceWith(<b><%= content(i).Value %></b>)  
        Next  
      End If  
  
      ' Replace <audience> elements with <i>.  
      content = (From element In desc...<audience>).ToList()  
  
      If content.Count > 0 Then  
        For i = 0 To content.Count - 1  
          content(i).ReplaceWith(<i><%= content(i).Value %></i>)  
        Next  
      End If  
  
      ' Return the updated contents of the <Description> element.  
      Return <p><%= desc.Nodes %></p>  
    End Function  
    ```  
  
5.  保存更改。  
  
6.  按 F5 以运行此代码。 产生的保存的文档将如下所示︰  
  
    ```  
    <?xml version="1.0"?>  
    <html>  
      <body>  
        <div>  
          <h1>XML Developer's Guide</h1>  
          <h3>By Garghentini, Davide</h3>  
          <h3>Price = 44.95</h3>  
          <h2>Description</h2>  
          <p>  
            An in-depth look at creating applications  
            with <b>XML</b>. For   
            <i>beginners</i> or   
            <i>advanced</i> developers.  
          </p>  
          <hr />  
        </div>  
        <div>  
          <h1>Developing Applications with Visual Basic .NET</h1>  
          <h3>By Spencer, Phil</h3>  
          <h3>Price = 45.95</h3>  
          <h2>Description</h2>  
          <p>  
            Get the expert insights, practical code   
            samples, and best practices you need   
            to advance your expertise with <b>Visual   
            Basic .NET</b>. Learn how to create faster,  
            more reliable applications based on  
            professional, pragmatic guidance by today's   
            top <i>developers</i>.  
          </p>  
          <hr />  
        </div>  
      </body>  
    </html>  
    ```  
  
## <a name="see-also"></a>另请参阅  
 [XML 文本](../../../../visual-basic/language-reference/xml-literals/index.md)   
 [在 Visual Basic 中操作 XML](../../../../visual-basic/programming-guide/language-features/xml/manipulating-xml.md)   
 [XML](../../../../visual-basic/programming-guide/language-features/xml/index.md)   
 [如何︰ 从文件、 字符串或流加载 XML](../../../../visual-basic/programming-guide/language-features/xml/how-to-load-xml-from-a-file-string-or-stream.md)   
 [LINQ](../../../../visual-basic/programming-guide/language-features/linq/index.md)   
 [在 Visual Basic 中的 LINQ 简介](../../../../visual-basic/programming-guide/language-features/linq/introduction-to-linq.md)

