---
title: "如何：指定客户端凭据类型 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "安全凭据, 添加到 SOAP 消息"
  - "WCF, 安全"
ms.assetid: 10f51bee-5f92-4c1a-9126-fa5418535d8f
caps.latest.revision: 8
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 8
---
# 如何：指定客户端凭据类型
设置安全模式（传输或消息）后，您可以设置客户端凭据类型。此属性指定客户端凭据类型必须提供哪种类型向服务进行身份验证。[!INCLUDE[crabout](../../../includes/crabout-md.md)] 设置安全模式（设置客户端凭据类型前的必需步骤），请参见 [如何：设置安全模式](../../../docs/framework/wcf/how-to-set-the-security-mode.md)。  
  
### 在代码中设置客户端凭据类型  
  
1.  创建服务将使用的绑定的实例。本示例使用 <xref:System.ServiceModel.WSHttpBinding> 绑定。  
  
2.  将 <xref:System.ServiceModel.WSHttpSecurity.Mode%2A> 属性设置为适当的值。本示例使用 Message 模式。  
  
3.  将 <xref:System.ServiceModel.MessageSecurityOverHttp.ClientCredentialType%2A> 属性设置为适当的值。本示例将其设置为使用 Windows 身份验证 \(<xref:System.ServiceModel.MessageCredentialType>\)。  
  
     [!code-csharp[c_ProgrammingSecurity#14](../../../samples/snippets/csharp/VS_Snippets_CFX/c_programmingsecurity/cs/source.cs#14)]
     [!code-vb[c_ProgrammingSecurity#14](../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_programmingsecurity/vb/source.vb#14)]  
  
### 在配置中设置客户端凭据类型  
  
1.  向配置文件中添加一个 [\<system.serviceModel\>](../../../docs/framework/configure-apps/file-schema/wcf/system-servicemodel.md) 元素。  
  
2.  添加一个 [\<绑定\>](../../../docs/framework/configure-apps/file-schema/wcf/bindings.md) 元素作为子元素。  
  
3.  添加一个相应的绑定。本示例使用 [\<wsHttpBinding\>](../../../docs/framework/configure-apps/file-schema/wcf/wshttpbinding.md) 元素。  
  
4.  添加一个 [\<绑定\>](../../../docs/framework/misc/binding.md) 元素，并将 `name` 属性设置为适当的值。本示例使用名称“SecureBinding”。  
  
5.  添加一个 `<security>` 绑定。将 `mode` 属性设置为适当的值。本示例将其设置为 `"Message"`。  
  
6.  添加一个 `<message>` 或 `<transport>` 元素，具体由安全模式确定。将 `clientCredentialType` 属性设置为适当的值。本示例使用 `"Windows"`。  
  
    ```  
    <system.serviceModel>  
      <bindings>  
        <wsHttpBinding>  
          <binding name="SecureBinding">  
            <security mode="Message">  
                 <message clientCredentialType="Windows" />  
             </security>  
          </binding>  
        </wsHttpBinding>  
      </bindings>  
    </system.serviceModel>  
    ```  
  
## 请参阅  
 [保证服务的安全](../../../docs/framework/wcf/securing-services.md)   
 [如何：设置安全模式](../../../docs/framework/wcf/how-to-set-the-security-mode.md)