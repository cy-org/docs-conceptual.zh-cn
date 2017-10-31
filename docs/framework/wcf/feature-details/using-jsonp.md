---
title: "使用 JSONP | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: f386718c-b4ba-4931-a610-40c27a46672a
caps.latest.revision: 7
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 7
---
# 使用 JSONP
JSON Padding \(JSONP\) 是一种在 Web 浏览器中启用跨站点脚本支持的机制。  JSONP 是围绕 Web 浏览器的功能而设计的，用于从检索当前所加载文档的站点之外的站点加载脚本。  该机制的工作原理是使用用户定义的回调函数名来填充 JSON 负载，如下面的示例所示。  
  
```  
callback({"a" = \"b\" });  
```  
  
 在上例中，JSON 负载 `{"a" = \"b\"}` 包装在函数调用 `callback` 中。  必须已在当前网页中定义回调函数。  JSONP 响应的内容类型是“application\/javascript”。  
  
## 使用 JSONP  
 JSONP 不会自动启用。  若要启用 JSONP，请在某个 HTTP 标准终结点（<xref:System.ServiceModel.Description.WebHttpEndpoint> 或 <xref:System.ServiceModel.Description.WebScriptEndpoint>）上将 `javascriptCallbackEnabled` 特性设置为 `true`，如下面的示例所示。  
  
```xml  
<system.serviceModel>  
    <standardEndpoints>  
      <webHttpEndpoint>  
        <standardEndpoint name="" javascriptCallbackEnabled="true"/>  
      </webHttpEndpoint>  
    </standardEndpoints>     
  </system.serviceModel>  
```  
  
 可以在称为回调的查询变量中指定回调函数的名称，如下面的 URL 中所示。  
  
```  
http://baseaddress/Service/RestService?callback=functionName  
```  
  
 调用时，该服务将发送如下响应。  
  
```jscript  
functionName({"root":"Something});  
```  
  
 也可以通过对服务类应用 <xref:System.ServiceModel.Web.JavascriptCallbackBehaviorAttribute> 来指定回调函数名称，如下面的示例所示。  
  
```csharp  
[ServiceContract]  
[JavascriptCallbackBehavior(ParameterName = "$callback")]  
public class Service1  
{  
    [OperationContract]  
    [WebGet(ResponseFormat=WebMessageFormat.Json)]  
    public string GetData()  
    {              
    }  
}  
```  
  
 对于上面显示的服务，将发出如下请求。  
  
```  
http://baseaddress/Service/RestService?$callback=anotherFunction  
```  
  
 调用时，该服务通过以下内容进行响应。  
  
```  
anotherFunction ({"root":"Something});  
```  
  
## HTTP 状态代码  
 具有 200 以外的 HTTP 状态代码的 JSONP 响应包括另一个参数，该参数使用 HTTP 状态代码的数字表示形式，如下面的示例所示。  
  
```  
anotherFunction ({"root":"Something}, 201);  
```  
  
## 验证  
 启用 JSONP 后将执行以下验证：  
  
-   如果启用了 `javascriptCallback`，请求中存在回调查询字符串参数，且将响应格式设置为 JSON，WCF 基础结构将引发异常。  
  
-   如果请求包含回调查询字符串参数，但操作不是 HTTP GET，则将忽略回调参数。  
  
-   如果回调名称为 `null` 或空字符串，则响应的格式不会设置为 JSONP。  
  
## 请参阅  
 [WCF Web HTTP 编程模型概述](../../../../docs/framework/wcf/feature-details/wcf-web-http-programming-model-overview.md)