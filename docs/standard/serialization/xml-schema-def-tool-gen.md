---
title: 'How to: Use the XML Schema Definition Tool to Generate Classes and XML Schema Documents'
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
- generating XML classes using XML Schema Definition tool
- generating XML Schema Document using XML Schema Definition tool
- XML Schema Definition tool, using to generate classes that conform to specific schema
- XML Schema Definition tool, using to generate XML Schema Document
ms.assetid: 51f0edc3-993d-4051-b7f2-77753694d3d1
caps.latest.revision: 5
author: Erikre
ms.author: erikre
manager: erikre
ms.translationtype: HT
ms.sourcegitcommit: 717bcb6f9f72a728d77e2847096ea558a9c50902
ms.openlocfilehash: 3d0d7a6fa5f8b6108567de02cfaec6f1fea71796
ms.contentlocale: zh-cn
ms.lasthandoff: 08/21/2017

---
# <a name="how-to-use-the-xml-schema-definition-tool-to-generate-classes-and-xml-schema-documents"></a>How to: Use the XML Schema Definition Tool to Generate Classes and XML Schema Documents
使用 XML 架构定义工具 (Xsd.exe) 可以生成描述类的 XML 架构，也可以生成 XML 架构定义的类。 下面的过程说明如何执行这两种操作。  
  
### <a name="to-generate-classes-that-conform-to-a-specific-schema"></a>生成符合特定架构的类  
  
1.  打开命令提示。  
  
2.  将 XML 架构作为参数传递给 XML 架构定义工具，该工具将创建与 XML 架构精确匹配的一组类，例如：  
  
    ```  
    xsd mySchema.xsd  
    ```  
  
     该工具只能处理引用万维网联合会 2001 年 3 月 16 日的 XML 规范的架构。 换句话说，XML 架构命名空间必须是“http://www.w3.org/2001/XMLSchema”，如下面的示例所示。  
  
    ```xml  
    <?xml version="1.0" encoding="utf-8"?>  
    <xs:schema attributeFormDefault="qualified" elementFormDefault="qualified" targetNamespace="" xmlns:xs="http://www.w3.org/2001/XMLSchema">  
    ```  
  
3.  必要时用方法、属性或字段修改类。 有关利用特性修改类的详细信息，请参阅[使用特性控制 XML 序列化](../../../docs/standard/serialization/controlling-xml-serialization-using-attributes.md)和[控制编码的 SOAP 序列化的特性](../../../docs/standard/serialization/attributes-that-control-encoded-soap-serialization.md)。  
  
 当序列化一个或多个类的实例后，检查生成的 XML 流的架构通常非常有用。 例如，您可能发布架构以供其他人使用，或者可能将其与想达成一致的架构进行比较。  
  
#### <a name="to-generate-an-xml-schema-document-from-a-set-of-classes"></a>从一组类生成 XML 架构文档  
  
1.  将一个或多个类编译成 DLL。  
  
2.  打开命令提示。  
  
3.  将 DLL 作为参数传递给 Xsd.exe，例如：  
  
    ```  
    xsd MyFile.dll  
    ```  
  
     架构将被写入，以名称“schema0.xsd”开头。  
  
## <a name="see-also"></a>另请参阅  
 <xref:System.Data.DataSet>   
 [XML 架构定义工具和 XML 序列化](../../../docs/standard/serialization/the-xml-schema-definition-tool-and-xml-serialization.md)   
 [XML 序列化简介](../../../docs/standard/serialization/introducing-xml-serialization.md)   
 [XML 架构定义工具 (Xsd.exe)](../../../docs/standard/serialization/xml-schema-definition-tool-xsd-exe.md)   
 <xref:System.Xml.Serialization.XmlSerializer>   
 [如何：序列化对象](../../../docs/standard/serialization/how-to-serialize-an-object.md)   
 [如何：反序列化对象](../../../docs/standard/serialization/how-to-deserialize-an-object.md)

