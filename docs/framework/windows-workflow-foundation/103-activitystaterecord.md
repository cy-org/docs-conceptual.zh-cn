---
title: "103 - ActivityStateRecord | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 57636a9a-561e-44aa-aef9-1f1894aaa6dd
caps.latest.revision: 6
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 6
---
# 103 - ActivityStateRecord
## 属性  
  
|||  
|-|-|  
|Id|103|  
|Keywords|EndToEndMonitoring、Troubleshooting、HealthMonitoring、WFTracking|  
|级别|信息|  
|通道|Microsoft\-Windows\-应用程序服务器\-应用程序\/分析|  
  
## 说明  
 当工作流实例中的某个活动发出 ActivityStateRecord 时，ETW 跟踪参与者将发出此事件。  
  
## 消息  
 TrackRecord \= ActivityStateRecord, InstanceID \= %1, RecordNumber\=%2, EventTime\=%3, State \= %4, Name\=%5, ActivityId\=%6, ActivityInstanceId\=%7, ActivityTypeName\=%8, Arguments\=%9, Variables\=%10, Annotations\=%11, ProfileName \= %12  
  
## 详细信息  
  
|数据项名称|数据项类型|说明|  
|-----------|-----------|--------|  
|InstanceId|xs:GUID|工作流的实例 ID|  
|RecordNumber|xs:long|发出的记录的序列号|  
|EventTime|xs:dateTime|发出该事件时的 UTC 时间|  
|State|xs:string|活动的状态|  
|Name|xs:string|发出该事件的活动的显示名称|  
|ActivityId|xs:string|发出的活动的活动 ID|  
|ActivityInstanceId|xs:string|发出的活动的活动实例 ID|  
|ActivityTypeName|xs:string|发出的活动的类型名称|  
|Arguments|xs:string|在此事件中跟踪的参数。这些值存储在一个 xml 元素中，格式为 \<items\>\<\> item  name \= "argumentName" type\="System.String"\<argumentValue\>\<\/item\>\/items。如果未跟踪任何参数，则该字符串包含 \<items\/\>。ETW 事件大小受到 ETW 缓冲区大小或 ETW 事件最大负载的限制。如果事件的大小超出 ETW 限制，则通过丢弃批注并将批注值替换为 \<items\>...\<\/items\> 来截断事件。以下类型以从 ToString\(\) 返回时的值存储：string、char、bool、int、short、long、uint、ushort、ulong、System.Single、float、double、System.Guid、System.DateTimeOffset、System.DateTime。所有其他类型使用 System.Runtime.Serialization.NetDataContractSerializer 进行序列化。|  
|Variables|xs:string|在此事件中跟踪的变量。这些值存储在一个 xml 元素中，格式为 \<items\>\<\> item  name \= "variableName" type\="System.String"\<variableValue\>\<\/item\>\/items。如果未跟踪任何变量，则该字符串包含 \<items\/\>。ETW 事件大小受到 ETW 缓冲区大小或 ETW 事件最大负载的限制。如果事件的大小超出 ETW 限制，则通过丢弃批注并将变量值替换为 \<items\>...\<\/items\> 来截断事件。以下类型以从 ToString\(\) 返回时的值存储：string、char、bool、int、short、long、uint、ushort、ulong、System.Single、float、double、System.Guid、System.DateTimeOffset、System.DateTime。所有其他类型使用 System.Runtime.Serialization.NetDataContractSerializer 进行序列化。|  
|Annotations|xs:string|已添加到此事件中的批注。这些值存储在一个 xml 元素中，格式为 \<items\>\<\> item  name \= "annotationName" type\="System.String"\<annotationValue\>\<\/item\>\/items。如果未指定任何批注，则该字符串包含 \<items\/\>。ETW 事件大小受到 ETW 缓冲区大小或 ETW 事件最大负载的限制。如果事件的大小超出 ETW 限制，则通过丢弃批注并将批注值替换为 \<items\>...\<\/items\> 来截断事件。|  
|ProfileName|xs:string|导致发出此事件的跟踪配置文件的名称|  
|HostReference|xs:string|对于 Web 承载的服务，此字段唯一标识 Web 层次结构中的服务。此字段的格式定义为“网站名称应用程序虚拟路径&#124;服务虚拟路径&#124;服务名称”，示例：“默认网站\/CalculatorApplication&#124;\/CalculatorService.svc&#124;CalculatorService”|  
|AppDomain|xs:string|由 AppDomain.CurrentDomain.FriendlyName 返回的字符串。|