---
title: "System.Web.Routing 集成 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 31fe2a4f-5c47-4e5d-8ee1-84c524609d41
caps.latest.revision: 7
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 7
---
# System.Web.Routing 集成
在 Internet 信息服务 \(IIS\) 中承载 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 时，需要将一个 .svc 文件放在虚拟目录中。此 .svc 文件应指定所用的服务主机工厂以及实现该服务的类。对服务发出请求时，在 URI 中指定 .svc 文件，例如 http:\/\/contoso.com\/EmployeeServce.svc。对于编写 REST 服务的程序员，此类型的 URI 并非最佳选择。REST 服务的 URI 指定的是特定资源，通常没有任何扩展。<xref:System.Web.Routing> 集成功能可用于承载响应无扩展的 URI 的 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] REST 服务。[!INCLUDE[crabout](../../../../includes/crabout-md.md)] 请参见路由 [ASP.NET 网路由](http://go.microsoft.com/fwlink/?LinkId=184660) 和 [AspNetRouteIntegration](../../../../docs/framework/wcf/samples/aspnetrouteintegration.md) 示例。  
  
## 使用 System.Web.Routing 集成  
 若要使用 <xref:System.Web.Routing> 集成功能，请使用 <xref:System.ServiceModel.Activation.ServiceRoute> 类创建一个或多个路由，然后将这些路由添加到 Global.asax 文件中的 <xref:System.Web.Routing.RouteTable>。这些路由可指定服务所响应的相对 URI。下面的示例演示如何执行此操作。  
  
```  
<%@ Application Language="C#" %>  
<%@ Import Namespace="System.Web.Routing" %>  
<%@ Import Namespace="System.ServiceModel.Activation" %>  
<%@ Import Namespace="System.ServiceModel.Web " %>  
  
<script RunAt="server">  
    void Application_Start(object sender, EventArgs e)  
    {  
        RegisterRoutes(RouteTable.Routes);  
    }  
  
    private void RegisterRoutes(RouteCollection routes)  
    {  
        routes.Add(new ServiceRoute("Customers", new WebServiceHostFactory(), typeof(Service)));   
   }  
</script>  
  
```  
  
 这示例将具有以 Customers 开头的相对 URI 的所有请求路由到 `Service` 服务。  
  
 在 Web.config 文件中，必须添加 `System.Web.Routing.UrlRoutingModule` 模块，将 `runAllManagedModulesForAllRequests` 特性设置为 `true`，以及将 `UrlRoutingHandler` 处理程序添加到 `<system.webServer>` 元素，如下面的示例所示。  
  
```xml  
<system.webServer>  
      <modules runAllManagedModulesForAllRequests="true">  
        <add name="UrlRoutingModule" type="System.Web.Routing.UrlRoutingModule, System.Web, Version=4.0.0.0, Culture=neutral, PublicKeyToken=b03f5f7f11d50a3a" />  
      </modules>  
      <handlers>  
        <add name="UrlRoutingHandler" preCondition="integratedMode" verb="*" path="UrlRouting.axd"/>  
      </handlers>  
    </system.webServer>  
```  
  
 此示例将加载路由所需的模块和处理程序。[!INCLUDE[crdefault](../../../../includes/crdefault-md.md)][路由](../../../../docs/framework/wcf/feature-details/routing.md).另外，还必须在 `<serviceHostingEnvironment>` 元素中将 `aspNetCompatibilityEnabled` 特性设置为 `true`，如下面的示例所示。  
  
```  
<system.serviceModel>  
    <serviceHostingEnvironment aspNetCompatibilityEnabled="true"/>  
        <!-- ... -->  
    </system.serviceModel>  
```  
  
 实现该服务的类必须启用 ASP.NET 兼容性要求，如下面的示例所示。  
  
```  
[ServiceContract]  
[AspNetCompatibilityRequirements(RequirementsMode=AspNetCompatibilityRequirementsMode.Allowed)]  
    public class Service  
    {  
        // ...  
    }  
```  
  
## 请参阅  
 [WCF Web HTTP 编程模型](../../../../docs/framework/wcf/feature-details/wcf-web-http-programming-model.md)   
 [ASP.NET 路由](http://go.microsoft.com/fwlink/?LinkId=184660)