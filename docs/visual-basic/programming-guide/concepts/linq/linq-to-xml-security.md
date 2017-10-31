---
title: "LINQ to XML 安全性 (Visual Basic 中) |Microsoft 文档"
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
ms.assetid: d99b4af2-d447-4a3b-991b-6da0231a8637
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
ms.openlocfilehash: 559bf330640840a310ff947cac118953d1df1a13
ms.lasthandoff: 03/13/2017

---
# <a name="linq-to-xml-security-visual-basic"></a>LINQ to XML 安全性 (Visual Basic)
本主题说明与 LINQ to XML 相关的安全问题。 此外，它还提供减轻安全隐患的一些指导。  
  
## <a name="linq-to-xml-security-overview"></a>LINQ to XML 安全性概述  
 在旨在提高编程方便性和使服务器端应用程序具有严格安全要求两者之间，LINQ to XML 更倾向于前者。 多数 XML 方案均涉及处理受信任的 XML 文档，而不涉及处理上载到服务器的不受信任的 XML 文档。 LINQ to XML 针对这些方案进行了优化。  
  
 如果必须处理来自未知源的不受信任的数据时，Microsoft 建议使用的实例<xref:System.Xml.XmlReader>已配置为筛除已知 XML 拒绝服务 (DoS) 攻击的类。</xref:System.Xml.XmlReader>  
  
 如果已配置<xref:System.Xml.XmlReader>以缓解拒绝服务攻击的可能性，可以使用该读取器填充 LINQ to XML 树，同时仍想获得的程序员的工作效率增强功能的 LINQ to XML。</xref:System.Xml.XmlReader> 许多缓解技术均涉及创建配置为可缓解安全问题的读取器，然后通过配置的读取器实例化 XML 树。  
  
 由于文档不受大小、深度、元素名称大小等的限制，因此 XML 从本质上就容易受到拒绝服务攻击。 不管使用哪个组件处理 XML，都应该始终准备好在应用程序域使用过多资源的情况下回收应用程序域。  
  
## <a name="mitigation-of-xml-xsd-xpath-and-xslt-attacks"></a>缓解 XML、XSD、XPath 和 XSLT 攻击  
 LINQ to XML 是基于<xref:System.Xml.XmlReader>和<xref:System.Xml.XmlWriter>。</xref:System.Xml.XmlWriter> </xref:System.Xml.XmlReader> LINQ to XML 通过中的扩展方法支持 XSD 和 XPath<xref:System.Xml.Schema?displayProperty=fullName>和<xref:System.Xml.XPath?displayProperty=fullName>命名空间。</xref:System.Xml.XPath?displayProperty=fullName> </xref:System.Xml.Schema?displayProperty=fullName> 使用<xref:System.Xml.XmlReader>， <xref:System.Xml.XPath.XPathNavigator>，和<xref:System.Xml.XmlWriter>在结合 LINQ to XML 类时，您可以调用 XSLT 来转换 XML 树。</xref:System.Xml.XmlWriter> </xref:System.Xml.XPath.XPathNavigator> </xref:System.Xml.XmlReader>  
  
 如果您在较不安全的环境中操作，有许多与 XML 相关联的安全问题和中的类使用<xref:System.Xml?displayProperty=fullName>， <xref:System.Xml.Schema?displayProperty=fullName>， <xref:System.Xml.XPath?displayProperty=fullName>，和<xref:System.Xml.Xsl?displayProperty=fullName>。</xref:System.Xml.Xsl?displayProperty=fullName> </xref:System.Xml.XPath?displayProperty=fullName> </xref:System.Xml.Schema?displayProperty=fullName> </xref:System.Xml?displayProperty=fullName> 这些问题包括但不限于以下问题：  
  
-   XSD、XPath 和 XSLT 是基于字符串的语言，您可以使用此语言指定消耗很多时间和内存的操作。 从不受信任的源获取 XSD、XPath 或 XSLT 字符串的应用程序程序员应当负责验证这些字符串以确保其中不包含恶意内容，或监视这些字符串并尽量避免计算这些字符串时消耗过多的系统资源。  
  
-   XSD 架构（包括内联架构）从本质上就容易受到拒绝服务攻击，因此不应接受来自不受信任的源的架构。  
  
-   XSD 和 XSLT 可能包括对其他文件的引用，这种引用可能导致跨区和跨域攻击。  
  
-   DTD 中的外部实体可能会导致跨区和跨域攻击。  
  
-   DTD 容易受到拒绝服务攻击。  
  
-   异常深的 XML 文档可能引起拒绝服务问题；您可能需要限制 XML 文档的深度。  
  
-   不接受支持组件，如<xref:System.Xml.NameTable>， <xref:System.Xml.XmlNamespaceManager>，和<xref:System.Xml.XmlResolver>来自不受信任的程序集对象。</xref:System.Xml.XmlResolver> </xref:System.Xml.XmlNamespaceManager> </xref:System.Xml.NameTable>  
  
-   分块区读取数据以缓解大文档攻击。  
  
-   XSLT 样式表中的脚本块易于受到多种攻击。  
  
-   构造动态 XPath 表达式之前需仔细验证这些表达式。  
  
## <a name="linq-to-xml-security-issues"></a>LINQ to XML 安全问题  
 本主题中介绍的安全问题不区分顺序。 所有问题都很重要，都应得到相应解决。  
  
 成功的特权提升攻击可使恶意程序集能够更好地控制其环境。 成功的特权提升攻击可能导致数据泄露、拒绝服务等。  
  
 应用程序不应该向未经授权查看数据的用户泄露数据。  
  
 拒绝服务攻击会导致 XML 分析器或 LINQ to XML 消耗过多的内存或 CPU 时间。 拒绝服务攻击的严重性可视为比特权提升攻击或数据泄露攻击的严重性低。 但在服务器需要处理来自不受信任的源的 XML 文档的方案中，拒绝服务攻击很重要。  
  
### <a name="exceptions-and-error-messages-might-reveal-data"></a>异常和错误消息可能会泄露数据  
 错误说明中可能会显示数据，如正在转换的数据、文件名或实现详细信息。 不应向不受信任的调用方公开错误消息。 您应该捕捉所有错误并用自己的自定义错误消息报告错误。  
  
### <a name="do-not-call-codeaccesspermissionsassert-in-an-event-handler"></a>不要在事件处理程序中调用 CodeAccessPermissions.Assert  
 程序集可具有较低或较高的权限。 程序集的权限越高，其对计算机及其环境的控制程度也就越高。  
  
 如果具有较高权限的程序集中的代码调用<xref:System.Security.CodeAccessPermission.Assert%2A?displayProperty=fullName>中事件处理程序，然后将 XML 树传递给恶意程序集，具有受限制的权限，则恶意程序集可能会导致引发事件。</xref:System.Security.CodeAccessPermission.Assert%2A?displayProperty=fullName> 由于该事件运行具有较高权限的程序集中的代码，因此恶意程序集将使用提升的特权运行。  
  
 Microsoft 建议您永远不会调用<xref:System.Security.CodeAccessPermission.Assert%2A?displayProperty=fullName>事件处理程序中。</xref:System.Security.CodeAccessPermission.Assert%2A?displayProperty=fullName>  
  
### <a name="dtds-are-not-secure"></a>DTD 不安全  
 DTD 中的实体在本质上就不安全。 包含 DTD 的恶意 XML 文档可使分析器使用全部内存和 CPU 时间，从而导致拒绝服务攻击。 因此，在 LINQ to XML 中，默认情况下关闭 DTD 处理。 您不应接受来自不受信任源的 DTD。  
  
 接受来自不受信任源的 DTD 的一个示例是：允许 Web 用户上载引用 DTD 和 DTD 文件的 XML 文件的 Web 应用程序。 在验证该文件时，恶意 DTD 会在您的服务器上执行拒绝服务攻击。 接受来自不受信任源的 DTD 的另一个示例是：引用网络共享上也允许匿名 FTP 访问的 DTD。  
  
### <a name="avoid-excessive-buffer-allocation"></a>避免分配过多的缓冲区  
 应用程序开发人员应该知道，过大的数据源可能导致资源耗尽和拒绝服务攻击。  
  
 如果恶意用户提交或上载非常大的 XML 文档，则可能导致 LINQ to XML 使用过多的系统资源。 这可能构成拒绝服务攻击。 若要避免此情形，您可以设置<xref:System.Xml.XmlReaderSettings.MaxCharactersInDocument%2A?displayProperty=fullName>属性，并创建一个读取器，然后限制在可以加载的文档的大小。</xref:System.Xml.XmlReaderSettings.MaxCharactersInDocument%2A?displayProperty=fullName> 然后使用该读取器创建 XML 树。  
  
 例如，如果您知道预计最大的来自不受信任的源 XML 文档的大小将会不超过 50k 字节，设置<xref:System.Xml.XmlReaderSettings.MaxCharactersInDocument%2A?displayProperty=fullName>为 100000。</xref:System.Xml.XmlReaderSettings.MaxCharactersInDocument%2A?displayProperty=fullName> 这不会妨碍您处理 XML 文档，同时还可在要上载的文档会使用大量内存的情况下缓解拒绝服务威胁。  
  
### <a name="avoid-excess-entity-expansion"></a>避免过度扩展实体  
 使用 DTD 时的一种已知拒绝服务攻击是导致过度扩展实体的文档造成的。 若要避免此情形，您可以设置<xref:System.Xml.XmlReaderSettings.MaxCharactersFromEntities%2A?displayProperty=fullName>属性，并创建然后限制读取器中从扩展实体产生的字符数。</xref:System.Xml.XmlReaderSettings.MaxCharactersFromEntities%2A?displayProperty=fullName> 然后使用该读取器创建 XML 树。  
  
### <a name="limit-the-depth-of-the-xml-hierarchy"></a>限制 XML 层次结构的深度  
 在提交具有过深层次结构的文档时，会发生一种可能的拒绝服务攻击。 若要避免此情形，您可以将包装<xref:System.Xml.XmlReader>在您自己的可计算元素深度的类。</xref:System.Xml.XmlReader> 如果深度超过预设的合理等级，您可以终止处理恶意文档。  
  
### <a name="protect-against-untrusted-xmlreader-or-xmlwriter-implementations"></a>防止不受信任的 XmlReader 或 XmlWriter 实现  
 管理员应验证任何外部提供<xref:System.Xml.XmlReader>或<xref:System.Xml.XmlWriter>实现具有强名称且已在计算机配置中注册。</xref:System.Xml.XmlWriter> </xref:System.Xml.XmlReader> 这可防止加载伪装成读取器或编写器的恶意代码。  
  
### <a name="periodically-free-objects-that-reference-xname"></a>定期释放引用 XName 的对象  
 若要防止某些类型的攻击，应用程序程序员应当释放引用的所有对象<xref:System.Xml.Linq.XName>规律地定期应用程序域中的对象。</xref:System.Xml.Linq.XName>  
  
### <a name="protect-against-random-xml-names"></a>防止随机 XML 名称  
 不受信任源中获取数据的应用程序应考虑使用<xref:System.Xml.XmlReader>包装在自定义代码来检查是否可能会出现随机 XML 名称和命名空间。</xref:System.Xml.XmlReader> 如果检测到这样的随机 XML 名称和命名空间，则应用程序可以终止处理恶意文档。  
  
 您可能需要将任何给定命名空间中的名称数目（包括不在命名空间中的名称）限制为合理的极限。  
  
### <a name="annotations-are-accessible-by-software-components-that-share-a-linq-to-xml-tree"></a>通过共享 LINQ to XML 树的软件组件可以访问批注  
 LINQ to XML 可用于生成处理管道，其中的不同应用程序组件可分别加载、验证、查询、转换、更新和保存在组件之间作为 XML 树传递的 XML 数据。 这有助于优化性能，因为仅在管道末端消耗加载对象并将对象序列化为 XML 文本的系统资源。 但开发人员必须知道，由一个组件创建的所有批注和事件处理程序都可以由其他组件访问。 如果组件的信任级别不同，这可能会造成很多安全漏洞。 若要在低信任级别的组件之间生成安全管道，在将数据传递给不受信任的组件之前，您必须将 LINQ to XML 对象序列化为 XML 文本。  
  
 某些安全功能是由公共语言运行库 (CLR) 提供的。 例如，不包括私有类的组件无法访问由该类键控的批注。 但是，不能读取批注的组件却可以删除该批注。 这可能用作篡改攻击。  
  
## <a name="see-also"></a>另请参阅  
 [编程指南 (LINQ to XML) (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/programming-guide-linq-to-xml.md)
