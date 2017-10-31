---
title: "如何：配置基本 Windows Communication Foundation 客户端 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
helpviewer_keywords: 
  - "WCF 客户端 [WCF], 配置"
ms.assetid: d067b86d-afb0-47bf-94f6-45180a3d8d78
caps.latest.revision: 47
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 47
---
# 如何：配置基本 Windows Communication Foundation 客户端
这是创建基本 [!INCLUDE[indigo1](../../../includes/indigo1-md.md)] 应用程序所需的六项任务中的第五项任务。  有关全部六项任务的概述，请参见[入门教程](../../../docs/framework/wcf/getting-started-tutorial.md)主题。  
  
 本主题讨论使用 [!INCLUDE[vs_current_long](../../../includes/vs-current-long-md.md)] 的“添加服务引用”功能或[ServiceModel 元数据实用工具 \(Svcutil.exe\)](../../../docs/framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md) 生成的客户端配置文件。  配置客户端包括指定客户端用于访问服务的终结点。  每个终结点都有一个地址、一个绑定和一个协定，所有这些元素都必须在配置客户端的过程中指定。  
  
### 配置 Windows Communication Foundation 客户端  
  
1.  从 GettingStartedClient 项目打开生成的配置文件 \(App.config\)。  下面的示例显示了生成的配置文件。  请在 [\<system.serviceModel\>](../../../docs/framework/configure-apps/file-schema/wcf/system-servicemodel.md)[\<endpoint\> 节下查找](http://msdn.microsoft.com/zh-cn/13aa23b7-2f08-4add-8dbf-a99f8127c017) 元素。  
  
    ```  
    <?xml version="1.0" encoding="utf-8" ?>  
    <configuration>  
        <startup>   
          <!-- specifies the version of WCF to use-->  
            <supportedRuntime version="v4.0" sku=".NETFramework,Version=v4.5,Profile=Client" />  
        </startup>  
        <system.serviceModel>  
            <bindings>  
                <!-- Uses wsHttpBinding-->  
                <wsHttpBinding>  
                    <binding name="WSHttpBinding_ICalculator" />  
                </wsHttpBinding>  
            </bindings>  
            <client>  
                <!-- specifies the endpoint to use when calling the service -->  
                <endpoint address="http://localhost:8000/ServiceModelSamples/Service/CalculatorService"  
                    binding="wsHttpBinding" bindingConfiguration="WSHttpBinding_ICalculator"  
                    contract="ServiceReference1.ICalculator" name="WSHttpBinding_ICalculator">  
                    <identity>  
                        <userPrincipalName value="migree@redmond.corp.microsoft.com" />  
                    </identity>  
                </endpoint>  
            </client>  
        </system.serviceModel>  
    </configuration><?xml version="1.0" encoding="utf-8" ?>  
    <configuration>  
        <startup>   
            <supportedRuntime version="v4.0" sku=".NETFramework,Version=v4.5,Profile=Client" />  
        </startup>  
        <system.serviceModel>  
            <bindings>  
                <wsHttpBinding>  
                    <binding name="WSHttpBinding_ICalculator" />  
                </wsHttpBinding>  
            </bindings>  
            <client>  
                <endpoint address="http://localhost:8000/ServiceModelSamples/Service/CalculatorService"  
                    binding="wsHttpBinding" bindingConfiguration="WSHttpBinding_ICalculator"  
                    contract="ServiceReference1.ICalculator" name="WSHttpBinding_ICalculator">  
                    <identity>  
                        <userPrincipalName value="migree@redmond.corp.microsoft.com" />  
                    </identity>  
                </endpoint>  
            </client>  
        </system.serviceModel>  
    </configuration>   
    ```  
  
     此示例配置的终结点可供客户端在访问位于以下地址的服务时使用：http:\/\/localhost:8000\/ServiceModelSamples\/Service\/CalculatorService  
  
     该终结点元素指定 `ServiceReference1.ICalculator` 服务约定用于 WCF 客户端和服务之间的通信。  使用系统提供的 <xref:System.ServiceModel.WsHttpBinding> 配置 WCF 通道。  此约定是使用 Visual Studio 中的“添加服务引用”生成的。  它基本上是在 GettingStartedLib 项目中定义的约定的副本。  <xref:System.ServiceModel.WsHttpBinding> 绑定指定 HTTP 作为传输协议、可互操作安全性以及其他配置详细信息。  
  
2.  [!INCLUDE[crabout](../../../includes/crabout-md.md)]如何在此配置下使用生成的客户端的更多信息，请参见[如何：使用客户端](../../../docs/framework/wcf/how-to-use-a-wcf-client.md)。  
  
## 请参阅  
 [使用绑定配置服务和客户端](../../../docs/framework/wcf/using-bindings-to-configure-services-and-clients.md)   
 [ServiceModel 元数据实用工具 \(Svcutil.exe\)](../../../docs/framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md)   
 [如何：创建客户端](../../../docs/framework/wcf/how-to-create-a-wcf-client.md)   
 [入门](../../../docs/framework/wcf/samples/getting-started-sample.md)   
 [自承载](../../../docs/framework/wcf/samples/self-host.md)