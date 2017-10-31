---
title: "Contract | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: aa00f6b3-7e1f-4213-841a-206463fca20b
caps.latest.revision: 7
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 7
---
# Contract
Contract  
  
## 语法  
  
```  
class Contract  
{  
  sint32 AppDomainId;  
  Behavior Behaviors[];  
  string Name;  
  string Namespace;  
  Operation Operations[];  
  sint32 ProcessId;  
  Contract ref;  
  string SessionMode;  
  string Type;  
};  
```  
  
## 方法  
 Contract 类不定义任何方法。  
  
## 属性  
 Contract 类具有下列属性：  
  
### AppDomainId  
 数据类型：sint32  
  
 访问类型：只读  
  
 承载协定的 appdomain 的 appdomain ID。  
  
### Behaviors  
 数据类型：Behavior array  
  
 访问类型：只读  
  
 与此协定关联的行为。  
  
### Name  
 数据类型：String  
  
 访问类型：只读  
  
 WSDL 中协定的名称。  
  
### 命名空间  
 数据类型：String  
  
 访问类型：只读  
  
 WSDL 中 `portType` 元素的命名空间。  
  
### Operations  
 数据类型：操作数组  
  
 访问类型：只读  
  
 此协定的操作。  
  
### ProcessId  
 数据类型：sint32  
  
 访问类型：只读  
  
 承载此协定的进程的进程 ID。  
  
### ref  
 数据类型：Contract  
  
 访问类型：只读  
  
 协定为双工协定时的回调类型。  
  
### SessionMode  
 数据类型：String  
  
 访问类型：只读  
  
 指示协定是否要求与此协定关联的绑定来使用通道会话。  
  
### Type  
 数据类型：String  
  
 访问类型：只读  
  
 协定的类型。  
  
## 要求  
  
|MOF|已在 Servicemodel.mof 中声明。|  
|---------|------------------------------|  
|Namespace|已在 root\\ServiceModel 中定义|  
  
## 请参阅  
 <xref:System.ServiceModel.Description.ContractDescription>