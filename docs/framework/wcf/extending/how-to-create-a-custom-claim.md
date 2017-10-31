---
title: "如何：创建自定义声明 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: d619976b-eda3-475e-ac23-c7988a2dceb0
caps.latest.revision: 8
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 8
---
# 如何：创建自定义声明
中的标识模型基础结构[!INCLUDE[indigo1](../../../../includes/indigo1-md.md)]提供了这两个帮助器函数用于创建一组内置的声明类型和权限<xref:System.IdentityModel.Claims.Claim>具有这些类型和权限的实例。 这些内置的声明用于对 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 默认支持的客户端凭据类型中的信息进行建模。 在许多情况下，这些内置的声明足够满足需要，然而一些应用程序可能需要自定义声明。 声明由声明类型、要应用该声明的资源和在该资源上断言的权限组成。 本主题描述如何创建自定义声明。  
  
### <a name="to-create-a-custom-claim-that-is-based-on-a-primitive-data-type"></a>创建基于基元数据类型的自定义声明  
  
1.  通过传递声明类型、 资源值和从右到创建自定义声明<xref:System.IdentityModel.Claims.Claim.%23ctor%28System.String%2CSystem.Object%2CSystem.String%29>构造函数。  
  
    1.  确定声明类型的唯一值。  
  
         声明类型是一个唯一的字符串标识符。 自定义声明的设计者负责确保声明类型所使用的字符串标识符是唯一的。 有关由定义的声明类型的列表[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]，请参阅<xref:System.IdentityModel.Claims.ClaimTypes>类。  
  
    2.  选择资源的基元数据类型和值。  
  
         资源是一个对象。 该资源的 CLR 类型可以是基元，如<xref:System.String>或<xref:System.Int32>，或任何可序列化的类型。 资源的 CLR 类型必须是可序列化的，因为 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 会在不同时刻将声明序列化。 基元类型是可序列化的类型。  
  
    3.  选择 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 定义的一个权限，或者为自定义权限选择一个唯一值。  
  
         权限是一个唯一的字符串标识符。 通过定义的权限[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]中定义<xref:System.IdentityModel.Claims.Rights>类。  
  
         自定义声明的设计者负责确保权限所使用的字符串标识符是唯一的。  
  
         下面的代码示例创建了一个声明类型的自定义声明`http://example.org/claims/simplecustomclaim`，资源名称为`Driver's License`，且<xref:System.IdentityModel.Claims.Rights.PossessProperty%2A>右侧。  
  
     [!code-csharp[c_CustomClaim#4](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_customclaim/cs/c_customclaim.cs#4)]
     [!code-vb[c_CustomClaim#4](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_customclaim/vb/c_customclaim.vb#4)]  
  
### <a name="to-create-a-custom-claim-that-is-based-on-a-non-primitive-data-type"></a>创建基于非基元数据类型的自定义声明  
  
1.  通过传递声明类型、 资源值和从右到创建自定义声明<xref:System.IdentityModel.Claims.Claim.%23ctor%28System.String%2CSystem.Object%2CSystem.String%29>构造函数。  
  
    1.  确定声明类型的唯一值。  
  
         声明类型是一个唯一的字符串标识符。 自定义声明的设计者负责确保声明类型所使用的字符串标识符是唯一的。 有关由定义的声明类型的列表[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]，请参阅<xref:System.IdentityModel.Claims.ClaimTypes>类。  
  
    2.  为资源选择或定义一个可序列化的非基元类型。  
  
         资源是一个对象。 资源的 CLR 类型必须是可序列化的，因为 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 会在不同时刻将声明序列化。 基元类型本身是可序列化的类型。  
  
         当定义新类型时，将应用<xref:System.Runtime.Serialization.DataContractAttribute>到类。 此外将应用<xref:System.Runtime.Serialization.DataMemberAttribute>属性设为新类型的需要作为声明的一部分进行序列化的所有成员。  
  
         下面的代码示例定义了一个名为 `MyResourceType` 的自定义资源类型。  
  
         [!code-csharp[c_CustomClaim#2](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_customclaim/cs/c_customclaim.cs#2)]
         <!-- TODO: review snippet reference [!code-vb[c_CustomClaim#2](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_customclaim/vb/c_customclaim.vb#2)]  -->  
  
    3.  选择 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 定义的一个权限，或者为自定义权限选择一个唯一值。  
  
         权限是一个唯一的字符串标识符。 通过定义的权限[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]中定义<xref:System.IdentityModel.Claims.Rights>类。  
  
         自定义声明的设计者负责确保权限所使用的字符串标识符是唯一的。  
  
         下面的代码示例创建了一个声明类型的自定义声明`http://example.org/claims/complexcustomclaim`，自定义资源类型的`MyResourceType`，且<xref:System.IdentityModel.Claims.Rights.PossessProperty%2A>右侧。  
  
     [!code-csharp[c_CustomClaim#5](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_customclaim/cs/c_customclaim.cs#5)]
     <!-- TODO: review snippet reference [!code-vb[c_CustomClaim#5](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_customclaim/vb/c_customclaim.vb#5)]  -->  
  
## <a name="example"></a>示例  
 下面的代码示例演示如何创建一个具有基元资源类型的自定义声明和一个具有非基元资源类型的自定义声明。  
  
 [!code-csharp[c_CustomClaim#0](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_customclaim/cs/c_customclaim.cs#0)]
 [!code-vb[c_CustomClaim#0](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_customclaim/vb/c_customclaim.vb#0)]  
  
## <a name="see-also"></a>另请参阅  
 <xref:System.IdentityModel.Claims.Claim>   
 <xref:System.IdentityModel.Claims.Rights>   
 <xref:System.IdentityModel.Claims.ClaimTypes>   
 <xref:System.Runtime.Serialization.DataContractAttribute>   
 <xref:System.Runtime.Serialization.DataMemberAttribute>   
 [使用标识模型管理声明和授权](../../../../docs/framework/wcf/feature-details/managing-claims-and-authorization-with-the-identity-model.md)   
 [使用标识模型管理声明和授权](../../../../docs/framework/wcf/feature-details/managing-claims-and-authorization-with-the-identity-model.md)