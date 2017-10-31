---
title: "如何：将程序集加载到应用程序域中"
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
- application domains, loading assemblies
- loading assemblies
ms.assetid: 1432aa2d-bd83-4346-bf3b-a1b7920e2aa9
caps.latest.revision: 16
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.translationtype: HT
ms.sourcegitcommit: 75642ff3beb4462faa9068db76c89f3cb5f75ab8
ms.openlocfilehash: c319da0f8e6f3cdfb83e659a778136d668699834
ms.contentlocale: zh-cn
ms.lasthandoff: 08/10/2017

---
# <a name="how-to-load-assemblies-into-an-application-domain"></a>如何：将程序集加载到应用程序域中
可通过多种方法将程序集加载到应用程序域中。 推荐方法是使用 <xref:System.Reflection.Assembly?displayProperty=fullName> 类的 `static`（在 Visual Basic 中为 `Shared`）<xref:System.Reflection.Assembly.Load%2A> 方法。 加载程序集的其他方法包括：  
  
-   <xref:System.Reflection.Assembly> 类的 <xref:System.Reflection.Assembly.LoadFrom%2A> 方法加载已给定其文件位置的程序集。 通过此方法加载程序集将使用不同的加载上下文。  
  
-   <xref:System.Reflection.Assembly.ReflectionOnlyLoad%2A> 和 <xref:System.Reflection.Assembly.ReflectionOnlyLoadFrom%2A> 方法将程序集加载到仅反射上下文中。 可检查但不可执行加载到该上下文中的程序集，允许检查以其他平台为目标的程序集。 请参阅[如何：将程序集加载到仅反射上下文中](../../../docs/framework/reflection-and-codedom/how-to-load-assemblies-into-the-reflection-only-context.md)。  
  
> [!NOTE]
>  仅反射上下文是 .NET Framework 2.0 版中的新增功能。  
  
-   <xref:System.AppDomain> 类的 <xref:System.AppDomain.CreateInstance%2A> 和 <xref:System.AppDomain.CreateInstanceAndUnwrap%2A> 等方法可将程序集加载到应用程序域中。  
  
-   <xref:System.Type> 类的 <xref:System.Type.GetType%2A> 方法可加载程序集。  
  
-   <xref:System.AppDomain?displayProperty=fullName> 类的 <xref:System.AppDomain.Load%2A> 方法可加载程序集，但主要用于实现 COM 互操作性。 不应使用该方法将程序集加载到除从其中调用该方法的应用程序域以外的其他应用程序域。  
  
> [!NOTE]
>  从 .NET Framework 2.0 版开始，对于使用版本号高于当前已加载运行时的 .NET Framework 版本所编译的程序集，运行时将不再加载此类程序集。 这同样适用于主版本号和次版本号的组合。  
  
 可指定在应用程序域间共享已加载程序集的实时 (JIT) 编译代码的方式。 有关详细信息，请参阅[应用程序域和程序集](http://msdn.microsoft.com/en-us/433b04ae-4ba8-4849-9dbd-79194f240346)。  
  
## <a name="example"></a>示例  
 以下代码将名为“example.exe”或“example.dll”的程序集加载到当前应用程序域中，从该程序集获取名为 `Example` 的类型，为该类型获取名为 `MethodA` 的参数方法，然后执行该方法。 有关从已加载程序集中获取信息的完整讨论，请参阅[动态加载和使用类型](../../../docs/framework/reflection-and-codedom/dynamically-loading-and-using-types.md)。  
  
 [!code-cpp[System.AppDomain.Load#2](../../../samples/snippets/cpp/VS_Snippets_CLR_System/system.appdomain.load/cpp/source2.cpp#2)] [!code-csharp[System.AppDomain.Load#2](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.appdomain.load/cs/source2.cs#2)] [!code-vb[System.AppDomain.Load#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.appdomain.load/vb/source2.vb#2)]  
  
## <a name="see-also"></a>另请参阅  
 <xref:System.Reflection.Assembly.ReflectionOnlyLoad%2A>   
 [对应用程序域进行编程](http://msdn.microsoft.com/en-us/bd36055b-56bd-43eb-b4d8-820c37172131)   
 [反射](../../../docs/framework/reflection-and-codedom/reflection.md)   
 [使用应用程序域](../../../docs/framework/app-domains/use.md)   
 [如何：将程序集加载到仅反射上下文中](../../../docs/framework/reflection-and-codedom/how-to-load-assemblies-into-the-reflection-only-context.md)   
 [应用程序域和程序集](http://msdn.microsoft.com/en-us/433b04ae-4ba8-4849-9dbd-79194f240346)

