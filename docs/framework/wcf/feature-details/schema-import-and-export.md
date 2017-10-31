---
title: "架构导入和导出 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "WCF, 架构导入和导出"
  - "XsdDataContractExporter 类"
  - "XsdDataContractImporter 类"
ms.assetid: 0da32b50-ccd9-463a-844c-7fe803d3bf44
caps.latest.revision: 14
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 14
---
# 架构导入和导出
[!INCLUDE[indigo1](../../../../includes/indigo1-md.md)]包括新的序列化引擎， <xref:System.Runtime.Serialization.DataContractSerializer>。 `DataContractSerializer` 在 [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] 对象和 XML 之间进行转换（双向）。 除了序列化程序本身，[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 还包括关联的架构导入和架构导出机制。 *架构*是的 XML 序列化程序生成或反序列化程序可以访问的形状的正式、 精确和计算机可读说明。 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 使用万维网联合会 (W3C) XML 架构定义语言 (XSD) 作为其架构表示形式，它可以与许多第三方平台广泛互操作。  
  
 架构导入组件<xref:System.Runtime.Serialization.XsdDataContractImporter>使用 XSD 架构文档并生成[!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)]类 （通常为数据协定类），使序列化的格式对应于给定架构。  
  
 例如，以下架构片段：  
  
 [!code-csharp[c_SchemaImportExport#8](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_schemaimportexport/cs/source.cs#8)]
 [!code-vb[c_SchemaImportExport#8](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_schemaimportexport/vb/source.vb#8)]  
  
 生成以下类型（略经简化以便于阅读）。  
  
 [!code-csharp[c_SchemaImportExport#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_schemaimportexport/cs/source.cs#1)]
 [!code-vb[c_SchemaImportExport#1](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_schemaimportexport/vb/source.vb#1)]  
  
 请注意生成的类型遵循几个数据协定最佳做法 (位于[最佳做法︰ 数据协定版本管理](../../../../docs/framework/wcf/best-practices-data-contract-versioning.md)):  
  
-   该类型实现<xref:System.Runtime.Serialization.IExtensibleDataObject>接口。 [!INCLUDE[crdefault](../../../../includes/crdefault-md.md)][向前兼容的数据协定](../../../../docs/framework/wcf/feature-details/forward-compatible-data-contracts.md)。  
  
-   数据成员作为封装私有字段的公共属性来实现。  
  
-   此类是一个分部类，不修改生成的代码就可以添加内容。  
  
 <xref:System.Runtime.Serialization.XsdDataContractExporter>可进行反向操作 — 采用进行序列化的类型`DataContractSerializer`并生成 XSD 架构文档。  
  
## <a name="fidelity-is-not-guaranteed"></a>不保证保真  
 不保证进行往返行程的架构或类型完全保真。 (A*往返*是指导入架构以创建一组类，并导出结果以重新创建架构。)可能不会返回相同的架构。 反向过程也不保证保真。 （导出类型以生成其架构，然后重新导入此类型。 不太可能返回相同的类型。）  
  
## <a name="supported-types"></a>支持的类型  
 数据协定模型只支持有限的 WC3 架构子集。 导入过程中任何不符合此子集的架构都将导致异常。 例如，没有办法可以指定数据协定的数据成员应该作为 XML 属性进行序列化。 这样，由于不能用正确的 XML 投影生成数据协定，需要使用 XML 属性的架构将不受支持，并且将在导入过程中导致异常。  
  
 例如，不能使用默认导入设置导入以下架构片段。  
  
 <!-- TODO: review snippet reference [!code[c_SchemaImportExport#9](../../../../samples/snippets/common/VS_Snippets_CFX/c_schemaimportexport/common/source.config#9)]  -->  
  
 [!INCLUDE[crdefault](../../../../includes/crdefault-md.md)][数据协定架构参考](../../../../docs/framework/wcf/feature-details/data-contract-schema-reference.md)。 如果架构不符合数据协定规则，请使用另一个序列化引擎。 例如， <xref:System.Xml.Serialization.XmlSerializer>使用其自己的独立架构导入机制。 另有一种特殊的导入模式，可在其中扩展所支持架构的范围。 [!INCLUDE[crdefault](../../../../includes/crdefault-md.md)]有关生成的部分<xref:System.Xml.Serialization.IXmlSerializable>中的类型[导入架构以生成类](../../../../docs/framework/wcf/feature-details/importing-schema-to-generate-classes.md)。  
  
 `XsdDataContractExporter` 支持可以用 [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] 序列化的任何 `DataContractSerializer` 类型。 [!INCLUDE[crdefault](../../../../includes/crdefault-md.md)][支持的数据协定序列化程序类型](../../../../docs/framework/wcf/feature-details/types-supported-by-the-data-contract-serializer.md)。 请注意使用生成该架构`XsdDataContractExporter`是正常情况下有效的数据，`XsdDataContractImporter`可以使用 (除非<xref:System.Xml.Serialization.XmlSchemaProviderAttribute>用于自定义该架构)。  
  
 [!INCLUDE[crabout](../../../../includes/crabout-md.md)]使用<xref:System.Runtime.Serialization.XsdDataContractImporter>，请参阅[导入架构以生成类](../../../../docs/framework/wcf/feature-details/importing-schema-to-generate-classes.md)。  
  
 [!INCLUDE[crabout](../../../../includes/crabout-md.md)]使用<xref:System.Runtime.Serialization.XsdDataContractExporter>，请参阅[从类导出架构](../../../../docs/framework/wcf/feature-details/exporting-schemas-from-classes.md)。  
  
## <a name="see-also"></a>另请参阅  
 <xref:System.Runtime.Serialization.DataContractSerializer>   
 <xref:System.Runtime.Serialization.XsdDataContractImporter>   
 <xref:System.Runtime.Serialization.XsdDataContractExporter>   
 [导入架构以生成类](../../../../docs/framework/wcf/feature-details/importing-schema-to-generate-classes.md)   
 [从类导出架构](../../../../docs/framework/wcf/feature-details/exporting-schemas-from-classes.md)