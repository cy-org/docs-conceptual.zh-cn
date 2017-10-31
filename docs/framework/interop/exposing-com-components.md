---
title: "向 .NET Framework 公开 COM 组件"
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
- exposing COM components to .NET Framework
- interoperation with unmanaged code, exposing COM components
- COM interop, exposing COM components
ms.assetid: e78b14f1-e487-43cd-9c6d-1a07483f1730
caps.latest.revision: 11
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: c0fcf7bec289d64b1faceef00b01278fa45caab0
ms.contentlocale: zh-cn
ms.lasthandoff: 08/21/2017

---
# <a name="exposing-com-components-to-the-net-framework"></a>向 .NET Framework 公开 COM 组件
本部分概述向托管代码公开现有 COM 组件所需的步骤。 有关编写与 .NET Framework 紧密集成的 COM 服务器的详细信息，请参阅[互操作的设计注意事项](http://msdn.microsoft.com/en-us/b59637f6-fe35-40d6-ae72-901e7a707689)。  
  
 作为中间层业务应用程序或独立功能，现有 COM 组件是托管代码中的宝贵资源。 理想的组件具有主互操作程序集，且完全符合 COM 实施的编程标准。  
  
#### <a name="to-expose-com-components-to-the-net-framework"></a>向 .NET Framework 公开 COM 组件  
  
1.  [将类型库当作程序集导入](../../../docs/framework/interop/importing-a-type-library-as-an-assembly.md)。  
  
     公共语言运行时需要包括 COM 类型在内的所有类型的元数据。 有多种方法来获取包含 COM 类型（作为元数据导入）的程序集。  
  
2.  [在托管代码中创建 COM 类型](http://msdn.microsoft.com/en-us/1a95a8ca-c8b8-4464-90b0-5ee1a1135b66)。  
  
     可检查 COM 类型、激活实例，并采用在任何托管类型上进行调用的方式在 COM 对象上调用方法。  
  
3.  [编译互操作项目](../../../docs/framework/interop/compiling-an-interop-project.md)。  
  
     [!INCLUDE[winsdklong](../../../includes/winsdklong-md.md)] 为符合公共语言规范 (CLS) 的多种语言提供编译器，包括 [!INCLUDE[vbprvblong](../../../includes/vbprvblong-md.md)]、C# 和 C++。  
  
4.  [部署互操作应用程序](../../../docs/framework/interop/deploying-an-interop-application.md)。  
  
     最好将互操作应用程序部署为全局程序集缓存中具有[强名称](../../../docs/framework/app-domains/strong-named-assemblies.md)的签名程序集。  
  
## <a name="see-also"></a>另请参阅  
 [与非托管代码交互操作](../../../docs/framework/interop/index.md)   
 [互操作的设计注意事项](http://msdn.microsoft.com/en-us/b59637f6-fe35-40d6-ae72-901e7a707689)   
 [COM 互操作示例：.NET 客户端和 COM 服务器](../../../docs/framework/interop/com-interop-sample-net-client-and-com-server.md)   
 [语言独立性和与语言无关的组件](../../../docs/standard/language-independence-and-language-independent-components.md)   
 [Gacutil.exe（全局程序集缓存工具）](../../../docs/framework/tools/gacutil-exe-gac-tool.md)

