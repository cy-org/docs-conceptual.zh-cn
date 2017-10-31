---
title: "&lt;commonParameters&gt; 的 &lt;add&gt; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 3713bf25-20c8-455f-bb85-de46b6487932
caps.latest.revision: 5
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 5
---
# &lt;commonParameters&gt; 的 &lt;add&gt;
指定在多个服务之间全局使用的参数的名称\/值对。  此参数通常包括可由持久性服务共享的数据库连接字符串。  
  
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
  
|特性|描述|  
|--------|--------|  
|name|为服务指定的参数的名称。|  
|值|为服务指定的参数的值。|  
  
### 子元素  
 无。  
  
### 父元素  
  
|元素|描述|  
|--------|--------|  
|[\<commonParameters\>](http://msdn.microsoft.com/zh-cn/d0e1e6fc-985a-4713-b7da-194e30dfab4c)|服务使用的公用参数的集合。  此集合通常将包括可由持久性服务共享的数据库连接字符串。|  
  
## 备注  
 `<commonParameters>` 元素定义在多个服务之间全局使用的任何参数，例如，使用 <xref:System.Workflow.Runtime.Hosting.SharedConnectionWorkflowCommitWorkBatchService> 时的`ConnectionString`。  
  
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
  
 有关使用配置文件控制 Windows Workflow Foundation 主机应用程序的 <xref:System.Workflow.Runtime.WorkflowRuntime> 对象的行为的更多信息，请参见[Workflow Configuration Files](http://msdn.microsoft.com/zh-cn/ada4bb90-6c9d-4f3d-a9d0-b559bb0f9909)。  
  
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
 [\<commonParameters\>](http://msdn.microsoft.com/zh-cn/d0e1e6fc-985a-4713-b7da-194e30dfab4c)