---
title: "匿名客户端的传输安全 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 056653a5-384e-4a02-ae3c-1b0157d2ccb4
caps.latest.revision: 14
author: "BrucePerlerMS"
ms.author: "bruceper"
manager: "mbaldwin"
caps.handback.revision: 14
---
# 匿名客户端的传输安全
此 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 方案使用传输安全 \(HTTPS\) 确保保密性和完整性。必须使用安全套接字层 \(SSL\) 证书对服务器进行身份验证，并且客户端必须信任服务器的证书。客户端不通过任何机制进行身份验证，因此是匿名的。  
  
 有关示例应用程序，请参见 [WS 传输安全](../../../../docs/framework/wcf/samples/ws-transport-security.md)。[!INCLUDE[crabout](../../../../includes/crabout-md.md)]传输安全的更多信息，请参见[传输安全概述](../../../../docs/framework/wcf/feature-details/transport-security-overview.md)。  
  
 [!INCLUDE[crabout](../../../../includes/crabout-md.md)]将证书用于服务的更多信息，请参见[使用证书](../../../../docs/framework/wcf/feature-details/working-with-certificates.md)和[如何：使用 SSL 证书配置端口](../../../../docs/framework/wcf/feature-details/how-to-configure-a-port-with-an-ssl-certificate.md)。  
  
 ![对匿名客户端使用传输安全性](../../../../docs/framework/wcf/feature-details/media/8fa2e931-0cfb-4aaa-9272-91d652b85d8d.gif "8fa2e931\-0cfb\-4aaa\-9272\-91d652b85d8d")  
  
|特征|说明|  
|--------|--------|  
|安全模式|传输|  
|互操作性|与现有 Web 服务和客户端|  
|身份验证（服务器）<br /><br /> 身份验证（客户端）|是<br /><br /> 应用程序级（无 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 支持）|  
|完整性|是|  
|保密性|是|  
|Transport|HTTPS|  
|绑定|<xref:System.ServiceModel.WsHttpBinding>|  
  
## 服务  
 下面的代码和配置应独立运行。执行下列操作之一：  
  
-   使用代码（而不使用配置）创建独立服务。  
  
-   使用提供的配置创建服务，但不定义任何终结点。  
  
### 代码  
 下面的代码演示如何使用传输安全创建终结点：  
  
 [!code-csharp[c_SecurityScenarios#5](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_securityscenarios/cs/source.cs#5)]
 [!code-vb[c_SecurityScenarios#5](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_securityscenarios/vb/source.vb#5)]  
  
### 配置  
 下面的代码使用配置设置相同的终结点。客户端不通过任何机制进行身份验证，因此是匿名的。  
  
```  
<?xml version="1.0" encoding="utf-8"?>  
<configuration>  
  <system.serviceModel>  
    <services>  
      <service name="ServiceModel.Calculator">  
        <endpoint address="http://localhost/Calculator"   
                  binding="wsHttpBinding"  
                  bindingConfiguration="WSHttpBinding_ICalculator"   
                  name="SecuredByTransportEndpoint"  
                  contract="ServiceModel.ICalculator" />  
      </service>  
    </services>  
    <bindings>  
      <wsHttpBinding>  
        <binding name="WSHttpBinding_ICalculator">  
          <security mode="Transport">  
            <transport clientCredentialType="None" />  
          </security>  
        </binding>  
      </wsHttpBinding>  
    </bindings>  
    <client />  
  </system.serviceModel>  
</configuration>  
```  
  
## 客户端  
 下面的代码和配置将独立运行。执行下列操作之一：  
  
-   使用代码（和客户端代码）创建独立客户端。  
  
-   创建不定义任何终结点地址的客户端。而使用将配置名称作为参数的客户端构造函数。例如：  
  
     [!code-csharp[C_SecurityScenarios#0](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_securityscenarios/cs/source.cs#0)]
     [!code-vb[C_SecurityScenarios#0](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_securityscenarios/vb/source.vb#0)]  
  
### 代码  
 [!code-csharp[c_SecurityScenarios#6](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_securityscenarios/cs/source.cs#6)]
 [!code-vb[c_SecurityScenarios#6](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_securityscenarios/vb/source.vb#6)]  
  
### 配置  
 下面的配置可代替代码用于设置服务。  
  
```  
<configuration>  
  <system.serviceModel>  
    <bindings>  
      <wsHttpBinding>  
        <binding name="WSHttpBinding_ICalculator" >  
          <security mode="Transport">  
            <transport clientCredentialType="None" />  
          </security>  
        </binding>  
      </wsHttpBinding>  
    </bindings>  
    <client>  
      <endpoint address="https://machineName/Calculator"   
                binding="wsHttpBinding"  
                bindingConfiguration="WSHttpBinding_ICalculator"   
                contract="ICalculator"  
                name="WSHttpBinding_ICalculator" />  
    </client>  
  </system.serviceModel>  
</configuration>  
```  
  
## 请参阅  
 [安全性概述](../../../../docs/framework/wcf/feature-details/security-overview.md)   
 [WS 传输安全](../../../../docs/framework/wcf/samples/ws-transport-security.md)   
 [传输安全概述](../../../../docs/framework/wcf/feature-details/transport-security-overview.md)   
 [Windows Server App Fabric 的安全模型](http://go.microsoft.com/fwlink/?LinkID=201279&clcid=0x804)