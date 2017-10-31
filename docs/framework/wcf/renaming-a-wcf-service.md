---
title: "重命名 WCF 服务 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 14235a65-b1c5-409d-b6cc-a979acd54bbd
caps.latest.revision: 4
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 4
---
# 重命名 WCF 服务
本主题介绍如何重命名 [!INCLUDE[indigo1](../../../includes/indigo1-md.md)] 服务。  
  
## 重命名 WCF 服务  
 若要在 [!INCLUDE[indigo1](../../../includes/indigo1-md.md)] 模板中重命名服务，请执行以下步骤：  
  
-   更改实现该服务的类的名称。  
  
-   在该服务的配置文件中，将服务的名称更改为选定的新名称，如以下示例中所示。配置文件可以是 app.config 或 web.config 文件，具体取决于宿主模型。  
  
```  
<system.servicemodel>  
   <services>  
      <service name=”WcfService.NewName”>  
      </service>  
   </services>  
</system.servicemodel>  
```  
  
-   如果服务是 Web 承载的，则该服务使用 \*.svc 文件。打开 svc 文件并修改服务的名称，如以下示例中所示。由于没有 svc 文件，因此对于自承载的应用程序来说，此步骤不是必需的。  
  
```  
<%@ ServiceHost Service=”WcfService.NewName”>  
```  
  
## 重命名 WCF 服务协定  
  
-   若要重命名服务协定，请执行下列步骤：  
  
-   更改服务协定的名称。  
  
-   在该服务的配置文件中，将服务协定的名称更改为选定的新名称，如以下示例中所示。配置文件可以是 app.config 或 web.config 文件，具体取决于宿主模型。  
  
```  
<system.servicemodel>  
   <services>  
      <service>  
         <endpoint contract=”WcfService.NewContractName” />  
      </service>  
   </services>  
</system.servicemodel>  
```