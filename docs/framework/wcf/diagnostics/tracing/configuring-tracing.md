---
title: "配置跟踪 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "跟踪 [WCF]"
ms.assetid: 82922010-e8b3-40eb-98c4-10fc05c6d65d
caps.latest.revision: 53
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 53
---
# 配置跟踪
本主题描述您可以如何启用跟踪，配置要发出跟踪的跟踪源并设置跟踪级别，设置活动跟踪和传播以支持端对端的跟踪关联，以及设置要访问跟踪的跟踪侦听器。  
  
 有关生产或调试环境中的跟踪设置建议，请参阅[跟踪和消息日志记录的推荐设置](../../../../../docs/framework/wcf/diagnostics/tracing/recommended-settings-for-tracing-and-message-logging.md)。  
  
> [!IMPORTANT]
>  在 Windows 8 中，您必须提升运行程序应用程序（作为管理员运行），以便为您的应用程序来生成跟踪日志。  
  
## 启用跟踪  
 [!INCLUDE[indigo1](../../../../../includes/indigo1-md.md)] 输出以下用于诊断跟踪的数据：  
  
-   对进程里程碑的跟踪跨应用程序的所有组件，如操作调用、代码异常、警告及其他重大处理事件。  
  
-   跟踪功能出现故障时发生的 Windows 错误事件。请参见[事件日志记录](../../../../../docs/framework/wcf/diagnostics/event-logging/index.md)。  
  
 [!INCLUDE[indigo2](../../../../../includes/indigo2-md.md)] 跟踪建立在 <xref:System.Diagnostics> 之上。若要使用跟踪，应在配置文件或代码中定义跟踪源。[!INCLUDE[indigo2](../../../../../includes/indigo2-md.md)]定义每个 [!INCLUDE[indigo2](../../../../../includes/indigo2-md.md)] 程序集的跟踪源。`System.ServiceModel` 跟踪源是最常见的 [!INCLUDE[indigo2](../../../../../includes/indigo2-md.md)] 跟踪源，它跨 [!INCLUDE[indigo2](../../../../../includes/indigo2-md.md)] 通信堆栈（从进入\/离开传输到进入\/离开用户代码）记录处理里程碑。`System.ServiceModel.MessageLogging` 跟踪源记录流过系统的所有消息。  
  
 默认情况下不启用跟踪。若要激活跟踪，必须创建一个跟踪侦听器并在配置中为选定的跟踪源设置除“Off”以外的跟踪级别；否则，[!INCLUDE[indigo2](../../../../../includes/indigo2-md.md)] 不会生成任何跟踪。如果不指定侦听器，则会自动禁用跟踪。如果定义侦听器，但不指定级别，则默认情况下级别将设置为“Off”，这意味着不会发出任何跟踪。  
  
 如果您使用 [!INCLUDE[indigo2](../../../../../includes/indigo2-md.md)] 扩展点（如自定义操作调用程序），则应发出自己的跟踪。这是因为在实现了扩展点的情况下，[!INCLUDE[indigo2](../../../../../includes/indigo2-md.md)] 不再在默认路径中发出标准跟踪。如果未通过发出跟踪实现手动跟踪支持，则可能看不到预期跟踪。  
  
 可以通过编辑应用程序的配置文件（对于 Web 承载的应用程序，为 Web.config；对于自承载的应用程序，为 Appname.exe.config）来配置跟踪。下面的示例演示如何进行这样的编辑。有关这些设置的更多信息，请参见“配置要使用跟踪的跟踪侦听器”一节。  
  
```  
<configuration>  
   <system.diagnostics>  
      <sources>  
            <source name="System.ServiceModel"   
                    switchValue="Information, ActivityTracing"  
                    propagateActivity="true">  
            <listeners>  
               <add name="traceListener"   
                   type="System.Diagnostics.XmlWriterTraceListener"   
                   initializeData= "c:\log\Traces.svclog" />  
            </listeners>  
         </source>  
      </sources>  
   </system.diagnostics>  
</configuration>  
```  
  
> [!NOTE]
>  若要在 [!INCLUDE[vs_current_short](../../../../../includes/vs-current-short-md.md)] 中编辑 [!INCLUDE[indigo2](../../../../../includes/indigo2-md.md)] 服务项目的配置文件，请在**“解决方案资源管理器”**中右键单击应用程序的配置文件：对于 Web 承载的应用程序，为 Web.config 文件；对于自承载的应用程序，则为 Appname.exe.config 文件。然后选择**“编辑 WCF 配置”**上下文菜单项。这将启动 [配置编辑器工具 \(SvcConfigEditor.exe\)](../../../../../docs/framework/wcf/configuration-editor-tool-svcconfigeditor-exe.md)，可以通过它使用图形用户界面来修改 [!INCLUDE[indigo2](../../../../../includes/indigo2-md.md)] 服务的配置设置。  
  
## 配置要发出跟踪的跟踪源  
 [!INCLUDE[indigo2](../../../../../includes/indigo2-md.md)] 为每个程序集定义一个跟踪源。在程序集中生成的跟踪由为该跟踪源定义的侦听器访问。定义下列跟踪源：  
  
-   System.ServiceModel：每当读取配置、在传输或安全处理中处理消息、在用户代码中调度消息时，记录 [!INCLUDE[indigo2](../../../../../includes/indigo2-md.md)] 处理的所有阶段。  
  
-   System.ServiceModel.MessageLogging：记录流过系统的所有消息。  
  
-   System.IdentityModel。  
  
-   System.ServiceModel.Activation。  
  
-   System.IO.Log：记录公用日志文件系统 \(CLFS\) 的 .NET Framework 接口。  
  
-   System.Runtime.Serialization：在读\/写对象时进行记录。  
  
-   CardSpace。  
  
 可以将每个跟踪源配置为使用相同（共享）的侦听器，如下面的配置示例中所示。  
  
```  
<configuration>  
    <system.diagnostics>  
        <sources>  
            <source name="System.ServiceModel"   
                    switchValue="Information, ActivityTracing"  
                    propagateActivity="true">  
                <listeners>  
                    <add name="xml" />  
                </listeners>  
            </source>  
            <source name="CardSpace">  
                <listeners>  
                    <add name="xml" />  
                </listeners>  
            </source>  
            <source name="System.IO.Log">  
                <listeners>  
                    <add name="xml" />  
                </listeners>  
            </source>  
            <source name="System.Runtime.Serialization">  
                <listeners>  
                    <add name="xml" />  
                </listeners>  
            </source>  
            <source name="System.IdentityModel">  
                <listeners>  
                    <add name="xml" />  
                </listeners>  
            </source>  
        </sources>  
  
        <sharedListeners>  
            <add name="xml"  
                 type="System.Diagnostics.XmlWriterTraceListener"  
                 initializeData="c:\log\Traces.svclog" />  
        </sharedListeners>  
    </system.diagnostics>  
</configuration>  
```  
  
 另外，还可以添加用户定义的跟踪源来发出用户代码跟踪，如下面的示例所示。  
  
```  
<system.diagnostics>  
   <sources>  
       <source name="UserTraceSource" switchValue="Warning, ActivityTracing" >  
          <listeners>  
              <add name="xml"  
                 type="System.Diagnostics.XmlWriterTraceListener"  
                 initializeData="C:\logs\UserTraces.svclog" />  
          </listeners>  
       </source>  
   </sources>  
   <trace autoflush="true" />   
</system.diagnostics>  
```  
  
 [!INCLUDE[crabout](../../../../../includes/crabout-md.md)]创建用户定义的跟踪源的更多信息，请参见[扩展跟踪](../../../../../docs/framework/wcf/samples/extending-tracing.md)。  
  
## 配置要使用跟踪的跟踪侦听器  
 在运行时，[!INCLUDE[indigo2](../../../../../includes/indigo2-md.md)] 向处理数据的侦听器输送跟踪数据。[!INCLUDE[indigo2](../../../../../includes/indigo2-md.md)] 为 <xref:System.Diagnostics> 提供多个预定义的侦听器，这些侦听器用于输出的格式有所不同。您也可以添加自定义侦听器类型。  
  
 可以使用 `add` 指定要使用的跟踪侦听器的名称和类型。在示例配置中，将侦听器命名为 `traceListener` 并添加了标准 .NET Framework 跟踪侦听器 \(`System.Diagnostics.XmlWriterTraceListener`\) 作为要使用的类型。可以为每个源添加任意数目的跟踪侦听器。如果跟踪侦听器发出对文件的跟踪，则您必须在配置文件中指定输出文件的位置和名称。通过将 `initializeData` 设置为该侦听器的文件名称来完成此操作。如果不指定文件名，则会基于所用的侦听器类型生成一个随机文件名。如果使用 <xref:System.Diagnostics.XmlWriterTraceListener>，则会生成不带扩展名的文件名。如果实现自定义侦听器，则也可以使用此属性来接收除文件名以外的初始化数据。例如，可以为此属性指定数据库标识符。  
  
 可以将自定义跟踪侦听器配置为在网络上发送跟踪，例如，发送到远程数据库。作为应用程序部署人员，您应对远程计算机上的跟踪日志施加适当的访问控制。  
  
 您也可以通过编程方式配置跟踪侦听器。[!INCLUDE[crdefault](../../../../../includes/crdefault-md.md)][如何：创建和初始化跟踪侦听器](http://go.microsoft.com/fwlink/?LinkId=94648)（可能为英文网页）和[创建自定义 TraceListener](http://go.microsoft.com/fwlink/?LinkId=96239)（可能为英文网页）。  
  
> [!CAUTION]
>  由于 `System.Diagnostics.XmlWriterTraceListener` 不是线程安全的，因此，跟踪源可能会在输出跟踪时以独占方式锁定资源。当多个线程输出对配置为使用此侦听器的跟踪源的跟踪时，可能会出现资源争用，这会致使重大的性能问题。若要解决此问题，应实现一个线程安全的自定义侦听器。  
  
## 跟踪级别  
 跟踪级别由跟踪源的 `switchValue` 设置控制。下表中描述了可用的跟踪级别。  
  
|跟踪级别|被跟踪事件的特性|被跟踪事件的内容|被跟踪事件|用户目标|  
|----------|--------------|--------------|-----------|----------|  
|Off|N\/A|N\/A|不发出任何跟踪。|不可用|  
|Critical|“负”事件：表示意外处理或错误条件的事件。||将记录包括下列各项的未经处理的异常：<br /><br /> -   OutOfMemoryException<br />-   ThreadAbortException（CLR 调用任何 ThreadAbortExceptionHandler）<br />-   StackOverflowException（无法捕获）<br />-   ConfigurationErrorsException<br />-   SEHException<br />-   应用程序启动错误<br />-   故障快速报警事件<br />-   系统挂起<br />-   病毒消息：致使应用程序失败的消息跟踪。|管理员<br /><br /> 应用程序开发人员|  
|错误|“负”事件：表示意外处理或错误条件的事件。|已发生意外处理。应用程序未能执行预期的任务。然而，应用程序仍处于开启状态并在运行。|记录所有异常。|Administrators<br /><br /> 应用程序开发人员|  
|警告|“负”事件：表示意外处理或错误条件的事件。|可能的问题已经出现或可能出现，但是，应用程序仍在正常工作。不过，该应用程序可能不会继续正常工作。|-   该应用程序正在接收的请求数比其遏制设置所允许的数目要多。<br />-   接收队列接近于为其配置的最大容量。<br />-   已经超时。<br />-   凭据被拒绝。|Administrators<br /><br /> 应用程序开发人员|  
|信息|“正”事件：对成功里程碑进行标记的事件|应用程序执行的重要和成功里程碑，而不考虑该应用程序是否工作正常。|通常，生成对监视和诊断系统状态、测量性能或执行分析十分有用的消息。可以使用此类信息规划容量和管理性能：<br /><br /> -   创建通道。<br />-   创建终结点侦听器。<br />-   消息进入\/离开传输。<br />-   检索安全令牌。<br />-   读取配置设置。|Administrators<br /><br /> 应用程序开发人员<br /><br /> 产品开发人员。|  
|详细|“正”事件：对成功里程碑进行标记的事件。|发出用户代码和服务的低级别事件。|通常，可以使用此级别进行调试或应用程序优化。<br /><br /> -   已理解消息头。|Administrators<br /><br /> 应用程序开发人员<br /><br /> 产品开发人员。|  
|活动跟踪||处理活动与组件之间的流事件。|此级别允许管理员和开发人员关联同一应用程序域中的各应用程序：<br /><br /> -   活动边界跟踪，如启动\/停止。<br />-   传输跟踪。|全部|  
|全部||应用程序可能工作正常。发出所有事件。|先前的所有事件。|全部|  
  
 从“详细”到“严重”的级别彼此堆叠，即每个跟踪级别都包括其上除“禁用”级别以外的所有级别。例如，在“警告”级别进行侦听的侦听器会接收到“严重”、“错误”和“警告”跟踪。“全部”级别包括从“详细”到“严重”的事件以及活动跟踪事件。  
  
> [!CAUTION]
>  “信息”、“详细”和“ActivityTracing”级别会生成大量跟踪，这可能会对消息吞吐量产生不利影响（如果计算机上的所有可用资源均已用尽）。  
  
## 配置用于关联的活动跟踪和传播  
 为 `switchValue` 属性指定的 `activityTracing` 值用于启用活动跟踪，这会在终结点内发出活动边界跟踪和传输跟踪。  
  
> [!NOTE]
>  如果启用了活动跟踪，则在使用 [!INCLUDE[indigo2](../../../../../includes/indigo2-md.md)] 中的某些扩展功能时，可能会收到 <xref:System.NullReferenceException>。要解决此问题，请检查应用程序配置文件，并确保跟踪源的 `switchValue` 属性未设置为 `activityTracing`。  
  
 `propagateActivity` 属性指示是否应将活动传播到参与消息交换的其他终结点。将此值设置为 `true` 后，可以获取由任意两个终结点生成的跟踪文件，然后观察某一终结点上的一组跟踪是如何流向另一终结点上的一组跟踪的。  
  
 [!INCLUDE[crabout](../../../../../includes/crabout-md.md)]活动跟踪和传播的更多信息，请参见[传播](../../../../../docs/framework/wcf/diagnostics/tracing/propagation.md)。  
  
 `propagateActivity` 和 `ActivityTracing`布尔值均适用于 System.ServiceModel TraceSource。`ActivityTracing`值还适用于任何跟踪源，包括 [!INCLUDE[indigo2](../../../../../includes/indigo2-md.md)] 或用户定义的跟踪源。  
  
 不能将 `propagateActivity` 属性与用户定义的跟踪源一起使用。对于用户代码活动 ID 传播，请确保未设置 ServiceModel `ActivityTracing`，而同时仍将 ServiceModel `propagateActivity` 属性设置为 `true`。  
  
## 请参阅  
 [跟踪](../../../../../docs/framework/wcf/diagnostics/tracing/index.md)   
 [管理和诊断](../../../../../docs/framework/wcf/diagnostics/index.md)   
 [How to: Create and Initialize Trace Listeners（如何：创建和初始化跟踪侦听器）](http://go.microsoft.com/fwlink/?LinkId=94648)   
 [Creating a Custom TraceListener（创建自定义 TraceListener）](http://go.microsoft.com/fwlink/?LinkId=96239)