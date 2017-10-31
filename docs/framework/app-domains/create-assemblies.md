---
title: "创建程序集"
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
- assemblies [.NET Framework], multifile
- single-file assemblies
- assemblies [.NET Framework], creating
- multifile assemblies
ms.assetid: 54832ee9-dca8-4c8b-913c-c0b9d265e9a4
caps.latest.revision: 8
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: 583c448bd939cd4d1d16bff372afff4172dcf985
ms.contentlocale: zh-cn
ms.lasthandoff: 07/28/2017

---
# <a name="creating-assemblies"></a>创建程序集
可以使用 [!INCLUDE[vsprvslong](../../../includes/vsprvslong-md.md)] 等 IDE 或 [!INCLUDE[winsdklong](../../../includes/winsdklong-md.md)] 提供的编译器和工具来创建单文件或多文件程序集。 最简单的程序集是具有简单名称并加载到单个应用程序域的单个文件。 此程序集不能被应用程序目录之外的其他程序集引用，并且不执行版本检查。 若要卸载该程序集组成的应用程序，只需删除它所在的目录即可。 对许多开发者来说，拥有这些功能的程序集能够满足他们部署应用程序的所有需要。  
  
 可以从多个代码模块和资源文件创建多文件程序集。 也可以创建可以由多个应用程序共享的程序集。 共享程序集必须具有强名称，并且可以部署在全局程序集缓存中。  
  
 将代码模块和资源分组成程序集时有多个选项，具体取决于以下因素：  
  
-   版本管理  
  
     版本信息应相同的组模块。  
  
-   部署  
  
     支持你的部署模型的组代码模块和资源。  
  
-   重用  
  
     从逻辑上来说可以一起用于实现某个目的的组模块。 例如，不经常用于维护程序的类型和类构成的程序集可以放入同一程序集。 此外，要与多个应用程序共享的类型应归入一个程序集，并且此程序集必须使用强名称进行签名。  
  
-   安全性  
  
     包含需要相同安全权限的的类型的组模块。  
  
-   范围  
  
     所包含类型的可见性限为同一个程序集的组模块。  
  
 公共语言运行时程序集可用于非托管 COM 应用程序时，必须考虑特殊注意事项。 有关使用非托管代码的详细信息，请参阅[向 COM 公开 .NET Framework 组件](../../../docs/framework/interop/exposing-dotnet-components-to-com.md)。  
  
## <a name="see-also"></a>另请参阅  
 [使用程序集编程](../../../docs/framework/app-domains/programming-with-assemblies.md)   
 [程序集版本控制](../../../docs/framework/app-domains/assembly-versioning.md)   
 [如何：生成单文件程序集](../../../docs/framework/app-domains/how-to-build-a-single-file-assembly.md)   
 [如何：生成多文件程序集](../../../docs/framework/app-domains/how-to-build-a-multifile-assembly.md)   
 [运行时如何定位程序集](../../../docs/framework/deployment/how-the-runtime-locates-assemblies.md)   
 [多文件程序集](../../../docs/framework/app-domains/multifile-assemblies.md)

