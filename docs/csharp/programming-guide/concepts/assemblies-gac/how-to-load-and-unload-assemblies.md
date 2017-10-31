---
title: "如何：加载和卸载程序集 (C#)"
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
ms.assetid: 6a4f490f-3576-471f-9533-003737cad4a3
caps.latest.revision: 3
author: BillWagner
ms.author: wiwagn
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: 6bf6de24f4cbc3f3bd855b6d2cafa8120ebd90ee
ms.contentlocale: zh-cn
ms.lasthandoff: 07/28/2017

---
# <a name="how-to-load-and-unload-assemblies-c"></a>如何：加载和卸载程序集 (C#)
在生成时自动加载程序所引用的程序集，但也可以在运行时将特定的程序集加载到当前的应用程序域。 有关详细信息，请参阅 [How to: Load Assemblies into an Application Domain](../../../../framework/app-domains/how-to-load-assemblies-into-an-application-domain.md)（如何：将程序集加载到应用程序域中）。  
  
 在没有卸载所有包含单个程序集的应用程序域之前，无法卸载此程序集。 即使程序集不在范围之内，在卸载包含它的所有应用程序域之前，实际的程序集文件都将保持加载状态。  
  
 如果想要卸载某些程序集而不是其他程序集，请考虑创建一个新的应用程序域，在此域中执行代码，然后卸载此应用程序域。 有关详细信息，请参阅 [How to: Unload an Application Domain](../../../../framework/app-domains/how-to-unload-an-application-domain.md)（如何：卸载应用程序域）。  
  
### <a name="to-load-an-assembly-into-an-application-domain"></a>将程序集加载到应用程序域中  
  
1.  使用 <xref:System.AppDomain> 和 <xref:System.Reflection> 类中包含的几种加载方法中的一种。 有关详细信息，请参阅 [How to: Load Assemblies into an Application Domain](../../../../framework/app-domains/how-to-load-assemblies-into-an-application-domain.md)（如何：将程序集加载到应用程序域中）。  
  
### <a name="to-unload-an-application-domain"></a>卸载应用程序域  
  
1.  在没有卸载所有包含单个程序集的应用程序域之前，无法卸载此程序集。 使用 <xref:System.AppDomain> 中的 `Unload` 方法卸载应用程序域。 有关详细信息，请参阅 [How to: Unload an Application Domain](../../../../framework/app-domains/how-to-unload-an-application-domain.md)（如何：卸载应用程序域）。  
  
## <a name="see-also"></a>请参阅  
 [C# 编程指南](../../../../csharp/programming-guide/index.md)   
 [程序集和全局程序集缓存 (C#)](../../../../csharp/programming-guide/concepts/assemblies-gac/index.md)   
 [如何：将程序集加载到应用程序域中](../../../../framework/app-domains/how-to-load-assemblies-into-an-application-domain.md)

