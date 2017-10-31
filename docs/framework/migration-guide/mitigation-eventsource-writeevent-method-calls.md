---
title: "迁移：EventSource.WriteEvent 方法调用"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology:
- dotnet-clr
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 327a9fdb-ba8e-40f7-89e5-4c89b46e594f
caps.latest.revision: 6
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: 270f89183bced5d07598b1731f18acf90ec9715a
ms.contentlocale: zh-cn
ms.lasthandoff: 07/28/2017

---
# <a name="mitigation-eventsourcewriteevent-method-calls"></a>迁移：EventSource.WriteEvent 方法调用
[!INCLUDE[net_v451](../../../includes/net-v451-md.md)] 强制在从 <xref:System.Diagnostics.Tracing.EventSource?displayProperty=fullName> 派生的类中的 ETW 事件方法与其基类的 <xref:System.Diagnostics.Tracing.EventSource.WriteEvent%2A> 方法之间实施协定。 ETW 事件方法必须向 <xref:System.Diagnostics.Tracing.EventSource.WriteEvent%2A> 方法传递事件 ID，后跟传递给该事件方法的相同参数。  
  
## <a name="impact"></a>影响  
 按以下方式定义的 ETW 事件方法会使协定中断：  
  
```  
[Event(2, Level = EventLevel.Informational)]  
public void Info2(string message)  
{  
   base.WriteEvent(2, message, "-");  
}  
```  
  
 如果 <xref:System.IndexOutOfRangeException> 对象正在读取 <xref:System.Diagnostics.Tracing.EventListener> 数据，则违反此协定时，会引发 <xref:System.Diagnostics.Tracing.EventSource> 异常。  
  
 此 ETW 事件方法的定义应遵循以下模式：  
  
```  
[Event(2, Level = EventLevel.Informational)]  
public void Info2(string message)  
{  
   base.WriteEvent(2, message);  
}  
```  
  
## <a name="mitigation"></a>缓解操作  
 必须修改现有代码以符合所需模式。  
  
 可以通过定义两个方法来调用 <xref:System.Diagnostics.Tracing.EventSource.WriteEvent%2A> 方法，来最大程度减少必须更改的代码量，如下所示：  
  
```  
[NonEvent]  
public void Info2(string message)  
{  
   Info2Internal(message, "-");  
}  
  
public void Info2Internal(string message, string prefix)  
{  
   WriteEvent(2, message, prefix);  
}  
```  
  
## <a name="see-also"></a>另请参阅  
 [运行时更改](../../../docs/framework/migration-guide/runtime-changes-in-the-net-framework-4-5-1.md)

