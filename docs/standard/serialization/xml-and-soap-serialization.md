---
title: "XML 和 SOAP 序列化"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- SOAP, XML serialization
- XML serialization, SOAP
- serialization, SOAP
- serialization, about serialization
- XML serialization
- serialization
ms.assetid: 832ac524-21bc-419a-a27b-ca8bfc45840f
caps.latest.revision: 4
author: Erikre
ms.author: erikre
manager: erikre
ms.translationtype: HT
ms.sourcegitcommit: 717bcb6f9f72a728d77e2847096ea558a9c50902
ms.openlocfilehash: 412468a03c15cedaa77a5e10be41793565039c4d
ms.contentlocale: zh-cn
ms.lasthandoff: 08/21/2017

---
# <a name="xml-and-soap-serialization"></a>XML 和 SOAP 序列化
XML 序列化将对象的公共字段和属性或者方法的参数及返回值转换（序列化）为符合特定 XML 架构定义语言 (XSD) 文档的 XML 流。 XML 序列化会生成强类型类，同时将公共属性和字段转换为序列格式（在此情况下为 XML），以便存储或传输。  
  
 由于 XML 是开放式的标准，因此可以根据需要由任何应用程序处理 XML 流，而与平台无关。 例如，用 ASP.NET 创建的 XML Web services 使用 <xref:System.Xml.Serialization.XmlSerializer> 类来创建 XML 流，这些流在整个 Internet 中或在 Intranet 上的 XML Web services 应用程序之间传递数据。 相反，反序列化采用这样一个 XML 流并重新构造对象。  
  
 XML 序列化还可用于将对象序列化为符合 SOAP 规范的 XML 流。 SOAP 是一种基于 XML 的协议，它是专门为使用 XML 来传输过程调用而设计的。  
  
 若要序列化或反序列化对象，请使用 <xref:System.Xml.Serialization.XmlSerializer> 类。 要创建待序列化的类，请使用 XML 架构定义工具。  
  
## <a name="in-this-section"></a>本节内容  
 [XML 序列化简介](../../../docs/standard/serialization/introducing-xml-serialization.md)  
 提供序列化（尤其是 XML 序列化）的一般定义。  
  
 [如何：序列化对象](../../../docs/standard/serialization/how-to-serialize-an-object.md)  
 提供序列化对象的分步说明。  
  
 [如何：反序列化对象](../../../docs/standard/serialization/how-to-deserialize-an-object.md)  
 提供反序列化对象的分步说明。  
  
 [XML 序列化示例](../../../docs/standard/serialization/examples-of-xml-serialization.md)  
 提供说明 XML 序列化基础的示例。  
  
 [XML 架构定义工具和 XML 序列化](../../../docs/standard/serialization/the-xml-schema-definition-tool-and-xml-serialization.md)  
 描述如何使用 XML 架构定义工具创建遵循特定 XML 架构定义语言 (XSD) 架构的类，或者利用 .dll 文件生成 XML 架构。  
  
 [使用属性控制 XML 序列化](../../../docs/standard/serialization/controlling-xml-serialization-using-attributes.md)  
 描述如何使用属性控制序列化。  
  
 [用来控制 XML 序列化的属性](../../../docs/standard/serialization/attributes-that-control-xml-serialization.md)  
 列出用于控制 XML 序列化的属性。  
  
 [如何：指定 XML 流的替代元素名称](../../../docs/standard/serialization/how-to-specify-an-alternate-element-name-for-an-xml-stream.md)  
 提供一个高级方案，显示如何通过重写序列化来生成多个 XML 流。  
  
 [如何：控制派生类的序列化](../../../docs/standard/serialization/how-to-control-serialization-of-derived-classes.md)  
 提供如何控制派生类的序列化的示例。  
  
 [如何：限定 XML 元素和 XML 属性名](../../../docs/standard/serialization/how-to-qualify-xml-element-and-xml-attribute-names.md)  
 描述如何定义和控制 XML 命名空间在 XML 流中的使用方式。  
  
 [使用 XML Web services 进行 XML 序列化](../../../docs/standard/serialization/xml-serialization-with-xml-web-services.md)  
 说明如何在 XML Web services 中使用 XML 序列化。  
  
 [如何：将对象序列化为 SOAP 编码的 XML 流](../../../docs/standard/serialization/how-to-serialize-an-object-as-a-soap-encoded-xml-stream.md)  
 描述如何使用 <xref:System.Xml.Serialization.XmlSerializer> 类来创建编码的 SOAP XML 流，这些流符合万维网联合会 (www.w3.org) 文档“简单对象访问协议 (SOAP) 1.1”(Simple Object Access Protocol (SOAP) 1.1) 的第 5 节。  
  
 [如何：重写编码的 SOAP XML 序列化](../../../docs/standard/serialization/how-to-override-encoded-soap-xml-serialization.md)  
 描述将对象的 XML 序列化重写为 SOAP 消息的过程。  
  
 [用来控制编码的 SOAP 序列化的属性](../../../docs/standard/serialization/attributes-that-control-encoded-soap-serialization.md)  
 列出用于控制 SOAP 编码的序列化的属性。  
  
 [\<system.xml.serialization> 元素](../../../docs/standard/serialization/system-xml-serialization-element.md)  
 用于控制 XML 序列化的顶级配置元素。  
  
 [\<dateTimeSerialization> 元素](../../../docs/standard/serialization/datetimeserialization-element.md)  
 控制 <xref:System.DateTime> 对象的序列化模式。  
  
 [\<schemaImporterExtensions> 元素](../../../docs/standard/serialization/schemaimporterextensions-element.md)  
 包含 <xref:System.Xml.Serialization.XmlSchemaImporter> 类所使用的类型。  
  
 [\<xmlSchemaImporterExtensions> 的 \<add> 元素](../../../docs/standard/serialization/add-element-for-xmlschemaimporterextensions.md)  
 添加 <xref:System.Xml.Serialization.XmlSchemaImporter> 类所使用的类型。  
  
## <a name="related-sections"></a>相关章节  
 [高级开发技术](http://msdn.microsoft.com/en-us/c4a7e341-f0c6-4df4-a74f-223387ac6e4e)  
 提供链接来指向关于 .NET Framework 中完善的开发任务和技术的更多信息。  
  
 [使用 ASP.NET 创建的 XML Web service 以及 XML Web Service 客户端](http://msdn.microsoft.com/en-us/1e64af78-d705-4384-b08d-591a45f4379c)  
 提供一些主题，描述并说明如何使用 ASP.NET 对 XML Web services 进行编程。  
  
## <a name="see-also"></a>另请参阅  
 [二进制序列化](../../../docs/standard/serialization/binary-serialization.md)

