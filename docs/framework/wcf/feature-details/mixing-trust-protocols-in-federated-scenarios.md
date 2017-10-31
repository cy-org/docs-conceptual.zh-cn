---
title: "在联合方案中混合信任协议 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: d7b5fee9-2246-4b09-b8d7-9e63cb817279
caps.latest.revision: 7
author: "BrucePerlerMS"
ms.author: "bruceper"
manager: "mbaldwin"
caps.handback.revision: 7
---
# 在联合方案中混合信任协议
联合客户端与服务进行通信时，有些服务的信任版本与安全令牌服务 \(STS\) 的信任版本不同。  服务 WSDL 包含的 `RequestSecurityTokenTemplate` 断言可能具有与 STS 不同版本的 WS\-Trust 元素。  在这些情况下，[!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 客户端会转换从 `RequestSecurityTokenTemplate` 接收的 WS\-Trust 元素以匹配 STS 信任版本。  [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 只处理标准绑定的不匹配信任版本。  [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 识别的所有标准算法参数都是标准绑定的一部份。  本主题介绍 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 在服务与 STS 分别具有各种信任设置时的行为。  
  
## RP Feb 2005 和 STS Feb 2005  
 依赖方 \(RP\) 的 WSDL 在 `RequestSecurityTokenTemplate` 节中包含以下元素：  
  
-   `CanonicalizationAlgorithm`  
  
-   `EncryptionAlgorithm`  
  
-   `EncryptWith`  
  
-   `SignWith`  
  
-   `KeySize`  
  
-   `KeyType`  
  
 客户端配置文件包含一个参数列表。  
  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 无法区分客户端参数和服务参数；它添加所有参数并在 `RequestSecurityTokenTemplate` \(RST\) 中发送这些参数。  
  
## RP Trust 1.3 和 STS Trust 1.3  
 RP 的 WSDL 在 `RequestSecurityTokenTemplate` 节中包含以下元素：  
  
-   `CanonicalizationAlgorithm`  
  
-   `EncryptionAlgorithm`  
  
-   `EncryptWith`  
  
-   `SignWith`  
  
-   `KeySize`  
  
-   `KeyType`  
  
-   `KeyWrapAlgorithm`  
  
 客户端配置文件包含一个 `secondaryParameters` 元素，该元素包装 RP 所指定的参数。  
  
 如果 `EncryptionAlgorithm`、`CanonicalizationAlgorithm` 和 `KeyWrapAlgorithm` 元素存在于 `SecondaryParameters` 元素内，则 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 将从 RST 下的顶级元素移除这三个元素。  [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 将 `SecondaryParameters` 元素不经修改地追加到传出 RST 中。  
  
## RP Trust Feb 2005 和 STS Trust 1.3  
 RP 的 WSDL 在 `RequestSecurityTokenTemplate` 节中包含以下元素：  
  
-   `CanonicalizationAlgorithm`  
  
-   `EncryptionAlgorithm`  
  
-   `EncryptWith`  
  
-   `SignWith`  
  
-   `KeySize`  
  
-   `KeyType`  
  
 客户端配置文件包含一个参数列表。  
  
 在客户端配置文件中，[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 无法区分服务参数与客户端参数。  因此 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 将所有参数都转换为 Trust 1.3 版命名空间。  
  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 按以下方式处理 `KeyType`、`KeySize` 和 `TokenType` 元素：  
  
-   下载 WSDL，创建绑定，并从 RP 参数分配 `KeyType`、`KeySize` 和 `TokenType`。  随后会生成客户端配置文件。  
  
-   客户端现在可以更改配置文件中的任何参数。  
  
-   在运行时，[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 将除 `KeyType`、`KeySize` 和 `TokenType` 之外的所有指定参数复制到客户端配置文件的 `AdditionalTokenParameters` 节中，因为这三个参数的版本问题在配置文件生成期间已得到解决。  
  
## RP Trust 1.3 和 STS Trust Feb 2005  
 RP 的 WSDL 在 `RequestSecurityTokenTemplate` 节中包含以下元素：  
  
-   `CanonicalizationAlgorithm`  
  
-   `EncryptionAlgorithm`  
  
-   `EncryptWith`  
  
-   `SignWith`  
  
-   `KeySize`  
  
-   `KeyType`  
  
-   `KeyWrapAlgorithm`  
  
 客户端配置文件包含一个 `secondaryParamters` 元素，该元素包装 RP 所指定的参数。  
  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 将 `SecondaryParameters` 节中指定的所有参数复制到顶级 RST 元素中，但不会将这些参数转换为 2005 WS\-Trust 命名空间。