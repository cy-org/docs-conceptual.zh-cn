---
title: "TransactionFlowBindingElement | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 0a9656fe-2400-45ca-ad79-92715c8cf190
caps.latest.revision: 8
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 8
---
# TransactionFlowBindingElement
TransactionFlowBindingElement  
  
## 语法  
  
```  
class TransactionFlowBindingElement : BindingElement  
{  
  string IssuedTokens;  
  string TransactionProtocol;  
  boolean Transactions;  
};  
```  
  
## 方法  
 TransactionFlowBindingElement 类未定义任何方法。  
  
## 属性  
 TransactionFlowBindingElement 类具有以下属性：  
  
### IssuedTokens  
 数据类型：String  
  
 访问类型：只读  
  
 指定对已颁发的安全令牌标头（来自 WS\-Trust 的 IssuedTokens）的要求。  
  
### TransactionProtocol  
 数据类型：String  
  
 访问类型：只读  
  
 对事务进行流处理时使用的事务处理协议。  
  
### Transactions  
 数据类型：Boolean  
  
 访问类型：只读  
  
 指示是否支持传入事务。  
  
## 要求  
  
|MOF|已在 Servicemodel.mof 中声明。|  
|---------|------------------------------|  
|命名空间|已在 root\\ServiceModel 中定义|  
  
## 请参阅  
 <xref:System.ServiceModel.Channels.TransactionFlowBindingElement>