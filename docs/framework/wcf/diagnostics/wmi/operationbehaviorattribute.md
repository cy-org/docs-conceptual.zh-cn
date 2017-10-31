---
title: "OperationBehaviorAttribute | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 8c9b0755-9e83-411f-bdcb-61a586022797
caps.latest.revision: 7
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 7
---
# OperationBehaviorAttribute
OperationBehaviorAttribute  
  
## 语法  
  
```  
class OperationBehaviorAttribute : Behavior  
{  
  boolean AutoDisposeParameters;  
  string Impersonation;  
  string ReleaseInstanceMode;  
  boolean TransactionAutoComplete;  
  boolean TransactionScopeRequired;  
};  
```  
  
## 方法  
 OperationBehaviorAttribute 类不定义任何方法。  
  
## 属性  
 OperationBehaviorAttribute 类具有下列属性：  
  
### AutoDisposeParameters  
 数据类型：Boolean  
  
 访问类型：只读  
  
 参数自动释放功能的状态。  
  
### Impersonation  
 数据类型：String  
  
 访问类型：只读  
  
 指示操作支持的调用方模拟级别。  
  
### ReleaseInstanceMode  
 数据类型：String  
  
 访问类型：只读  
  
 指示操作调用过程中何时回收对象。  
  
### TransactionAutoComplete  
 数据类型：Boolean  
  
 访问类型：只读  
  
 指示在未发生未处理的异常的情况下是否自动提交当前事务。  
  
### TransactionScopeRequired  
 数据类型：Boolean  
  
 访问类型：只读  
  
 指示操作是否需要事务处理。  
  
## 要求  
  
|MOF|已在 Servicemodel.mof 中声明。|  
|---------|------------------------------|  
|命名空间|已在 root\\ServiceModel 中定义|  
  
## 请参阅  
 <xref:System.ServiceModel.OperationBehaviorAttribute>