---
title: "分层配置模型 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 28dcc698-226c-4b77-9e51-8bf45a36216c
caps.latest.revision: 12
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 12
---
# 分层配置模型
此示例演示如何实现服务配置文件的层次结构。它还演示如何从层次结构中较高的级别继承绑定、服务行为和终结点行为。  
  
## 示例详细信息  
 为 [!INCLUDE[netfx40_long](../../../../includes/netfx40-long-md.md)] 中的 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 开发的功能之一是分层配置模型中的改进。分层配置模型的一个示例是通过 Machine.config \-\> Rootweb.config \-\> Web.config 定义的模型。在 [!INCLUDE[netfx40_short](../../../../includes/netfx40-short-md.md)] 中，那些在配置层次结构的较高级别中定义的绑定和行为将添加到没有显式配置的服务中。此示例演示如何通过依赖于在计算机或应用程序级别定义的配置元素来简化服务配置。  
  
 此示例包含三个级别的层次结构中定义的九个服务。`Service1` 在根处。`Service2` 和 `Service3` 类继承 `Service1` 中的默认元素。`Service4`、`Service5`、 `Service6` 和 `Service7` 在层次结构的第三层定义，继承 `Service3` 中的默认元素。最后，`Service10` 和 `Service11` 位于层次结构的第四层。  
  
 所有这些服务都实现 `IDesc` 协定。下面是 `IDesc` 接口的定义，它显示了此接口中公开的方法。`IDesc` 接口在 Service1.cs 中定义。  
  
```  
// Define a service contract  
[ServiceContract(Namespace="http://Microsoft.Samples.ConfigHierarchicalModel")]  
public interface IDesc  
{  
    [OperationContract]  
    List<string> ListEndpoints();  
    [OperationContract]  
    List<string> ListServiceBehaviors();  
    [OperationContract]  
    List<string> ListEndpointBehaviors();  
}  
  
```  
  
 这些服务的方法的实现是简单的。`ListEndpoints` 遍历所有服务终结点，并返回该服务的所有终结点的列表。`ListServiceBehaviors` 遍历所有行为添加到服务并返回所有服务行为与服务相关联的列表。`ListEndpointBehaviors` 其行为方式类似于 `ListServiceBehaviors`，但相反，它返回的终结点行为列表。  
  
 通过此实现，客户端可以知道服务公开了多少终结点，以及哪些服务行为和终结点行为已添加到该服务中。已作为该示例的一部分实现的客户端在该解决方案中添加一个对所有服务的服务引用，并为每个服务显示这些元素。  
  
## 使用此示例  
  
#### 运行客户端  
  
1.  使用 [!INCLUDE[vs_current_long](../../../../includes/vs-current-long-md.md)] 打开 ConfigHierarchicalModel.sln 文件。  
  
2.  客户端项目尚未设置为启动项目，请执行下列步骤。  
  
    1.  在**“解决方案资源管理器”**中，右击该解决方案，然后选择**“属性”**。  
  
    2.  在**“通用属性”**中，选择**“启动项目”**，然后单击**“单启动项目”**。  
  
    3.  从**“单启动项目”**下拉列表中选择**“客户端”**。  
  
    4.  单击**“确定”**关闭对话框。  
  
3.  要生成此示例，按 Ctrl\+Shift\+B。  
  
4.  若要运行客户端，请按 Ctrl\+F5。  
  
> [!NOTE]
>  如果这些步骤不起作用，则通过以下步骤来确保已正确设置环境。  
>   
>  1.  请确保已执行 [Windows Communication Foundation 示例的一次性安装过程](../../../../docs/framework/wcf/samples/one-time-setup-procedure-for-the-wcf-samples.md)。  
> 2.  若要生成解决方案，请按照[生成 Windows Communication Foundation 示例](../../../../docs/framework/wcf/samples/building-the-samples.md)中的说明进行操作。  
> 3.  若要用单机配置或多计算机配置来运行示例，请按照[运行 Windows Communication Foundation 示例](../../../../docs/framework/wcf/samples/running-the-samples.md)中的说明进行操作。  
  
> [!IMPORTANT]
>  您的计算机上可能已安装这些示例。在继续操作之前，请先检查以下（默认）目录：  
>   
>  `<安装驱动器>:\WF_WCF_Samples`  
>   
>  如果此目录不存在，请访问[针对 .NET Framework 4 的 Windows Communication Foundation \(WCF\) 和 Windows Workflow Foundation \(WF\) 示例](http://go.microsoft.com/fwlink/?LinkId=150780)（可能为英文网页），下载所有 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 和 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 示例。此示例位于以下目录。  
>   
>  `<安装驱动器>:\WF_WCF_Samples\WCF\Basic\Services\ConfigHierarchicalModel`  
  
## 请参阅  
 [AppFabric 管理示例](http://go.microsoft.com/fwlink/?LinkId=193960)