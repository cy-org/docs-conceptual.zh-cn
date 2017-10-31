---
title: "如何：确定程序集的完全限定的名称"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology:
- dotnet-bcl
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- names [.NET Framework], fully qualified type names
- names [.NET Framework], assemblies
- assemblies [.NET Framework], names
ms.assetid: 009dae23-e1f6-4a64-9a9a-32e4c34802b0
caps.latest.revision: 13
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: 673c836ea761c24e2627e97ab3bcb5dd3c35d141
ms.contentlocale: zh-cn
ms.lasthandoff: 07/28/2017

---
# <a name="how-to-determine-an-assembly39s-fully-qualified-name"></a>如何：确定程序集的完全限定的名称
若要在全局程序集缓存中查找一个程序集的完全限定名，请使用全局程序集缓存工具 ([Gacutil.exe](../../../docs/framework/tools/gacutil-exe-gac-tool.md))。 请参阅[如何：查看全局程序集缓存的内容](../../../docs/framework/app-domains/how-to-view-the-contents-of-the-gac.md)。  
  
 对于不在全局程序集缓存中的程序集，可以通过多种方式获取完全限定的程序集名称：可使用代码将信息输出到控制台或变量，也可使用 [Ildasm.exe（IL 反汇编程序）](../../../docs/framework/tools/ildasm-exe-il-disassembler.md)检查包含完全限定名的程序集元数据。  
  
-   如果应用程序已加载程序集，则可检索 <xref:System.Reflection.Assembly.FullName%2A?displayProperty=fullName> 属性的值在以获取完全限定名。 无论 GAC 是否包含程序集，均可使用此方法。 说明如示例所示。  
  
-   如果知道程序集的文件系统路径，则可调用静态（Visual Basic 中的 `Shared`）<xref:System.Reflection.AssemblyName.GetAssemblyName%2A?displayProperty=fullName> 方法获取完全限定的程序集名称。 下面是一个简单的示例。  
  
     [!code-csharp[System.Reflection.AssemblyName.GetAssemblyName#1](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.reflection.assemblyname.getassemblyname/cs/getassemblyname1.cs#1)]  [!code-vb[System.Reflection.AssemblyName.GetAssemblyName#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.reflection.assemblyname.getassemblyname/vb/getassemblyname1.vb#1)]  
  
-   可使用 [Ildasm.exe（IL 反汇编程序）](../../../docs/framework/tools/ildasm-exe-il-disassembler.md)检查包含完全限定名的程序集元数据。  
  
 有关设置程序集特性（如版本、区域性和程序集名称）的详细信息，请参阅[设置程序集特性](../../../docs/framework/app-domains/set-assembly-attributes.md)。 有关为程序集提供强名称的详细信息，请参阅[创建并使用强名称程序集](../../../docs/framework/app-domains/create-and-use-strong-named-assemblies.md)。  
  
## <a name="example"></a>示例  
 以下代码示例显示了如何向控制台显示包含指定类的程序集的完全限定名。 因为它检索应用程序已加载的程序集的名称，所以程序集是否位于 GAC 中并不重要。  
  
 [!code-cpp[Assembly.Fullname#2](../../../samples/snippets/cpp/VS_Snippets_CLR/Assembly.FullName/CPP/example2.cpp#2)] [!code-csharp[Assembly.Fullname#2](../../../samples/snippets/csharp/VS_Snippets_CLR/Assembly.FullName/CS/example2.cs#2)] [!code-vb[Assembly.Fullname#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Assembly.FullName/VB/example2.vb#2)]  
  
## <a name="see-also"></a>另请参阅  
 [程序集名称](../../../docs/framework/app-domains/assembly-names.md)   
 [创建程序集](../../../docs/framework/app-domains/create-assemblies.md)   
 [创建和使用具有强名称的程序集](../../../docs/framework/app-domains/create-and-use-strong-named-assemblies.md)   
 [全局程序集缓存](../../../docs/framework/app-domains/gac.md)   
 [运行时如何定位程序集](../../../docs/framework/deployment/how-the-runtime-locates-assemblies.md)   
 [使用程序集编程](../../../docs/framework/app-domains/programming-with-assemblies.md)

