---
title: "如何：设置最大时钟偏差 | Microsoft Docs"
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
  - "MaxClockSkew 属性"
  - "WCF, 自定义绑定"
ms.assetid: 491d1705-eb29-43c2-a44c-c0cf996f74eb
caps.latest.revision: 13
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 13
---
# 如何：设置最大时钟偏差
如果两台计算机上的时钟设置不同，时间关键函数可能无法正常执行。  若要减小这种可能性，可以将 `MaxClockSkew` 属性设置为一个 <xref:System.TimeSpan>。  可在两个类上获得此属性：  
  
 <xref:System.ServiceModel.Channels.LocalClientSecuritySettings>  
  
 <xref:System.ServiceModel.Channels.LocalServiceSecuritySettings>  
  
> [!IMPORTANT]
>  重要事项   对于安全对话，在引导服务或客户端时，必须对 `MaxClockSkew` 属性进行更改。  为此，必须在 <xref:System.ServiceModel.Channels.SecurityBindingElement> 返回的 <xref:System.ServiceModel.Security.Tokens.SecureConversationSecurityTokenParameters.BootstrapSecurityBindingElement%2A> 上设置该属性。  
  
 若要更改系统提供的绑定之一上的属性，必须在绑定集合中找到安全绑定元素，然后将 `MaxClockSkew` 属性设置为一个新值。  两个类派生自 <xref:System.ServiceModel.Channels.SecurityBindingElement>: <xref:System.ServiceModel.Channels.SymmetricSecurityBindingElement> 和 <xref:System.ServiceModel.Channels.AsymmetricSecurityBindingElement>。  从该集合中检索安全绑定时，必须将其强制转换为上述类型之一，以便正确设置 `MaxClockSkew` 属性。  下面的示例使用了一个 <xref:System.ServiceModel.WSHttpBinding>，它使用了 <xref:System.ServiceModel.Channels.SymmetricSecurityBindingElement>。  有关指定在系统提供的每个绑定中使用哪种类型的安全绑定的列表，请参见[系统提供的绑定](../../../../docs/framework/wcf/system-provided-bindings.md)。  
  
### 在代码中使用新的时钟偏差值创建自定义绑定  
  
1.  > [!WARNING]
    >  注意   在代码中添加对以下命名空间的引用：<xref:System.ServiceModel.Channels>、<xref:System.ServiceModel.Description>、<xref:System.Security.Permissions> 和 <xref:System.ServiceModel.Security.Tokens>。  
  
     创建 <xref:System.ServiceModel.WSHttpBinding> 类的一个实例，并将其安全模式设置为 <xref:System.ServiceModel.SecurityMode>。  
  
2.  调用 <xref:System.ServiceModel.Channels.BindingElementCollection> 方法，以此创建 <xref:System.ServiceModel.WSHttpBinding.CreateBindingElements%2A> 的一个新实例。  
  
3.  使用 <xref:System.ServiceModel.Channels.BindingElementCollection.Find%2A> 类的 <xref:System.ServiceModel.Channels.BindingElementCollection> 方法来查找安全绑定元素。  
  
4.  使用 <xref:System.ServiceModel.Channels.BindingElementCollection.Find%2A> 方法时，将其强制转换为实际类型。  下面的示例将其强制转换为 <xref:System.ServiceModel.Channels.SymmetricSecurityBindingElement> 类型。  
  
5.  设置安全绑定元素上的 <xref:System.ServiceModel.Channels.LocalServiceSecuritySettings.MaxClockSkew%2A> 属性。  
  
6.  使用适当的服务类型和基址创建一个 <xref:System.ServiceModel.ServiceHost>。  
  
7.  使用 <xref:System.ServiceModel.ServiceHost.AddServiceEndpoint%2A> 方法添加一个终结点并包含该 <xref:System.ServiceModel.Channels.CustomBinding>。  
  
     [!code-csharp[c_MaxClockSkew#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_maxclockskew/cs/source.cs#1)]
     [!code-vb[c_MaxClockSkew#1](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_maxclockskew/vb/source.vb#1)]  
  
### 在配置中设置 MaxClockSkew  
  
1.  在 [\<绑定\>](../../../../docs/framework/configure-apps/file-schema/wcf/bindings.md) 元素节创建一个 [\<customBinding\>](../../../../docs/framework/configure-apps/file-schema/wcf/custombinding.md)。  
  
2.  创建一个 [\<绑定\>](../../../../docs/framework/misc/binding.md) 元素，并将 `name` 属性设置为适当的值。  下面的示例将其设置为 `MaxClockSkewBinding`。  
  
3.  添加一个编码元素。  下面的示例添加一个 [\<textMessageEncoding\>](../../../../docs/framework/configure-apps/file-schema/wcf/textmessageencoding.md)。  
  
4.  添加 [\<安全性\>](../../../../docs/framework/configure-apps/file-schema/wcf/security-of-custombinding.md)，并将 `authenticationMode` 属性设置为适当的设置。  下面的示例将该属性设置为 `Kerberos`，以指定服务使用 Windows 身份验证。  
  
5.  添加一个 [\<localServiceSettings\>](../../../../docs/framework/configure-apps/file-schema/wcf/localservicesettings-element.md)，并将 `maxClockSkew` 属性设置 `"##:##:##"` 形式的值。  下面的示例将其设置为 7 分钟。  还可以根据需要添加一个 [\<localServiceSettings\>](../../../../docs/framework/configure-apps/file-schema/wcf/localservicesettings-element.md)，并将 `maxClockSkew` 属性设置为适当的设置。  
  
6.  添加一个传输元素。  下面的示例使用 [\<httpTransport\>](../../../../docs/framework/configure-apps/file-schema/wcf/httptransport.md)。  
  
7.  对于安全对话，在引导时安全设置必须出现在 [\<secureConversationBootstrap\>](../../../../docs/framework/configure-apps/file-schema/wcf/secureconversationbootstrap.md) 元素中。  
  
    ```  
  
    <bindings>  
      <customBinding>  
        <binding name="MaxClockSkewBinding">  
            <textMessageEncoding />  
            <security authenticationMode="Kerberos">  
               <localClientSettings maxClockSkew="00:07:00" />  
               <localServiceSettings maxClockSkew="00:07:00" />  
               <secureConversationBootstrap>  
                  <localClientSettings maxClockSkew="00:30:00" />  
                  <localServiceSettings maxClockSkew="00:30:00" />  
               </secureConversationBootstrap>  
            </security>  
            <httpTransport />  
        </binding>  
      </customBinding>  
    </bindings>  
  
    ```  
  
## 请参阅  
 <xref:System.ServiceModel.Channels.LocalClientSecuritySettings>   
 <xref:System.ServiceModel.Channels.LocalServiceSecuritySettings>   
 <xref:System.ServiceModel.Channels.CustomBinding>   
 [如何：使用 SecurityBindingElement 创建自定义绑定](../../../../docs/framework/wcf/feature-details/how-to-create-a-custom-binding-using-the-securitybindingelement.md)