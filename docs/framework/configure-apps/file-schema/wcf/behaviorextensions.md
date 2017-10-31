---
title: "&lt;behaviorExtensions&gt; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 59f2791a-c78f-40d7-aa80-0d9cd10135d9
caps.latest.revision: 9
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 9
---
# &lt;behaviorExtensions&gt;
用户可以使用行为扩展来创建用户定义的行为元素。  这些元素可与标准的 Windows Communication Foundation \(WCF\) 行为元素一起使用。  `behaviorExtensions` 节定义了元素，使其可用于配置中。  下面是一个典型的行为扩展示例。  
  
```  
<system.serviceModel>  
    <extensions>  
        <behaviorExtensions>  
            <add name="myBehavior" type="Microsoft.ServiceModel.Samples.MyBehaviorSection, MyBehavior,  
                Version=1.0.0.0, Culture=neutral, PublicKeyToken=null" />  
       </behaviorExtensions>  
    </extensions>  
</system.serviceModel>  
```  
  
 若要向元素添加配置功能，需要编写和注册配置元素。  有关这方面的更多信息，请参见 <xref:System.Configuration> 文档。  
  
 在定义元素及其配置类型之后，可以使用扩展，如以下示例所示。  
  
```  
<behaviors>  
    <behavior configurationName="testChannelBehavior">  
        <myBehavior />  
        <channelSecurity cacheCookies="false" detectReplays="false" maxCachedNonces="9"  
            maxClockSkew="00:00:03" maxCookieCachingTime="00:07:24" replayWindow="00:07:22.2190000" />  
    </behavior>  
</behaviors>  
```  
  
## 安全性  
 强烈建议在 `machine.config` 和 `app.config` 文件中注册类型时使用完全限定的程序集名称。  如果没有唯一定义类型，则 CLR 类型加载程序将按照指定的顺序在以下位置中搜索类型：  
  
 如果已经知道类型的程序集，则加载程序将搜索配置文件的重定向位置、GAC、使用配置信息的当前程序集以及应用程序基目录。  如果程序集未知，则加载程序将搜索当前程序集、mscorlib 以及 `TypeResolve` 事件处理程序返回的位置。  通过使用“类型转发”机制和 AppDomain.TypeResolve 事件之类的挂钩，可以修改此 CLR 搜索顺序。  
  
 攻击者可以利用 CLR 搜索顺序来执行未授权的代码。  通过使用完全限定的（强）名称，可以唯一标识类型并进一步提高系统的安全性。  
  
 有关更多信息，请参见[运行时如何定位程序集](http://go.microsoft.com/fwlink/?LinkId=95336)（可能为英文网页）和 <xref:System.AppDomain.TypeResolve>。  
  
## 请参阅  
 <xref:System.ServiceModel.Configuration.BehaviorExtensionElement>   
 [使用行为配置和扩展运行时](../../../../../docs/framework/wcf/extending/configuring-and-extending-the-runtime-with-behaviors.md)