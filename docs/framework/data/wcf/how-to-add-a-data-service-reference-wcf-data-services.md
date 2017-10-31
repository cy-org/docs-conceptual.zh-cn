---
title: "如何：添加数据服务引用（WCF 数据服务） | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-oob"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "WCF 数据服务, 配置"
ms.assetid: 62c6f318-3ee1-433a-b7a3-efa234c3034c
caps.latest.revision: 2
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 2
---
# 如何：添加数据服务引用（WCF 数据服务）
可以使用 Visual Studio 中的**“添加服务引用”**对话框添加对 [!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)] 的引用。  这使您可以更轻松地在使用 Visual Studio 开发的客户端应用程序中访问数据服务。  完成此过程后，会基于从数据服务获取的元数据生成数据类。  有关详细信息，请参阅[生成数据服务客户端库](../../../../docs/framework/data/wcf/generating-the-data-service-client-library-wcf-data-services.md)。  
  
### 添加数据服务引用  
  
1.  （可选）如果数据服务不是解决方案的一部分，且未运行，请启动数据服务，并记下数据服务的 URI。  
  
2.  右击客户端项目，然后选择**“添加服务引用”**。  
  
3.  如果数据服务是当前解决方案的一部分，请单击**“发现”**。  
  
     \- 或 \-  
  
     在**“地址”**文本框中，键入数据服务的基 URL，例如 `http://localhost:1234/Northwind.svc`，然后单击**“转到”**。  
  
4.  单击“确定”。  
  
     这样会添加一个新的代码文件，该文件包含用于访问作为对象的数据服务资源并与其交互的数据类。  
  
## 请参阅  
 [快速入门](../../../../docs/framework/data/wcf/quickstart-wcf-data-services.md)