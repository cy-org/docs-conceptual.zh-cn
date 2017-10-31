---
title: "Operation 类 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: b19d1496-ef06-4d0c-b2ae-e728ec00cca0
caps.latest.revision: 8
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 8
---
# Operation 类
Operation  
  
## 语法  
  
```  
class Operation  
{  
  string Action;  
  boolean AsyncPattern;  
  Behavior Behaviors[];  
  boolean IsCallback;  
  boolean IsInitiating;  
  boolean IsOneWay;  
  boolean IsTerminating;  
  string MethodSignature;  
  string Name;  
  string ParameterTypes[];  
  string ReplyAction;  
  string ReturnType;  
};  
```  
  
## 方法  
 Operation 类不定义任何方法。  
  
## 属性  
 Operation 类具有下列属性：  
  
### Action  
 数据类型：String  
  
 访问类型：只读  
  
 请求消息的 WS\-Addressing 操作。  
  
### AsyncPattern  
 数据类型：Boolean  
  
 访问类型：只读  
  
 指示使用服务协定中的 `Begin` \[左\/右尖括号\] 和 `End` \[左\/右尖括号\] 方法对异步实现某个操作。  
  
### Behaviors  
 数据类型：Behavior array  
  
 访问类型：只读  
  
 与此操作关联的行为。  
  
### IsCallback  
 数据类型：Boolean  
  
 访问类型：只读  
  
 如果操作为回调操作，则为 True。  
  
### IsInitiating  
 数据类型：Boolean  
  
 访问类型：只读  
  
 指示方法是否实现了可以启动服务器上的某个会话的操作。  
  
### IsOneWay  
 数据类型：Boolean  
  
 访问类型：只读  
  
 指示操作是否返回答复消息。  
  
### IsTerminating  
 数据类型：Boolean  
  
 访问类型：只读  
  
 指示操作是否返回答复消息。  
  
### MethodSignature  
 数据类型：String  
  
 访问类型：只读  
  
 操作的方法签名。  
  
### Name  
 数据类型：String  
  
 访问类型：只读  
  
 操作的名称。  
  
### ParameterTypes  
 数据类型：String array  
  
 访问类型：只读  
  
 操作的参数类型。  
  
### ReplyAction  
 数据类型：String  
  
 访问类型：只读  
  
 用于该操作答复消息的 SOAP 操作的值。  
  
### ReturnType  
 数据类型：String  
  
 访问类型：只读  
  
 操作的返回类型。  
  
## 要求  
  
|MOF|已在 Servicemodel.mof 中声明。|  
|---------|------------------------------|  
|命名空间|已在 root\\ServiceModel 中定义|  
  
## 请参阅  
 <xref:System.ServiceModel.Description.OperationDescription>