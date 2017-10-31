---
title: "异常 Thrown_V1 ETW 事件"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology:
- dotnet-clr
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- ExceptionThrown_V1 event [.NET Framework]
- ETW, ExceptionThrown_V1 event (CLR)
ms.assetid: 0d3da389-6b7b-40f6-a877-fac546d6019c
caps.latest.revision: 6
author: mairaw
ms.author: mairaw
manager: wpickett
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: dcf3390821c4210ced4c43dab5a94c93802d5f9d
ms.contentlocale: zh-cn
ms.lasthandoff: 08/21/2017

---
# <a name="exception-thrownv1-etw-event"></a>异常 Thrown_V1 ETW 事件
该事件捕获有关引发的异常的信息。  
  
 下表显示了引发事件的关键字以及事件的级别。 （有关详细信息，请参阅 [CLR ETW Keywords and Levels](../../../docs/framework/performance/clr-etw-keywords-and-levels.md)。）  
  
|引发事件的关键字|级别|  
|-----------------------------------|-----------|  
|`ExceptionKeyword` (0x8000)|警告 (2)|  
  
 下表显示了事件信息。  
  
|Event|事件 ID|在发生以下情况时引发|  
|-----------|--------------|-----------------|  
|`ExceptionThrown_V1`|80|引发托管异常。|  
  
 下表显示了事件数据。  
  
|字段名|数据类型|描述|  
|----------------|---------------|-----------------|  
|异常类型|win:UnicodeString|异常的类型，例如，`System.NullReferenceException`。|  
|异常消息|win:UnicodeString|实际的异常消息。|  
|EIPCodeThrow|win:Pointer|指向异常发生位置的指令指针。|  
|ExceptionHR|win:UInt32|异常 [HRESULT](http://go.microsoft.com/fwlink/?LinkId=179679)。|  
|ExceptionFlags|win:UInt16|0x01: HasInnerException（参阅 Visual Basic 文档中的 [CLR ETW 事件](../../../docs/framework/performance/clr-etw-events.md)）。<br /><br /> 0x02: IsNestedException。<br /><br /> 0x04: IsRethrownException。<br /><br /> 0x08: IsCorruptedStateException（表示进程状态已损坏，请参阅 MSDN 上的[处理损坏状态异常](http://go.microsoft.com/fwlink/?LinkId=179681)）。<br /><br /> 0x10: IsCLSCompliant（从 <xref:System.Exception> 派生的异常符合 CLS，此外的其他异常均不符合 CLS）。|  
|ClrInstanceID|win:UInt16|CLR 或 CoreCLR 的实例的唯一 ID。|  
  
## <a name="see-also"></a>另请参阅  
 [CLR ETW 事件](../../../docs/framework/performance/clr-etw-events.md)

