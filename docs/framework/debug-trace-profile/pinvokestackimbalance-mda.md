---
title: pInvokeStackImbalance MDA
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
- signatures, platform invoke
- stack depth
- platform invoke stack imbalance
- MDAs (managed debugging assistants), platform invoke
- platform invoke, run-time errors
- PInvokeStackImbalance MDA
- managed debugging assistants (MDAs), platform invoke
ms.assetid: 34ddc6bd-1675-4f35-86aa-de1645d5c631
caps.latest.revision: 16
author: mairaw
ms.author: mairaw
manager: wpickett
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: c7dcab401da29798365f4cbb5477dd0fb154c830
ms.contentlocale: zh-cn
ms.lasthandoff: 08/21/2017

---
# <a name="pinvokestackimbalance-mda"></a>pInvokeStackImbalance MDA
给定 <xref:System.Runtime.InteropServices.DllImportAttribute> 属性中指定的调用约定以及托管签名中的参数声明，当 CLR 检测到平台 invoke 调用之后的堆栈深度与预期堆栈深度不匹配时，激活 `pInvokeStackImbalance` 托管调试助手 (MDA)。  
  
> [!NOTE]
>  仅为 32 位 x86 平台实现 `pInvokeStackImbalance` MDA。  
  
> [!NOTE]
>  在 .NET Framework 3.5 版中，默认禁用 `pInvokeStackImbalance` MDA。 在 Visual Studio 2005 中使用 .NET Framework 3.5 版时，`pInvokeStackImbalance` MDA 将出现在“异常”对话框的“托管调试助手”列表中（单击“调试”菜单上的“异常”时显示）。 但是，选中或清除 `pInvokeStackImbalance` 的“引发”复选框不会启用或禁用 MDA；它仅控制在 MDA 处于激活状态时 Visual Studio 是否引发异常。  
  
## <a name="symptoms"></a>症状  
 进行平台 invoke 调用时或之后，应用程序会遭遇访问冲突或内存损坏。  
  
## <a name="cause"></a>原因  
 平台 invoke 调用的托管签名可能不匹配正在被调用的方法的非托管签名。  这种不匹配可能是由于没有声明参数的正确数量或没有指定参数的适当大小的托管签名所导致的。  MDA 也可因调用约定（可能由 <xref:System.Runtime.InteropServices.DllImportAttribute> 属性指定）不匹配非托管调用约定而激活。  
  
## <a name="resolution"></a>解决方法  
 检查托管平台调用签名和调用约定，以确认它与本机目标的签名和调用约定匹配。  请尝试在托管端和非托管端上显式指定调用约定。 非托管函数也可能（尽管可能性不太大）出于某种原因（例如非托管编译器中的 bug）使堆栈不平衡。  
  
## <a name="effect-on-the-runtime"></a>对运行时的影响  
 强制所有平台 invoke 调用都采用 CLR 中的非优化路径。  
  
## <a name="output"></a>输出  
 MDA 消息会提供正导致堆栈不平衡的平台 invoke 方法调用的名称。  方法 `SampleMethod` 上的平台 invoke 调用的示例消息为：  
  
```  
A call to PInvoke function 'SampleMethod' has unbalanced the stack.   
This is likely because the managed PInvoke signature does not match   
the unmanaged target signature. Check that the calling convention and   
parameters of the PInvoke signature match the target unmanaged signature.  
```  
  
## <a name="configuration"></a>配置  
  
```xml  
<mdaConfig>  
  <assistants>  
    <pInvokeStackImbalance />  
  </assistants>  
</mdaConfig>  
```  
  
## <a name="see-also"></a>另请参阅  
 <xref:System.Runtime.InteropServices.MarshalAsAttribute>   
 [使用托管调试助手诊断错误](../../../docs/framework/debug-trace-profile/diagnosing-errors-with-managed-debugging-assistants.md)   
 [互操作封送处理](../../../docs/framework/interop/interop-marshaling.md)

