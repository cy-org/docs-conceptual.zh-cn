---
title: exceptionSwallowedOnCallFromCom MDA
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
- messages, informational
- informational messages
- managed debugging assistants (MDAs), exceptions
- exception handling, managed debugging assistants
- MDAs (managed debugging assistants), exceptions
- ExceptionSwallowedOnCallFromCOM MDA
ms.assetid: 55d6ab12-f251-4aab-aa64-aacbe9d9f974
caps.latest.revision: 13
author: mairaw
ms.author: mairaw
manager: wpickett
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: 386ee77bd701f8737f496e867ffd26a07b9cd303
ms.contentlocale: zh-cn
ms.lasthandoff: 08/21/2017

---
# <a name="exceptionswallowedoncallfromcom-mda"></a>exceptionSwallowedOnCallFromCom MDA
如果在通过不具有非托管 HRESULT 返回类型的方法从 COM 中调用公共语言运行时 (CLR) 代码时，引发了一个异常，将激活 `exceptionSwallowedOnCallFromCOM` 托管调试助手 (MDA)。  
  
## <a name="symptoms"></a>症状  
 调用 COM 中的某个托管组件返回值 FALSE 或 0。 或者，如果该方法具有 void 返回类型，则可能没有任何迹象显示在执行该方法期间引发了异常。 在这种情况下，将以静默方式捕获异常并且执行将返回到 COM 调用方。  
  
## <a name="cause"></a>原因  
 引发了一个异常，但是没有有效的方法来报告该异常。  
  
## <a name="resolution"></a>解决方法  
 仅提供信息，不一定会指出 Bug。  
  
## <a name="effect-on-the-runtime"></a>对运行时的影响  
 此 MDA 对 CLR 无任何影响。 它只报告有关以静默方式捕获的异常的数据。  
  
## <a name="output"></a>输出  
 信息性消息包括方法名称、类型名称和异常消息。  
  
## <a name="configuration"></a>配置  
  
```xml  
<mdaConfig>  
  <assistants>  
    <exceptionSwallowedOnCallFromCom />  
  </assistants>  
</mdaConfig>  
```  
  
## <a name="see-also"></a>另请参阅  
 <xref:System.Runtime.InteropServices.MarshalAsAttribute>   
 [使用托管调试助手诊断错误](../../../docs/framework/debug-trace-profile/diagnosing-errors-with-managed-debugging-assistants.md)   
 [互操作封送处理](../../../docs/framework/interop/interop-marshaling.md)

