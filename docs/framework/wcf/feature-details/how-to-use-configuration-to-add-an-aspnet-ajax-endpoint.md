---
title: "如何：使用配置来添加 ASP.NET AJAX 终结点 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 7cd0099e-dc3a-47e4-a38c-6e10f997f6ea
caps.latest.revision: 14
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 14
---
# 如何：使用配置来添加 ASP.NET AJAX 终结点
[!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 允许您创建一个服务来提供一个支持 ASP.NET AJAX 的终结点，并且可以从客户端 Web 站点上的 JavaScript 中调用该终结点。若要创建这样的终结点，可以使用配置文件（与使用所有其他 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 终结点一样），或使用不要求任何配置元素的方法。本主题演示配置方法。  
  
 使服务终结点成为支持 ASP.NET AJAX 的终结点的部分过程包括：配置终结点以使用 <xref:System.ServiceModel.WebHttpBinding> 以及添加 [\<enableWebScript\>](../../../../docs/framework/configure-apps/file-schema/wcf/enablewebscript.md) 终结点行为。配置终结点后，实现和承载服务的步骤与任何 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 服务使用的步骤类似。有关可运行示例，请参见[使用 HTTP POST 的 AJAX 服务](../../../../docs/framework/wcf/samples/ajax-service-using-http-post.md)。  
  
 [!INCLUDE[crabout](../../../../includes/crabout-md.md)]如何在不使用配置的情况下配置 ASP.NET AJAX 终结点的更多信息，请参见[如何：在不使用配置的情况下添加 ASP.NET AJAX 终结点](../../../../docs/framework/wcf/feature-details/how-to-add-an-aspnet-ajax-endpoint-without-using-configuration.md)。  
  
### 创建基本 WCF 服务  
  
1.  通过用 <xref:System.ServiceModel.ServiceContractAttribute> 属性标记的接口定义基本 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 服务协定。用 <xref:System.ServiceModel.OperationContractAttribute> 标记每个操作。确保设置 <xref:System.ServiceModel.ServiceContractAttribute.Namespace%2A> 属性。  
  
    ```  
    [ServiceContract(Namespace = "MyService")]  
    public interface ICalculator  
    {  
        [OperationContract]  
         // This operation returns the sum of d1 and d2.  
        double Add(double n1, double n2);  
  
        //Other operations omitted…  
  
    }  
    ```  
  
2.  使用 `CalculatorService` 实现 `ICalculator` 服务协定。  
  
    ```  
    public class CalculatorService : ICalculator  
    {  
        public double Add(double n1, double n2)  
        {  
            return n1 + n2;  
        }  
  
    //Other operations omitted…  
    ```  
  
3.  定义 `ICalculator` 和 `CalculatorService` 实现的命名空间，方法是将它们放置在一个命名空间块中。  
  
    ```  
    Namespace Microsoft.Ajax.Samples  
    {  
        //Include the code for ICalculator and Caculator here.  
    }  
    ```  
  
### 创建服务的 ASP.NET AJAX 终结点  
  
1.  创建一个行为配置，并指定服务的支持 ASP.NET AJAX 的终结点的 [\<enableWebScript\>](../../../../docs/framework/configure-apps/file-schema/wcf/enablewebscript.md) 行为。  
  
    ```  
    <system.serviceModel>  
        <behaviors>  
            <endpointBehaviors>  
                <behavior name="AspNetAjaxBehavior">  
                    <enableWebScript />  
                </behavior>  
            </endpointBehaviors>  
        </behaviors>  
    </system.serviceModel>  
    ```  
  
2.  为使用 <xref:System.ServiceModel.WebHttpBinding> 和前面的步骤中定义的 ASP.NET AJAX 行为的服务创建终结点。  
  
    ```  
    <system.serviceModel>  
        <services>  
            <service name="Microsoft.Ajax.Samples.CalculatorService">  
                <endpoint address=""  
                    behaviorConfiguration="AspNetAjaxBehavior"   
                    binding="webHttpBinding"  
                    contract="Microsoft.Ajax.Samples.ICalculator" />  
            </service>  
        </services>  
    </system.serviceModel>   
    ```  
  
### 在 IIS 中承载服务  
  
1.  若要在 IIS 中承载服务，请使用应用程序中的 .svc 扩展创建名为 service 的新文件。编辑此文件，在其中为服务添加适当的 [@ServiceHost](../../../../docs/framework/configure-apps/file-schema/wcf-directive/servicehost.md) 指令信息。例如，`CalculatorService` 示例的服务文件中的内容包含以下信息。  
  
    ```  
    <%@ServiceHost   
    language=c#   
    Debug="true"   
    Service="Microsoft.Ajax.Samples.CalculatorService"  
    %>  
    ```  
  
2.  [!INCLUDE[crabout](../../../../includes/crabout-md.md)]在 IIS 中承载的更多信息，请参见[如何：在 IIS 中承载 WCF 服务](../../../../docs/framework/wcf/feature-details/how-to-host-a-wcf-service-in-iis.md)。  
  
### 调用服务  
  
1.  在相对于 .svc 文件的空地址处配置终结点，这样便可以使用服务了。可通过向 service.svc\/\<操作\>（例如，表示 `Add` 操作的 service.svc\/Add）发送请求来调用服务。可以通过在 ASP.NET AJAX 脚本管理器控件的脚本集合中输入终结点 URL 来使用它。有关示例，请参见[使用 HTTP POST 的 AJAX 服务](../../../../docs/framework/wcf/samples/ajax-service-using-http-post.md)。  
  
## 请参阅  
 [为 ASP.NET AJAX 创建 WCF 服务](../../../../docs/framework/wcf/feature-details/creating-wcf-services-for-aspnet-ajax.md)   
 [如何：将启用了 AJAX 的 ASP.NET Web 服务迁移到 WCF](../../../../docs/framework/wcf/feature-details/how-to-migrate-ajax-enabled-aspnet-web-services-to-wcf.md)