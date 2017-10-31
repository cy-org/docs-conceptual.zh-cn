---
title: "与非托管代码交互操作"
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
- unmanaged code, interoperation
- managed code, interoperation with unmanaged code
- .NET Framework, interoperation with unmanaged code
- unmanaged code
- interoperation with unmanaged code
- interoperation with unmanaged code, about interoperation
- components [.NET Framework], interoperation with unmanaged code
ms.assetid: ccb68ce7-b0e9-4ffb-839d-03b1cd2c1258
caps.latest.revision: 15
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: ff86b062efddde6f97555efb97247f60a6e1db98
ms.contentlocale: zh-cn
ms.lasthandoff: 09/07/2017

---
# <a name="interoperating-with-unmanaged-code"></a>与非托管代码交互操作
.NET Framework 提升与 COM 组件、COM+ 服务、外部类型库和许多操作系统服务的交互。 托管和非托管对象模型之间的数据类型、方法签名和错误处理机制有所不同。 要简化 .NET Framework 组件和非托管代码之间的互操作并简化迁移路径，公共语言运行时需对客户端和服务器隐藏这些对象模型中的差异。  
  
 在运行时控制下执行的代码称为托管代码。 反之，在运行时以外运行的代码称为非托管代码。 COM 组件、ActiveX 接口和 Win32 API 函数都是非托管代码的示例。  
  
## <a name="in-this-section"></a>本节内容  
 [与非托管代码交互操作帮助主题](http://msdn.microsoft.com/en-us/ec21c6e1-e233-4cd9-95ae-b9b9cf807f9d)  
 提供了与非托管代码交互操作相关的概念性文档中的所有帮助主题的链接。  
  
 [向 .NET Framework 公开 COM 组件](../../../docs/framework/interop/exposing-com-components.md)  
 描述如何使用 .NET Framework 应用程序的 COM 组件。  
  
 [向 COM 公开 .NET Framework 组件](../../../docs/framework/interop/exposing-dotnet-components-to-com.md)  
 描述如何使用 COM 应用程序的 .NET Framework 组件。  
  
 [使用非托管 DLL 函数](../../../docs/framework/interop/consuming-unmanaged-dll-functions.md)  
 描述如何使用平台调用调用非托管 DLL 函数。  
  
 [互操作的设计注意事项](http://msdn.microsoft.com/en-us/b59637f6-fe35-40d6-ae72-901e7a707689)  
 提供有关编写集成 COM 组件的提示。  
  
 [互操作封送处理](../../../docs/framework/interop/interop-marshaling.md)  
 描述 COM 互操作和平台调用的封送处理。  
  
 [如何：映射 HRESULT 和异常](../../../docs/framework/interop/how-to-map-hresults-and-exceptions.md)  
 描述异常和 HRESULT 之间的映射。  
  
 [使用泛型类型进行交互操作](http://msdn.microsoft.com/en-us/26b88e03-085b-4b53-94ba-a5a9c709ce58)  
 描述用于 COM 互操作时的泛型类型行为。  
  
## <a name="related-sections"></a>相关章节  
 [高级 COM 互操作性](http://msdn.microsoft.com/en-us/3ada36e5-2390-4d70-b490-6ad8de92f2fb)  
 提供一些链接，指向关于将 COM 组件并入 .NET Framework 应用程序中的详细信息。

