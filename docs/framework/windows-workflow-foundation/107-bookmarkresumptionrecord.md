---
title: "107 -- BookmarkResumptionRecord | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: aa2d37ed-2bfa-439b-89e8-a9354027f155
caps.latest.revision: 5
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 5
---
# 107 -- BookmarkResumptionRecord
## 属性  
  
|||  
|-|-|  
|Id|107|  
|关键字|EndToEndMonitoring、Troubleshooting、HealthMonitoring、WFTracking|  
|级别|信息|  
|通道|Microsoft\-Windows\-应用程序服务器\-应用程序\/分析|  
  
## 说明  
 在工作流实例发出 BookmarkResumptionRecord 时，ETW 跟踪参与者将发出此事件。  
  
## 消息  
 TrackRecord \= BookmarkResumptionRecord, InstanceID\=%1, RecordNumber\=%2,EventTime\=%3, Name\=%4, SubInstanceID\=%5,  OwnerActivityName\=%6, OwnerActivityId \=%7, OwnerActivityInstanceId\=%8, OwnerActivityTypeName\=%9, Annotations\=%10, ProfileName \= %11  
  
## 详细信息  
  
|数据项名称|数据项类型|说明|  
|-----------|-----------|--------|  
|InstanceId|xs:GUID|工作流的实例 ID|  
|RecordNumber|xs:long|发出的记录的序列号|  
|EventTime|xs:dateTime|发出该事件时的 UTC 时间|  
|Name|xs:string|继续的书签的名称|  
|SubInstanceID|xs:GUID|书签范围的 ID|  
|OwnerActivityName|xs:string|书签活动的名称|  
|OwnerActivityId|xs:string|书签活动的 ID|  
|OwnerActivityInstanceId|xs:string|书签活动的实例 ID|  
|OwnerActivityTypeName|xs:string|书签活动的类型|  
|Annotations|xs:string|已添加到此事件中的批注。这些值存储在一个 xml 元素中，格式为 \<items\>\<\> item  name \= "annotationName" type\="System.String"\<annotationValue\>\<\/item\>\/items。如果未指定任何批注，则该字符串包含 \<items\/\>。ETW 事件大小受到 ETW 缓冲区大小或 ETW 事件最大负载的限制。如果事件的大小超出 ETW 限制，则通过丢弃批注并将批注值替换为 \<items\>...\<\/items\> 来截断事件。|  
|ProfileName|xs:string|导致发出此事件的跟踪配置文件的名称|  
|HostReference|xs:string|对于 Web 承载的服务，此字段唯一标识 Web 层次结构中的服务。此字段的格式定义为“网站名称应用程序虚拟路径&#124;服务虚拟路径&#124;服务名称”，示例：“默认网站\/CalculatorApplication&#124;\/CalculatorService.svc&#124;CalculatorService”|  
|AppDomain|xs:string|由 AppDomain.CurrentDomain.FriendlyName 返回的字符串。|