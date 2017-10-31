---
title: "在 Visual Basic 中的 XML IntelliSense |Microsoft 文档"
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
- Visual Basic code, XML
- XML IntelliSense [Visual Basic]
- XML [Visual Basic], IntelliSense
- IntelliSense [Visual Basic], XML
ms.assetid: 59506ce9-d64e-417e-90fc-e9fe19f0a8fa
caps.latest.revision: 27
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
ms.openlocfilehash: 8c43db3d2010e4fa92eebeec8a973c50052b1340
ms.contentlocale: zh-cn
ms.lasthandoff: 03/13/2017

---
# <a name="xml-intellisense-in-visual-basic"></a>Visual Basic 中的 XML IntelliSense
Visual Basic 代码编辑器包括提供 XML 架构中定义的元素的单词自动完成的 XML IntelliSense 功能。 如果您在项目中包含的 XML 架构定义 (XSD) 文件，并使用导入架构的目标命名空间`Imports`语句中，代码编辑器中将包括的 XSD 架构中的元素，在 IntelliSense 列表中的有效成员变量<xref:System.Xml.Linq.XElement>和<xref:System.Xml.Linq.XDocument>对象。</xref:System.Xml.Linq.XDocument> </xref:System.Xml.Linq.XElement> 下图显示了 IntelliSense 成员列表的<xref:System.Xml.Linq.XElement>对象。</xref:System.Xml.Linq.XElement>  
  
 ![在 Visual Basic 中的 XML IntelliSense](../../../../visual-basic/programming-guide/language-features/xml/media/xml_intellisense.png "XML_Intellisense")  
XML IntelliSense  
  
## <a name="enabling-xml-intellisense-in-visual-basic"></a>在 Visual Basic 中启用 XML IntelliSense  
 若要启用 XML IntelliSense 在 Visual Basic 中，必须在 Visual Basic 项目中包括 XSD 架构文件。 您还必须导入的 XSD 架构的目标命名空间到代码文件使用`Imports`语句。 或者，您可以通过将添加的目标命名空间到项目级别命名空间列表**引用**Visual Basic 项目设计器的页面。 有关示例，请参阅[如何︰ 在 Visual Basic 中启用 XML IntelliSense](../../../../visual-basic/programming-guide/language-features/xml/how-to-enable-xml-intellisense.md)。 有关详细信息，请参阅[Imports 语句 (XML Namespace)](../../../../visual-basic/language-reference/statements/imports-statement-xml-namespace.md)和[，项目设计器 (Visual Basic 中) 引用页](https://docs.microsoft.com/visualstudio/ide/reference/references-page-project-designer-visual-basic)。  
  
 请注意，默认您无法看到在 Visual Basic 项目的 XSD 架构文件。 您可能需要单击**显示所有文件**按钮以选择要包括在项目中的 XSD 文件。  
  
### <a name="generating-a-schema-file-schema-inference"></a>生成架构文件 （架构推断）  
 可以通过使用 Visual Studio XML 工具推断 XSD 架构来创建针对现有的 XML 文件的 XSD 架构。  
  
-   从 SP1 开始，您可以使用 XML 到架构向导创建的 XML 架构集，则会推断从一个或多个 XML 文档并将其包含您的项目。 可以使用文本文件、 XML 从 HTTP Internet 地址或键入或粘贴到 XML 到架构向导的 XML 形式的 XML 文档的任意组合。 若要访问 XML 到架构向导，请单击**添加新项**上**项目**菜单上，并添加**XML 到架构**模板**数据**或**常用项**模板组。 包括了要推断从 XML 架构集的所有 XML 文档源之后，单击**确定**创建推断出的架构集。 有关详细信息，请参阅[XML 到架构向导](../../../../visual-basic/programming-guide/language-features/xml/xml-to-schema-wizard.md)。  
  
-   Visual Studio XML 编辑器还可用于推断 XSD 架构将设置从 XML 文件。 要创建 XML 架构使用 XML 编辑器设置，请在 Visual Studio XML 设计器中打开 XML 文件，然后单击**Create Schema**上**XML**菜单。 在创建 XSD 架构集后，可以将所创建的架构集保存到一个或多个 XSD 文件并将它们包括在你的项目。 有关详细信息，请参阅[如何︰ 在 Visual Basic 中启用 XML IntelliSense](../../../../visual-basic/programming-guide/language-features/xml/how-to-enable-xml-intellisense.md)。  
  
 请注意，可能从多个用于具有相同的架构的 XML 文档推断不同的 XSD 架构集。 这可发生在一个 XML 文件中而不是在另一台，找到特定的元素和属性时也顺序不同，例如包含元素。 使用 XSD 架构推断时，应检查推断的 XSD 架构集的完整性和精确性。  
  
## <a name="member-list"></a>成员列表  
 键入句点 （.） 来分隔的一个实例后<xref:System.Xml.Linq.XElement>或<xref:System.Xml.Linq.XDocument>对象 (或实例`IEnumerable(Of XElement)`或`IEnumerable(Of XDocument)`)，Visual Basic IntelliSense 将显示可能的对象成员的列表。</xref:System.Xml.Linq.XDocument> </xref:System.Xml.Linq.XElement> 初始列表中包括三个选项，表示 XML 轴属性，如下面的列表中所述。  
  
|选项|说明|  
|---|---|  
|**\< >**|选择此选项以显示可能的子列表元素。 有关详细信息，请参阅[XML 元素文本](../../../../visual-basic/language-reference/xml-literals/xml-element-literal.md)和<xref:System.Xml.Linq.XContainer.Elements%2A>方法。</xref:System.Xml.Linq.XContainer.Elements%2A>|  
|**@**|选择此选项以显示可能的属性的列表。 有关详细信息，请参阅[XML 轴属性](../../../../visual-basic/language-reference/xml-axis/xml-axis-properties.md)。此选项才可用仅适用于对象类型<xref:System.Xml.Linq.XElement>。</xref:System.Xml.Linq.XElement>|  
|**…\< >**|选择此选项以显示可能的子代元素的列表。 有关详细信息，请参阅[如何︰ 访问 XML 后代元素](../../../../visual-basic/programming-guide/language-features/xml/how-to-access-xml-descendant-elements.md)和<xref:System.Xml.Linq.XContainer.Elements%2A>方法。</xref:System.Xml.Linq.XContainer.Elements%2A>|  
  
 选择或开始键入任何从列表中的 XML 选项。 成员列表中将显示从 XML 架构中特定于所选的选项的潜在成员。 如果您有 XML 命名空间导入与特定的 XML 命名空间前缀相关联，在成员列表中包含的潜在的 XML 命名空间前缀列表。  
  
 例如，考虑下面的 XSD 架构。  
  
```xml  
<?xml version="1.0" encoding="utf-8"?>  
<xs:schema attributeFormDefault="unqualified"   
           elementFormDefault="qualified"   
           targetNamespace="http://SamplePurchaseOrder"   
           xmlns:xs="http://www.w3.org/2001/XMLSchema">  
  <xs:element name="PurchaseOrders">  
    <xs:complexType>  
      <xs:sequence>  
        <xs:element name="PurchaseOrder">  
          <xs:complexType>  
            <xs:sequence>  
              <xs:element name="Address" />  
              <xs:element name="Items" />  
              <xs:element name="Comment" />  
            </xs:sequence>  
            <xs:attribute name="PurchaseOrderNumber" type="xs:unsignedShort" use="required" />  
            <xs:attribute name="OrderDate" type="xs:string" use="required" />  
          </xs:complexType>  
        </xs:element>  
      </xs:sequence>  
    </xs:complexType>  
  </xs:element>  
</xs:schema>  
```  
  
 有效的 XSD 架构的 XML 将如下所示。  
  
```xml  
<?xml version="1.0"?>  
<PurchaseOrders xmlns="http://SamplePurchaseOrder">  
  <PurchaseOrder PurchaseOrderNumber="12345" OrderDate="2000-1-1">  
    <Address />  
    <Items />  
    <Comment />  
  </PurchaseOrder>  
</PurchaseOrders>  
```  
  
 如果您在项目中包括此 XSD 架构文件并将从 XSD 架构的目标命名空间导入您的代码文件或项目，Visual Basic IntelliSense 将显示架构中的成员，键入您的 Visual Basic 代码。 如果您键入以下 XSD 架构的目标命名空间将作为默认命名空间导入，IntelliSense 将显示可能的子元素的列表`PurchaseOrder`XML 元素。  
  
```  
Dim po = <PurchaseOrder />  
po.<  
```  
  
 列表由地址、 注释和项元素组成。  
  
### <a name="certainty-levels-for-intellisense-list-items"></a>智能感知列表项的确定性级别  
 确定要用于智能感知的 XSD 类型并不精确。 因此，XML IntelliSense 通常将显示可能成员的扩展的列表。 若要帮助您从 IntelliSense 成员列表中选择一项，项将显示相对值的指示的 XML IntelliSense 的特定成员具有的确定性级别。  
  
 有时 XML IntelliSense 可以识别的 XSD 架构中特定类型。 在这些情况下，它将具有高确定性级别中显示可能的子元素、 属性或该 XSD 类型的子代元素。 带有复选标记，这些项进行标识。  
  
 但是，有时 XML IntelliSense 不能用于标识特定类型的 XSD 架构中。 在这些情况下，它将与低确定性级别显示可能的子元素、 属性或项目的 XSD 架构中的子代元素的扩展的的列表。 使用问号来标识这些项。  
  
## <a name="see-also"></a>另请参阅  
 [如何︰ 启用在 Visual Basic 中的 XML IntelliSense](../../../../visual-basic/programming-guide/language-features/xml/how-to-enable-xml-intellisense.md)   
 [XML 到架构向导](../../../../visual-basic/programming-guide/language-features/xml/xml-to-schema-wizard.md)   
 [Imports 语句 (XML Namespace)](../../../../visual-basic/language-reference/statements/imports-statement-xml-namespace.md)   
 [XML 元素文本](../../../../visual-basic/language-reference/xml-literals/xml-element-literal.md)   
 [XML 特性轴属性](../../../../visual-basic/language-reference/xml-axis/xml-attribute-axis-property.md)   
 [XML 子代轴属性](../../../../visual-basic/language-reference/xml-axis/xml-descendant-axis-property.md)   
 [项目设计器 ->“引用”页 (Visual Basic)](https://docs.microsoft.com/visualstudio/ide/reference/references-page-project-designer-visual-basic)
