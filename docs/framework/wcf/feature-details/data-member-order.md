---
title: "数据成员顺序 | Microsoft Docs"
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
  - "数据协定 [WCF], 对成员排序"
ms.assetid: 0658a47d-b6e5-4ae0-ba72-ababc3c6ff33
caps.latest.revision: 17
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 17
---
# 数据成员顺序
在一些应用程序中，有必要知道各个数据成员中数据的发送顺序或预期接收顺序（比如序列化 XML 中数据的显示顺序）。有时，必须要更改此顺序。本主题说明排序规则。  
  
## 基本规则  
 数据排序的基本规则包括：  
  
-   如果数据协定类型是继承层次结构的一部分，则其基类型的数据成员始终排在第一位。  
  
-   排在下一位的是当前类型的数据成员（按字母顺序排列），这些成员未设置 <xref:System.Runtime.Serialization.DataMemberAttribute> 属性 \(attribute\) 的 <xref:System.Runtime.Serialization.DataMemberAttribute.Order%2A> 属性 \(property\)。  
  
-   再下面是设置了 <xref:System.Runtime.Serialization.DataMemberAttribute> 属性 \(attribute\) 的 <xref:System.Runtime.Serialization.DataMemberAttribute.Order%2A> 属性 \(property\) 的任何数据成员。这些成员首先按 `Order` 属性的值排序，如果多个成员具有特定的 `Order` 值，则按字母顺序排列。可以跳过 Order 值。  
  
 字母顺序是通过调用 <xref:System.String.CompareOrdinal%2A> 方法确定的。  
  
## 示例  
 考虑下列代码。  
  
 [!code-csharp[C_DataContractNames#4](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_datacontractnames/cs/source.cs#4)]
 [!code-vb[C_DataContractNames#4](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_datacontractnames/vb/source.vb#4)]  
  
 生成的 XML 类似于以下形式。  
  
```  
<DerivedType>  
    <!-- Zebra is a base data member, and appears first. -->  
    <zebra/>   
  
    <!-- Cat has no Order, appears alphabetically first. -->  
    <cat/>  
  
   <!-- Dog has no Order, appears alphabetically last. -->  
    <dog/>   
  
    <!-- Bird is the member with the smallest Order value -->  
    <bird/>  
  
    <!-- Albatross has the next Order value, alphabetically first. -->  
    <albatross/>  
  
    <!-- Parrot, with the next Order value, alphabetically last. -->  
     <parrot/>  
  
    <!-- Antelope is the member with the highest Order value. Note that   
    Order=2 is skipped -->  
     <antelope/>   
</DerivedType>  
```  
  
## 请参阅  
 <xref:System.Runtime.Serialization.DataContractAttribute>   
 [数据协定等效性](../../../../docs/framework/wcf/feature-details/data-contract-equivalence.md)   
 [使用数据协定](../../../../docs/framework/wcf/feature-details/using-data-contracts.md)