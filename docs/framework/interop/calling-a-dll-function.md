---
title: "调用 DLL 函数"
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
- unmanaged functions, calling
- unmanaged functions
- COM interop, platform invoke
- platform invoke, calling unmanaged functions
- interoperation with unmanaged code, platform invoke
- DLL functions
ms.assetid: 113646de-7ea0-4f0e-8df0-c46dab3e8733
caps.latest.revision: 12
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: b676599513b923ae46d6ec27d7506435d9cbfcd2
ms.contentlocale: zh-cn
ms.lasthandoff: 08/21/2017

---
# <a name="calling-a-dll-function"></a>调用 DLL 函数
尽管调用非托管 DLL 函数与调用其他托管代码几乎完全相同，但有一些差异会使 DLL 函数一开始令人感到迷惑。 本部分介绍的主题描述了与一些与调用相关的异常问题。  
  
 从平台调用返回的结构必须是在托管代码和非托管代码中表示形式相同的数据类型。 这些类型称为 blittable 类型，因为它们不需要转换（请参阅 [Blittable 类型和非 Blittable 类型](../../../docs/framework/interop/blittable-and-non-blittable-types.md)）。 若要调用返回类型为 non-blittable 结构的函数，可定义与 non-blittable 类型大小相同的 blittable 帮助程序类型，并在函数返回后转换数据。  
  
## <a name="in-this-section"></a>本节内容  
 [传递结构](../../../docs/framework/interop/passing-structures.md)  
 确定使用预定义布局传递数据结构的问题。  
  
 [回调函数](../../../docs/framework/interop/callback-functions.md)  
 提供有关回调函数的基本信息。  
  
 [如何：实现回调函数](../../../docs/framework/interop/how-to-implement-callback-functions.md)  
 描述如何在托管代码中实现回调函数。  
  
## <a name="related-sections"></a>相关章节  
 [使用非托管 DLL 函数](../../../docs/framework/interop/consuming-unmanaged-dll-functions.md)  
 描述如何使用平台调用调用非托管 DLL 函数。  
  
 [用平台调用封送数据](../../../docs/framework/interop/marshaling-data-with-platform-invoke.md)  
 描述如何声明方法参数以及如何将自变量传递给由非托管库导出的函数。

