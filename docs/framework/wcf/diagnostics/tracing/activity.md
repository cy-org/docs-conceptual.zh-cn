---
title: "活动 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 70471705-f55f-4da1-919f-4b580f172665
caps.latest.revision: 10
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 10
---
# 活动
本主题介绍 [!INCLUDE[indigo1](../../../../../includes/indigo1-md.md)] 跟踪模型中的活动跟踪。活动是帮助用户缩小故障范围的处理单位。在同一活动中发生的错误直接相关。例如，消息解密失败可导致操作失败。操作失败和消息解密失败的跟踪出现在同一活动中，表明解密错误和请求错误之间直接相关。  
  
## 配置活动跟踪  
 [!INCLUDE[indigo2](../../../../../includes/indigo2-md.md)] 提供了用于处理应用程序的预定义活动（请参见[活动列表](../../../../../docs/framework/wcf/diagnostics/tracing/activity-list.md)）。您还可以用编程方式定义活动，以便对用户跟踪进行分组。有关更多信息，请参见[发出用户代码跟踪](../../../../../docs/framework/wcf/diagnostics/tracing/emitting-user-code-traces.md)。  
  
 若要在运行时发出活动跟踪，请对 `System.ServiceModel` 跟踪源或其他 [!INCLUDE[indigo2](../../../../../includes/indigo2-md.md)] 或自定义跟踪源使用 `ActivityTracing` 设置，如下面的配置代码所示。  
  
```  
<source name="System.ServiceModel" switchValue="Verbose,ActivityTracing">  
```  
  
 若要了解有关所使用的配置元素和属性的更多信息，请参见[配置跟踪](../../../../../docs/framework/wcf/diagnostics/tracing/configuring-tracing.md)主题。  
  
## 查看活动  
 可以在[服务跟踪查看器工具 \(SvcTraceViewer.exe\)](../../../../../docs/framework/wcf/service-trace-viewer-tool-svctraceviewer-exe.md)中查看活动及其效用。启用 ActivityTracing 后，此工具将获得跟踪并基于活动对它们进行分类。您还可以查看跟踪传输。跟踪传输指示不同的活动如何互相关联。您可以看到某个特定活动导致另外一个活动启动。例如，消息请求可启动安全握手以获取安全对话令牌。  
  
### 在服务跟踪查看器中关联活动  
 服务跟踪查看器工具提供了两个活动视图：  
  
-   **“列表”**视图，其中，活动 ID 用于跨进程直接将跟踪相互关联。来自不同进程（例如，客户端和服务），但具有相同活动 ID 的跟踪被分组到同一活动中。因此，如果在服务上发生一个错误，然后该错误又导致客户端上发生错误，那么这两个错误都将出现在该工具的同一活动视图中。  
  
-   **“图形”**视图，其中，活动按进程分组。在此视图中，具有相同活动 ID 的客户端和服务的跟踪位于不同的活动中。为了将位于不同进程但具有相同活动 ID 的活动相互关联，该工具显示了跨越相关活动的消息流。  
  
 有关更多信息以及服务跟踪查看器工具的图形视图，请参见[服务跟踪查看器工具 \(SvcTraceViewer.exe\)](../../../../../docs/framework/wcf/service-trace-viewer-tool-svctraceviewer-exe.md)和[使用服务跟踪查看器查看相关跟踪和进行故障诊断](../../../../../docs/framework/wcf/diagnostics/tracing/using-service-trace-viewer-for-viewing-correlated-traces-and-troubleshooting.md)。  
  
## 定义活动范围  
 活动是在设计时定义的，并且表示一个逻辑工作单元。所发出的具有相同活动标识符的跟踪直接相关，它们都属于同一个活动。因为一个活动可能跨越终结点边界（例如请求），因此为活动定义两个范围。  
  
-   `Global` 范围，限于每个应用程序。在此范围中，活动由其 128 位全局唯一活动标识符 gAId 进行标识。gAid 是跨越终结点传播的内容。  
  
-   以终结点为边界的 `Local` 范围。在此范围中，活动由它的 gAId 以及发出活动跟踪的跟踪源名称和进程 ID 标识。这三部分内容构成了本地活动 ID，即 lAId。lAId 用于定义活动的（本地）边界。  
  
## 跟踪架构  
 可以使用任何架构以及跨 Microsoft 平台发出跟踪。“e2e”（表示“端到端”）是一种常用的架构。此架构包含一个 128 位标识符 \(gAId\)、跟踪源名称和进程 ID。在托管代码中，<xref:System.Diagnostics.XmlWriterTraceListener> 可在 E2E 架构中发出跟踪。  
  
 开发人员可以通过使用线程本地存储 \(TLS\) 上的 Guid 设置 <xref:System.Diagnostics.CorrelationManager.ActivityId%2A> 属性来设置随跟踪发出的 AID。下面的示例对此进行说明。  
  
```  
// set the current Activity ID to a new GUID.  
CorrelationManager.ActivityId = Guid.NewGuid();  
```  
  
 使用跟踪源发出跟踪时，设置 TLS 中的 gAId 非常简单，如下面的示例所示。  
  
```  
TraceSource traceSource = new TraceSource("myTraceSource");  
traceSource.TraceEvent(TraceEventType.Warning, eventId, "Information");  
```  
  
 发出的跟踪将包含当前 TLS 中的 gAId、作为参数传递给跟踪源构造函数的跟踪源名称和当前进程的 ID。  
  
## 活动生存期  
 用最严格的术语表述，活动的证据从第一次在发出的跟踪中使用活动 ID 时开始，到最后一次在发出的跟踪中使用活动 ID 时结束。<xref:System.Diagnostics> 提供了一组预定义的跟踪类型（包括“开始”和“停止”），以便显式标记活动生存期边界。  
  
-   开始：指示活动开始。“开始”跟踪提供开始一个新的处理里程碑的记录。它包含给定进程中给定跟踪源的新活动 ID，但是，当活动 ID 跨越终结点传播时除外 — 在这种情况下，我们会在每个终结点中看到一个“开始”跟踪。开始新活动的示例包括创建新的处理线程或进入新的公共方法。  
  
-   停止：指示活动结束。“停止”跟踪提供结束现有处理里程碑的记录。它包含给定进程中给定跟踪源的现有活动 ID，但在终结点之间传播活动 ID 时除外。在这种情况下，我们会在每个终结点中看到一个“停止”跟踪。停止活动的示例包括终止处理线程或退出以“开始”跟踪表示开始的方法。  
  
-   挂起：指示活动的处理已挂起。“挂起”跟踪包含一个现有活动 ID，其处理预期稍后将继续。在“挂起”和“恢复”事件之间，不会从当前跟踪源发出具有此 ID 的跟踪。示例包括调用外部库函数或等待资源（如 I\/O 完成端口）时暂停一个活动。  
  
-   恢复：指示继续处理活动。“恢复”跟踪包含一个现有活动 ID，从当前跟踪源发出的最后一个有关它的跟踪是“挂起”跟踪。示例包括从对外部库函数的调用返回或发出让资源（如 I\/O 完成端口）恢复处理的信号。  
  
-   转换：因为一些活动是由其他活动导致的或与其他活动相关，所以可以通过“转换”跟踪将活动相互关联。转换跟踪记录了活动之间的定向关系。  
  
 “开始”和“停止”跟踪并不是关联所必需的。然而，它们可以帮助提高性能、分析和验证活动范围。  
  
 使用这些类型时，工具可以优化跟踪日志的导航以查找同一活动的直接相关事件，或者如果工具追踪传输跟踪，可查找相关活动中的事件。例如，当工具遇到开始\/停止跟踪时，将停止分析给定活动的日志。  
  
 这些跟踪类型也可以用于分析。在开始和停止标记之间消耗的资源表示活动的全部时间，包括所包含的逻辑活动时间。减去“挂起”和“恢复”跟踪之间的时间间隔就得到实际活动时间。  
  
 “停止”跟踪还对验证已实现活动的范围特别有用。如果某些处理跟踪出现在停止跟踪之后，而不是出现在给定活动之内，这可能暗示代码有缺陷。  
  
## 活动跟踪使用指南  
 以下是使用 ActivityTracing 跟踪（开始、停止、挂起、恢复和转换）的指南。  
  
-   跟踪是一个定向循环图，而不是树。可以将控制返回到生成活动的活动。  
  
-   活动表示一个处理边界，该边界对于系统管理员可能很有意义，或者可以用来实现可支持性。  
  
-   无论是在客户端上还是在服务器上，每个 [!INCLUDE[indigo2](../../../../../includes/indigo2-md.md)] 方法都由开始一个新活动、然后（工作完成后）结束该新活动并返回到环境活动来限定。  
  
-   长时间运行（正在运行）的活动（例如，侦听连接或等待消息）由相应的开始\/停止标记表示。  
  
-   由接收或处理消息触发的活动由跟踪边界来表示。  
  
-   活动表示的是活动本身，而未必是对象。应该将活动理解为“这是在 ...（发出有意义的跟踪）时发生的”。  
  
## 请参阅  
 [配置跟踪](../../../../../docs/framework/wcf/diagnostics/tracing/configuring-tracing.md)   
 [使用服务跟踪查看器查看相关跟踪和进行故障诊断](../../../../../docs/framework/wcf/diagnostics/tracing/using-service-trace-viewer-for-viewing-correlated-traces-and-troubleshooting.md)   
 [端到端跟踪方案](../../../../../docs/framework/wcf/diagnostics/tracing/end-to-end-tracing-scenarios.md)   
 [服务跟踪查看器工具 \(SvcTraceViewer.exe\)](../../../../../docs/framework/wcf/service-trace-viewer-tool-svctraceviewer-exe.md)   
 [发出用户代码跟踪](../../../../../docs/framework/wcf/diagnostics/tracing/emitting-user-code-traces.md)