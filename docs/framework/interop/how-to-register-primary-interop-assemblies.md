---
title: "如何：注册主互操作程序集"
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
- registering primary interop assemblies
- primary interop assemblies, registering
ms.assetid: 4b2fcf8a-429d-43ce-8334-e026040be8bb
caps.latest.revision: 8
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: 81b57a73b8c5118af9cf2867902b849d73820e83
ms.contentlocale: zh-cn
ms.lasthandoff: 08/21/2017

---
# <a name="how-to-register-primary-interop-assemblies"></a>如何：注册主互操作程序集
类仅能由 COM 互操作封送，并总是作为接口封送。 在某些情况下用来将该类封送的接口称为类接口。 有关使用选择的接口重写类接口的信息，请参阅 [COM可调用包装器](../../../docs/framework/interop/com-callable-wrapper.md)。  
  
 尽管任何想要从 .NET Framework 应用程序使用 COM 类型的开发人员都可以生成互操作程序集，但这样做会产生一个问题。 每次一名开发人员导入 COM 类型库并对其进行签名时，该开发人员就创建了一组与另一个开发人员所导入和签名的类型不兼容的唯一类型。 此类型不兼容性问题的解决方案是每个开发人员都获取供应商提供并签名的主互操作程序集。  
  
 如果你打算向其他应用程序公开第三方 COM 类型，请始终使用与定义的类型库相同的发布者所提供的主互操作程序集。 除了提供有保证的类型兼容性，主互操作程序集通常由供应商自定义以增强互操作性。  
  
 即使你不打算公开第三方 COM 类型，使用主互操作程序集也可以使与 COM 组件进行互操作的任务变得更简单。 但是，此策略不会提供对供应商可能对主互操作程序集中定义的类型所进行的更改的隔离。 当你的应用程序需要此类隔离时，请生成自己的互操作程序集，而不是使用主互操作程序集。  
  
 必须在开发计算机上注册所有需要的主互操作程序集，然后才能通过 [!INCLUDE[vsprvsext](../../../includes/vsprvsext-md.md)] 引用它们。 Visual Studio 在你第一次从 COM 类型库引用类型时会查找并使用主互操作程序集。 如果 Visual Studio 找不到与该类型库关联的主互操作程序集，它会提示你获取它，或提出创建一个互操作程序集。 同样，[类型库导入程序 (Tlbimp.exe)](../../../docs/framework/tools/tlbimp-exe-type-library-importer.md) 也使用注册表来定位主互操作程序集。  
  
 尽管没有必要注册主互操作程序集（除非你打算使用 Visual Studio），但注册可提供两大好处：  
  
-   在原始类型库的注册表项下清楚地标记已注册的主互操作程序集。 注册是在你的计算机上定位主互操作程序集的最佳方式。  
  
-   如果在将来某个时间你使用 Visual Studio 引用具有未注册的主互操作程序集的类型，可以避免意外地生成和使用新的互操作程序集。  
  
 使用[程序集注册工具 (Regasm.exe)](../../../docs/framework/tools/regasm-exe-assembly-registration-tool.md) 注册主互操作程序集。  
  
### <a name="to-register-a-primary-interop-assembly"></a>注册主互操作程序集  
  
1.  在命令提示符处，键入：  
  
     regasm assemblyname  
  
     在此命令中，assemblyname 是已注册的程序集的文件名。 Regasm.exe 会在与原始类型库相同的注册表项下为主互操作程序集添加一个条目。  
  
## <a name="example"></a>示例  
 下列示例注册 `CompanyA.UtilLib.dll` 主互操作程序集。  
  
```  
regasm CompanyA.UtilLib.dll  
```  
  
## <a name="see-also"></a>另请参阅  
 [用主互操作程序集编程](http://msdn.microsoft.com/en-us/306fa1d6-0703-4004-9e93-d0a57f1be81e)   
 [定位主互操作程序集](http://msdn.microsoft.com/en-us/d6768e4b-cd80-414d-a4f8-05d979eb393b)   
 [重新分发主互操作程序集](http://msdn.microsoft.com/en-us/e76384f0-d631-474c-bdbd-13884cba0265)

