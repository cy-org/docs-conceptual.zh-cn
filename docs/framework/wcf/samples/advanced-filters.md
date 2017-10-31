---
title: "高级筛选器 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 8d81590f-e036-4f96-824a-4a187f462764
caps.latest.revision: 23
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 23
---
# 高级筛选器
此示例演示 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 路由服务。路由服务是一个 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 组件，使用该组件可方便地在您的应用程序中包含基于内容的路由器。此示例采用标准的 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 计算器示例，使用路由服务进行通信。此示例演示如何使用消息筛选器和消息筛选器表定义基于内容的路由逻辑。  
  
> [!IMPORTANT]
>  您的计算机上可能已安装这些示例。在继续操作之前，请先检查以下（默认）目录。  
>   
>  `<安装驱动器>:\WF_WCF_Samples`  
>   
>  如果此目录不存在，请访问[针对 .NET Framework 4 的 Windows Communication Foundation \(WCF\) 和 Windows Workflow Foundation \(WF\) 示例](http://go.microsoft.com/fwlink/?LinkId=150780)（可能为英文网页），下载所有 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 和 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 示例。此示例位于以下目录：  
>   
>  `<安装驱动器>:\WF_WCF_Samples\WCF\Basic\RoutingServices\AdvancedFilters`  
  
## 示例详细信息  
 下表显示添加到路由服务的消息筛选器表的消息筛选器。  
  
|筛选器|规则|优先级|  
|---------|--------|---------|  
|是否（具有标头）|舍入|2|  
|是否（在 Ep2 上出现）|常规|1|  
|是否（出现时带有 Address2）|舍入|1|  
|是否 \(RoundRobin1\)|常规|0|  
|是否 \(RoundRobin2\)|舍入|0|  
  
 这些消息筛选器和消息筛选器表可通过代码创建和配置，也可在应用程序配置文件中创建和配置。对于此示例，您可找到通过 RoutingService\\routing.cs 文件中的代码定义或在 RoutingService\\App.config 应用程序配置文件中定义的消息筛选器和消息筛选器表。以下各段介绍如何通过代码为此示例创建消息筛选器和消息筛选器表。  
  
 首先，<xref:System.ServiceModel.Dispatcher.XPathMessageFilter> 会查找自定义标头。请注意，<xref:System.ServiceModel.WSHttpBinding> 会产生使用 SOAP 1.2 的信封版本，因此会 XPath 语句会定义为使用 SOAP 1.2 命名空间。<xref:System.ServiceModel.Dispatcher.XPathMessageFilter> 的默认命名空间管理器已为 SOAP 1.2 命名空间定义了一个可以使用的前缀 \/s12。但是，默认命名空间管理器没有客户端用于定义实际标头值的自定义命名空间，因此必须定义前缀。出现时带有此标头的任何消息都与此筛选器匹配。  
  
```  
XPathMessageContext namespaceManager = new XPathMessageContext();  
namespaceManager.AddNamespace("custom", "http://my.custom.namespace/");  
  
XPathMessageFilter xpathFilter = new XPathMessageFilter("/s12:Envelope/s12:Header/custom:RoundingCalculator = 1", namespaceManager);  
  
```  
  
 第二个筛选器是 <xref:System.ServiceModel.Dispatcher.EndpointNameMessageFilter>，与在 `calculatorEndpoint` 上接收到的任何消息匹配。创建服务终结点对象时会定义终结点名称。  
  
```  
EndpointNameMessageFilter endpointNameFilter = new EndpointNameMessageFilter("calculatorEndpoint");  
  
```  
  
 第三个筛选器是 <xref:System.ServiceModel.Dispatcher.PrefixEndpointAddressMessageFilter>。此筛选器与在地址匹配于所提供地址前缀（或前面部分）的终结点上出现的所有消息都匹配。在此示例中，地址前缀定义为“http:\/\/localhost\/routingservice\/router\/rounding\/”。这就是说，此筛选器与发送到“http:\/\/localhost\/routingservice\/router\/rounding\/\*”的所有传入消息都匹配。在本例中，这些消息即是在地址为“http:\/\/localhost\/routingservice\/router\/rounding\/calculator”的舍入计算器终结点上出现的消息。  
  
```  
PrefixEndpointAddressMessageFilter prefixAddressFilter = new PrefixEndpointAddressMessageFilter(new EndpointAddress("http://localhost/routingservice/router/rounding/"));  
  
```  
  
 最后两个消息筛选器是自定义 <xref:System.ServiceModel.Dispatcher.MessageFilter>s.在此示例中，"封合写" 使用消息筛选器。此消息筛选器在提供的 RoutingService\\RoundRobinMessageFilter.cs 文件中创建。这些筛选器设置为同一个组时，会交替报告它们与消息匹配以及不匹配，这样，每次只有其中一个筛选器进行 `true` 响应。  
  
```  
RoundRobinMessageFilter roundRobinFilter1 = new RoundRobinMessageFilter("group1");  
  
RoundRobinMessageFilter roundRobinFilter2 = new RoundRobinMessageFilter("group1");  
  
```  
  
 接下来，所有这些消息都会添加到 <xref:System.ServiceModel.Dispatcher.MessageFilterTable%601>。这样做可指定优先级，以影响消息筛选器表执行筛选器的顺序。筛选器的优先级越高，就会越早执行；筛选器优先级越低，就会越晚执行。因此优先级为 2 的筛选器会在优先级为 1 的筛选器之前执行。如果未指定优先级，则默认优先级为 0。消息筛选器表会先执行给定优先级别的所有筛选器，然后再移动到下一个较低优先级别。如果在特定优先级发现匹配项，则消息筛选器表不会继续尝试在下一个较低优先级查找匹配项。  
  
> [!NOTE]
>  虽然此示例演示如何使用消息筛选器优先级，但一般而言，设计和配置筛选器使之不需要设置优先顺序便可正常运行，这样的设计性能更高且效果更好。  
  
 要添加的第一个筛选器是 XPath 筛选器，其优先级设置为 2。这是执行的第一个消息筛选器。如果该筛选器发现自定义标头，则无论其他筛选器的筛选结果如何，都会将消息路由到舍入计算器终结点。  
  
 添加两个优先级为 1 的筛选器。同样，仅当优先级为 2 的 XPath 筛选器与消息不匹配时，才会运行这两个筛选器。这两个筛选器演示在消息出现时确定其目标位置的两种不同方法。因为这两个筛选器可以有效地检查消息是否到达两个终结点中的一个，所以它们可以按相同优先级别运行，原因是它们不会同时返回 `true`。  
  
 最后，按优先级 0（最低优先级）运行 RoundRobin 消息筛选器。因为这些筛选器配置有相同组名，所以每次只有其中一个筛选器匹配。因为具有自定义标头的所有消息都已路由并发送到特定的虚拟化终结点，所以 RoundRobin 消息筛选器仅处理发送到没有自定义标头的默认路由器终结点的消息。因为这些消息在每次调用时都会启用一个消息，所以一半操作会转到常规计算器终结点，另一半操作会转到舍入计算器终结点。  
  
#### 使用此示例  
  
1.  使用 [!INCLUDE[vs_current_long](../../../../includes/vs-current-long-md.md)] 打开 AdvancedFilters.sln。  
  
2.  若要打开**“解决方案资源管理器”**，请从**“视图”**菜单中选择**“解决方案资源管理器”**。  
  
3.  在 [!INCLUDE[vs_current_short](../../../../includes/vs-current-short-md.md)] 中按 F5 或 Ctrl\+Shift\+B。  
  
    1.  如果希望在按 F5 时自动启动所需的项目，请右击解决方案，然后选择**“属性”**。在左侧窗格中的**“通用属性”**下选择**“启动项目”**。选中**“多启动项目”**单选按钮，并将所有项目设置为具有**“启动”**操作。  
  
    2.  如果使用 Ctrl\+Shift\+B 生成项目，则必须启动以下应用程序：  
  
        1.  计算器客户端 \(.\/CalculatorClient\/bin\/client.exe\)  
  
        2.  计算器服务 \(.\/CalculatorService\/bin\/service.exe\)  
  
        3.  路由计算器服务 \(.\/RoundingCalcService\/bin\/service.exe\)  
  
        4.  路由服务 \(.\/RoutingService\/bin\/RoutingService.exe\)  
  
4.  在计算器客户端的控制台窗口中，按 Enter 启动客户端。客户端将返回可供选择的目标终结点的列表。  
  
5.  键入目标终结点的对应字母并按 ENTER 以选择该终结点。  
  
6.  接下来，客户端将询问您是否要添加自定义标头。按 Y 表示“是”，或按 N 表示“否”，然后按 ENTER。  
  
7.  根据进行的选择，应看到不同的输出。  
  
    1.  如果将自定义标头添加到消息中，则会返回以下输出。  
  
        ```Output  
        Add(100,15.99) = 116  
        Subtract(145,76.54) = 68.5  
        Multiply(9,81.25) = 731.3  
        Divide(22,7) = 3.1  
  
        ```  
  
    2.  如果选择没有自定义标头的舍入计算器终结点，则会返回以下输出。  
  
        ```Output  
        Add(100,15.99) = 116  
        Subtract(145,76.54) = 68.5  
        Multiply(9,81.25) = 731.3  
        Divide(22,7) = 3.1  
  
        ```  
  
    3.  如果选择没有自定义标头的常规计算器终结点，则会返回以下输出。  
  
        ```Output  
        Add(100,15.99) = 115.99  
        Subtract(145,76.54) = 68。46  
        Multiply(9,81.25) = 731.25  
        Divide(22,7) = 3.14285714285714  
  
        ```  
  
    4.  如果选择没有自定义标头的默认路由器终结点，则会返回以下输出。  
  
        ```Output  
        Add(100,15.99) = 116  
        Subtract(145,76.54) = 68.46  
        Multiply(9,81.25) = 731.3  
        Divide(22,7) = 3.14285714285714  
  
        ```  
  
8.  计算器服务和舍入计算器服务也会向其各自的控制台窗口输出调用的操作的日志。  
  
9. 在客户端控制台窗口中，键入 `quit` 并按 ENTER 退出。  
  
10. 在服务控制台窗口中按 ENTER 终止服务。  
  
## 可通过代码或 App.config 进行配置  
 所提供的示例配置为使用 App.config 文件来定义路由器行为。也可将 RoutingService\\App.config 文件的名称更改为另一个名称，使之无法识别，并在 RoutingService\\routing.cs 中取消对 `ConfigureRouterViaCode()` 的方法调用的注释。以上任一方法都可产生相同的路由器行为。  
  
### 方案  
 此示例演示的路由器充当基于内容的路由器，从而可以通过一个终结点公开多种服务类型或实现。  
  
### 实际方案  
 Contoso 希望虚拟化其所有服务以仅公开一个终结点，这些服务通过该终结点可提供对多种不同类型的服务的访问。在这种情况下，这些服务利用路由服务的基于内容的路由功能，以确定应将传入请求发送到哪个位置。  
  
## 请参阅  
 [AppFabric 承载和持久性示例](http://go.microsoft.com/fwlink/?LinkId=193961)