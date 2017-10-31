---
title: "&lt;basicHttpBinding&gt; 的 &lt;transport&gt; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 4c5ba293-3d7e-47a6-b84e-e9022857b7e5
caps.latest.revision: 18
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 18
---
# &lt;basicHttpBinding&gt; 的 &lt;transport&gt;
为 HTTP 传输定义控制身份验证参数的属性。  
  
## 语法  
  
```  
<basicHttpBinding>  
    <binding>  
        <security  
        mode="None|Transport|Message|TransportWithMessageCredential|TransportCredentialOnly">  
            <transport clientCredentialType="None|Basic|Digest|Ntlm|Windows"  
             proxyCredentialType="None|Basic|Digest|Ntlm|Windows" realm="string" >  
                <extendedProtectionPolicy  
                     policyEnforcement="Never|WhenSupported|Always"  
                     protectionScenario="TransportSelected|TrustedProxy">  
                    <customServiceNames></customServiceNames>  
                        </extendedProtectionPolicy>  
            </transport>  
        </security>  
    </binding>  
</basicHttpBinding>  
```  
  
## 特性和元素  
 下列各节描述了特性、子元素和父元素。  
  
### 特性  
  
|特性|描述|  
|--------|--------|  
|clientCredentialType|-   指定要在使用 HTTP 身份验证执行客户端身份验证时使用的凭据类型。  默认值为 `None`。  此属性的类型为 <xref:System.ServiceModel.HttpClientCredentialType>。|  
|proxyCredentialType|-   指定通过 HTTP 使用代理在域中执行客户端身份验证时要使用的凭据类型。  只有当父 `security` 元素的 `mode` 属性为 `Transport` 或 `TransportCredentialsOnly` 时，此属性才适用。  此属性的类型为 <xref:System.ServiceModel.HttpProxyCredentialType>。|  
|realm|一个字符串，指定摘要式或基本身份验证的 HTTP 身份验证方案所使用的领域。  默认值为一个空字符串。|  
|policyEnforcement|此枚举指定应何时强制实施 <xref:System.Security.Authentication.ExtendedProtectionPolicy>。<br /><br /> 1.  Never – 绝不强制实施此策略（禁用扩展保护）。<br />2.  WhenSupported – 仅在客户端支持扩展保护时才强制实施此策略。<br />3.  Always – 总是强制实施此策略。  不支持扩展保护的客户端将无法进行身份验证。|  
|protectionScenario|此枚举指定此策略强制实施的保护方案。|  
  
## clientCredentialType 属性  
  
|值|描述|  
|-------|--------|  
|无|在传输过程中不能保证消息的安全。|  
|Basic|指定基本身份验证。|  
|摘要|指定摘要式身份验证。|  
|Ntlm|指定 NTLM 身份验证（如果可能且 Windows 身份验证失败）。|  
|Windows|指定 Windows 集成身份验证。|  
  
## proxyCredentialType 属性  
  
|值|描述|  
|-------|--------|  
|无|-   在传输过程中不能保证消息的安全。|  
|Basic|指定“RFC 2617 – HTTP 身份验证：基本和摘要式身份验证”所定义的基本身份验证。|  
|摘要|指定“RFC 2617 – HTTP 身份验证：基本和摘要式身份验证”所定义的摘要式身份验证。|  
|Ntlm|指定 NTLM 身份验证（如果可能且 Windows 身份验证失败）。|  
|Windows|指定 Windows 集成身份验证。|  
|证书|使用证书执行客户端身份验证。  此选项只在父 `security` 元素的 `Mode` 属性设置为“Transport”时才起作用，如果该属性设置为“TransportCredentialOnly”，则此选项将不起作用。|  
  
### 子元素  
 无  
  
### 父元素  
  
|元素|描述|  
|--------|--------|  
|[\<安全性\>](../../../../../docs/framework/configure-apps/file-schema/wcf/security-of-basichttpbinding.md)|定义 [\<basicHttpBinding\>](../../../../../docs/framework/configure-apps/file-schema/wcf/basichttpbinding.md)的安全功能。|  
  
## 示例  
 下面的示例演示如何对基本绑定使用 SSL 传输安全。  默认情况下，基本绑定支持 HTTP 通信。  
  
```  
<system.serviceModel>  
   <services>  
      <service   
          type="Microsoft.ServiceModel.Samples.CalculatorService"  
          behaviorConfiguration="CalculatorServiceBehavior">  
         <endpoint address=""  
               binding="basicHttpBinding"  
               bindingConfiguration="Binding1"   
               contract="Microsoft.ServiceModel.Samples.ICalculator" />  
      </service>  
   </services>  
    <bindings>  
        <basicHttpBinding>  
        <!-- Configure basicHttpBinding with Transport security -- >  
        <!-- mode and clientCredentialType set to None.-->  
           <binding name="Binding1">  
               <security mode="Transport">  
                   <transport clientCredentialType="None"  
                              proxyCredentialType="None">  
                       <extendedProtectionPolicy  
                          policyEnforcement="WhenSupported"  
                          protectionScenario="TransportSelected">  
                    <customServiceNames></customServiceNames>  
                       </extendedProtectionPolicy>  
               </security>  
           </binding>  
        </basicHttpBinding>  
    </bindings>  
</system.serviceModel>  
```  
  
## 请参阅  
 <xref:System.ServiceModel.Configuration.BasicHttpSecurityElement.Transport%2A>   
 <xref:System.ServiceModel.BasicHttpSecurity.Transport%2A>   
 <xref:System.ServiceModel.Configuration.HttpTransportSecurityElement>   
 <xref:System.ServiceModel.HttpTransportSecurity>   
 [保护服务和客户端的安全](../../../../../docs/framework/wcf/feature-details/securing-services-and-clients.md)   
 [绑定](../../../../../docs/framework/wcf/bindings.md)   
 [配置系统提供的绑定](../../../../../docs/framework/wcf/feature-details/configuring-system-provided-bindings.md)   
 [Using Bindings to Configure Windows Communication Foundation Services and Clients](http://msdn.microsoft.com/zh-cn/bd8b277b-932f-472f-a42a-b02bb5257dfb)   
 [\<绑定\>](../../../../../docs/framework/misc/binding.md)