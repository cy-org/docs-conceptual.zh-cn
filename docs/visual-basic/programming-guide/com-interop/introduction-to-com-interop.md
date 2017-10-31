---
title: "COM 互操作 (Visual Basic 中) 的简介 |Microsoft 文档"
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
dev_langs:
- VB
helpviewer_keywords:
- interop assemblies
- COM interop, about COM interop
ms.assetid: 8bd62e68-383d-407f-998b-29aa0ce0fd67
caps.latest.revision: 12
author: dotnet-bot
ms.author: dotnetcontent
translation.priority.ht:
- cs-cz
- de-de
- es-es
- fr-fr
- it-it
- ja-jp
- ko-kr
- pl-pl
- pt-br
- ru-ru
- tr-tr
- zh-cn
- zh-tw
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 8866dbadca040c57ed2b59540dd2c341eb81758c
ms.lasthandoff: 03/13/2017

---
# <a name="introduction-to-com-interop-visual-basic"></a>COM 互操作介绍 (Visual Basic)
组件对象模型 (COM)，可以对其他组件和主机应用程序公开其功能的对象。 虽然 COM 对象已被 Windows 多年编程的基础，面向公共语言运行时 (CLR) 的应用程序提供了许多优点。  
  
 [!INCLUDE[dnprdnshort](../../../csharp/getting-started/includes/dnprdnshort_md.md)]应用程序将最终取代那些 com 开发 到那时，你可能需要使用或创建 COM 对象使用[!INCLUDE[vsprvs](../../../csharp/includes/vsprvs_md.md)]。 通过 COM 互操作性或*COM 互操作*，使您能够使用现有的 COM 对象时转换到[!INCLUDE[dnprdnshort](../../../csharp/getting-started/includes/dnprdnshort_md.md)]按您自己的节奏。  
  
 通过使用[!INCLUDE[dnprdnshort](../../../csharp/getting-started/includes/dnprdnshort_md.md)]若要创建 COM 组件，可以使用免注册 COM 互操作。 这样就可以控制哪些 DLL 版本启用多个版本已安装的计算机上，并且可让最终用户使用 XCOPY 或 FTP 将复制到其计算机上的相应目录的应用程序可以运行时。 有关详细信息，请参阅[免注册 COM 互操作](http://msdn.microsoft.com/library/90f308b9-82dc-414a-bce1-77e0155e56bd)。  
  
## <a name="managed-code-and-data"></a>托管的代码和数据  
 有关开发的代码[!INCLUDE[dnprdnshort](../../../csharp/getting-started/includes/dnprdnshort_md.md)]称为*托管代码*，并包含由 CLR 使用元数据。 所使用的数据[!INCLUDE[dnprdnshort](../../../csharp/getting-started/includes/dnprdnshort_md.md)]应用程序称为*托管数据*因为运行时管理与数据相关的任务，比如分配和回收内存以及执行类型检查。 默认情况下，[!INCLUDE[vbprvblong](../../../visual-basic/developing-apps/customizing-extending-my/includes/vbprvblong_md.md)]使用托管代码和数据，但是您可以访问的非托管的代码和数据的 COM 对象使用互操作程序集 （请参阅本页后面的说明）。  
  
## <a name="assemblies"></a>程序集  
 程序集是主要构建基块的[!INCLUDE[dnprdnshort](../../../csharp/getting-started/includes/dnprdnshort_md.md)]应用程序。 它是功能的一个已生成、 版本控制，并作为单个实现单元包含一个或多个文件已部署的集合。 每个程序集包含程序集清单。  
  
## <a name="type-libraries-and-assembly-manifests"></a>类型库和程序集清单  
 类型库描述 COM 对象，如成员名称和数据类型的特征。 程序集清单执行的相同函数[!INCLUDE[dnprdnshort](../../../csharp/getting-started/includes/dnprdnshort_md.md)]应用程序。 它们包括以下信息︰  
  
-   程序集标识、 版本、 区域性和数字签名。  
  
-   组成程序集实现的文件。  
  
-   类型和构成该程序集的资源。 这包括那些从其导出。  
  
-   对其他程序集的编译时依赖项。  
  
-   要正确运行所必需的程序集所需的权限。  
  
 有关程序集和程序集清单的详细信息，请参阅[程序集和全局程序集缓存](../../../visual-basic/programming-guide/concepts/assemblies-gac/index.md)。  
  
### <a name="importing-and-exporting-type-libraries"></a>导入和导出类型库  
 [!INCLUDE[vsprvs](../../../csharp/includes/vsprvs_md.md)]包含一个实用工具，Tlbimp，它允许您将信息导入从类型库到[!INCLUDE[dnprdnshort](../../../csharp/getting-started/includes/dnprdnshort_md.md)]应用程序。 通过使用 Tlbexp 实用程序，可以从程序集生成类型库。  
  
 Tlbimp 和 Tlbexp 有关的信息，请参阅[Tlbimp.exe （类型库导入程序）](http://msdn.microsoft.com/library/ec0a8d63-11b3-4acd-b398-da1e37e97382)和[Tlbexp.exe （类型库导出程序）](http://msdn.microsoft.com/library/a487d61b-d166-467b-a7ca-d8b52fbff42d)。  
  
## <a name="interop-assemblies"></a>互操作程序集  
 互操作程序集是[!INCLUDE[dnprdnshort](../../../csharp/getting-started/includes/dnprdnshort_md.md)]代码的桥之间托管和非托管的程序集，将 COM 对象成员映射到等效[!INCLUDE[dnprdnshort](../../../csharp/getting-started/includes/dnprdnshort_md.md)]托管成员。 互操作程序集由创建[!INCLUDE[vbprvblong](../../../visual-basic/developing-apps/customizing-extending-my/includes/vbprvblong_md.md)]处理很多使用 COM 对象，如互操作封送处理的详细信息。  
  
## <a name="interoperability-marshaling"></a>互操作封送处理  
 所有[!INCLUDE[dnprdnshort](../../../csharp/getting-started/includes/dnprdnshort_md.md)]应用程序共享一组实现的对象，而不考虑使用的编程语言的互操作性的公共类型。 参数和返回值的 COM 对象有时使用不同于在托管代码中使用的数据类型。 *互操作封送处理*为它们移动到和从 COM 对象包装参数和返回值为等效的数据类型的过程。 有关详细信息，请参阅[互操作封送处理](http://msdn.microsoft.com/library/115f7a2f-d422-4605-ab36-13a8dd28142a)。  
  
## <a name="see-also"></a>另请参阅  
 [COM 互操作](../../../visual-basic/programming-guide/com-interop/index.md)   
 [演练︰ 用 COM 对象实现继承](../../../visual-basic/programming-guide/com-interop/walkthrough-implementing-inheritance-with-com-objects.md)   
 [与非托管代码交互操作](https://msdn.microsoft.com/library/sd10k43k)   
 [互操作性疑难解答](../../../visual-basic/programming-guide/com-interop/troubleshooting-interoperability.md)   
 [程序集和全局程序集缓存](../../../visual-basic/programming-guide/concepts/assemblies-gac/index.md)   
 [Tlbimp.exe （类型库导入程序）](http://msdn.microsoft.com/library/ec0a8d63-11b3-4acd-b398-da1e37e97382)   
 [Tlbexp.exe （类型库导出程序）](http://msdn.microsoft.com/library/a487d61b-d166-467b-a7ca-d8b52fbff42d)   
 [互操作封送处理](http://msdn.microsoft.com/library/115f7a2f-d422-4605-ab36-13a8dd28142a)   
 [免注册 COM 互操作](http://msdn.microsoft.com/library/90f308b9-82dc-414a-bce1-77e0155e56bd)
