---
title: "使用数据协定 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
helpviewer_keywords: 
  - "DataContractAttribute 类"
  - "WCF, 数据"
  - "数据协定 [WCF]"
ms.assetid: a3ae7b21-c15c-4c05-abd8-f483bcbf31af
caps.latest.revision: 38
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 38
---
# 使用数据协定
“数据协定”是在服务与客户端之间达成的正式协议，用于以抽象方式描述要交换的数据。 也就是说，为了进行通信，客户端和服务不必共享相同的类型，而只需共享相同的数据协定。 数据协定为每个参数或返回类型精确定义为进行交换而序列化哪些数据（将哪些数据转换为 XML）。  
  
## 数据协定基本知识  
 默认情况下，[!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 使用称为数据协定序列化程序的序列化引擎对数据进行序列化和反序列化（与 XML 进行相互转换）。 所有 [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] 基元类型（如整型和字符串型）以及某些被视为基元的类型（如 <xref:System.DateTime> 和 <xref:System.Xml.XmlElement>）无需做其他任何准备工作就可序列化并被视为拥有默认数据协定。 许多 [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] 类型也具有现有数据协定。 有关可序列化类型的完整列表，请参阅[数据协定序列化程序支持的类型](../../../../docs/framework/wcf/feature-details/types-supported-by-the-data-contract-serializer.md)。  
  
 必须为所创建的新复杂类型定义数据协定才能序列化这些类型。 默认情况下，<xref:System.Runtime.Serialization.DataContractSerializer> 推断数据协定并序列化所有公共可见类型。 类型的所有公共读\/写属性和字段均被序列化。 可以使用 <xref:System.Runtime.Serialization.IgnoreDataMemberAttribute> 从序列化中剔除某些成员。 还可以使用 <xref:System.Runtime.Serialization.DataContractAttribute> 和 <xref:System.Runtime.Serialization.DataMemberAttribute> 属性显式创建数据协定。 正常情况下可通过将 <xref:System.Runtime.Serialization.DataContractAttribute> 属性应用到该类型来完成该任务。 可以将此属性应用到类、结构和枚举。 然后必须将 <xref:System.Runtime.Serialization.DataMemberAttribute> 属性应用到数据协定类型的每个成员，以指示这些成员为数据成员，即应进行序列化。[!INCLUDE[crdefault](../../../../includes/crdefault-md.md)] [可序列化类型](../../../../docs/framework/wcf/feature-details/serializable-types.md).  
  
### 示例  
 下面的示例演示已经显式应用了 <xref:System.ServiceModel.ServiceContractAttribute> 和 <xref:System.ServiceModel.OperationContractAttribute> 属性的服务协定（接口）。 该示例演示基元类型不要求数据协定，而复杂类型却对此有要求。  
  
 [!code-csharp[C_DataContract#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_datacontract/cs/source.cs#1)]
 [!code-vb[C_DataContract#1](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_datacontract/vb/source.vb#1)]  
  
 下面的示例演示如何通过将 `MyTypes.PurchaseOrder` 和 <xref:System.Runtime.Serialization.DataContractAttribute> 属性应用于类及其成员来创建 <xref:System.Runtime.Serialization.DataMemberAttribute> 类型的数据协定。  
  
 [!code-csharp[C_DataContract#2](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_datacontract/cs/source.cs#2)]
 [!code-vb[C_DataContract#2](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_datacontract/vb/source.vb#2)]  
  
### 备注  
 下面的注释提供在创建数据协定时需要考虑的事项：  
  
-   仅当用于未标记的类型时，才接受 <xref:System.Runtime.Serialization.IgnoreDataMemberAttribute> 属性。 这包括未使用 <xref:System.Runtime.Serialization.DataContractAttribute>、<xref:System.SerializableAttribute>、<xref:System.Runtime.Serialization.CollectionDataContractAttribute> 或 <xref:System.Runtime.Serialization.EnumMemberAttribute> 属性之一标记的类型，或通过任何其他方式（如 <xref:System.Xml.Serialization.IXmlSerializable>）标记为可序列化的类型。  
  
-   可以将 <xref:System.Runtime.Serialization.DataMemberAttribute> 属性 \(Attribute\) 应用于字段和属性 \(Property\)。  
  
-   成员可访问性级别（internal、private、protected 或 public）对数据协定无任何影响。  
  
-   如果将 <xref:System.Runtime.Serialization.DataMemberAttribute> 属性应用于静态成员，则将忽略该属性。  
  
-   在序列化期间，为属性数据成员调用 property\-get 代码来获取要序列化的属性的值。  
  
-   在反序列化期间，首先创建一个未初始化的对象，而不在该类型上调用任何构造函数。 然后反序列化所有数据成员。  
  
-   在反序列化期间，为属性数据成员调用 property\-set 代码，将属性设置为要反序列化的值。  
  
-   对于将要生效的数据协定，它必须能序列化其所有数据成员。 有关可序列化类型的完整列表，请参阅[数据协定序列化程序支持的类型](../../../../docs/framework/wcf/feature-details/types-supported-by-the-data-contract-serializer.md)。  
  
     泛型类型的处理方式与非泛型类型完全相同。 泛型参数无特殊要求。 例如，请注意以下类型：  
  
 [!code-csharp[C_DataContract#3](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_datacontract/cs/source.cs#3)]
 [!code-vb[C_DataContract#3](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_datacontract/vb/source.vb#3)]  
  
 无论用于泛型类型参数 \(`T`\) 的类型能否序列化，此类型都可序列化。 因为它必须能序列化所有数据成员，所以下面的类型仅在泛型类型参数也可序列化时才可序列化，如以下代码所示。  
  
 [!code-csharp[C_DataContract#4](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_datacontract/cs/source.cs#4)]
 [!code-vb[C_DataContract#4](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_datacontract/vb/source.vb#4)]  
  
 有关定义数据协定的 WCF 服务的完整代码示例，请参阅[基本数据协定](../../../../docs/framework/wcf/samples/basic-data-contract.md)示例。  
  
## 请参阅  
 <xref:System.Runtime.Serialization.DataMemberAttribute>   
 <xref:System.Runtime.Serialization.DataContractAttribute>   
 [可序列化类型](../../../../docs/framework/wcf/feature-details/serializable-types.md)   
 [数据协定名称](../../../../docs/framework/wcf/feature-details/data-contract-names.md)   
 [数据协定等效性](../../../../docs/framework/wcf/feature-details/data-contract-equivalence.md)   
 [数据成员顺序](../../../../docs/framework/wcf/feature-details/data-member-order.md)   
 [数据协定已知类型](../../../../docs/framework/wcf/feature-details/data-contract-known-types.md)   
 [向前兼容的数据协定](../../../../docs/framework/wcf/feature-details/forward-compatible-data-contracts.md)   
 [数据协定版本管理](../../../../docs/framework/wcf/feature-details/data-contract-versioning.md)   
 [版本容错序列化回调](../../../../docs/framework/wcf/feature-details/version-tolerant-serialization-callbacks.md)   
 [数据成员默认值](../../../../docs/framework/wcf/feature-details/data-member-default-values.md)   
 [数据协定序列化程序支持的类型](../../../../docs/framework/wcf/feature-details/types-supported-by-the-data-contract-serializer.md)   
 [如何：创建类或结构的基本数据协定](../../../../docs/framework/wcf/feature-details/how-to-create-a-basic-data-contract-for-a-class-or-structure.md)