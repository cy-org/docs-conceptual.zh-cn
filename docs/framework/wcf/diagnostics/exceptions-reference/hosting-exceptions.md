---
title: "承载异常 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: ad9e14f8-fa17-4d59-b365-fe0e7ec17c98
caps.latest.revision: 5
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 5
---
# 承载异常
本主题列出了由承载生成的所有异常。  
  
## 异常列表  
  
|资源代码|资源字符串|  
|----------|-----------|  
|Hosting\_AddressIsAbsoluteUri|不允许完整的 URI。对于 ServiceHostingEnvironment.EnsureServiceAvailable API，不允许完整的 URI。对相应的服务使用虚拟路径。|  
|Hosting\_BuildProviderCouldNotCreateType|在服务编译期间，无法加载指定的 CLR 类型。请确认此类型或者是在位于应用程序的 \\\\App\_Code 目录中的源文件中定义的（包含在位于应用程序的 \\\\bin 目录中的已编译程序集中），或者存在于安装在 Global Assembly Cache 中的程序集中。类型名区分大小写。诸如 \\\\App\_Code 和 \\\\bin 这样的目录必须位于应用程序的根目录中。\\\\App\_Code 和 \\\\bin 目录不能嵌套在子目录中。|