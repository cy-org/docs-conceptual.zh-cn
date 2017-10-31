---
title: "承载工作流服务 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 2d55217e-8697-4113-94ce-10b60863342e
caps.latest.revision: 12
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 12
---
# 承载工作流服务
工作流服务在承载后才能对传入消息做出响应。工作流服务使用的是 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 消息传递基础结构，因此承载的方式也类似。工作流服务与 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 服务类似，可以承载于任何托管应用程序、Internet 信息服务 \(IIS\) 或 Windows 进程激活服务 \(WAS\)。此外，工作流服务还可以承载于 Windows Server App Fabric 下。[!INCLUDE[crabout](../../../../includes/crabout-md.md)] Windows Server App Fabric 的更多信息，请参见 [Windows Server App Fabric 文档](http://go.microsoft.com/fwlink/?LinkId=193037)、 [AppFabric 承载功能](http://go.microsoft.com/fwlink/?LinkId=196494) 和 [AppFabric 承载概念](http://go.microsoft.com/fwlink/?LinkId=196495)。[!INCLUDE[crabout](../../../../includes/crabout-md.md)] 到主机的各种方式 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 服务，请参见 [承载服务](../../../../docs/framework/wcf/hosting-services.md)。  
  
## 在托管应用程序中承载  
 若要在托管应用程序中承载工作流服务，请使用 <xref:System.ServiceModel.Activities.WorkflowServiceHost> 类。<xref:System.ServiceModel.Activities.WorkflowServiceHost> 构造函数可用于指定单一工作流服务实例、工作流服务定义或使用工作流消息传递活动的活动。调用 <xref:System.ServiceModel.Activities.WorkflowServiceHost.Open%2A> 将导致服务开始侦听传入消息。  
  
## 在 IIS 或 WAS 下承载  
 在 IIS 或 WAS 下承载工作流服务时，涉及到创建虚拟目录以及将定义服务及其行为的文件放在该虚拟目录中。此时可能出现以下几种情况：  
  
-   将定义工作流服务的 .xamlx 文件放在 IIS\/WAS 虚拟目录中，同时放入指定服务行为、终结点和其他配置元素的 Web.config 文件。  
  
-   将定义工作流服务的 .xamlx 文件放在 IIS\/WAS 虚拟目录中。.xamlx 文件指定要公开的终结点。终结点将在 `WorkflowService.Endpoints` 元素中指定，如下面的示例所示。  
  
    ```  
    <WorkflowService xmlns="http://schemas.microsoft.com/netfx/2009/xaml/servicemodel"  xmlns:p1="http://schemas.microsoft.com/netfx/2009/xaml/activities" xmlns:sad="clr-namespace:System.Activities.Debugger;assembly=System.Activities" xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml">  
      <WorkflowService.Endpoints>  
        <Endpoint ServiceContractName="IWorkFlowEchoService" AddressUri="">  
          <Endpoint.Binding>  
            <BasicHttpBinding />  
          </Endpoint.Binding>  
        </Endpoint>  
      </WorkflowService.Endpoints>  
    <!-- ... -->  
    </WorkflowService>  
  
    ```  
  
    > [!NOTE]
    >  不能在 .xamlx 文件中指定行为，因此，如果需要指定行为设置，则必须使用 Web.config。  
  
-   将定义工作流服务的 .xamlx 文件放在一个 IIS\/WAS 虚拟目录中。另外，将一个 .svc 文件放在该虚拟目录中。使用 .svc 文件可以指定自定义 Web 服务主机工厂、应用自定义行为或者从自定义位置加载配置。  
  
-   将一个程序集放在 IIS\/WAS 虚拟目录中，该程序集包含一个使用 WCF 消息传递活动的活动。  
  
 定义工作流服务的 .xamlx 文件必须包含 \<`Service`\> 根元素或包含派生自 <xref:System.Workflow.ComponentModel.Activity> 的任何类型的根元素。使用 [!INCLUDE[vs_current_long](../../../../includes/vs-current-long-md.md)] 活动模板时将创建 .xamlx 文件，使用 WCF 工作流服务模板时将创建 .xamlx 文件。  
  
## 在 Windows Server App Fabric 下承载工作流服务  
 在 Windows Server App Fabric 下承载工作流服务的方式与在 IIS\/WAS 下的承载方式相同。唯一区别在于会安装 Windows Server App Fabric。Windows Server App Fabric 提供了添加到 Internet 信息服务管理器的工具，以及 powershell commandlets。这些工具可简化工作流服务和 WCF 服务的部署、管理和跟踪。.[!INCLUDE[crabout](../../../../includes/crabout-md.md)] Windows Server App Fabric 的更多信息，请参见 [Windows Server App Fabric](http://go.microsoft.com/fwlink/?LinkId=193037)  
  
## 引用自定义活动  
 必须将对自定义活动的引用添加到 \<`Assemblies`\> 节中的 \<`System.Web.Compilation`\> 下面，以便将这些引用加载到应用程序域，并且 XAML 反序列化程序能够找到各类型。可以在应用程序级别进行这些设置；如果要将这些设置应用于计算机上的所有应用程序，则可在根 Web.config 中进行这些设置。  
  
## 部署  
 系统中已经创建 Web 部署工具，以方便部署作业。通过使用该工具，可以在 IIS 6.0 和 IIS 7.0 之间迁移应用程序，同步服务器场，并打包、存档和部署 Web 应用程序。[!INCLUDE[crdefault](../../../../includes/crdefault-md.md)][MS 部署工具](http://go.microsoft.com/fwlink/?LinkId=178690)  
  
## 请参阅  
 [工作流服务主机内部机制](../../../../docs/framework/wcf/feature-details/workflow-service-host-internals.md)   
 [配置 WorkflowServiceHost](../../../../docs/framework/wcf/feature-details/configuring-workflowservicehost.md)