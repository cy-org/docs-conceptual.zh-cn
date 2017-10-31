---
title: "任务并行库和 PLINQ 中的 ETW 事件"
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
- tasks, ETW events
ms.assetid: 87a9cff5-d86f-4e44-a06e-d12764d0dce2
caps.latest.revision: 7
author: mairaw
ms.author: mairaw
manager: wpickett
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: 9de80f9f2319caefbb7b716e17c43fddf9db67e4
ms.contentlocale: zh-cn
ms.lasthandoff: 08/21/2017

---
# <a name="etw-events-in-task-parallel-library-and-plinq"></a>任务并行库和 PLINQ 中的 ETW 事件
任务并行库和 PLINQ 均可生成 Windows 事件跟踪 (ETW) 事件，通过 Windows 性能分析器等工具使用这些事件可分析并排除应用程序故障。 但在大多数情况下，分析并行应用程序代码的最佳方式是使用 [!INCLUDE[vsUltShort](../../../includes/vsultshort-md.md)] 中的[并发可视化工具](/visualstudio/profiling/concurrency-visualizer)。  
  
## <a name="task-parallel-library-etw-events"></a>任务并行库 ETW 事件  
 在 EVENT_HEADER 结构中，<xref:System.Threading.Tasks.Parallel.For%2A?displayProperty=fullName><xref:System.Threading.Tasks.Parallel.ForEach%2A?displayProperty=fullName> 和 <xref:System.Threading.Tasks.Parallel.Invoke%2A?displayProperty=fullName> 生成的事件的 ProviderId GUID 为：  
  
```  
0x2e5dba47, 0xa3d2, 0x4d16, 0x8e, 0xe0, 0x66, 0x71, 0xff, 0xdc, 0xd7, 0xb5  
```  
  
### <a name="parallel-loop-begin"></a>并行循环开始  
 EVENT_DESCRIPTOR.Task = 1  
  
 EVENT_DESCRIPTOR.Id = 1  
  
#### <a name="user-data"></a>用户数据  
  
|**Name**|**类型**|**描述**|  
|--------------|--------------|---------------------|  
|OriginatingTaskSchedulerID|<xref:System.Int32?displayProperty=fullName>|启动循环的 TaskScheduler 的 ID。|  
|OriginatingTaskID|<xref:System.Int32?displayProperty=fullName>|启动循环的任务的 ID。|  
|ForkJoinContextID|<xref:System.Int32?displayProperty=fullName>|用于为具有分叉/联接语义的事件指示嵌套和对的唯一标识符。|  
|OperationType|<xref:System.Int32?displayProperty=fullName>|指示循环的类型：<br /><br /> 1 = ParallelInvoke<br /><br /> 2 = ParallelFor<br /><br /> 3 = ParallelForEach|  
|InclusiveFrom|<xref:System.Int64?displayProperty=fullName>|循环计数器的起始值|  
|ExclusiveTo|<xref:System.Int64?displayProperty=fullName>|循环计数器的结束值|  
  
### <a name="parallel-loop-end"></a>并行循环结束  
 EVENT_DESCRIPTOR.Task = 2  
  
 EVENT_DESCRIPTOR.Id = 2  
  
#### <a name="user-data"></a>用户数据  
  
|**Name**|**类型**|**描述**|  
|--------------|--------------|---------------------|  
|OriginatingTaskSchedulerID|<xref:System.Int32?displayProperty=fullName>|启动循环的 TaskScheduler 的 ID。|  
|OriginatingTaskID|<xref:System.Int32?displayProperty=fullName>|启动循环的任务的 ID。|  
|ForkJoinContextID|<xref:System.Int32?displayProperty=fullName>|用于为具有分叉/联接语义的事件指示嵌套和对的唯一标识符。|  
|totalIterations|<xref:System.Int64?displayProperty=fullName>|迭代总次数|  
  
### <a name="parallel-invoke-begin"></a>并行调用开始  
 EVENT_DESCRIPTOR.Task = 3  
  
 EVENT_DESCRIPTOR.Id = 3  
  
#### <a name="user-data"></a>用户数据  
  
|**Name**|**类型**|**描述**|  
|--------------|--------------|---------------------|  
|OriginatingTaskSchedulerID|<xref:System.Int32?displayProperty=fullName>|启动循环的 TaskScheduler 的 ID。|  
|OriginatingTaskID|<xref:System.Int32?displayProperty=fullName>|启动循环的任务的 ID。|  
|ForkJoinContextID|<xref:System.Int32?displayProperty=fullName>|用于为具有分叉/联接语义的事件指示嵌套和对的唯一标识符。|  
|totalIterations|<xref:System.Int64?displayProperty=fullName>|迭代总次数|  
|operationType|<xref:System.Int32?displayProperty=fullName>|指示循环的类型：<br /><br /> 1 = ParallelInvoke<br /><br /> 2 = ParallelFor<br /><br /> 3 = ParallelForEach|  
|ActionCount|<xref:System.Int32?displayProperty=fullName>|将在并行调用中执行的操作数。|  
  
### <a name="parallel-invoke-end"></a>并行调用结束  
 EVENT_DESCRIPTOR.Task = 4  
  
 EVENT_DESCRIPTOR.Id = 4  
  
#### <a name="user-data"></a>用户数据  
  
|**Name**|**类型**|**描述**|  
|--------------|--------------|---------------------|  
|OriginatingTaskSchedulerID|<xref:System.Int32?displayProperty=fullName>|启动循环的 TaskScheduler 的 ID。|  
|OriginatingTaskID|<xref:System.Int32?displayProperty=fullName>|启动循环的任务的 ID。|  
|ForkJoinContextID|<xref:System.Int32?displayProperty=fullName>|用于为具有分叉/联接语义的事件指示嵌套和对的唯一标识符。|  
  
## <a name="plinq-etw-events"></a>PINQ ETW 事件  
 PLINQ 的 EVENT_HEADER.ProviderId GUID 为：  
  
```  
0x159eeeec, 0x4a14, 0x4418, 0xa8, 0xfe, 0xfa, 0xab, 0xcd, 0x98, 0x78, 0x87  
```  
  
### <a name="parallel-query-begin"></a>并行查询开始  
 EVENT_DESCRIPTOR.Task = 1  
  
 EVENT_DESCRIPTOR.Id = 1  
  
#### <a name="user-data"></a>用户数据  
  
|**Name**|**类型**|**描述**|  
|--------------|--------------|---------------------|  
|OriginatingTaskSchedulerID|<xref:System.Int32?displayProperty=fullName>|启动循环的 TaskScheduler 的 ID。|  
|OriginatingTaskID|<xref:System.Int32?displayProperty=fullName>|启动循环的任务的 ID。|  
|QueryID|<xref:System.Int32?displayProperty=fullName>|唯一的查询标识符。|  
  
### <a name="parallel-query-end"></a>并行查询结束  
 EVENT_DESCRIPTOR.Task = 2  
  
 EVENT_DESCRIPTOR.Id = 2  
  
#### <a name="user-data"></a>用户数据  
  
|**Name**|**类型**|**描述**|  
|--------------|--------------|---------------------|  
|OriginatingTaskSchedulerID|<xref:System.Int32?displayProperty=fullName>|启动循环的 TaskScheduler 的 ID。|  
|OriginatingTaskID|<xref:System.Int32?displayProperty=fullName>|启动循环的任务的 ID。|  
|QueryID|<xref:System.Int32?displayProperty=fullName>|唯一的查询标识符。|  
  
## <a name="see-also"></a>另请参阅  
 [.NET Framework 中的 ETW 事件](../../../docs/framework/performance/etw-events.md)   
 [任务并行库 (TPL)](../../../docs/standard/parallel-programming/task-parallel-library-tpl.md)   
 [并行 LINQ (PLINQ)](../../../docs/standard/parallel-programming/parallel-linq-plinq.md)

