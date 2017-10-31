---
title: "&lt;filters&gt; 的 &lt;add&gt; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: e3bf437c-dd99-49f3-9792-9a8721e6eaad
caps.latest.revision: 4
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 4
---
# &lt;filters&gt; 的 &lt;add&gt;
一个 XPath 筛选器，用于指定要记录的消息的种类。  
  
## 语法  
  
```  
  
<filters>  
   <add filter="String"/>  
</filters>  
```  
  
## 特性和元素  
 下列各节描述了特性、子元素和父元素。  
  
### 特性  
  
|特性|描述|  
|--------|--------|  
|筛选器|一个字符串，用于指定由 XPath 1.0 表达式定义的 XML 文档的查询。  有关详细信息，请参阅<xref:System.ServiceModel.Dispatcher.XPathMessageFilter>。|  
  
### 子元素  
 无。  
  
### 父元素  
  
|元素|描述|  
|--------|--------|  
|[\<筛选器\>](../../../../../docs/framework/configure-apps/file-schema/wcf/filters.md)|包含用于控制所记录的消息类型的 XPath 筛选器集合。|  
  
## 备注  
 如果将 `logMessagesAtTransportLevel` 指定为 `true`，筛选器将只应用于传输层。  筛选器不影响服务级别和格式不正确的消息日志记录。  
  
 若要向集合添加筛选器，请使用 `add` 关键字。  如果定义一个或多个筛选器，则仅记录与其中至少一个筛选器相匹配的消息。  如果未定义任何筛选器，则所有消息都可通过。  
  
 筛选器支持完整的 XPath 语法，并按照其在配置文件中出现的顺序进行应用。  存在语法错误的筛选器会导致配置异常。  
  
 下面的示例演示如何配置一个筛选器，它仅记录具有 SOAP 标头部分的消息。  
  
## 示例  
 下面的示例演示如何配置一个筛选器，它仅记录具有 SOAP 标头部分的消息。  
  
```  
<messageLogging logEntireMessage="true"  
     logMalformedMessages="true" logMessagesAtServiceLevel="true"  
     logMessagesAtTransportLevel="true" maxMessagesToLog="420”>  
     <filters>  
        <add xmlns:soap="http://www.w3.org/2003/05/soap-envelope">  
                        /soap:Envelope/soap:Headers  
        </add>  
     </filters>  
</messageLogging>  
```  
  
## 请参阅  
 <xref:System.ServiceModel.Configuration.DiagnosticSection>   
 <xref:System.ServiceModel.Diagnostics>   
 <xref:System.ServiceModel.Configuration.DiagnosticSection.MessageLogging%2A>   
 <xref:System.ServiceModel.Configuration.MessageLoggingElement>   
 <xref:System.ServiceModel.Configuration.MessageLoggingElement.Filters%2A>   
 <xref:System.ServiceModel.Configuration.XpathMessageFilterElement>   
 <xref:System.ServiceModel.Dispatcher.XPathMessageFilter>   
 [配置消息日志记录](../../../../../docs/framework/wcf/diagnostics/configuring-message-logging.md)   
 [配置消息日志记录](../../../../../docs/framework/wcf/diagnostics/configuring-message-logging.md)   
 [\<messageLogging\>](../../../../../docs/framework/configure-apps/file-schema/wcf/messagelogging.md)