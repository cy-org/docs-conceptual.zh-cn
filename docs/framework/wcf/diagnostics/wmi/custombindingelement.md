---
title: "CustomBindingElement | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: df959dc5-1aef-4338-a123-6ff3e7bc37af
caps.latest.revision: 9
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 9
---
# CustomBindingElement
CustomBindingElement  
  
## 语法  
  
```  
class CustomBindingElement : BindingElement  
{  
  string Name;  
};  
```  
  
## 方法  
 CustomBindingElement 类未定义任何方法。  
  
## 属性  
 CustomBindingElement 类具有以下属性：  
  
### 名称  
 数据类型：String  
  
 访问类型：只读  
  
 一个包含绑定的配置名称的字符串。  此值是用户定义的一个字符串，可充当自定义绑定的标识字符串。  
  
## 要求  
  
|MOF|已在 Servicemodel.mof 中声明。|  
|---------|------------------------------|  
|命名空间|已在 root\\ServiceModel 中定义|  
  
## 请参阅  
 <xref:System.ServiceModel.Channels.CustomBinding>