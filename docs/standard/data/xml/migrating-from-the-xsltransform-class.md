---
title: "从 XslTransform 类迁移 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-standard"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
ms.assetid: 9404d758-679f-4ffb-995d-3d07d817659e
caps.latest.revision: 3
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 3
---
# 从 XslTransform 类迁移
在 [!INCLUDE[vsprvslong](../../../../includes/vsprvslong-md.md)] 版本中重新设计了 XSLT 体系结构。  <xref:System.Xml.Xsl.XslTransform> 类已被 <xref:System.Xml.Xsl.XslCompiledTransform> 类所取代。  
  
 以下各节说明 <xref:System.Xml.Xsl.XslCompiledTransform> 和 <xref:System.Xml.Xsl.XslTransform> 类之间的一些主要区别。  
  
## 性能  
 <xref:System.Xml.Xsl.XslCompiledTransform> 类在性能方面进行了许多改进。  新的 XSLT 处理器将 XSLT 样式表编译为公共中间格式，与公共语言运行库 \(CLR\) 对其他编程语言的操作类似。  样式表编译后，可以缓存并重复使用。  
  
 <xref:System.Xml.Xsl.XslCompiledTransform> 类还进行了其他优化，使其比 <xref:System.Xml.Xsl.XslTransform> 类快得多。  
  
> [!NOTE]
>  尽管 <xref:System.Xml.Xsl.XslCompiledTransform> 类的总体性能优于 <xref:System.Xml.Xsl.XslTransform> 类，但在首次对转换调用时，<xref:System.Xml.Xsl.XslCompiledTransform> 类的 <xref:System.Xml.Xsl.XslCompiledTransform.Load%2A> 方法可能比 <xref:System.Xml.Xsl.XslTransform> 类的 <xref:System.Xml.Xsl.XslTransform.Load%2A> 方法慢。  这是因为必须先编译 XSLT 文件，才能加载该文件。  有关更多信息，请参见以下博客帖子：[XslCompiledTransform 比 XslTransform 慢？](http://go.microsoft.com/fwlink/?LinkId=130590)（可能为英文网页）  
  
## 安全性  
 默认情况下，<xref:System.Xml.Xsl.XslCompiledTransform> 类禁用对 XSLT `document()` 函数和嵌入式脚本的支持。  通过创建启用这些功能的 <xref:System.Xml.Xsl.XsltSettings> 对象并将其传递给 <xref:System.Xml.Xsl.XslCompiledTransform.Load%2A> 方法，可以启用这些功能。  下面的示例演示如何启用脚本并执行 XSLT 转换。  
  
 [!code-csharp[XML_Migration#16](../../../../samples/snippets/csharp/VS_Snippets_Data/XML_Migration/CS/migration.cs#16)]
 [!code-vb[XML_Migration#16](../../../../samples/snippets/visualbasic/VS_Snippets_Data/XML_Migration/VB/migration.vb#16)]  
  
 有关详细信息，请参阅[XSLT 安全注意事项](../../../../docs/standard/data/xml/xslt-security-considerations.md)。  
  
## 新功能  
  
### 临时文件  
 在 XSLT 处理过程中有时会生成临时文件。  如果样式表包含脚本块或是在将调试设置设为 true 时进行编译的，则可能会在 %TEMP% 文件夹中创建临时文件。  可能会存在由于计时问题而不删除某些临时文件的情况。  例如，如果文件正在由当前的 AppDomain 或调试器使用，则 <xref:System.CodeDom.Compiler.TempFileCollection> 对象的终结器将无法移除这些文件。  
  
 <xref:System.Xml.Xsl.XslCompiledTransform.TemporaryFiles%2A> 属性可用于进行附加清理，以确保从客户端中移除所有临时文件。  
  
### 对 xsl:output 元素和 XmlWriter 的支持  
 在将转换输出发送到 <xref:System.Xml.XmlWriter> 对象时，<xref:System.Xml.Xsl.XslTransform> 类忽略 `xsl:output` 设置。  <xref:System.Xml.Xsl.XslCompiledTransform> 类具有一个 <xref:System.Xml.Xsl.XslCompiledTransform.OutputSettings%2A> 属性，它可返回一个 <xref:System.Xml.XmlWriterSettings> 对象，该对象包含从样式表的 `xsl:output` 元素派生的输出信息。  <xref:System.Xml.XmlWriterSettings> 对象用于创建具有正确设置的 <xref:System.Xml.XmlWriter> 对象，可将该对象传递给 <xref:System.Xml.Xsl.XslCompiledTransform.Transform%2A> 方法。  下面的 C\# 代码阐释这一行为：  
  
```  
// Create the XslTransform object and load the style sheet.  
XslCompiledTransform xslt = new XslCompiledTransform();  
xslt.Load(stylesheet);  
  
// Load the file to transform.  
XPathDocument doc = new XPathDocument(filename);  
  
// Create the writer.  
XmlWriter writer = XmlWriter.Create(Console.Out, xslt.OutputSettings);  
  
// Transform the file and send the output to the console.  
xslt.Transform(doc, writer);  
writer.Close();  
```  
  
### 调试选项  
 <xref:System.Xml.Xsl.XslCompiledTransform> 类可以生成调试信息，使您可以使用 Microsoft [!INCLUDE[vsprvs](../../../../includes/vsprvs-md.md)] 调试器调试样式表。  有关更多信息，请参见<xref:System.Xml.Xsl.XslCompiledTransform.%23ctor%28System.Boolean%29>。  
  
## 行为差异  
  
### 转换为 XmlReader  
 <xref:System.Xml.Xsl.XslTransform> 类具有多个作为 <xref:System.Xml.XmlReader> 对象返回转换结果的 Transform 重载。  这些重载可用于将转换结果加载到内存表示形式（如 <xref:System.Xml.XmlDocument> 或 <xref:System.Xml.XPath.XPathDocument>），而不会增加对生成的 XML 树进行序列化和反序列化所造成的开销。  下面的 C\# 代码演示如何将转换结果加载到 <xref:System.Xml.XmlDocument> 对象。  
  
```  
// Load the style sheet  
XslTransform xslt = new XslTransform();  
xslt.Load("MyStylesheet.xsl");  
  
// Transform input document to XmlDocument for additional processing  
XmlDocument doc = new XmlDocument();  
doc.Load(xslt.Transform(input, (XsltArgumentList)null));  
```  
  
 <xref:System.Xml.Xsl.XslCompiledTransform> 类不支持转换为 <xref:System.Xml.XmlReader> 对象。  不过，通过使用 <xref:System.Xml.XPath.XPathNavigator.CreateNavigator%2A> 方法直接从 <xref:System.Xml.XmlWriter> 中加载生成的 XML 树，您可以执行类似操作。  下面的 C\# 代码演示如何使用 <xref:System.Xml.Xsl.XslCompiledTransform> 完成相同的任务。  
  
```  
// Transform input document to XmlDocument for additional processing  
XmlDocument doc = new XmlDocument();  
using (XmlWriter writer = doc.CreateNavigator().AppendChild()) {  
    xslt.Transform(input, (XsltArgumentList)null, writer);  
}  
```  
  
### 任意行为  
 W3C XSL 转换 \(XSLT\) 1.0 版建议中涉及到实现提供者可以在哪些方面确定如何处理某种情况。  这些方面被认为是任意行为。  在有些方面，<xref:System.Xml.Xsl.XslCompiledTransform> 行为不同于 <xref:System.Xml.Xsl.XslTransform> 类。  有关详细信息，请参阅[可恢复的 XSLT 错误](../../../../docs/standard/data/xml/recoverable-xslt-errors.md)。  
  
### 扩展对象和脚本函数  
 <xref:System.Xml.Xsl.XslCompiledTransform> 介绍对使用脚本函数的两个新限制：  
  
-   从 XPath 表达式中只能调用公共方法。  
  
-   重载之间可以基于参数数量进行区分。  如果多个重载具有相同数量的参数，则将引发异常。  
  
 在 <xref:System.Xml.Xsl.XslCompiledTransform> 中，脚本函数的绑定（方法名称查找）发生在编译时，当使用 <xref:System.Xml.Xsl.XslCompiledTransform> 加载由 XslTranform 使用的样式表时，这些样式表可能会引发异常。  
  
 <xref:System.Xml.Xsl.XslCompiledTransform> 支持在 `msxsl:script` 元素中具有 `msxsl:using` 和 `msxsl:assembly` 子元素。  `msxsl:using` 和 `msxsl:assembly` 元素用于声明其他命名空间和程序集，以便在脚本块中使用。  有关更多信息，请参见[使用 msxsl:script 的脚本块](../../../../docs/standard/data/xml/script-blocks-using-msxsl-script.md)。  
  
 <xref:System.Xml.Xsl.XslCompiledTransform> 禁止扩展对象具有相同数量的参数的多个重载。  
  
### MSXML 函数  
 已向 <xref:System.Xml.Xsl.XslCompiledTransform> 类添加对其他 MSXML 函数的支持。  下面的列表说明新增或改进功能：  
  
-   msxsl:node\-set：<xref:System.Xml.Xsl.XslTransform> 要求 [node\-set 函数](http://msdn.microsoft.com/zh-cn/87b6b3f4-16f4-4fa3-8103-d62a679ac2a7) 函数的参数是结果树片段。  <xref:System.Xml.Xsl.XslCompiledTransform> 类没有此要求。  
  
-   msxsl:version：<xref:System.Xml.Xsl.XslCompiledTransform> 中支持此函数。  
  
-   XPath 扩展函数：现在支持 [ms:string\-compare 函数](http://msdn.microsoft.com/zh-cn/20616b82-9e27-444c-b714-4f1e09b73aee)、[ms:utc 函数](http://msdn.microsoft.com/zh-cn/ef26fc88-84c6-4fb9-9c3b-f2f5264b864f)、[ms:namespace\-uri 函数](http://msdn.microsoft.com/zh-cn/91f9cabf-ab93-4dbe-9c12-e6a75214f4c7)、[ms:local\-name 函数](http://msdn.microsoft.com/zh-cn/10ed60a1-17a9-4d74-8b98-7940ac97c0b5)、[ms:number 函数](http://msdn.microsoft.com/zh-cn/b94fc08e-1f31-4f48-b1a8-6d78c1b5d954)、[ms:format\-date 函数](http://msdn.microsoft.com/zh-cn/51f35609-89a9-4098-a166-88bf01300bf5) 和 [ms:format\-time 函数](http://msdn.microsoft.com/zh-cn/e5c2df2d-e8fb-4a8f-bfc0-db84ea12a5d5) 函数。  
  
-   与架构相关的 XPath 扩展函数：这些函数不受 <xref:System.Xml.Xsl.XslCompiledTransform> 本机支持。  但是，它们可以作为扩展函数实现。  
  
## 请参阅  
 [XSLT 转换](../../../../docs/standard/data/xml/xslt-transformations.md)   
 [使用 XslCompiledTransform 类](../../../../docs/standard/data/xml/using-the-xslcompiledtransform-class.md)