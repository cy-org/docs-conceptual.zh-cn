---
title: "HTTPS、通过 TCP 的 SSL 与 SOAP 安全之间的证书验证差异 | Microsoft Docs"
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
  - "证书 [WCF], 验证差异"
ms.assetid: 953a219f-4745-4019-9894-c70704f352e6
caps.latest.revision: 14
author: "BrucePerlerMS"
ms.author: "bruceper"
manager: "mbaldwin"
caps.handback.revision: 14
---
# HTTPS、通过 TCP 的 SSL 与 SOAP 安全之间的证书验证差异
除了通过 HTTP \(HTTPS\) 或 TCP 的传输层安全 \(TLS\) 之外，您还可以在 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 中使用具有消息层 \(SOAP\) 安全的证书。本主题介绍此类证书的验证方式的差异。  
  
## 验证 HTTPS 客户端证书  
 当使用 HTTPS 在客户端和服务间通信时，客户端用于向服务进行身份验证的证书必须支持链信任。也就是说，它必须链至受信任的根证书颁发机构。否则，HTTP 层将引发 <xref:System.Net.WebException>，并显示消息“远程服务器返回错误：\(403\) 禁止。”[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 将此异常包装为 <xref:System.ServiceModel.Security.MessageSecurityException>。  
  
## 验证 HTTPS 服务证书  
 当使用 HTTPS 在客户端和服务间通信时，服务器身份验证使用的证书默认情况下必须支持链信任。也就是说，它必须链至受信任的根证书颁发机构。不会执行任何在线检查来查看证书是否已吊销。可以通过注册 <xref:System.Net.Security.RemoteCertificateValidationCallback> 回调来重写此行为，如以下代码所示。  
  
 [!code-csharp[c_CertificateValidationDifferences#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_certificatevalidationdifferences/cs/source.cs#1)]
 <!-- TODO: review snippet reference [!code-vb[c_CertificateValidationDifferences#1](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_certificatevalidationdifferences/vb/source.vb#1)]  -->  
  
 其中，`ValidateServerCertificate` 的签名如下：  
  
 [!code-csharp[c_CertificateValidationDifferences#2](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_certificatevalidationdifferences/cs/source.cs#2)]
 [!code-vb[c_CertificateValidationDifferences#2](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_certificatevalidationdifferences/vb/source.vb#2)]  
  
 实现 `ValidateServerCertificate` 可以执行客户端应用程序开发人员认为在验证服务证书时有必要进行的任何检查。  
  
## 验证通过 TCP 的 SSL 或 SOAP 安全中的客户端证书  
 使用通过 TCP 的安全套接字层 \(SSL\) 或消息 \(SOAP\) 安全时，根据 <xref:System.ServiceModel.Security.X509ClientCertificateAuthentication> 类的 <xref:System.ServiceModel.Security.X509ClientCertificateAuthentication.CertificateValidationMode%2A> 属性值验证客户端证书。该属性设置为 <xref:System.ServiceModel.Security.X509CertificateValidationMode> 值之一。根据 <xref:System.ServiceModel.Security.X509ClientCertificateAuthentication> 类的 <xref:System.ServiceModel.Security.X509ClientCertificateAuthentication.RevocationMode%2A> 属性值的值来执行吊销检查。该属性设置为 <xref:System.Security.Cryptography.X509Certificates.X509RevocationMode> 值之一。  
  
 [!code-csharp[c_CertificateValidationDifferences#3](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_certificatevalidationdifferences/cs/source.cs#3)]
 [!code-vb[c_CertificateValidationDifferences#3](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_certificatevalidationdifferences/vb/source.vb#3)]  
  
## 验证通过 TCP 的 SSL 和 SOAP 安全中的服务证书  
 使用通过 TCP 的 SSL 或 \(SOAP\) 消息安全时，根据 <xref:System.ServiceModel.Security.X509ServiceCertificateAuthentication> 类的 <xref:System.ServiceModel.Security.X509ServiceCertificateAuthentication.CertificateValidationMode%2A> 属性值来验证服务证书。该属性设置为 <xref:System.ServiceModel.Security.X509CertificateValidationMode> 值之一。  
  
 根据 <xref:System.ServiceModel.Security.X509ServiceCertificateAuthentication> 类的 <xref:System.ServiceModel.Security.X509ServiceCertificateAuthentication.RevocationMode%2A> 属性值的值来执行吊销检查。该属性设置为 <xref:System.Security.Cryptography.X509Certificates.X509RevocationMode> 值之一。  
  
 [!code-csharp[c_CertificateValidationDifferences#4](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_certificatevalidationdifferences/cs/source.cs#4)]
 [!code-vb[c_CertificateValidationDifferences#4](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_certificatevalidationdifferences/vb/source.vb#4)]  
  
## 请参阅  
 <xref:System.Net.Security.RemoteCertificateValidationCallback>   
 [使用证书](../../../../docs/framework/wcf/feature-details/working-with-certificates.md)