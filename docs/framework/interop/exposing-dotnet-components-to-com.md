---
title: "向 COM 公开 .NET Framework 组件"
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
- interoperation with unmanaged code, exposing .NET Framework components
- COM interop, exposing COM components
ms.assetid: e42a65f7-1e61-411f-b09a-aca1bbce24c6
caps.latest.revision: 6
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: 8248d78ffa7360f838ceb0389686ab9b348ffd8d
ms.contentlocale: zh-cn
ms.lasthandoff: 08/21/2017

---
# <a name="exposing-net-framework-components-to-com"></a>向 COM 公开 .NET Framework 组件
对开发人员而言，编写 .NET 类型以及从非托管代码使用该类型是不同的活动。 本部分介绍编写与 COM 客户端互操作的托管代码的几个提示：  
  
-   [为互操作限定 .NET 类型](../../../docs/framework/interop/qualifying-net-types-for-interoperation.md)。  
  
     要向 COM 公开的所有托管类型、方法、属性、字段和事件都必须是公开的。 各类型必须具有公共默认构造函数，通过 COM 只能调用该构造函数。  
  
-   [应用互操作属性](../../../docs/framework/interop/applying-interop-attributes.md)。  
  
     托管代码中的自定义属性可增强组件的互操作性。  
  
-   [将 COM 的程序集打包](../../../docs/framework/interop/packaging-an-assembly-for-com.md)。  
  
     COM 开发人员可能会要求用户总结引用和部署程序集所涉及的步骤。  
  
 此外，本部分还确定了从 COM 客户端使用托管类型的相关任务。  
  
#### <a name="to-consume-a-managed-type-from-com"></a>从 COM 使用托管类型  
  
1.  [向 COM 注册程序集](../../../docs/framework/interop/registering-assemblies-with-com.md)。  
  
     必须在设计时注册程序集（和类型库）中的类型。 如果安装程序未注册程序集，请指示 COM 开发人员使用 Regasm.exe。  
  
2.  [从 COM 引用 .NET 类型](../../../docs/framework/interop/how-to-reference-net-types-from-com.md)。  
  
     COM 开发人员可使用当前使用的相同工具和技术引用程序集中的类型。  
  
3.  [调用 .NET 对象](http://msdn.microsoft.com/en-us/40c9626c-aea6-4bad-b8f0-c1de462efd33)。  
  
     COM 开发人员可采用在任何非托管类型上调用方法的方式在 .NET 对象上调用方法。 例如，COM CoCreateInstance API 激活 .NET 对象。  
  
4.  [为 COM 访问部署应用程序](http://msdn.microsoft.com/en-us/fb63564c-c1b9-4655-a094-a235625882ce)。  
  
     具有强名称的程序集可安装在全局程序集缓存中，并向其发布者请求签名。 不具有强名称的程序集必须安装在客户端的应用程序目录中。  
  
## <a name="see-also"></a>另请参阅  
 [与非托管代码交互操作](../../../docs/framework/interop/index.md)   
 [COM 互操作示例：COM 客户端和 .NET 服务器](../../../docs/framework/interop/com-interop-sample-com-client-and-net-server.md)

