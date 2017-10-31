---
title: "如何：自定义系统提供的绑定 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: f8b97862-e8bb-470d-8b96-07733c21fe26
caps.latest.revision: 10
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 10
---
# 如何：自定义系统提供的绑定
[!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 包含若干个系统提供的绑定，这些绑定允许您配置基础绑定元素的某些属性，但不是全部的属性。  本主题演示如何设置绑定元素上的属性以创建自定义绑定。  
  
 [!INCLUDE[crabout](../../../../includes/crabout-md.md)]如何直接创建和配置绑定元素而不使用系统提供的绑定的更多信息，请参见[自定义绑定](../../../../docs/framework/wcf/extending/custom-bindings.md)。  
  
 [!INCLUDE[crabout](../../../../includes/crabout-md.md)]创建并扩展自定义绑定的更多信息，请参见[扩展绑定](../../../../docs/framework/wcf/extending/extending-bindings.md)。  
  
 在 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 中，所有绑定都由绑定元素组成。  每个绑定元素都是从 <xref:System.ServiceModel.Channels.BindingElement> 类派生的。  系统提供的绑定（如 <xref:System.ServiceModel.BasicHttpBinding>）可创建和配置各自的绑定元素。  本主题演示如何访问和更改这些绑定元素的属性，这些属性不会直接在绑定上公开，具体而言，这些属性不会直接在 <xref:System.ServiceModel.BasicHttpBinding> 类上公开。  
  
 各个绑定元素都包含在由 <xref:System.ServiceModel.Channels.BindingElementCollection> 类表示的集合中，并按如下顺序添加：事务流、可靠会话、安全、复合双工、单向、流安全、消息编码和传输协议。  请注意，并不是每个绑定中都需要所列的所有绑定元素。  用户定义的绑定元素也可以出现在此绑定元素集合中，但必须按前面所述的相同顺序出现。  例如，用户定义的传输协议必须为绑定元素集合中的最后一个元素。  
  
 <xref:System.ServiceModel.BasicHttpBinding> 类包含三个绑定元素：  
  
1.  可选的安全绑定元素，即，与 HTTP 传输协议（消息级安全）一起使用的 <xref:System.ServiceModel.Channels.AsymmetricSecurityBindingElement> 类，或在传输协议层提供安全性时使用的 <xref:System.ServiceModel.Channels.TransportSecurityBindingElement> 类（这种情况下将使用 HTTPS 传输协议）。  
  
2.  必需的消息编码器绑定元素，即，<xref:System.ServiceModel.Channels.TextMessageEncodingBindingElement> 或 <xref:System.ServiceModel.Channels.MtomMessageEncodingBindingElement>。  
  
3.  必需的传输绑定元素，即，<xref:System.ServiceModel.Channels.HttpTransportBindingElement> 或 <xref:System.ServiceModel.Channels.HttpsTransportBindingElement>。  
  
 在此示例中，创建绑定的一个实例，并从中生成自定义绑定，再检查自定义绑定中的绑定元素，在发现 HTTP 绑定元素时，将其 `KeepAliveEnabled` 属性设置为 `false`。  由于在 `BasicHttpBinding` 上未直接公开 `KeepAliveEnabled` 属性，因此必须创建一个自定义绑定以向下导航至绑定元素，并设置此属性。  
  
### 修改系统提供的绑定  
  
1.  创建 <xref:System.ServiceModel.BasicHttpBinding> 类的一个实例，并将其安全模式设置为消息级。  
  
     [!code-csharp[C_HowTo_ChangeStandardBinding#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_howto_changestandardbinding/cs/program.cs#1)]
     [!code-vb[C_HowTo_ChangeStandardBinding#1](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_howto_changestandardbinding/vb/program.vb#1)]  
  
2.  从该绑定创建一个自定义绑定，并从该自定义绑定的一个属性创建 <xref:System.ServiceModel.Channels.BindingElementCollection> 类。  
  
     [!code-csharp[C_HowTo_ChangeStandardBinding#2](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_howto_changestandardbinding/cs/program.cs#2)]
     [!code-vb[C_HowTo_ChangeStandardBinding#2](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_howto_changestandardbinding/vb/program.vb#2)]  
  
3.  循环通过 <xref:System.ServiceModel.Channels.BindingElementCollection> 类，并在查找 <xref:System.ServiceModel.Channels.HttpTransportBindingElement> 类时，将其 <xref:System.ServiceModel.Channels.HttpTransportBindingElement.KeepAliveEnabled%2A> 属性设置为 `false`。  
  
     [!code-csharp[C_HowTo_ChangeStandardBinding#3](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_howto_changestandardbinding/cs/program.cs#3)]
     [!code-vb[C_HowTo_ChangeStandardBinding#3](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_howto_changestandardbinding/vb/program.vb#3)]  
  
## 请参阅  
 <xref:System.ServiceModel.Channels.HttpTransportBindingElement>   
 <xref:System.ServiceModel.BasicHttpBinding>   
 <xref:System.ServiceModel.Channels.CustomBinding>   
 [自定义绑定](../../../../docs/framework/wcf/extending/custom-bindings.md)