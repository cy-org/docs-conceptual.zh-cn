---
title: "类型等效性和嵌入的互操作类型"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology:
- dotnet-clr
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- type equivalence
- embedded interop types
- primary interop assemblies,not necessary in CLR version 4
- NoPIA
ms.assetid: 78892eba-2a58-4165-b4b1-0250ee2f41dc
caps.latest.revision: 17
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: e9a7b39047edcd8e2c770e17a33dd73e75ee5083
ms.contentlocale: zh-cn
ms.lasthandoff: 08/21/2017

---
# <a name="type-equivalence-and-embedded-interop-types"></a>类型等效性和嵌入的互操作类型
从 [!INCLUDE[net_v40_long](../../../includes/net-v40-long-md.md)] 开始，公共语言运行时支持将 COM 类型的类型信息直接嵌入到托管程序集中，而不要求托管程序集从 Interop 程序集中获取 COM 类型的类型信息。 由于嵌入式类型信息仅包含托管程序集实际使用的类型和成员，因此两个托管程序集可能具有相同 COM 类型的不同视图。 每个托管程序集都有不同的 <xref:System.Type> 对象来表示其 COM 类型视图。 公共语言运行时支持接口、结构、枚举和委托等不同视图之间的类型等效性。  
  
 类型等效性意味着从一个托管程序集传递到另一个托管程序集的 COM 对象可以转换为接收程序集中适当的托管类型。  
  
> [!NOTE]
>  类型等效性和嵌入式互操作类型简化了使用 COM 组件的应用程序和加载项的部署，因为无需与应用程序一起部署互操作程序集。 如果共享 COM 组件的开发人员希望较早版本的 .NET Framework 使用其组件，他们仍须创建主互操作程序集 (PIA)。  
  
## <a name="type-equivalence"></a>类型等效性  
 COM 类型的等效性支持接口、结构、枚举和委托。 如果满足以下所有条件，则 COM 类型符合等效条件：  
  
-   类型是两个接口、两个结构、两个枚举或两个委托。  
  
-   类型具有相同标识，如下节所述。  
  
-   两种类型都符合类型等效性，如[针对类型等效性标记 COM 类型](#type_equiv)部分所述。  
  
### <a name="type-identity"></a>类型标识  
 范围和标识匹配时，确定两种类型具有相同标识，换句话说，如果它们各自具有 <xref:System.Runtime.InteropServices.TypeIdentifierAttribute> 属性，并且两个属性都具有匹配的 <xref:System.Runtime.InteropServices.TypeIdentifierAttribute.Scope%2A> 和 <xref:System.Runtime.InteropServices.TypeIdentifierAttribute.Identifier%2A> 属性。 <xref:System.Runtime.InteropServices.TypeIdentifierAttribute.Scope%2A> 的比较不区分大小写。  
  
 如果一个类型不具有 <xref:System.Runtime.InteropServices.TypeIdentifierAttribute> 属性，或者如果它有一个不指定范围和标识符的 <xref:System.Runtime.InteropServices.TypeIdentifierAttribute> 属性，仍可将该类型视为等效性，如下所示：  
  
-   对于接口，使用 <xref:System.Runtime.InteropServices.GuidAttribute> 的值而不使用 <xref:System.Runtime.InteropServices.TypeIdentifierAttribute.Scope%2A?displayProperty=fullName> 属性，使用 <xref:System.Type.FullName%2A?displayProperty=fullName> 属性（即类型名称，包括命名空间），而不使用 <xref:System.Runtime.InteropServices.TypeIdentifierAttribute.Identifier%2A?displayProperty=fullName> 属性。  
  
-   对于结构、枚举和委托，使用包含程序集的 <xref:System.Runtime.InteropServices.GuidAttribute> 而不使用 <xref:System.Runtime.InteropServices.TypeIdentifierAttribute.Scope%2A> 属性，使用 <xref:System.Type.FullName%2A?displayProperty=fullName> 属性而不使用 <xref:System.Runtime.InteropServices.TypeIdentifierAttribute.Identifier%2A> 属性。  
  
<a name="type_equiv"></a>   
### <a name="marking-com-types-for-type-equivalence"></a>针对类型等效性标记 COM 类型  
 可通过两种方式将类型标记为符合类型等效性：  
  
-   将 <xref:System.Runtime.InteropServices.TypeIdentifierAttribute> 属性应用于该类型。  
  
-   将该类型设为 COM 导入类型。 若接口有 <xref:System.Runtime.InteropServices.ComImportAttribute> 属性，则它是 COM 导入类型。 如果定义了其程序集具有 <xref:System.Runtime.InteropServices.ImportedFromTypeLibAttribute> 属性，则接口、结构、枚举或委托是 COM 导入类型。  
  
## <a name="see-also"></a>另请参阅  
 <xref:System.Type.IsEquivalentTo%2A>   
 [在托管代码中使用 COM 类型](http://msdn.microsoft.com/en-us/1a95a8ca-c8b8-4464-90b0-5ee1a1135b66)   
 [将类型库作为程序集导入](../../../docs/framework/interop/importing-a-type-library-as-an-assembly.md)

