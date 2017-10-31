---
title: "将 COM 的程序集打包"
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
- exposing .NET Framework components to COM
- COM interop, packaging assemblies
- packaging assemblies for COM
- Tlbexp.exe
- TypeLibConverter class
- .NET Services Installation tool
- Assembly Registration tool
- Type Library Exporter
- Reqsvcs.exe
- interoperation with unmanaged code, exposing .NET Framework components
- interoperation with unmanaged code, packaging assemblies
- COM interop, exposing COM components
- Reqasm.exe
ms.assetid: 39dc55aa-f2a1-4093-87bb-f1c0edb6e761
caps.latest.revision: 10
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: 73866ddc1e8199dfad188179dc668bc31ab3c93d
ms.contentlocale: zh-cn
ms.lasthandoff: 08/21/2017

---
# <a name="packaging-an-assembly-for-com"></a>将 COM 的程序集打包
COM 开发人员可从其计划纳入应用程序的托管类型相关信息中受益：  
  
-   COM 应用程序可使用的类型列表  
  
     某些托管类型对 COM 不可见；某些可见但不可创建；某些既可见又可创建。 程序集可以包括不可见、可见、不可创建和可创建类型的任何组合。 为实现完整性，请确定打算公开到 COM 的程序集中的类型，尤其是当这些类型是公开到 .NET framework 中类型的子集时。  
  
     有关其他信息，请参阅[为互操作限定 .NET 类型](../../../docs/framework/interop/qualifying-net-types-for-interoperation.md)。  
  
-   版本控制说明  
  
     实现类接口（COM 互操作生成的接口）的托管类受版本控制限制。  
  
     有关如何使用类接口的指南，请参阅[类接口简介](http://msdn.microsoft.com/en-us/733c0dd2-12e5-46e6-8de1-39d5b25df024)。  
  
-   部署说明  
  
     发布者签名的具有强名称的程序集可安装到全局程序集缓存。 未签名程序集必须作为专用程序集安装在用户计算机上。  
  
     有关其他信息，请参阅[程序集安全注意事项](../../../docs/framework/app-domains/assembly-security-considerations.md)。  
  
-   类型库所含内容  
  
     大多数类型在由 COM 应用程序使用时都需要类型库。 可生成类型库或使 COM 开发人员执行此任务。 [!INCLUDE[winsdklong](../../../includes/winsdklong-md.md)] 为生成类型库提供以下选项：  
  
    -   [类型库导出程序](#cpconpackagingassemblyforcomanchor1)  
  
    -   [TypeLibConverter 类](#cpconpackagingassemblyforcomanchor2)  
  
    -   [程序集注册工具](#cpconpackagingassemblyforcomanchor3)  
  
    -   [.NET 服务安装工具](#cpconpackagingassemblyforcomanchor4)  
  
     无论选择的机制如何，生成的类型库中仅包含所提供程序集中定义的公共类型。  
  
     可将类型库打包为单独文件，或将其作为 Win32 资源文件嵌入基于 .NET 的应用程序。 Microsoft Visual Basic 6.0 自动执行此任务；但若 [!INCLUDE[vbprvbext](../../../includes/vbprvbext-md.md)]，必须手动嵌入类型库。 有关说明，请参阅[如何：将类型库作为 Win32 资源嵌入基于 .NET 的应用程序](http://msdn.microsoft.com/en-us/c97b4b8c-2ab7-4ac7-8fc8-0ba5c5d59c44)。  
  
<a name="cpconpackagingassemblyforcomanchor1"></a>   
## <a name="type-library-exporter"></a>类型库导出程序  
 [类型库导出程序 (Tlbexp.exe)](../../../docs/framework/tools/tlbexp-exe-type-library-exporter.md) 是命令行工具，可将程序集中包含的类和接口转换为 COM 类型库。 一旦类的类型信息可用，COM 客户端就可创建 .NET 类的实例，并调用实例的方法，就像它是 COM 对象一样。 Tlbexp.exe 一次转换整个程序集。 不能使用 Tlbexp.exe 生成程序集中定义的类型子集的类型信息。  
  
<a name="cpconpackagingassemblyforcomanchor2"></a>   
## <a name="typelibconverter-class"></a>TypeLibConverter 类  
 位于 System.Runtime.Interop 命名空间中的 <xref:System.Runtime.InteropServices.TypeLibConverter> 类将程序集中包含的类和接口转换为 COM 类型库。 此 API 生成与类型库导出程序相同的类型信息，如上节所述。  
  
 TypeLibConverter 类实现 <xref:System.Runtime.InteropServices.ITypeLibConverter>。  
  
<a name="cpconpackagingassemblyforcomanchor3"></a>   
## <a name="assembly-registration-tool"></a>程序集注册工具  
 [程序集注册工具 (Regasm.exe)](../../../docs/framework/tools/regasm-exe-assembly-registration-tool.md) 可在应用 /tlb: 选项时生成并注册类型库。 COM 客户端要求在 Windows 注册表中安装类型库。 如果不使用此选项，Regasm.exe 仅在程序集而非类型库中注册类型。 在程序集中注册类型和注册类型库是不同的活动。  
  
<a name="cpconpackagingassemblyforcomanchor4"></a>   
## <a name="net-services-installation-tool"></a>.NET 服务安装工具  
 [.NET 服务安装工具 (Regsvcs.exe)](../../../docs/framework/tools/regsvcs-exe-net-services-installation-tool.md) 将托管类添加到 Windows 2000 组件服务，并在单个工具中组合多个任务。 除加载和注册程序集外，Regsvcs.exe 还可将类型库生成、注册和安装到现有 COM+ 1.0 应用程序。  
  
## <a name="see-also"></a>另请参阅  
 <xref:System.Runtime.InteropServices.TypeLibConverter>   
 <xref:System.Runtime.InteropServices.ITypeLibConverter>   
 [向 COM 公开 .NET Framework 组件](../../../docs/framework/interop/exposing-dotnet-components-to-com.md)   
 [为互操作限定 .NET 类型](../../../docs/framework/interop/qualifying-net-types-for-interoperation.md)   
 [类接口简介](http://msdn.microsoft.com/en-us/733c0dd2-12e5-46e6-8de1-39d5b25df024)   
 [程序集安全注意事项](../../../docs/framework/app-domains/assembly-security-considerations.md)   
 [Tlbexp.exe（类型库导出程序）](../../../docs/framework/tools/tlbexp-exe-type-library-exporter.md)   
 [向 COM 注册程序集](../../../docs/framework/interop/registering-assemblies-with-com.md)   
 [如何：将类型库作为 Win32 资源嵌入应用程序](http://msdn.microsoft.com/en-us/c97b4b8c-2ab7-4ac7-8fc8-0ba5c5d59c44)

