---
title: "如何：卸载应用程序域"
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
- Unload method
- application domains, unloading
- unloading application domains
ms.assetid: f356116d-e415-4f7c-a332-6e6a60227192
caps.latest.revision: 10
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: eefaf670202e6b4977d75fffa906f1b07053eb3e
ms.contentlocale: zh-cn
ms.lasthandoff: 07/28/2017

---
# <a name="how-to-unload-an-application-domain"></a>如何：卸载应用程序域
完成使用应用程序域时，可使用 <xref:System.AppDomain.Unload%2A?displayProperty=fullName> 方法将其卸载。 **Unload** 方法会正常关闭指定的应用程序域。 卸载过程中，任何新线程都无法访问该应用程序域，并且会释放所有特性于应用程序域的数据结构。  
  
 加载到应用程序域中的所有程序集都会被移除，无法再使用。 如果应用程序域中的程序集不特定于域，则程序集的数据会保留在内存中，直到整个进程关闭。 除了关闭整个进程，没有机制可以卸载非特定于域的程序集。 在某些情况下，卸载应用程序域的请求会不起作用，并导致 <xref:System.CannotUnloadAppDomainException>。  
  
 以下示例新建名为 `MyDomain` 的应用程序域，并将一些信息输出至控制台，然后卸载应用程序域。 请注意，代码随后会尝试将卸载的应用程序域的友好名称输出至控制台。 此操作生成一个异常，该异常由程序结尾处的 try/catch 语句处理。  
  
## <a name="example"></a>示例  
 [!code-cpp[System.AppDomain.Load#3](../../../samples/snippets/cpp/VS_Snippets_CLR_System/system.appdomain.load/cpp/source3.cpp#3)][!code-csharp[System.AppDomain.Load#3](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.appdomain.load/cs/source3.cs#3)][!code-vb[System.AppDomain.Load#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.appdomain.load/vb/source3.vb#3)]  
  
## <a name="see-also"></a>另请参阅  
 [对应用程序域进行编程](http://msdn.microsoft.com/en-us/bd36055b-56bd-43eb-b4d8-820c37172131)   
 [如何：创建应用程序域](../../../docs/framework/app-domains/how-to-create-an-application-domain.md)   
 [使用应用程序域](../../../docs/framework/app-domains/use.md)

