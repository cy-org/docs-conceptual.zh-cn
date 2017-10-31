---
title: "如何：启用消息重播检测 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "重播检测 [WCF]"
  - "WCF 安全性"
  - "WCF, 自定义绑定"
  - "WCF, 安全性"
ms.assetid: 8b847e91-69a3-49e1-9e5f-0c455e50d804
caps.latest.revision: 10
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 10
---
# 如何：启用消息重播检测
当攻击者复制双方之间的消息流并将该消息流向一方或多方重播时，将发生重播攻击。除非攻击程度降低，否则受到攻击的计算机会将该流处理为合法消息，从而导致产生大量不良结果，例如某项的冗余排序。  
  
 [!INCLUDE[crabout](../../../../includes/crabout-md.md)]消息重播检测的更多信息，请参见[消息重播检测](http://go.microsoft.com/fwlink/?LinkId=88536)（可能为英文网页）。  
  
 下面的过程演示在用 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 控制重播检测时所使用的各种属性。  
  
### 使用代码在客户端上控制重播检测  
  
1.  创建要在 <xref:System.ServiceModel.Channels.CustomBinding> 中使用的 <xref:System.ServiceModel.Channels.SecurityBindingElement>。[!INCLUDE[crdefault](../../../../includes/crdefault-md.md)][如何：使用 SecurityBindingElement 创建自定义绑定](../../../../docs/framework/wcf/feature-details/how-to-create-a-custom-binding-using-the-securitybindingelement.md).下面的示例使用通过 <xref:System.ServiceModel.Channels.SecurityBindingElement> 类的 <xref:System.ServiceModel.Channels.SecurityBindingElement.CreateKerberosBindingElement%2A> 创建的 <xref:System.ServiceModel.Channels.SymmetricSecurityBindingElement>。  
  
2.  使用 <xref:System.ServiceModel.Channels.SecurityBindingElement.LocalClientSettings%2A> 属性返回对 <xref:System.ServiceModel.Channels.LocalClientSecuritySettings> 类的引用，并根据需要设置任何下列属性：  
  
    1.  `DetectReplay`.一个布尔值。该值控制客户端是否应当检测来自服务器的重播。默认值为 `true`。  
  
    2.  `MaxClockSkew`.<xref:System.TimeSpan> 值。控制重播机制在客户端和服务器之间可以容忍多大程度的时间偏差。该安全机制检查发送的时间戳，并确定在过去它是否返回过快。默认值为 5 分钟。  
  
    3.  `ReplayWindow`.`TimeSpan` 值。该值控制某消息在由服务器（通过中间方）发送之后、到达客户端之前在网络中存留的时间。客户端跟踪在最后一个 `ReplayWindow` 中发送的消息的签名，以进行重播检测。  
  
    4.  `ReplayCacheSize`.一个整数值。客户端在缓存中存储消息的签名。此设置指定缓存中可以存储的签名数目。如果最后一个重播窗口中发送的消息数达到缓存限制，则拒绝新消息，直到最旧的缓存签名达到时间限制为止。默认值为 500000。  
  
### 使用代码在服务上控制重播检测  
  
1.  创建要在 <xref:System.ServiceModel.Channels.CustomBinding> 中使用的 <xref:System.ServiceModel.Channels.SecurityBindingElement>。  
  
2.  使用 <xref:System.ServiceModel.Channels.SecurityBindingElement.LocalServiceSettings%2A> 属性返回对 <xref:System.ServiceModel.Channels.LocalServiceSecuritySettings> 类的引用，并按照上面所述设置这些属性。  
  
### 在客户端或服务的配置中控制重播检测  
  
1.  创建 [\<customBinding\>](../../../../docs/framework/configure-apps/file-schema/wcf/custombinding.md)。  
  
2.  创建 `<security>` 元素。  
  
3.  创建 [\<localClientSettings\>](../../../../docs/framework/configure-apps/file-schema/wcf/localclientsettings-element.md)或 [\<localServiceSettings\>](../../../../docs/framework/configure-apps/file-schema/wcf/localservicesettings-element.md)。  
  
4.  根据需要，设置下列属性值：`detectReplays`、`maxClockSkew`、`replayWindow` 和 `replayCacheSize`。下面的示例设置 `<localServiceSettings>``<localClientSettings> 和`  元素的属性：  
  
    ```  
    <customBinding>  
      <binding name="NewBinding0">  
       <textMessageEncoding />  
        <security>  
         <localClientSettings   
          replayCacheSize="800000"   
          maxClockSkew="00:03:00"  
          replayWindow="00:03:00" />  
         <localServiceSettings   
          replayCacheSize="800000"   
          maxClockSkew="00:03:00"  
          replayWindow="00:03:00" />  
        <secureConversationBootstrap />  
       </security>  
      <httpTransport />  
     </binding>  
    </customBinding>  
    ```  
  
## 示例  
 下面的示例使用 <xref:System.ServiceModel.Channels.SecurityBindingElement.CreateKerberosBindingElement%2A> 方法创建 <xref:System.ServiceModel.Channels.SymmetricSecurityBindingElement>，并设置绑定的重播属性。  
  
 [!code-csharp[c_ReplayDetection#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_replaydetection/cs/source.cs#1)]
 [!code-vb[c_ReplayDetection#1](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_replaydetection/vb/source.vb#1)]  
  
## 重播范围：仅限消息安全  
 请注意，下面的过程仅适用于“消息安全”模式。对于“传输”和“使用消息凭据传输”模式，传输机制将检测重播。  
  
## 安全对话说明  
 对于启用安全对话的绑定，可以针对应用程序通道和安全对话引导绑定来调整这些设置。例如，可以对应用程序通道关闭重播，但是对建立安全对话的引导通道启用重播。  
  
 如果不使用安全对话会话，则重播检测不保证在服务器场方案中和回收进程时检测重播。这适用于系统提供的下列绑定：  
  
-   <xref:System.ServiceModel.BasicHttpBinding>.  
  
-   与 <xref:System.ServiceModel.NonDualMessageSecurityOverHttp.EstablishSecurityContext%2A> 属性关联的 <xref:System.ServiceModel.WSHttpBinding> 设置为 `false`。  
  
## 编译代码  
  
-   编译该代码需要以下命名空间：  
  
-   <xref:System>  
  
-   <xref:System.ServiceModel>  
  
-   <xref:System.ServiceModel.Channels>  
  
## 请参阅  
 <xref:System.ServiceModel.Channels.LocalClientSecuritySettings>   
 <xref:System.ServiceModel.Channels.LocalServiceSecuritySettings>   
 [安全对话和安全会话](../../../../docs/framework/wcf/feature-details/secure-conversations-and-secure-sessions.md)   
 [\<localClientSettings\>](../../../../docs/framework/configure-apps/file-schema/wcf/localclientsettings-element.md)   
 [如何：使用 SecurityBindingElement 创建自定义绑定](../../../../docs/framework/wcf/feature-details/how-to-create-a-custom-binding-using-the-securitybindingelement.md)