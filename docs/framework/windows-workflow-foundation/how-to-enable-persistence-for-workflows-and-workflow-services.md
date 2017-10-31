---
title: "如何：对工作流和工作流服务启用持久性 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 2b1c8bf3-9866-45a4-b06d-ee562393e503
caps.latest.revision: 8
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 8
---
# 如何：对工作流和工作流服务启用持久性
本主题说明如何对工作流和工作流服务启用持久性。  
  
## 对工作流启用持久性  
 使用 <xref:System.Activities.WorkflowApplication> 类的 <xref:System.Activities.WorkflowApplication.InstanceStore%2A> 属性，可以将实例存储与 **WorkflowApplication** 相关联。<xref:System.Activities.WorkflowApplication.Persist%2A> 方法将工作流保存或持久保存到与应用程序关联的实例存储中。<xref:System.Activities.WorkflowApplication.Unload%2A> 方法将工作流保存到实例存储中，然后从内存中卸载该实例。**Load** 方法使用实例持久性存储中存储的工作流数据将工作流加载到内存中。  
  
 **Persist** 方法执行下列步骤：  
  
1.  暂停工作流计划程序并等待，直至工作流进入空闲状态。  
  
2.  将工作流持久保存或保存到持久性存储。  
  
3.  恢复工作流计划程序。  
  
 **Unload** 方法执行下列步骤：  
  
1.  暂停工作流计划程序并等待，直至工作流进入空闲状态。  
  
2.  将工作流持久保存或保存到持久性存储。  
  
3.  在内存中释放工作流实例。  
  
 当工作流位于非持久性区域中时，将阻止 **Persist** 和 **Unload** 方法，直到工作流退出非持久性区域为止。在完成非持久性区域之后，该方法将继续执行保存或卸载操作。如果在完成非持久性区域之前发生超时，或者如果持久性进程的时间太长，则将引发 TimeoutException。  
  
## 在代码中启动工作流服务的持久性  
 <xref:System.ServiceModel.WorkflowServiceHost> 类的 **DurableInstancingOptions** 成员具有一个名为 **InstanceStore** 的属性，可用于关联实例存储和 **WorkflowServiceHost**。  
  
```  
  
// wsh is an instance of WorkflowServiceHost class  
wsh.DurableInstancingOptions.InstanceStore = new SqlWorkflowInstanceStore();  
  
```  
  
 打开 **WorkflowServiceHost** 后，如果 **DurableInstancingOptions.InstanceStore** 不为空，则会自动启用持久性。  
  
 通常，服务行为通过使用 **InstanceStore** 属性来提供用于工作流服务主机的具体实例存储。例如，SqlWorkflowInstanceStoreBehavior 创建一个 **SqlWorkflowInstanceStore** 实例，并对其进行配置，然后将其赋给 **DurableInstancingOptions.InstanceStore**。  
  
## 使用应用程序配置文件启用工作流服务的持久性  
 可以通过将以下代码添加到您 app.config 或 web.config 文件使用应用程序配置文件来启用持久性：  
  
```xml  
<configuration>  
  <system.serviceModel>  
    <behaviors>  
      <serviceBehaviors>  
        <behavior name=”myBehavior”>  
          <SqlWorkflowInstanceStore connectionString=”Data Source=myDatatbaseServer;Initial Catalog=myPersistenceDatabase”>  
        </behavior>  
      </serviceBehaviors>  
    <behaviors>  
  </system.serviceModel>  
</configuration>  
  
```