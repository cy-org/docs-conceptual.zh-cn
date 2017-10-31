---
title: "如何：以一致的方式引用 X.509 证书 | Microsoft Docs"
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
  - "证书 [WCF], 引用 X.509 证书"
ms.assetid: a6de1c63-e450-4640-ad08-ad7302dbfbfc
caps.latest.revision: 6
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 6
---
# 如何：以一致的方式引用 X.509 证书
可以采用下列多种方式来标识证书：证书哈希、颁发者和序列号或者使用者密钥标识符 \(SKI\)。SKI 为证书的使用者公钥提供唯一标识，通常用于处理 XML 数字签名。作为 X.509 证书的一部分，SKI 值通常以“X.509 证书扩展”的形式出现.[!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 具有一个默认的“引用样式”，如果证书中缺少 SKI 扩展，则该样式将使用颁发者和序列号。如果证书中包含 SKI 扩展，该默认引用样式将使用 SKI 来指向证书。如果在应用程序开发过程中，将使用的证书从不使用 SKI 扩展的证书改换为使用 SKI 扩展的证书，则由 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 生成的消息中所使用的引用样式也会随之发生变化。  
  
 如果无论是否存在 SKI 扩展，都需要使用一致的引用样式，则可以配置所需的引用样式，如下面的代码中所示。  
  
## 示例  
 下面的示例创建一个自定义安全绑定元素，该元素使用一致的引用样式：颁发者名称和序列号。  
  
 [!code-csharp[c_ReferencingCertificatesConsistently#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_referencingcertificatesconsistently/cs/source.cs#1)]
 [!code-vb[c_ReferencingCertificatesConsistently#1](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_referencingcertificatesconsistently/vb/source.vb#1)]  
  
## 编译代码  
 编译该代码需要以下命名空间：  
  
-   <xref:System>  
  
-   <xref:System.ServiceModel>  
  
-   <xref:System.ServiceModel.Channels>  
  
-   <xref:System.ServiceModel.Security.Tokens>  
  
## 请参阅  
 [使用证书](../../../../docs/framework/wcf/feature-details/working-with-certificates.md)