---
title: "数据成员默认值 | Microsoft Docs"
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
  - "数据成员 [WCF]"
  - "数据成员 [WCF], 默认值"
ms.assetid: 53a3b505-4b27-444b-b079-0eb84a97cfd8
caps.latest.revision: 10
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 10
---
# 数据成员默认值
在 [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] 中，类型有一个概念，即默认值。例如，对于任何引用类型，默认值为 `null`，而整型的默认值为零。如果某个数据成员设置为其默认值，有时会希望序列化数据中不包含该数据成员。由于成员具有默认值，这个实际值不需要进行序列化；这样处理可以提高性能。  
  
 若要在序列化数据中忽略某个成员，请将 <xref:System.Runtime.Serialization.DataMemberAttribute> 属性 \(Attribute\) 的 <xref:System.Runtime.Serialization.DataMemberAttribute.EmitDefaultValue%2A> 属性 \(Property\) 设置为 `false`（默认值为 `true`）。  
  
> [!NOTE]
>  如果有特定需要（如实现互操作性或减小数据大小），应将 <xref:System.Runtime.Serialization.DataMemberAttribute.EmitDefaultValue%2A> 属性设置为 `false`。  
  
## 示例  
 下面的代码中，有几个成员的 <xref:System.Runtime.Serialization.DataMemberAttribute.EmitDefaultValue%2A> 设置为 `false`。  
  
 [!code-csharp[DataMemberAttribute#4](../../../../samples/snippets/csharp/VS_Snippets_CFX/datamemberattribute/cs/overview.cs#4)]
 [!code-vb[DataMemberAttribute#4](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/datamemberattribute/vb/overview.vb#4)]  
  
 如果序列化此类的实例，则结果如下：序列化 `employeeName` 和 `employeeID`。`employeeName` 的 null 值和 `employeeID` 的零值显式成为序列化数据的一部分。但是，`position`、`salary` 和 `bonus` 成员没有被序列化。最后，即使 <xref:System.Runtime.Serialization.DataMemberAttribute.EmitDefaultValue%2A> 属性设置为 `false`，由于 57800 不是 .NET 的整数默认值零，`targetSalary` 还是照常被序列化。  
  
### XML 表示形式  
 如果上一个示例序列化为 XML，则表示形式类似于下面的内容。  
  
```  
<Employee>  
   <employeeName xsi:nil="true" />  
   <employeeID>0</employeeID>  
<targetSalary>57800</targetSalary>  
</Employee>  
```  
  
 `xsi:nil` 属性是万维网联合会 \(W3C\) XML 架构实例命名空间中的一个特殊属性，它提供一种显式表示 null 值的可互操作方式。请注意，在 XML 中，没有 position、salary 和 bonus 数据成员的任何相关信息。接收端可将它们分别解释为 `null`、零和 `null`。无法确保第三方反序列化程序可以进行正确的解释，这就是不建议使用这种模式的原因。<xref:System.Runtime.Serialization.DataContractSerializer> 类始终为缺少的值选择正确的解释。  
  
### 与 IsRequired 交互  
 正如[数据协定版本管理](../../../../docs/framework/wcf/feature-details/data-contract-versioning.md)中讨论的那样，<xref:System.Runtime.Serialization.DataMemberAttribute> 属性 \(Attribute\) 具有 <xref:System.Runtime.Serialization.DataMemberAttribute.IsRequired%2A> 属性 \(Property\)（默认值为 `false`）。该属性 \(Property\) 指示，当某个给定数据成员进行反序列化时，该数据成员是否必须出现在序列化数据中。如果 `IsRequired` 设置为 `true`（指示值必须存在）并且 <xref:System.Runtime.Serialization.DataMemberAttribute.EmitDefaultValue%2A> 设置为 `false`（指示如果值设置为其默认值，则该值不得存在），则由于结果相互矛盾，此数据成员的默认值无法序列化。如果这样的一个数据成员被设置为其默认值（通常为 `null` 或零）并且尝试进行序列化，则会引发 <xref:System.Runtime.Serialization.SerializationException>。  
  
### 架构表示形式  
 在[数据协定架构参考](../../../../docs/framework/wcf/feature-details/data-contract-schema-reference.md)中，详细讨论了当 `EmitDefaultValue` 属性设置为 `false` 时，数据成员的 XML 架构定义语言 \(XSD\) 架构表示形式。下面是简要概述：  
  
-   当 <xref:System.Runtime.Serialization.DataMemberAttribute.EmitDefaultValue%2A> 设置为 `false` 时，它在架构中表示为特定于 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 的批注。没有用于表示此信息的可交互操作方式。特别是，架构中的“default”属性不用于此目的，`minOccurs` 属性仅受 <xref:System.Runtime.Serialization.DataMemberAttribute.IsRequired%2A> 设置的影响，而 `nillable` 属性仅受数据成员类型的影响。  
  
-   要使用的实际默认值在架构中不存在。由接收终结点负责对缺少元素进行适当解释。  
  
 导入架构时，每当检测到前述特定于 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 的批注，<xref:System.Runtime.Serialization.DataMemberAttribute.EmitDefaultValue%2A> 属性都自动设置为 `false`。对于 `nillable` 属性设置为 `false` 的引用类型，该属性也设置为 `false`，以支持在使用 [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)] Web 服务时常遇到的特定互操作性方案。  
  
## 请参阅  
 <xref:System.Runtime.Serialization.DataMemberAttribute.EmitDefaultValue%2A>   
 <xref:System.Runtime.Serialization.DataMemberAttribute>