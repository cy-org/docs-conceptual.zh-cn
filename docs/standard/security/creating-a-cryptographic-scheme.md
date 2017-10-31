---
title: "创建加密方案 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-standard"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - "密码系统 [.NET Framework], 创建加密方案"
  - "加密 [.NET Framework], 创建加密方案"
ms.assetid: d40c509f-5a5e-46cc-94cb-a951e9ab6843
caps.latest.revision: 8
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 8
---
# 创建加密方案
可结合使用 .NET Framework 的加密组件来创建不同的方案，以加密和解密数据。  
  
 用于加密和解密数据的简单加密方案可能指定以下步骤：  
  
1.  每个参与方均生成一个公钥\/私钥对。  
  
2.  双方交换各自的公钥。  
  
3.  例如，每个参与方均生成一个用于加密 TripleDES 的密钥，并使用对方的公钥对新创建的密钥进行加密。  
  
4.  每个参与方都将数据发送给另一方，并以特定的顺序将对方的密钥与自身的密钥相结合，以创建新密钥。  
  
5.  然后，双方使用对称加密启动一个对话。  
  
 创建加密方案是一项重要任务。  有关使用加密的详细信息，请参阅 http:\/\/msdn.microsoft.com\/library 处平台 SDK 文档中的加密主题。  
  
## 请参阅  
 [加密服务](../../../docs/standard/security/cryptographic-services.md)