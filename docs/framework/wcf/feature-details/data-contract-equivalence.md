---
title: "数据协定等效性 | Microsoft Docs"
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
  - "数据协定 [WCF], 等效性"
ms.assetid: f06f3c7e-c235-4ec1-b200-68142edf1ed1
caps.latest.revision: 16
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 16
---
# 数据协定等效性
对于客户端要将某种类型的数据成功发送到服务，或者服务要将数据成功发送到客户端的情况，接收端上并不一定必须存在此发送数据类型。  唯一的要求是两种类型的数据协定应该等效。  （有时不要求严格等效，如[数据协定版本管理](../../../../docs/framework/wcf/feature-details/data-contract-versioning.md)中所述。）  
  
 要使数据协定等效，其命名空间和名称必须相同。  此外，某一端上的每个数据成员还必须在另一端上具有等效的数据成员。  
  
 要使数据成员等效，其名称必须相同。  此外，它们还必须表示同一类型的数据，也就是说，其数据协定必须等效。  
  
> [!NOTE]
>  请注意，数据协定名称和命名空间以及数据成员名称均区分大小写。  
  
 [!INCLUDE[crabout](../../../../includes/crabout-md.md)]数据协定名称和命名空间以及数据成员名称的更多信息，请参见[数据协定名称](../../../../docs/framework/wcf/feature-details/data-contract-names.md)。  
  
 如果同一端（发送方或接收方）存在两种类型，而其数据协定又不等效（例如，它们的数据成员不同），则不应为它们指定相同的名称和命名空间。  否则，可能会引发异常。  
  
 以下类型的数据协定是等效的：  
  
 [!code-csharp[C_DataContractNames#5](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_datacontractnames/cs/source.cs#5)]
 [!code-vb[C_DataContractNames#5](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_datacontractnames/vb/source.vb#5)]  
  
## 数据成员顺序和数据协定等效性  
 使用 <xref:System.Runtime.Serialization.DataMemberAttribute> 类的 <xref:System.Runtime.Serialization.DataMemberAttribute.Order%2A> 属性可能会影响数据协定等效性。  其成员必须以相同顺序出现，数据协定才能等效。  默认顺序是按字母顺序。  [!INCLUDE[crdefault](../../../../includes/crdefault-md.md)] [数据成员顺序](../../../../docs/framework/wcf/feature-details/data-member-order.md).  
  
 例如，以下代码生成的数据协定是等效的。  
  
 [!code-csharp[C_DataContractNames#6](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_datacontractnames/cs/source.cs#6)]
 [!code-vb[C_DataContractNames#6](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_datacontractnames/vb/source.vb#6)]  
  
 但是，以下代码生成的数据协定不是等效的。  
  
 [!code-csharp[C_DataContractNames#7](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_datacontractnames/cs/source.cs#7)]
 [!code-vb[C_DataContractNames#7](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_datacontractnames/vb/source.vb#7)]  
  
## 继承、接口和数据协定等效性  
 确定等效性时，对于从其他数据协定继承的数据协定，将被视为一个包含所有基类型的数据成员的数据协定。  请记住，数据成员的顺序必须匹配，并且基类型成员排在派生类型成员之前。  此外，如下面的代码示例所示，如果两个数据成员的顺序值相同，则这两个数据成员的顺序为按字母顺序。  [!INCLUDE[crdefault](../../../../includes/crdefault-md.md)] [数据成员顺序](../../../../docs/framework/wcf/feature-details/data-member-order.md).  
  
 在下面的示例中，类型为 `Employee` 的数据协定等效于类型为 `Worker` 的数据协定。  
  
 [!code-csharp[C_DataContractNames#8](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_datacontractnames/cs/source.cs#8)]
 [!code-vb[C_DataContractNames#8](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_datacontractnames/vb/source.vb#8)]  
  
 在客户端和服务之间传递参数和返回值时，如果接收终结点要求来自派生类的数据协定，则不能发送来自基类的数据协定。  这一点符合面向对象的编程原则。  在前面的示例中，如果要求 `Employee`，则不能发送 `Person` 类型的对象。  
  
 如果要求来自基类的数据协定，则可发送来自派生类的数据协定，但前提是接收终结点通过 <xref:System.Runtime.Serialization.KnownTypeAttribute>“知道”该派生类型。  [!INCLUDE[crdefault](../../../../includes/crdefault-md.md)] [数据协定已知类型](../../../../docs/framework/wcf/feature-details/data-contract-known-types.md).  在前面的示例中，当要求 `Person` 时，可以发送 `Employee` 类型的对象，但前提是接收方代码使用 <xref:System.Runtime.Serialization.KnownTypeAttribute> 将它包含在已知类型列表中。  
  
 在应用程序之间传递参数和返回值时，如果所需类型为接口，则等效于所需类型为 <xref:System.Object> 类型。  由于每种类型最终都派生自 <xref:System.Object>，因此所有数据协定最终都派生自 <xref:System.Object> 的数据协定。  这样，在要求使用接口时，就可以传递任何数据协定类型。  若要成功使用接口，还需要执行额外步骤；有关更多信息，请参见[数据协定已知类型](../../../../docs/framework/wcf/feature-details/data-contract-known-types.md)。  
  
## 请参阅  
 <xref:System.Runtime.Serialization.DataContractAttribute>   
 <xref:System.Runtime.Serialization.DataMemberAttribute>   
 [数据成员顺序](../../../../docs/framework/wcf/feature-details/data-member-order.md)   
 [数据协定已知类型](../../../../docs/framework/wcf/feature-details/data-contract-known-types.md)   
 [数据协定名称](../../../../docs/framework/wcf/feature-details/data-contract-names.md)