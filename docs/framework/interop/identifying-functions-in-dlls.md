---
title: "标识 DLL 中的函数"
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
- platform invoke, identifying functions
- COM interop, DLL functions
- unmanaged functions
- COM interop, platform invoke
- interoperation with unmanaged code, DLL functions
- interoperation with unmanaged code, platform invoke
- identifying DLL functions
- DLL functions
ms.assetid: 3e3f6780-6d90-4413-bad7-ba641220364d
caps.latest.revision: 9
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: b96ef668a8a11794b87d3cbe7c2ba864f8a75e2f
ms.contentlocale: zh-cn
ms.lasthandoff: 08/21/2017

---
# <a name="identifying-functions-in-dlls"></a>标识 DLL 中的函数
DLL 函数的标识由以下元素组成：  
  
-   函数名称或序号  
  
-   可以找到实现的 DLL 文件的名称  
  
 例如，指定 User32.dll 中的 MessageBox 函数可标识函数 (MessageBox) 及其位置（User32.dll、 User32 或 user32）。 Microsoft Windows 应用程序编程接口 (Win32 API) 可以包含每个处理字符和字符串的函数的两个版本：1 字节字符 ANSI 版本和 2 字节字符 Unicode 版本。 未指定时，由 <xref:System.Runtime.InteropServices.DllImportAttribute.CharSet> 字段表示的字符集默认为 ANSI。 某些函数可以具有两个以上的版本。  
  
 MessageBoxA 是 MessageBox 函数的 ANSI 入口点；MessageBoxW 是 Unicode 版本。 可以通过运行多种命令行工具列出特定 DLL（如 user32.dll）的函数名称。 例如，可以使用 `dumpbin /exports user32.dll` 或 `link /dump /exports user32.dll` 来获取函数名称。  
  
 可以将非托管函数重命名为代码内的任意名称，只要将新名称映射到 DLL 中的原始入口点。 有关重命名托管源代码中的非托管 DLL 函数的说明，请参见[指定入口点](../../../docs/framework/interop/specifying-an-entry-point.md)。  
  
 借助平台调用，可以通过调用 Win32 API 和其他 DLL 中的函数来控制操作系统的重要部分。 除了 Win32 API，还可通过平台调用获取许多其他 API 和 DLL。  
  
 下表描述了 Win32 API 中的多个常用的 DLL。  
  
|DLL|内容描述|  
|---------|-----------------------------|  
|GDI32.dll|图形设备接口 (GDI) 函数，用于设备输出，例如用于绘图和字体管理。|  
|Kernel32.dll|低级别的操作系统函数，用于内存管理和资源处理。|  
|User32.dll|Windows 管理函数，用于消息处理、计时器、菜单和通信。|  
  
 有关 Win32 API 的完整文档，请参阅平台 SDK。 有关演示如何构造要用于平台调用、基于 .NET 的声明的示例，请参阅[用平台调用封送数据](../../../docs/framework/interop/marshaling-data-with-platform-invoke.md)。  
  
## <a name="see-also"></a>另请参阅  
 [使用非托管 DLL 函数](../../../docs/framework/interop/consuming-unmanaged-dll-functions.md)   
 [指定入口点](../../../docs/framework/interop/specifying-an-entry-point.md)   
 [创建用于容纳 DLL 函数的类](../../../docs/framework/interop/creating-a-class-to-hold-dll-functions.md)   
 [在托管代码中创建原型](../../../docs/framework/interop/creating-prototypes-in-managed-code.md)   
 [调用 DLL 函数](../../../docs/framework/interop/calling-a-dll-function.md)

