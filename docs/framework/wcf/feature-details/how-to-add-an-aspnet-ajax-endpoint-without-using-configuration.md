---
title: "如何：在不使用配置的情况下添加 ASP.NET AJAX 终结点 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: b05c1742-8d0a-4673-9d71-725b18a3008e
caps.latest.revision: 14
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 14
---
# 如何：在不使用配置的情况下添加 ASP.NET AJAX 终结点
[!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 允许您创建一个服务来公开一个支持 ASP.NET AJAX 的终结点，并且可以从客户端网站上的 JavaScript 中调用该终结点。 若要创建这样的终结点，可以使用配置文件（与使用所有其他 WCF 终结点一样），或使用不要求任何配置元素的方法。 本主题演示第二种方法。  
  
 若要在不使用配置的情况下创建具有 ASP.NET AJAX 终结点的服务，则必须由 Internet 信息服务 (IIS) 来承载创建的服务。 若要激活 ASP.NET AJAX 终结点使用此方法，指定<xref:System.ServiceModel.Activation.WebScriptServiceHostFactory>作为 Factory 参数在[ @ServiceHost ](../../../../docs/framework/configure-apps/file-schema/wcf-directive/servicehost.md)指令的.svc 文件中。 此自定义工厂是一个组件，可自动将 ASP.NET AJAX 终结点配置为可以从客户端网站上的 JavaScript 中调用。  
  
 运行示例，请参阅[AJAX 服务而无需配置](../../../../docs/framework/wcf/samples/ajax-service-without-configuration.md)。  
  
 有关如何配置 ASP.NET AJAX 终结点使用配置元素的概要信息，请参阅[如何︰ 使用配置来添加 ASP.NET AJAX 终结点](../../../../docs/framework/wcf/feature-details/how-to-use-configuration-to-add-an-aspnet-ajax-endpoint.md)。  
  
### <a name="to-create-a-basic-wcf-service"></a>创建基本 WCF 服务  
  
1.  定义基本[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]接口的服务约定标有<xref:System.ServiceModel.ServiceContractAttribute>属性。 标记与每个操作<xref:System.ServiceModel.OperationContractAttribute>。 请务必设置<xref:System.ServiceModel.ServiceContractAttribute.Namespace%2A>属性。  
  
    ```  
    [ServiceContract(Namespace = "MyService")]]  
    public interface ICalculator  
    {  
        [OperationContract]  
        // This operation returns the sum of d1 and d2.  
        double Add(double n1, double n2);  
  
        //Other operations omitted…  
  
    }  
    ```  
  
2.  使用 `ICalculator` 实现 `CalculatorService` 服务协定。  
  
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
  
### <a name="to-host-the-service-in-internet-information-services-without-configuration"></a>在不使用配置的情况下在 Internet 信息服务中承载服务  
  
1.  在应用程序中创建一个名为 service 的新文件（扩展名为 .svc）。 编辑此文件添加适当的[ @ServiceHost ](../../../../docs/framework/configure-apps/file-schema/wcf-directive/servicehost.md)服务的指令信息。 指定<xref:System.ServiceModel.Activation.WebScriptServiceHostFactory>中使用，则[ @ServiceHost ](../../../../docs/framework/configure-apps/file-schema/wcf-directive/servicehost.md)指令以自动配置 ASP.NET AJAX 终结点。  
  
    ```  
    <%@ServiceHost   
        language=c#   
        Debug="true"   
        Service="Microsoft.Ajax.Samples.CalculatorService"  
        Factory=System.ServiceModel.Activation.WebScriptServiceHostFactory  
    %>  
    ```  
  
2.  生成服务并从客户端调用该服务。 在调用该服务时，Internet Information Services (IIS) 会将其激活。 [!INCLUDE[crabout](../../../../includes/crabout-md.md)]承载在 IIS 中，请参阅[如何︰ 承载在 IIS 中的 WCF 服务](../../../../docs/framework/wcf/feature-details/how-to-host-a-wcf-service-in-iis.md)。  
  
### <a name="to-call-the-service"></a>调用服务  
  
1.  相对于.svc 文件的空地址处配置终结点，这样服务现已推出，可以通过将请求发送到 service.svc/ 调用<>\> -例如，便`Add`操作。 可以通过在 ASP.NET AJAX 脚本管理器控件的“脚本”集合中输入服务 URL 来使用响应的服务。 有关示例，请参阅[AJAX 服务而无需配置](../../../../docs/framework/wcf/samples/ajax-service-without-configuration.md)。  
  
## <a name="example"></a>示例  
<!-- TODO: review snippet reference  [!CODE [Microsoft.Win32.RegistryKey#4](Microsoft.Win32.RegistryKey#4)]  -->  
  
 在相对于基 URL 的空地址处创建自动配置的终结点。 使用此方法也可以添加和使用配置文件。 如果配置文件包含终结点定义，则这些终结点将添加到自动配置的终结点中。  
  
 例如，service.svc 使用<xref:System.ServiceModel.Activation.WebScriptServiceHostFactory>而服务目录包含 Web.config 文件，用于定义相同的服务使用的终结点<xref:System.ServiceModel.BasicHttpBinding>在"soap"相对地址处。 在这种情况下，服务将包括两个终结点：一个在 service.svc 处（该终结点响应 ASP.NET AJAX 请求），另一个在 service.svc/soap 处（该终结点响应 SOAP 请求）。  
  
 如果配置文件定义的空相对地址处的终结点和<xref:System.ServiceModel.Activation.WebScriptServiceHostFactory>是使用，将引发异常并且该服务无法启动。  
  
 不能使用配置来修改自动配置终结点上的设置。 如果任何设置 （如读取器配额） 必须修改，您不能使用免配置方法通过删除<xref:System.ServiceModel.Activation.WebScriptServiceHostFactory>从.svc 文件并创建终结点的配置项。  
  
 如果您的服务需要 ASP.NET 兼容模式-例如，如果它使用<xref:System.Web.HttpContext>类或 ASP.NET 授权机制，则仍需要启用此模式配置文件。 所需的配置元素是[ <> \> ](../../../../docs/framework/configure-apps/file-schema/wcf/servicehostingenvironment.md)元素，它必须以如下方式添加。  
  
 `<system.serviceModel>`  
  
 `<serviceHostingEnvironment aspNetCompatibilityEnabled=”true” /> </system.serviceModel>`  
  
 [!INCLUDE[crdefault](../../../../includes/crdefault-md.md)][WCF 服务和 ASP.NET](../../../../docs/framework/wcf/feature-details/wcf-services-and-aspnet.md)主题。  
  
 <xref:System.ServiceModel.Activation.WebScriptServiceHostFactory>类作为派生的类的<xref:System.ServiceModel.Activation.ServiceHostFactory>。 服务主机工厂机制的详细说明，请参阅[扩展宿主使用 ServiceHostFactory](../../../../docs/framework/wcf/extending/extending-hosting-using-servicehostfactory.md)主题。  
  
## <a name="see-also"></a>另请参阅  
 [为 ASP.NET AJAX 创建 WCF 服务](../../../../docs/framework/wcf/feature-details/creating-wcf-services-for-aspnet-ajax.md)   
 [如何︰ 将启用 AJAX 的 ASP.NET Web 服务迁移到 WCF](../../../../docs/framework/wcf/feature-details/how-to-migrate-ajax-enabled-aspnet-web-services-to-wcf.md)