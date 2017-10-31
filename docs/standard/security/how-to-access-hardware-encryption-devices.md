---
title: "如何：访问硬件加密设备 | Microsoft Docs"
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
  - "密码系统"
  - "CspParameters"
  - "加密"
  - "硬件加密"
  - "密钥卡"
ms.assetid: b0e734df-6eb4-4b16-b48c-6f0fe82d5f17
caps.latest.revision: 9
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 9
---
# 如何：访问硬件加密设备
可使用 <xref:System.Security.Cryptography.CspParameters> 类来访问硬件加密设备。  例如，可以使用此类将你的应用程序与智能卡、硬件随机数字生成器或特定加密算法的硬件实现进行集成。  
  
 <xref:System.Security.Cryptography.CspParameters> 类会创建一个加密服务提供程序 \(CSP\)，该程序可访问正确安装的硬件加密设备。  你可以通过使用注册表编辑器 \(Regedit.exe\) 检查下列注册表项来验证 CSP 的可用性：HKEY\_LOCAL\_MACHINE\\Software\\Microsoft\\Cryptography\\Defaults\\Provider。  
  
### 使用密钥卡对数据进行签名  
  
1.  通过将整数提供程序类型和提供程序名称传递给构造函数，创建 <xref:System.Security.Cryptography.CspParameters> 类的新实例。  
  
2.  将适当的标志传递给新创建的 <xref:System.Security.Cryptography.CspParameters> 对象的 <xref:System.Security.Cryptography.CspParameters.Flags%2A> 属性。  例如，传递 <xref:System.Security.Cryptography.CspProviderFlags> 标志。  
  
3.  通过将 <xref:System.Security.Cryptography.CspParameters> 对象传递给构造函数，创建 <xref:System.Security.Cryptography.AsymmetricAlgorithm> 类（如 <xref:System.Security.Cryptography.RSACryptoServiceProvider> 类）的新实例。  
  
4.  使用其中一种 `Sign` 方法对你的数据进行签名，并使用其中一种 `Verify` 方法来验证你的数据。  
  
### 使用硬件随机数字生成器生成随机数  
  
1.  通过将整数提供程序类型和提供程序名称传递给构造函数，创建 <xref:System.Security.Cryptography.CspParameters> 类的新实例。  
  
2.  通过将 <xref:System.Security.Cryptography.CspParameters> 对象传递给构造函数，创建 <xref:System.Security.Cryptography.RNGCryptoServiceProvider> 的新实例。  
  
3.  使用 <xref:System.Security.Cryptography.RNGCryptoServiceProvider.GetBytes%2A> 或 <xref:System.Security.Cryptography.RNGCryptoServiceProvider.GetNonZeroBytes%2A> 方法创建一个随机值。  
  
## 示例  
 下列代码示例演示如何使用智能卡对数据进行签名。  此代码示例创建一个公开智能卡的 <xref:System.Security.Cryptography.CspParameters> 对象，然后使用 CSP 初始化 <xref:System.Security.Cryptography.RSACryptoServiceProvider> 对象。  然后此代码示例会对某些数据进行签名和验证。  
  
 [!code-cpp[Cryptography.SmartCardCSP#1](../../../samples/snippets/cpp/VS_Snippets_CLR/Cryptography.SmartCardCSP/CPP/Cryptography.SmartCardCSP.cpp#1)]
 [!code-csharp[Cryptography.SmartCardCSP#1](../../../samples/snippets/csharp/VS_Snippets_CLR/Cryptography.SmartCardCSP/CS/example.cs#1)]
 [!code-vb[Cryptography.SmartCardCSP#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Cryptography.SmartCardCSP/VB/example.vb#1)]  
  
## 编译代码  
  
-   包括 <xref:System> 和 <xref:System.Security.Cryptography> 命名空间。  
  
-   计算机上必须安装有智能卡读卡器和驱动程序。  
  
-   必须使用特定于读卡器的信息来初始化 <xref:System.Security.Cryptography.CspParameters> 对象。  有关详细信息，请参阅读卡器的文档。