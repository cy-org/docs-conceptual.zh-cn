---
title: "数据协定名称 | Microsoft Docs"
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
  - "数据协定 [WCF], 命名"
ms.assetid: 31f87e6c-247b-48f5-8e94-b9e1e33d8d09
caps.latest.revision: 27
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 27
---
# 数据协定名称
有时，客户端和服务不共享相同的类型。他们仍然可以将数据传递给对方，只要数据合同是双方等效。[数据协定等效性](../../../../docs/framework/wcf/feature-details/data-contract-equivalence.md) 基于数据协定和数据成员名称和映射类型和这些成员名称，提供了一个机制。本主题说明数据协定的命名规则以及创建名称时 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 基础结构的默认行为。  
  
## 基本规则  
 有关数据协定命名的基本规则包括：  
  
-   完全限定的数据协定名称由命名空间和名称组成。  
  
-   数据成员只有名称，而没有命名空间。  
  
-   处理数据协定时，[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 基础结构对于命名空间以及数据协定和数据成员的名称区分大小写。  
  
## 数据协定命名空间  
 数据协定命名空间采用统一资源标识符 \(URI\) 的形式。URI 可以是绝对的，也可以是相对的。默认情况下，会为特定类型的数据协定分配公共语言运行库 \(CLR\) 命名空间中该类型的命名空间。  
  
 默认情况下，任何给定的 CLR 命名空间（采用 *Clr.Namespace* 格式）都会映射到“http:\/\/schemas.datacontract.org\/2004\/07\/Clr.Namespace”命名空间。若要重写此默认值，请对整个模块或程序集应用 <xref:System.Runtime.Serialization.ContractNamespaceAttribute> 属性。或者，若要控制每种类型的数据协定命名空间，请设置 <xref:System.Runtime.Serialization.DataContractAttribute> 的 <xref:System.Runtime.Serialization.DataContractAttribute.Namespace%2A> 属性。  
  
> [!NOTE]
>  “http:\/\/schemas.microsoft.com\/2003\/10\/Serialization”是保留的命名空间，不能用作数据协定命名空间。  
  
> [!NOTE]
>  不能重写包含 `delegate` 声明的数据协定类型中的默认命名空间。  
  
## 数据协定名称  
 给定类型的默认数据协定名称是该类型的名称。若要重写默认值，请将 <xref:System.Runtime.Serialization.DataContractAttribute> 的 <xref:System.Runtime.Serialization.DataContractAttribute.Name%2A> 属性设置为其他名称。本主题中后面的“泛型类型的数据协定名称”中说明了泛型类型的特殊规则。  
  
## 数据成员名称  
 给定字段或属性的默认数据成员名称是该字段或属性的名称。若要重写默认值，请将 <xref:System.Runtime.Serialization.DataMemberAttribute> 的 <xref:System.Runtime.Serialization.DataMemberAttribute.Name%2A> 属性设置为其他值。  
  
### 示例  
 下面的示例演示如何重写数据协定和数据成员的默认命名行为。  
  
 [!code-csharp[C_DataContractNames#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_datacontractnames/cs/source.cs#1)]
 [!code-vb[C_DataContractNames#1](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_datacontractnames/vb/source.vb#1)]  
  
## 泛型类型的数据协定名称  
 确定泛型类型的数据协定名称具有特殊的规则。这些规则有助于避免在同一泛型类型的两个封闭式泛型之间发生数据协定名称冲突。  
  
 默认情况下，泛型类型的数据协定名称是该类型的名称后跟随字符串“Of”，后面跟随泛型参数的数据协定名称，后面跟随使用泛型参数的数据协定命名空间计算的哈希值。哈希值是作为唯一标识数据片段的“指纹”的数学函数的计算结果。当所有的泛型参数都是基元类型时，将忽略哈希值。  
  
 有关示例，请参见以下示例中的类型。  
  
 [!code-csharp[C_DataContractNames#2](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_datacontractnames/cs/source.cs#2)]
 [!code-vb[C_DataContractNames#2](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_datacontractnames/vb/source.vb#2)]  
  
 在此示例中，`Drawing<Square,RegularRedBrush>` 类型具有数据协定名称“DrawingOfSquareRedBrush5HWGAU6h”，其中“5HWGAU6h”是“urn:shapes”和“urn:default”命名空间的哈希值。`Drawing<Square,SpecialRedBrush>` 类型具有数据协定名称“DrawingOfSquareRedBrushjpB5LgQ\_S”，其中“jpB5LgQ\_S”是“urn:shapes”和“urn:special”命名空间的哈希值。请注意，如果不使用哈希值，则这两个名称将完全相同，因此会发生名称冲突。  
  
## 自定义泛型类型的数据协定名称  
 有时不允许为泛型类型生成数据协定名称，如前面所述。例如，您可能事先知道不会遇到名称冲突并且想删除哈希值。在这种情况下，您可以使用 `DataContractAttribute` 属性 \(attribute\) 的 <xref:System.Runtime.Serialization.DataContractAttribute.Name%2A> 属性 \(property\) 指定另一种方式生成名称。您可以在 `Name` 属性内的大括号中使用数字来引用泛型参数的数据协定名称。（0 指第一个参数，1 指第二个参数，依此类推。）可以在大括号内使用数字符号 \(\#\) 来引用哈希值。您可以多次使用这些引用，也可以不使用引用。  
  
 例如，可能对前面的泛型 `Drawing` 类型进行了声明，如以下示例所示。  
  
 [!code-csharp[c_DataContractNames#3](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_datacontractnames/cs/source.cs#3)]
 [!code-vb[c_DataContractNames#3](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_datacontractnames/vb/source.vb#3)]  
  
 在这种情况下，`Drawing<Square,RegularRedBrush>` 类型具有数据协定名称“Drawing\_using\_RedBrush\_brush\_and\_Square\_shape”。请注意，因为 <xref:System.Runtime.Serialization.DataContractAttribute.Name%2A> 属性中有一个“{\#}”，哈希值不是名称的一部分，因此该类型容易发生命名冲突；例如，`Drawing<Square,SpecialRedBrush>` 类型将具有完全相同的数据协定名称。  
  
## 请参阅  
 <xref:System.Runtime.Serialization.DataContractAttribute>   
 <xref:System.Runtime.Serialization.DataMemberAttribute>   
 <xref:System.Runtime.Serialization.ContractNamespaceAttribute>   
 [使用数据协定](../../../../docs/framework/wcf/feature-details/using-data-contracts.md)   
 [数据协定等效性](../../../../docs/framework/wcf/feature-details/data-contract-equivalence.md)   
 [Data Contract Names](../../../../docs/framework/wcf/feature-details/data-contract-names.md)   
 [数据协定版本管理](../../../../docs/framework/wcf/feature-details/data-contract-versioning.md)