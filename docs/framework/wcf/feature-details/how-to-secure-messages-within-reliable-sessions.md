---
title: "如何：在可靠会话内保护消息 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: aee33e50-936f-4486-9ca8-c1520c19a62d
caps.latest.revision: 8
author: "BrucePerlerMS"
ms.author: "bruceper"
manager: "mbaldwin"
caps.handback.revision: 8
---
# 如何：在可靠会话内保护消息
本主题概述了使用系统提供的绑定之一来启用在可靠会话内交换的消息的消息级安全所需的步骤。这些绑定支持这种会话，但默认情况下不支持。可使用代码以强制方式或在配置文件中以声明方式来启用安全的可靠会话。此过程使用客户端和服务配置文件来启用安全的可靠会话。  
  
 此过程由以下三个关键任务组成：  
  
1.  指定客户端和服务在可靠会话内交换消息。  
  
2.  在可靠会话内要求消息级安全。  
  
3.  指定客户端必须用来向服务进行身份验证的客户端凭据类型。  
  
 下面这一点在第一个任务中非常重要：终结点配置元素包含一个 `bindingConfiguration` 属性，该属性引用名为“MessageSecurity”（在本示例中）的绑定配置。[\<绑定\>](../../../../docs/framework/misc/binding.md) 配置元素然后可以引用此名称，通过将 [reliableSession](http://msdn.microsoft.com/zh-cn/9c93818a-7dfa-43d5-b3a1-1aafccf3a00b) 元素的 `enabled` 属性设置为 `true` 来启用可靠会话。通过将 `ordered` 属性设置为 `true`，可以要求可靠会话内的有序传送保证。  
  
 有关此配置过程基于的示例的源副本，请参见 [WS 可靠会话](../../../../docs/framework/wcf/samples/ws-reliable-session.md)。  
  
 第二项任务的基本项是通过将包含在客户端和服务的 \<`binding`\> 元素中的 \<`security`\> 元素的 `mode` 属性设置为 `Message` 来完成的。  
  
 第三项任务的基本项是通过将包含在客户端和服务的 \<`security`\> 元素中的 \<`message`\> 元素的 `clientCredentialType` 属性设置为 `Certificate` 来完成的。  
  
> [!NOTE]
>  在与可靠会话一起使用消息安全性时，如果未对客户端进行身份验证，则可靠消息将会尝试对客户端进行身份验证直到发生超时，而不是在首次失败时就引发异常。  
  
### 使用 WSHttpBinding 配置服务以使用可靠会话  
  
1.  此过程在[如何：在可靠会话内交换消息](../../../../docs/framework/wcf/feature-details/how-to-exchange-messages-within-a-reliable-session.md)中描述。  
  
### 使用 WSHttpBinding 配置客户端以使用可靠会话  
  
1.  此过程在[如何：在可靠会话内交换消息](../../../../docs/framework/wcf/feature-details/how-to-exchange-messages-within-a-reliable-session.md)中描述。  
  
### 在配置中设置模式和 ClientCredentialType  
  
1.  向配置文件的 [\<绑定\>](../../../../docs/framework/configure-apps/file-schema/wcf/bindings.md) 元素添加一个适当的绑定元素。下面的示例添加了一个 [\<wsHttpBinding\>](../../../../docs/framework/configure-apps/file-schema/wcf/wshttpbinding.md) 元素。  
  
2.  添加一个 \<`binding`\> 元素，并将其 `name` 属性设置为适当的值。  
  
3.  添加一个 `<security>` 元素，并将 `mode` 属性设置为 `Message`。  
  
     下面的示例将模式设置为 `Message`，并将 \<`message`\> 元素的 `clientCredentialType` 属性设置为 `Certificate`。  
  
    ```  
    <wsHttpBinding>  
    <binding name="MessageSecurity">  
        <security mode="Message" />  
           <message clientCredentialType = " Certificate" />  
        </security>  
    </binding>  
    </wsHttpBinding >  
    ```