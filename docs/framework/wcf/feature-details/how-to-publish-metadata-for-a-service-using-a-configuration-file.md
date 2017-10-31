---
title: "如何：使用配置文件发布服务的元数据 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: f061443f-92df-4824-b36a-609c4cd14a17
caps.latest.revision: 24
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 24
---
# 如何：使用配置文件发布服务的元数据
这是演示发布 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 服务的元数据的两个帮助主题之一。 有两种方式可以指定服务应如何发布元数据：使用配置文件和使用代码。 本主题演示如何使用配置文件发布服务的元数据。  
  
> [!CAUTION]
>  本主题演示如何以不安全的方式发布元数据。 任何客户端都可以检索服务的元数据。 如果您要求服务以安全方式发布元数据，请参阅[自定义安全元数据终结点](../../../../docs/framework/wcf/samples/custom-secure-metadata-endpoint.md)。  
  
 [!INCLUDE[crabout](../../../../includes/crabout-md.md)]发布元数据在代码中，请参阅[如何︰ 发布元数据服务使用代码](../../../../docs/framework/wcf/feature-details/how-to-publish-metadata-for-a-service-using-code.md)。 通过发布元数据，客户端可以使用 WS-Transfer GET 请求或使用 `?wsdl` 查询字符串的 HTTP/GET 来检索元数据。 若要确保代码能够工作，必须创建一个基本的 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 服务。 为了简单起见，将在以下代码中提供一个基本的自承载服务。  
  
```csharp  
using System;  
using System.Runtime.Serialization;  
using System.ServiceModel;  
using System.ServiceModel.Description;  
  
namespace Metadata.Samples  
{  
    [ServiceContract]  
    public interface ISimpleService  
    {  
        [OperationContract]  
        string SimpleMethod(string msg);  
    }  
  
    class SimpleService : ISimpleService  
    {  
        public string SimpleMethod(string msg)  
        {  
            Console.WriteLine("The caller passed in " + msg);  
            return "Hello " + msg;  
        }  
    }  
  
    class Program  
    {  
        static void Main(string[] args)  
        {  
            ServiceHost host = new ServiceHost(typeof(SimpleService),  
                new Uri("http://localhost:8001/MetadataSample"));   
            try  
            {  
                // Open the service host to accept incoming calls  
                host.Open();  
  
                // The service can now be accessed.  
                Console.WriteLine("The service is ready.");  
                Console.WriteLine("Press <ENTER> to terminate service.");  
                Console.WriteLine();  
                Console.ReadLine();  
  
                // Close the ServiceHostBase to shutdown the service.  
                host.Close();  
            }  
            catch (CommunicationException commProblem)  
            {  
                Console.WriteLine("There was a communication problem. " + commProblem.Message);  
                Console.Read();  
            }  
        }  
    }  
}  
```  
  
 此服务为自承载服务，并且是使用配置文件配置的。 下面的配置文件作为开始点。  
  
```xml  
<configuration>  
  <system.serviceModel>  
    <services>  
      <service name="Metadata.Example.SimpleService">  
        <endpoint address=""  
                  binding="basicHttpBinding"  
                  contract="Metadata.Example.ISimpleService" />  
      </service>  
    </services>  
    <behaviors>  
  
    </behaviors>  
  </system.serviceModel>  
</configuration>  
  
```  
  
### <a name="to-publish-metadata-for-a-wcf-service-using-an-application-configuration-file"></a>使用应用程序配置文件发布 WCF 服务的元数据  
  
1.  在 App.config 文件内，在结束 `</services>` 元素之后创建 `<behaviors>` 元素。  
  
  
  
2.  在 `<behaviors>` 元素内，添加一个 `<serviceBehaviors>` 元素。  
  
  
  
3.  向 `<behavior>``<serviceBehaviors>` 元素中添加一个 `name` 元素，并为 元素的 `<behavior>` 属性指定一个值。  
  
  
  
4.  向 `<serviceMetadata>` 元素中添加一个 `<behavior>` 元素。 将 `httpGetEnabled` 属性设置为 `true`，并将 `policyVersion` 属性设置为 Policy15。 `httpGetEnabled` 可让服务响应 HTTP GET 请求发出的元数据请求。 `policyVersion` 通知服务在生成元数据时应符合 WS-Policy 1.5。  
  
  
  
5.  将 `behaviorConfiguration` 特性添加到 `<service>` 元素，并指定在步骤 1 中添加的 `name` 元素的 `<behavior>` 特性，如下面的代码示例所示。  
  
    ```xml  
    <services>  
      <service  
          name="Metadata.Example.SimpleService"  
          behaviorConfiguration="SimpleServiceBehavior">  
        ...  
      </service>  
    </services>  
    <behaviors>  
      <serviceBehaviors>  
        <behavior name="SimpleServiceBehavior">  
          <serviceMetadata httpGetEnabled="True" policyVersion="Policy15" />  
        </behavior>  
      </serviceBehaviors>  
    </behaviors>  
    ```  
  
6.  添加一个或多个其协定设置为 `<endpoint>` 的 `IMetadataExchange` 元素，如下面的代码示例所示。  
  
    ```xml  
    <services>  
      <service  
          name="Metadata.Example.SimpleService"  
          behaviorConfiguration="SimpleServiceBehavior">  
  
        <endpoint address=""  
                  binding="wsHttpBinding"  
                  contract="Metadata.Example.ISimpleService" />  
  
        <endpoint address="mex"  
                  binding="mexHttpBinding"  
                  contract="IMetadataExchange" />  
      </service>  
    </services>  
    ```  
  
7.  对于上一步中添加的元数据终结点，将 `binding` 特性设置为下列值之一：  
  
    -   `mexHttpBinding`（对于 HTTP 发布）。  
  
    -   `mexHttpsBinding`（对于 HTTPS 发布）。  
  
    -   `mexNamedPipeBinding`（对于命名管道发布）。  
  
    -   `mexTcpBinding`（对于 TCP 发布）。  
  
8.  对于上一步中添加的元数据终结点，将地址设置为等于：  
  
    -   一个空字符串，以在基址和元数据绑定相同的情况下将主机应用程序的基址用作发布点。  
  
    -   一个相对地址，前提是主机应用程序具有一个基址。  
  
    -   一个绝对地址。  
  
9. 生成并运行控制台应用程序。  
  
10. 使用 Internet Explorer 浏览服务的基址（本示例中的 http://localhost:8001/MetadataSample）并验证是否已打开元数据发布。 如果未显示上述内容，则结果页顶部会显示消息：“Metadata publishing for this service is currently disabled”（当前禁用服务的元数据发布）。  
  
### <a name="to-use-default-endpoints"></a>使用默认终结点  
  
1.  若要配置使用默认终结点的服务的元数据，请指定<xref:System.ServiceModel.Description.ServiceMetadataBehavior>在配置文件如下所示的上一示例中，但不是指定任何终结点。 配置文件将类似如下所示。  
  
    ```xml  
    <configuration>  
      <system.serviceModel>  
        <behaviors>  
          <serviceBehaviors>  
            <behavior name="SimpleServiceBehavior">  
              <serviceMetadata httpGetEnabled="True" policyVersion="Policy12" />  
            </behavior>  
          </serviceBehaviors>  
        </behaviors>  
  
      </system.serviceModel>  
    </configuration>  
    ```  
  
     由于该服务有<xref:System.ServiceModel.Description.ServiceMetadataBehavior>与`httpGetEnabled`设置为`true`，因此服务了发布元数据启用，因为未显式不添加任何终结点，则运行时添加默认终结点。 [!INCLUDE[crabout](../../../../includes/crabout-md.md)]默认终结点、 绑定和行为，请参阅[简化配置](../../../../docs/framework/wcf/simplified-configuration.md)和[WCF 服务的简化配置](../../../../docs/framework/wcf/samples/simplified-configuration-for-wcf-services.md)。  
  
## <a name="example"></a>示例  
 下面的代码示例演示基本 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 服务的实现，以及发布服务的元数据的配置文件。  
  
```csharp  
using System;  
using System.Runtime.Serialization;  
using System.ServiceModel;  
using System.ServiceModel.Description;  
  
namespace Metadata.Samples  
{  
    [ServiceContract]  
    public interface ISimpleService  
    {  
        [OperationContract]  
        string SimpleMethod(string msg);  
    }  
  
    class SimpleService : ISimpleService  
    {  
        public string SimpleMethod(string msg)  
        {  
            Console.WriteLine("The caller passed in " + msg);  
            return "Hello " + msg;  
        }  
    }  
  
    class Program  
    {  
        static void Main(string[] args)  
        {  
            ServiceHost host = new ServiceHost(typeof(SimpleService),  
                new Uri("http://localhost:8001/MetadataSample"));   
            try  
            {  
                // Open the service host to accept incoming calls  
                host.Open();  
  
                // The service can now be accessed.  
                Console.WriteLine("The service is ready.");  
                Console.WriteLine("Press <ENTER> to terminate service.");  
                Console.WriteLine();  
                Console.ReadLine();  
  
                // Close the ServiceHostBase to shutdown the service.  
                host.Close();  
            }  
            catch (CommunicationException commProblem)  
            {  
                Console.WriteLine("There was a communication problem. " + commProblem.Message);  
                Console.Read();  
            }  
        }  
    }  
}  
```  
  
```xml  
<configuration>  
  <system.serviceModel>  
    <behaviors>  
      <serviceBehaviors>  
        <behavior name="SimpleServiceBehavior">  
          <serviceMetadata httpGetEnabled="True" policyVersion="Policy12" />  
          <serviceDebug includeExceptionDetailInFaults="False" />  
        </behavior>  
      </serviceBehaviors>  
    </behaviors>  
  </system.serviceModel>  
</configuration>  
```  
  
## <a name="see-also"></a>另请参阅  
 <xref:System.ServiceModel.Description.ServiceMetadataBehavior>   
 [如何︰ 承载于托管应用程序的 WCF 服务](../../../../docs/framework/wcf/how-to-host-a-wcf-service-in-a-managed-application.md)   
 [自承载](../../../../docs/framework/wcf/samples/self-host.md)   
 [元数据体系结构概述](../../../../docs/framework/wcf/feature-details/metadata-architecture-overview.md)   
 [使用元数据](../../../../docs/framework/wcf/feature-details/using-metadata.md)   
 [如何︰ 使用代码为服务中发布元数据](../../../../docs/framework/wcf/feature-details/how-to-publish-metadata-for-a-service-using-code.md)