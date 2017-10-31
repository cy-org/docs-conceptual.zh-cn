---
title: "数组 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-standard"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - "类库设计准则 [.NET Framework] 数组"
  - "数组 [.NET Framework] 使用准则"
  - "空数组"
ms.assetid: 66a1b3d8-6f3f-4715-b235-e1ff95e32d8e
caps.latest.revision: 18
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 18
---
# 数组
**✓ 执行** 更喜欢使用通过公共 Api 中的数组的集合。[集合](../../../docs/standard/design-guidelines/guidelines-for-collections.md) 部分提供有关如何选择集合和数组之间的详细信息。  
  
 **X 不** 使用只读数组字段。 该字段本身是只读的且无法更改，但可以更改数组中的元素。  
  
 **✓ 请考虑** 使用交错的数组而不多维数组。  
  
 交错的数组是包含也存在数组元素的数组。 构成元素的数组可以是不同的大小，以与多维数组相比某些集的数据 （例如，稀疏矩阵） 的不太浪费空间。 此外，CLR 优化交错数组的索引操作，因此它们可能会表现出更好的运行时性能在某些情况下。  
  
 *部分 © 2005年、 2009 Microsoft Corporation。 保留所有权利。*  
  
 *转载已获得的权限从 Pearson Education，Inc. [Framework 设计准则︰ 约定、 惯例和可重用的.NET 库，第二版模式](http://www.informit.com/store/framework-design-guidelines-conventions-idioms-and-9780321545619) 通过 Krzysztof Cwalina 和 Brad Abrams，作为 Microsoft Windows 开发系列的一部分发布 2008 年 10 月 22 日由 Addison\-wesley Professional。*  
  
## 请参阅  
 <xref:System.Array>   
 [Framework 设计准则](../../../docs/standard/design-guidelines/index.md)   
 [使用准则](../../../docs/standard/design-guidelines/usage-guidelines.md)