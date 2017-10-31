---
title: "Optimization for Shared Web Hosting | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-standard"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "garbage collection, Web hosting"
  - "garbage collection, optimizing"
  - "garbage collection, shared Web hosting"
ms.assetid: be98c0ab-7ef8-409f-8a0d-cb6e5b75ff20
caps.latest.revision: 8
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 8
---
# Optimization for Shared Web Hosting
如果您是通过承载若干个小型网站来共享的服务器的管理员，则可向 .NET Framework 目录下 Aspnet.config 文件中的 `runtime` 节点中添加以下 `gcTrimCommitOnLowMemory` 设置，以优化性能并增加网站容量：  
  
 `<gcTrimCommitOnLowMemory enabled="true|false"/>`  
  
> [!NOTE]
>  建议只将此设置用于共享 Web 宿主的情况。  
  
 由于垃圾回收器会保留内存以供将来分配，因此其提交空间可能多于真正需要的空间。  可以减小此空间，以适应系统内存负载较大的情况。  减小此提交空间可以提高性能并扩展容量，以承载更多站点。  
  
 启用 `gcTrimCommitOnLowMemory` 设置后，垃圾回收器将评估系统内存负载，并在负载达到 90% 时进入修整模式。  垃圾回收器将一直处于修整模式，直到负载下降到 85% 以下。  
  
 当情况允许时，垃圾回收器可以确定 `gcTrimCommitOnLowMemory` 设置对当前应用程序没有帮助，并将其忽略。  
  
## 示例  
 下面的 XML 片段演示如何启用 `gcTrimCommitOnLowMemory` 设置。  椭圆指示将在 `runtime` 节点中的其他设置。  
  
```  
<?xml version="1.0" encoding="UTF-8"?>  
<configuration>  
    <runtime>  
    . . .  
    <gcTrimCommitOnLowMemory enabled="true"/>  
    </runtime>  
    . . .  
</configuration>  
```  
  
## 请参阅  
 [Garbage Collection](../../../docs/standard/garbage-collection/index.md)