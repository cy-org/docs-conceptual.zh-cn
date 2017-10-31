---
title: "向前兼容的数据协定 | Microsoft Docs"
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
  - "数据协定 [WCF], 向前兼容性"
ms.assetid: 413c9044-26f8-4ecb-968c-18495ea52cd9
caps.latest.revision: 21
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 21
---
# 向前兼容的数据协定
[!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 数据协定系统的一个特征是协定能够以不间断的方式随着时间而逐步演化。也就是说，具有旧版本数据协定的客户端可以与具有相同数据协定的新版本的服务进行通信，或者具有新版本数据协定的客户端可以与相同数据协定的旧版本进行通信。[!INCLUDE[crdefault](../../../../includes/crdefault-md.md)][最佳做法：数据协定版本管理](../../../../docs/framework/wcf/best-practices-data-contract-versioning.md).  
  
 如果创建了现有数据协定的新版本，您可以根据需要来应用大多数版本管理功能。但是为了能正常工作，第一版的类型中必须内置一种称为“往返”的版本管理功能。  
  
## 往返  
 当数据从数据协定的新版本传递到旧版本，然后传递回新版本时，就发生了往返。往返保证了数据不会丢失。如果启用往返功能，则可以使类型向前兼容于数据协定版本管理模型所支持的任何未来更改。  
  
 若要对某一特定类型启用往返功能，该类型必须实现 <xref:System.Runtime.Serialization.IExtensibleDataObject> 接口。该接口包含一个属性，即 <xref:System.Runtime.Serialization.IExtensibleDataObject.ExtensionData%2A>（由 <xref:System.Runtime.Serialization.ExtensionDataObject> 类型返回）。该属性存储数据协定未来版本中对当前版本未知的所有数据。  
  
### 示例  
 下面的数据协定不向前兼容于未来的更改。  
  
 [!code-csharp[C_DataContract#7](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_datacontract/cs/source.cs#7)]
 [!code-vb[C_DataContract#7](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_datacontract/vb/source.vb#7)]  
  
 若要使该类型兼容于未来的更改（例如添加名为“phoneNumber”的新数据成员），应实现 <xref:System.Runtime.Serialization.IExtensibleDataObject> 接口。  
  
 [!code-csharp[C_DataContract#8](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_datacontract/cs/source.cs#8)]
 [!code-vb[C_DataContract#8](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_datacontract/vb/source.vb#8)]  
  
 当 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 基础结构遇到不属于原始数据协定的数据时，该数据被存储在该属性中并保留下来。除非是临时存储，否则不会以任何其他方式处理该数据。如果对象返回到它的起始位置，则原始（未知）数据也将返回。由此，数据完成了从起始终结点又回到起始终结点的往返过程而没有丢失。但请注意，如果起始终结点要求处理数据，则不会满足这一期望，该终结点必须以某种方式检测并调整更改。  
  
 <xref:System.Runtime.Serialization.ExtensionDataObject> 类型不包含公共方法或属性。因此，无法直接访问存储在 <xref:System.Runtime.Serialization.IExtensibleDataObject.ExtensionData%2A> 属性内部的数据。  
  
 通过在 <xref:System.Runtime.Serialization.DataContractSerializer> 构造函数中将 `ignoreExtensionDataObject` 设置为 `true`，或者在 <xref:System.ServiceModel.ServiceBehaviorAttribute> 中将 <xref:System.ServiceModel.ServiceBehaviorAttribute.IgnoreExtensionDataObject%2A> 属性设置为 `true`，可以关闭往返功能。当该功能关闭时，反序列化程序将不填充 <xref:System.Runtime.Serialization.IExtensibleDataObject.ExtensionData%2A> 属性，序列化程序也不发出该属性的内容。  
  
## 请参阅  
 <xref:System.Runtime.Serialization.IExtensibleDataObject>   
 <xref:System.Runtime.Serialization.ExtensionDataObject>   
 [数据协定版本管理](../../../../docs/framework/wcf/feature-details/data-contract-versioning.md)   
 [最佳做法：数据协定版本管理](../../../../docs/framework/wcf/best-practices-data-contract-versioning.md)