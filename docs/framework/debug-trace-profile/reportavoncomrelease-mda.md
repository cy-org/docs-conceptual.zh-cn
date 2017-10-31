---
title: reportAvOnComRelease MDA
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
- MDAs (managed debugging assistants), reference counting errors
- exceptions, reference counting errors
- ReportAvOnComRelease MDA
- COM release access violations
- user reference counting errors
- managed debugging assistants (MDAs), reference counting errors
- report access violation on Com release
- reference counting errors
ms.assetid: a2b86b63-08b2-4943-b344-3c2cf46ccd31
caps.latest.revision: 15
author: mairaw
ms.author: mairaw
manager: wpickett
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: d60b63977e8e05cfdb1103a2571ba8d986b98fbf
ms.contentlocale: zh-cn
ms.lasthandoff: 08/21/2017

---
# <a name="reportavoncomrelease-mda"></a>reportAvOnComRelease MDA
在执行 COM 互操作并将原始 COM 调用与 `reportAvOnComRelease` 或 <xref:System.Runtime.InteropServices.Marshal.Release%2A> 方法一起使用时，如果由于用户引用计数错误引发了异常，则将激活 <xref:System.Runtime.InteropServices.Marshal.ReleaseComObject%2A> 托管调试助手 (MDA)。  
  
## <a name="symptoms"></a>症状  
 访问冲突和内存损坏。  
  
## <a name="cause"></a>原因  
 偶尔，在执行 COM 互操作并将原始 COM 调用与 <xref:System.Runtime.InteropServices.Marshal.Release%2A> 或 <xref:System.Runtime.InteropServices.Marshal.ReleaseComObject%2A> 方法一起使用时，会由于用户引用计数错误而引发异常。 通常会丢弃此异常，因为如果不这样做，将会在 CLR 中引发访问冲突，进而导致 CLR 中止。 启用此助手后，除了丢弃这类异常外，还可以检测并报告这类异常。  
  
## <a name="resolution"></a>解决方法  
 检查你的引用计数代码并搜索是否存在错误，同时检查对象的本机客户端是否存在引用计数错误。  
  
## <a name="effect-on-the-runtime"></a>对运行时的影响  
 两种模式皆可用。 如果 `allowAv` 特性为 `true`，则助手会阻止运行时丢弃访问冲突。 如果 `allowAv` 为 `false`（这是默认设置），则运行时会丢弃访问冲突，但会向用户报告一条警告消息，指出引发了一个异常并丢弃了该异常。  
  
## <a name="output"></a>输出  
 如果可能，输出会 包括 COM 接口指针的原始 vtable。 否则，会显示一条信息性消息。  
  
## <a name="configuration"></a>配置  
  
```xml  
<mdaConfig>  
  <assistants>  
    <reportAvOnComRelease />  
  </assistants>  
</mdaConfig>  
```  
  
## <a name="see-also"></a>另请参阅  
 <xref:System.Runtime.InteropServices.MarshalAsAttribute>   
 [使用托管调试助手诊断错误](../../../docs/framework/debug-trace-profile/diagnosing-errors-with-managed-debugging-assistants.md)   
 [互操作封送处理](../../../docs/framework/interop/interop-marshaling.md)

