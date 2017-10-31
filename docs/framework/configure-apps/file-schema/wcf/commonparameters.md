---
title: "&lt;commonParameters&gt; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: ffc20832-34d6-4622-8174-81924fd53514
caps.latest.revision: 6
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 6
---
# &lt;commonParameters&gt;
表示在多个服务之间全局使用的参数的集合。  此集合通常将包括可由持久性服务共享的数据库连接字符串。  
  
## 语法  
  
```  
  
<workflowRuntime>  
   <commonParameters>  
      <add name="String" value="String" />  
   </commonParameters>  
</workflowRuntime>  
```  
  
## 特性和元素  
 下列各节描述了特性、子元素和父元素。  
  
### 特性  
 无。  
  
### 子元素  
  
|元素|描述|  
|--------|--------|  
|[\<添加\>](../../../../../docs/framework/configure-apps/file-schema/wcf/add-of-commonparameters.md)|将服务使用的公共参数的名称\/值对添加到集合。|  
  
### 父元素  
  
|元素|描述|  
|--------|--------|  
|[\<workflowRuntime\>](../../../../../docs/framework/configure-apps/file-schema/wcf/workflowruntime.md)|指定用于承载基于工作流的 [!INCLUDE[indigo1](../../../../../includes/indigo1-md.md)] 服务的 <xref:System.Workflow.Runtime.WorkflowRuntime> 实例的设置。|  
  
## 备注  
 `<commonParameters>` 元素定义在多个服务之间全局使用的任何参数，例如，使用 <xref:System.Workflow.Runtime.Hosting.SharedConnectionWorkflowCommitWorkBatchService> 时的`ConnectionString`。  
  
> [!NOTE]
>  如果在 `<commonParameters>` 一节中指定了 `ConnectionString` 值，则 SQL Tracking 服务并不始终使用该值。  它的某些操作可能会失败，例如检索 `StateMachineWorkflowInstance.StateHistory` 属性。  若要解决此问题，请在跟踪提供程序的配置节指定 `ConnectionString` 属性，如下面的示例所示。  
  
 `<add`  
  
 `type="System.Workflow.Runtime.Tracking.SqlTrackingService, System.Workflow.Runtime, Version=3.0.00000.0, Culture=neutral, PublicKeyToken=31bf3856ad364e35"`  
  
 `ConnectionString="Data Source=localhost;Initial Catalog=Partner20WFTP;Integrated Security=True;" />`  
  
 对于提交批处理工作进行永久性存储的服务，如 <xref:System.Workflow.Runtime.Hosting.DefaultWorkflowCommitWorkBatchService> 和 <xref:System.Workflow.Runtime.Hosting.SqlWorkflowPersistenceService>，可以通过使用 `EnableRetries` 参数来允许它们重试其事务，如以下示例所示：  
  
```  
<WorkflowRuntime Name="SampleApplication" UnloadOnIdle="false">  
    <commonParameters>  
        <add name="ConnectionString" value="Initial Catalog=WorkflowStore;Data Source=localhost;Integrated Security=SSPI;" />  
        <add name="EnableRetries" value="True" />  
    </commonParameters>  
    <Services>  
        <add type="System.Workflow.Runtime.Hosting.SqlWorkflowPersistenceService, System.Workflow.Runtime, Version=3.0.00000.0, Culture=neutral, PublicKeyToken=31bf3856ad364e35" EnableRetries="False" />   
     </Services>  
</WorkflowRuntime>  
```  
  
 请注意，`EnableRetries` 参数可以在全局级设置（如 *CommonParameters* 一节中所示），也可以为支持 `EnableRetries` 的个别服务设置（如 *Services* 一节中所示）。  
  
 下面的示例代码演示如何通过编程方式更改公共参数。  
  
```  
Configuration config=WebConfigurationManager.OpenWebConfiguration("/Workflow", "Default Web Site", null, "localhost");  
WorkflowRuntimeSection wfruntime=config.GetSection("WorkflowRuntime") as WorkflowRuntimeSection;  
NameValueConfigurationCollection commonParameters=wfruntime.CommonParameters;  
commonParameters["ConnectionString"].Value="another connection string";  
config.Save();  
```  
  
 有关使用配置文件控制 Windows Workflow Foundation 主机应用程序的 <xref:System.Workflow.Runtime.WorkflowRuntime> 对象的更多信息，请参见[Workflow Configuration Files](http://msdn.microsoft.com/zh-cn/ada4bb90-6c9d-4f3d-a9d0-b559bb0f9909)。  
  
## 示例  
  
```  
<commonParameters>  
   <add name="ConnectionString" value="Initial Catalog=WorkflowStore;Data Source=localhost;Integrated Security=SSPI;"/>  
   <add name="EnableRetries" value="true"/>  
</commonParameters>  
```  
  
## 请参阅  
 <xref:System.ServiceModel.Configuration.WorkflowRuntimeElement>   
 <xref:System.Workflow.Runtime.Configuration.WorkflowRuntimeServiceElement>   
 <xref:System.Workflow.Runtime.WorkflowRuntime>   
 <xref:System.Workflow.Runtime.Hosting.DefaultWorkflowCommitWorkBatchService>   
 <xref:System.Workflow.Runtime.Hosting.SqlWorkflowPersistenceService>   
 [Workflow Configuration Files](http://msdn.microsoft.com/zh-cn/ada4bb90-6c9d-4f3d-a9d0-b559bb0f9909)   
 [\<添加\>](../../../../../docs/framework/configure-apps/file-schema/wcf/add-of-commonparameters.md)