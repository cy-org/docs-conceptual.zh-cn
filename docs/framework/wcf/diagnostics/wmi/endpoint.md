---
title: "终结点 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: fe63370d-81a1-40f3-97c2-59cb357c78d2
caps.latest.revision: 9
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 9
---
# 终结点
终结点  
  
## 语法  
  
```  
class Endpoint  
{  
  string Address;  
  string AddressHeaders[];  
  string AddressIdentity;  
  sint32 AppDomainId;  
  Behavior Behaviors[];  
  Binding Binding;  
  string ContractName;  
  string CounterInstanceName;  
  string ListenUri;  
  string Name;  
  sint32 ProcessId;  
  Contract ref;  
};  
```  
  
## 方法  
 该终结点类定义以下方法。  
  
|方法|描述|  
|--------|--------|  
|[GetOperationCounterInstanceName](../../../../../docs/framework/wcf/diagnostics/wmi/getoperationcounterinstancename.md)|检索操作性能计数器实例名称|  
  
## 属性  
 该终结点类具有以下属性：  
  
### Address  
 数据类型：String  
  
 访问类型：只读  
  
 一个包含终结点地址的 URI。  
  
### AddressHeaders  
 数据类型：String array  
  
 访问类型：只读  
  
 附加到此终结点的地址头的集合。  
  
### AddressIdentity  
 数据类型：String  
  
 访问类型：只读  
  
 终结点的标识。  
  
### AppDomainId  
 数据类型：sint32  
  
 访问类型：只读  
  
 承载终结点的 AppDomain 的 AppDomain ID。  
  
### 行为  
 数据类型：Behavior array  
  
 访问类型：只读  
  
 此终结点所实现的行为的集合。  
  
### 绑定  
 数据类型：绑定  
  
 访问类型：只读  
  
 此终结点所使用的绑定。  
  
### ContractName  
 数据类型：String  
  
 访问类型：只读  
  
 一个字符串，指定此终结点公开了哪个协定。  
  
### CounterInstanceName  
 数据类型：String  
  
 访问类型：只读  
  
 该终结点的性能计数器的实例名称。  
  
### ListenUri  
 数据类型：String  
  
 访问类型：只读  
  
 终结点在其上侦听的 Uri。  
  
### 名称  
 数据类型：String  
  
 访问类型：只读  
  
 此终结点的唯一名称。  
  
### ProcessId  
 数据类型：sint32  
  
 访问类型：只读  
  
 承载该终结点的进程的进程 ID。  
  
### ref  
 数据类型：Contract  
  
 访问类型：只读  
  
 此终结点公开的协定。  
  
## 要求  
  
|MOF|已在 Servicemodel.mof 中声明。|  
|---------|------------------------------|  
|命名空间|已在 root\\ServiceModel 中定义|