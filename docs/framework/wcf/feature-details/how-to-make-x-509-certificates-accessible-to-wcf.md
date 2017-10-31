---
title: "如何：使 X.509 证书可由 WCF 访问 | Microsoft Docs"
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
  - "证书 [WCF], 使 X.509 证书可由 WCF 访问"
  - "X.509 证书 [WCF]"
  - "X.509 证书 [WCF], 使之可由 WCF 访问"
ms.assetid: a54e407c-c2b5-4319-a648-60e43413664b
caps.latest.revision: 7
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 7
---
# 如何：使 X.509 证书可由 WCF 访问
若要使 X.509 证书可由 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 访问，应用程序代码必须指定证书存储区的名称和位置。在某些情况下，进程标识必须具有对包含私钥的文件的访问权限，此私钥与 X.509 证书相关联。若要获取与证书存储区中的 X.509 证书关联的私钥，[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 必须有权这样做。默认情况下，只有所有者和“系统”帐户才可以访问证书的私钥。  
  
### 使 X.509 证书可由 WCF 访问  
  
1.  向 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 运行时所使用的帐户授予对包含与 X.509 证书关联的私钥的文件的读访问权限。  
  
    1.  确定 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 是否要求对 X.509 证书的私钥的读访问权限。  
  
         下表详细描述在使用某个 X.509 证书时是否必须提供私钥。  
  
        |X.509 证书用途|私钥|  
        |----------------|--------|  
        |对出站 SOAP 消息进行数字签名。|是|  
        |验证入站 SOAP 消息的签名。|否|  
        |对出站 SOAP 消息进行加密。|否|  
        |对入站 SOAP 消息进行解密。|是|  
  
    2.  确定在其中存储证书的存储区的位置和名称。  
  
         在其中存储证书的证书存储区要么在应用程序代码中指定，要么在配置中指定。例如，下面的示例指定证书位于名为 `My` 的 `CurrentUser` 证书存储区中。  
  
         [!code-csharp[x509Accessible#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/x509accessible/cs/source.cs#1)]
         [!code-vb[x509Accessible#1](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/x509accessible/vb/source.vb#1)]  
  
    3.  使用 [FindPrivateKey](../../../../docs/framework/wcf/samples/findprivatekey.md) 工具确定证书的私钥在计算机上的存储位置。  
  
         [FindPrivateKey](../../../../docs/framework/wcf/samples/findprivatekey.md) 工具需要证书存储区名称、证书存储区位置以及可以唯一标识此证书的某些信息。此工具接受将证书的主题名称或其指纹作为唯一标识符。[!INCLUDE[crabout](../../../../includes/crabout-md.md)]如何确定证书的指纹的更多信息，请参见[如何：检索证书的指纹](../../../../docs/framework/wcf/feature-details/how-to-retrieve-the-thumbprint-of-a-certificate.md)。  
  
         下面的代码示例使用 [FindPrivateKey](../../../../docs/framework/wcf/samples/findprivatekey.md) 工具来确定指纹为 `46 dd 0e 7a ed 0b 7a 31 9b 02 a3 a0 43 7a d8 3f 60 40 92 9d` 的证书的私钥在 `CurrentUser` 的 `My` 存储区中的位置。  
  
        ```  
        findprivatekey.exe My CurrentUser -t "46 dd 0e 7a ed 0b 7a 31 9b 02 a3 a0 43 7a d8 3f 60 40 92 9d" -a  
        ```  
  
    4.  确定 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 运行时所使用的帐户。  
  
         下表详细描述 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 运行时针对指定方案使用的帐户。  
  
        |方案|进程标识|  
        |--------|----------|  
        |客户端（控制台或 WinForms 应用程序）。|当前登录的用户。|  
        |自承载服务。|当前登录的用户。|  
        |在 IIS 6.0 \([!INCLUDE[ws2003](../../../../includes/ws2003-md.md)]\) 或 IIS 7.0 \([!INCLUDE[wv](../../../../includes/wv-md.md)]\) 中承载的服务。|NETWORK SERVICE|  
        |在 IIS 5.X \([!INCLUDE[wxp](../../../../includes/wxp-md.md)]\) 中承载的服务。|由 Machine.config 文件中的 `<processModel>` 元素控制。默认帐户为 ASPNET。|  
  
    5.  使用 cacls.exe 等工具向 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 运行时所使用的帐户授予对包含私钥的文件的读访问权限。  
  
         下面的代码示例编辑 \(\/E\) 指定文件的访问控制列表 \(ACL\)，以向“NETWORK SERVICE”帐户授予 \(\/G\) 对此文件的读 \(:R\) 访问权限。  
  
        ```  
        cacls.exe "C:\Documents and Settings\All Users\Application Data\Microsoft\Crypto\RSA\MachineKeys\8aeda5eb81555f14f8f9960745b5a40d_38f7de48-5ee9-452d-8a5a-92789d7110b1" /E /G "NETWORK SERVICE":R  
        ```  
  
## 请参阅  
 [FindPrivateKey](../../../../docs/framework/wcf/samples/findprivatekey.md)   
 [如何：检索证书的指纹](../../../../docs/framework/wcf/feature-details/how-to-retrieve-the-thumbprint-of-a-certificate.md)   
 [使用证书](../../../../docs/framework/wcf/feature-details/working-with-certificates.md)