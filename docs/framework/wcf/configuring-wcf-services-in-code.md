---
title: "在代码中配置 WCF 服务 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 193c725d-134f-4d31-a8f8-4e575233bff6
caps.latest.revision: 4
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 4
---
# 在代码中配置 WCF 服务
[!INCLUDE[indigo1](../../../includes/indigo1-md.md)] 允许开发人员使用配置文件或代码配置服务。当需要在配置后部署服务时，配置文件非常有用。在使用配置文件时，IT 专业人员只需要更新配置文件，不需要重新编译。但是，配置文件可能很复杂，并难以维护。不支持调试配置文件，并且配置元素被名称引用，这使得创作配置文件容易出错和较为困难。[!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 还允许您在代码中配置服务。在早期版本的 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)]（4.0 版及更早），在代码中配置服务在自我托管方案中很容易，<xref:System.ServiceModel.ServiceHost> 类允许您在调用 ServiceHost.Open 之前配置终结点和行为。但是，在 web 宿主方案中，不能直接访问 <xref:System.ServiceModel.ServiceHost> 类。要配置 web 宿主服务，需要创建创建了 <xref:System.ServiceModel.ServiceHost> 并执行任何所需配置的 <xref:System.ServiceModel.ServiceHostFactory>。从 .NET 4.5 开始，[!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 提供更简单的方法来在代码中配置自承载服务和 Web 承载的服务。  
  
## 配置方法  
 只须在您的服务实现类中使用以下前面定义名为`Configure`的公共静态方法：  
  
```csharp  
public static void Configure(ServiceConfiguration config)  
```  
  
 配置方法采用 <xref:System.ServiceModel.ServiceConfiguration> 实例，使开发者可以添加终结点和行为。在打开服务主机之前，由 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 调用此方法。定义时，将忽略 app.config 或 web.config 文件中指定的任何服务配置设置。  
  
 下面的代码段阐释了如何定义 `Configure` 方法和添加服务终结点、终结点行为以及服务行为：  
  
```csharp  
public class Service1 : IService1  
    {  
        public static void Configure(ServiceConfiguration config)  
        {  
            ServiceEndpoint se = new ServiceEndpoint(new ContractDescription("IService1"), new BasicHttpBinding(), new EndpointAddress("basic"));  
            se.Behaviors.Add(new MyEndpointBehavior());  
            config.AddServiceEndpoint(se);  
  
            config.Description.Behaviors.Add(new ServiceMetadataBehavior { HttpGetEnabled = true });  
            config.Description.Behaviors.Add(new ServiceDebugBehavior { IncludeExceptionDetailInFaults = true });  
        }  
  
        public string GetData(int value)  
        {  
            return string.Format("You entered: {0}", value);  
        }  
  
        public CompositeType GetDataUsingDataContract(CompositeType composite)  
        {  
            if (composite == null)  
            {  
                throw new ArgumentNullException("composite");  
            }  
            if (composite.BoolValue)  
            {  
                composite.StringValue += "Suffix";  
            }  
            return composite;  
        }  
    }  
```  
  
 要启用的协议（如服务的 https），可以显式添加使用协议的终结点，也可以通过调用 ServiceConfiguration.EnableProtocol\(Binding\) 自动添加终结点，进行调用可向与协议兼容的每个基址和定义每个服务协定添加终结点。下面的代码演示如何使用 ServiceConfiguration.EnableProtocol 方法：  
  
```csharp  
public class Service1 : IService1   
{   
    public string GetData(int value);   
    public static void Configure(ServiceConfiguration config)   
    {   
        // Enable “Add Service Reference” support   
       config.Description.Behaviors.Add( new ServiceMetadataBehavior { HttpGetEnabled = true });   
       // set up support for http, https, net.tcp, net.pipe   
       config.EnableProtocol(new BasicHttpBinding());   
       config.EnableProtocol(new BasicHttpBinding());   
       config.EnableProtocol(new NetTcpBinding());   
       config.EnableProtocol(new NetNamedPipeBinding());   
       // add an extra BasicHttpBinding endpoint at http:///basic   
       config.AddServiceEndpoint(typeof(IService1), new BasicHttpBinding(),"basic");   
    }   
}   
```  
  
 \<`protocolMappings`\> 部分中的设置仅在没有以编程方式向 <xref:System.ServiceModel.ServiceConfiguration> 添加应用程序终结点时使用。您可以选择通过调用 <xref:System.ServiceModel.ServiceConfiguration.LoadFromConfiguration%2A> 从默认应用程序配置文件加载服务配置，然后更改设置。<xref:System.ServiceModel.ServiceConfiguration> 类还允许您从集中式配置加载配置。 下面的代码演示如何实现：  
  
```  
public class Service1 : IService1   
{   
    public void DoWork();   
    public static void Configure(ServiceConfiguration config)   
    {   
          config.LoadFromConfiguration(ConfigurationManager.OpenMappedExeConfiguration(new ExeConfigurationFileMap { ExeConfigFilename = @"c:\sharedConfig\MyConfig.config" }, ConfigurationUserLevel.None));   
    }   
}  
  
```  
  
> [!IMPORTANT]
>  请注意，<xref:System.ServiceModel.LoadFromConfiguration%2A> 忽略\<`system.serviceModel`\> 标记的 \<`service`\> 内的 \<`host`\> 设置。在概念上，\<`host`\> 是关于主机配置而不是服务配置的，在配置方法执行之前进行加载。  
  
## 请参阅  
 [使用配置文件配置服务](../../../docs/framework/wcf/configuring-services-using-configuration-files.md)   
 [配置客户端行为](../../../docs/framework/wcf/configuring-client-behaviors.md)   
 [简化配置](../../../docs/framework/wcf/simplified-configuration.md)   
 [基于配置的激活](../../../docs/framework/wcf/samples/configuration-based-activation.md)   
 [配置](../../../docs/framework/wcf/samples/configuration-sample.md)   
 [IIS 和 WAS 中的基于配置的激活](../../../docs/framework/wcf/feature-details/configuration-based-activation-in-iis-and-was.md)   
 [配置和元数据支持](../../../docs/framework/wcf/extending/configuration-and-metadata-support.md)   
 [配置](../../../docs/framework/wcf/diagnostics/exceptions-reference/configuration.md)   
 [如何：在配置中指定服务绑定](../../../docs/framework/wcf/how-to-specify-a-service-binding-in-configuration.md)   
 [如何：在配置中创建服务终结点](../../../docs/framework/wcf/feature-details/how-to-create-a-service-endpoint-in-configuration.md)   
 [如何：使用配置文件发布服务的元数据](../../../docs/framework/wcf/feature-details/how-to-publish-metadata-for-a-service-using-a-configuration-file.md)   
 [如何：在配置中指定客户端绑定](../../../docs/framework/wcf/how-to-specify-a-client-binding-in-configuration.md)