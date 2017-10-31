---
title: "利用特性扩展元数据"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-standard
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- metadata, extending
- attributes [.NET Framework], metadata
- elements [.NET Framework], attributes
- common language runtime, attributes
- annotating programming elements
- keyword-like descriptive declarations
- runtime, attributes
- extending metadata
ms.assetid: 30386922-1e00-4602-9ebf-526b271a8b87
caps.latest.revision: 12
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: c2c8db8b200e38c87d5b79ba3bf6a870bf6640c7
ms.contentlocale: zh-cn
ms.lasthandoff: 09/05/2017

---
# <a name="extending-metadata-using-attributes"></a>利用特性扩展元数据
公共语言运行时使你能够添加类似于关键字的描述性声明（称为特性），以便批注编程元素（如类型、字段、方法和属性）。 编译运行时的代码时，它将被转换为 Microsoft 中间语言 (MSIL)，并和编译器生成的元数据一起放置在可移植可执行 (PE) 文件内。 特性使你能够将额外的描述性信息放到可使用运行时反射服务提取的元数据中。 当你声明派生自 <xref:System.Attribute?displayProperty=fullName> 的特殊类的实例时，编译器会创建特性。  
  
 .NET Framework 出于多种原因且为解决许多问题而使用特性。 特性描述如何将数据序列化、指定用于强制安全性的特征并限制通过实时 (JIT) 编译器进行优化，从而使代码易于调试。 特性还可记录文件的名称或代码的作者，或控制窗体开发过程中控件和成员的可见性。  
  
## <a name="related-topics"></a>相关主题  
  
|标题|描述|  
|-----------|-----------------|  
|[应用特性](../../../docs/standard/attributes/applying-attributes.md)|描述如何将特性应用于代码的元素。|  
|[编写自定义特性](../../../docs/standard/attributes/writing-custom-attributes.md)|描述如何设计自定义特性类。|  
|[检索存储在特性中的信息](../../../docs/standard/attributes/retrieving-information-stored-in-attributes.md)|描述如何检索加载到执行上下文中的代码的自定义特性。|  
|[元数据和自描述组件](../../../docs/standard/metadata-and-self-describing-components.md)|提供元数据的概述，并说明它是如何在 .NET Framework 可移植可执行 (PE) 文件中实现的。|  
|[如何：将程序集加载到仅反射上下文中](../../../docs/framework/reflection-and-codedom/how-to-load-assemblies-into-the-reflection-only-context.md)|说明如何检索仅反射上下文中的自定义特性信息。|  
  
## <a name="reference"></a>参考  
 <xref:System.Attribute?displayProperty=fullName>

