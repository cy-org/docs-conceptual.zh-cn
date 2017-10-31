---
title: "如何：验证 XML 文档的数字签名 | Microsoft Docs"
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
  - "检查签名"
  - "数字签名, 验证"
  - "签名, 加密"
  - "System.Security.Cryptography.RSACryptoServiceProvider 类"
  - "System.Security.Cryptography.SignedXml 类"
  - "验证签名"
  - "XML 数字签名"
ms.assetid: a4d5ceb1-b9f5-47e8-9e4a-a2b39110002f
caps.latest.revision: 8
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 8
---
# 如何：验证 XML 文档的数字签名
可以使用 <xref:System.Security.Cryptography.Xml> 命名空间中的类来验证签有数字签名的 XML 数据。  使用 XML 数字签名 \(XMLDSIG\)，你可以验证签名后的数据没有被更改。  有关 XMLDSIG 标准的详细信息，请参阅万维网联合会 \(W3C\) 规范（位于 http:\/\/www.w3.org\/TR\/xmldsig\-core\/）。  
  
 此过程中的代码示例演示了如何验证包含在 \<`Signature`\> 元素中的 XML 数字签名。  该示例检索密钥容器中 RSA 公钥，然后使用该密钥来验证签名。  
  
 有关如何创建可使用此技术验证的数字签名的信息，请参阅[如何：使用数字签名为 XML 文档签名](../../../docs/standard/security/how-to-sign-xml-documents-with-digital-signatures.md)。  
  
### 验证 XML 文档的数字签名  
  
1.  若要验证文档，必须使用用于签名的同一非对称密钥。  创建 <xref:System.Security.Cryptography.CspParameters> 对象，并指定用于签名的密钥容器的名称。  
  
     [!code-csharp[HowToVerifyXMLDocumentRSA#2](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToVerifyXMLDocumentRSA/cs/sample.cs#2)]
     [!code-vb[HowToVerifyXMLDocumentRSA#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToVerifyXMLDocumentRSA/vb/sample.vb#2)]  
  
2.  检索使用 <xref:System.Security.Cryptography.RSACryptoServiceProvider> 类的公钥。  当将 <xref:System.Security.Cryptography.CspParameters> 对象传递到 <xref:System.Security.Cryptography.RSACryptoServiceProvider> 类的构造函数中时，会按名称从密钥容器自动加载密钥。  
  
     [!code-csharp[HowToVerifyXMLDocumentRSA#3](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToVerifyXMLDocumentRSA/cs/sample.cs#3)]
     [!code-vb[HowToVerifyXMLDocumentRSA#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToVerifyXMLDocumentRSA/vb/sample.vb#3)]  
  
3.  通过从磁盘加载 XML 文件来创建 <xref:System.Xml.XmlDocument> 对象。  <xref:System.Xml.XmlDocument> 对象包含要验证的已签名 XML 文档。  
  
     [!code-csharp[HowToVerifyXMLDocumentRSA#4](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToVerifyXMLDocumentRSA/cs/sample.cs#4)]
     [!code-vb[HowToVerifyXMLDocumentRSA#4](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToVerifyXMLDocumentRSA/vb/sample.vb#4)]  
  
4.  创建一个新的 <xref:System.Security.Cryptography.Xml.SignedXml> 对象，并向其传递 <xref:System.Xml.XmlDocument> 对象。  
  
     [!code-csharp[HowToVerifyXMLDocumentRSA#5](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToVerifyXMLDocumentRSA/cs/sample.cs#5)]
     [!code-vb[HowToVerifyXMLDocumentRSA#5](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToVerifyXMLDocumentRSA/vb/sample.vb#5)]  
  
5.  找到 \<`signature`\> 元素，并创建新的 <xref:System.Xml.XmlNodeList> 对象。  
  
     [!code-csharp[HowToVerifyXMLDocumentRSA#6](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToVerifyXMLDocumentRSA/cs/sample.cs#6)]
     [!code-vb[HowToVerifyXMLDocumentRSA#6](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToVerifyXMLDocumentRSA/vb/sample.vb#6)]  
  
6.  将第一个 \<`signature`\> 元素的 XML 加载到 <xref:System.Security.Cryptography.Xml.SignedXml> 对象中。  
  
     [!code-csharp[HowToVerifyXMLDocumentRSA#7](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToVerifyXMLDocumentRSA/cs/sample.cs#7)]
     [!code-vb[HowToVerifyXMLDocumentRSA#7](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToVerifyXMLDocumentRSA/vb/sample.vb#7)]  
  
7.  使用 <xref:System.Security.Cryptography.Xml.SignedXml.CheckSignature%2A> 方法和 RSA 公钥检查签名。  此方法返回一个指示成功或失败的布尔值。  
  
     [!code-csharp[HowToVerifyXMLDocumentRSA#8](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToVerifyXMLDocumentRSA/cs/sample.cs#8)]
     [!code-vb[HowToVerifyXMLDocumentRSA#8](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToVerifyXMLDocumentRSA/vb/sample.vb#8)]  
  
## 示例  
 此示例假定名为 `"test.xml"` 的文件与已编译程序存在于同一目录中。  必须使用[如何：使用数字签名为 XML 文档签名](../../../docs/standard/security/how-to-sign-xml-documents-with-digital-signatures.md)中所述的技术对 `"test.xml"` 文件进行签名。  
  
 [!code-csharp[HowToVerifyXMLDocumentRSA#1](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToVerifyXMLDocumentRSA/cs/sample.cs#1)]
 [!code-vb[HowToVerifyXMLDocumentRSA#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToVerifyXMLDocumentRSA/vb/sample.vb#1)]  
  
## 编译代码  
  
-   若要编译此示例，需要包含对 `System.Security.dll` 的引用。  
  
-   包括以下命名空间：<xref:System.Xml>、<xref:System.Security.Cryptography> 和 <xref:System.Security.Cryptography.Xml>。  
  
## .NET Framework 安全性  
 切勿用纯文本存储或传输非对称密钥对的私钥。  有关对称和非对称加密密钥的详细信息，请参阅[生成加密和解密的密钥](../../../docs/standard/security/generating-keys-for-encryption-and-decryption.md)。  
  
 切勿将私钥直接嵌入到源代码中。  可通过使用 [Ildasm.exe（IL 反汇编程序）](../../../docs/framework/tools/ildasm-exe-il-disassembler.md) 或在文本编辑器（如记事本）中打开程序集的方式轻松从程序集中读取嵌入的密钥。  
  
## 请参阅  
 <xref:System.Security.Cryptography.Xml>   
 [如何：使用数字签名为 XML 文档签名](../../../docs/standard/security/how-to-sign-xml-documents-with-digital-signatures.md)