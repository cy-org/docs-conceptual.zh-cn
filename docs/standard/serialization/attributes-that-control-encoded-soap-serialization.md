---
title: "用来控制编码的 SOAP 序列化的属性"
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
- XML serialization, attributes
- attributes [.NET Framework], XML serialization
- serialization, attributes
ms.assetid: 93ee258c-9c0f-4a08-897c-c10db7a00f91
caps.latest.revision: 8
author: Erikre
ms.author: erikre
manager: erikre
ms.translationtype: HT
ms.sourcegitcommit: 717bcb6f9f72a728d77e2847096ea558a9c50902
ms.openlocfilehash: a6af8cd2560bb9c39657d8e5b088954996ba2a04
ms.contentlocale: zh-cn
ms.lasthandoff: 08/21/2017

---
# <a name="attributes-that-control-encoded-soap-serialization"></a>用来控制编码的 SOAP 序列化的属性 
命名为“简单对象访问协议 (SOAP) 1.1”(Simple Object Access Protocol (SOAP) 1.1) 的万维网联合会 (www.w3.org) 文档包含一个可选章节（第 5 节），该节描述了如何编码 SOAP 参数。 要符合该规范的第 5 节，必须使用在 <xref:System.Xml.Serialization> 命名空间中找到的一组特殊属性。 将这些特性适当应用于类和类的成员，然后使用 <xref:System.Xml.Serialization.XmlSerializer> 序列化一个或多个类的实例。  
  
 下表显示属性、属性的应用范围及其作用。 有关使用这些属性控制 XML 序列化的更多信息，请参阅[如何：将对象序列化为 SOAP 编码的 XML 流](../../../docs/standard/serialization/how-to-serialize-an-object-as-a-soap-encoded-xml-stream.md)和[如何：替代编码的 SOAP XML 序列化](../../../docs/standard/serialization/how-to-override-encoded-soap-xml-serialization.md)。  
  
 有关属性的详细信息，请参阅[属性](../../../docs/standard/attributes/index.md)。  
  
|特性|适用对象|指定|  
|---------------|----------------|---------------|  
|<xref:System.Xml.Serialization.SoapAttributeAttribute>|公共字段、属性、参数或返回值。|类成员将序列化为 XML 属性。|  
|<xref:System.Xml.Serialization.SoapElementAttribute>|公共字段、属性、参数或返回值。|类将序列化为 XML 元素。|  
|<xref:System.Xml.Serialization.SoapEnumAttribute>|作为枚举标识符的公共字段。|枚举成员的元素名称。|  
|<xref:System.Xml.Serialization.SoapIgnoreAttribute>|公共属性和公共字段。|序列化包含类时，应该忽略属性或字段。|  
|<xref:System.Xml.Serialization.SoapIncludeAttribute>|公共的派生类声明，以及 Web 服务描述语言 (WSDL) 文档的公共方法。|生成要在序列化时识别的架构时，应该将该类型包括在内。|  
|<xref:System.Xml.Serialization.SoapTypeAttribute>|公共类声明。|类应序列化为 XML 类型。|  
  
## <a name="see-also"></a>另请参阅  
 [XML 和 SOAP 序列化](../../../docs/standard/serialization/xml-and-soap-serialization.md)   
 [如何：将对象序列化为 SOAP 编码的 XML 流](../../../docs/standard/serialization/how-to-serialize-an-object-as-a-soap-encoded-xml-stream.md)   
 [如何：重写编码的 SOAP XML 序列化](../../../docs/standard/serialization/how-to-override-encoded-soap-xml-serialization.md)   
 [特性](../../../docs/standard/attributes/index.md)   
 <xref:System.Xml.Serialization.XmlSerializer>   
 [如何：序列化对象](../../../docs/standard/serialization/how-to-serialize-an-object.md)   
 [如何：反序列化对象](../../../docs/standard/serialization/how-to-deserialize-an-object.md)

