---
title: "如何：用非对称密钥对 XML 元素进行解密 | Microsoft Docs"
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
  - "非对称密钥"
  - "解密"
  - "System.Security.Cryptography.EncryptedXml 类"
  - "System.Security.Cryptography.RSACryptoServiceProvider 类"
  - "XML 加密"
ms.assetid: dd5de491-dafe-4b94-966d-99714b2e754a
caps.latest.revision: 14
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 14
---
# 如何：用非对称密钥对 XML 元素进行解密
可以使用 <xref:System.Security.Cryptography.Xml> 命名空间中的类对 XML 文档内的元素进行加密和解密。  XML 加密是交换或存储加密的 XML 数据的一种标准方式，使用后就无需担心数据被轻易读取。  有关 XML 加密标准的详细信息，请参阅万维网联合会 \(W3C\) 建议 [XML 签名语法和处理](http://go.microsoft.com/fwlink/?LinkID=136777)。  
  
 此步骤中的示例对使用[如何：用非对称密钥对 XML 元素进行加密](../../../docs/standard/security/how-to-encrypt-xml-elements-with-asymmetric-keys.md)中描述的方法进行加密的 XML 元素进行解密。  它找到一个 \<`EncryptedData`\> 元素，解密该元素，然后将其替换为原始纯文本 XML 元素。  
  
 此示例使用两个密钥对 XML 元素进行解密。  它从密钥容器中检索以前生成的 RSA 私钥，然后使用 RSA 密钥解密存储在 \<`EncryptedData`\> 元素的 \<`EncryptedKey`\> 元素中的会话密钥。  然后此示例使用会话密钥对 XML 元素进行解密。  
  
 此示例适用于以下情况：多个应用程序必须共享加密数据，或应用程序必须保存其每次运行之间的加密数据。  
  
### 用非对称密钥对 XML 元素进行解密  
  
1.  创建 <xref:System.Security.Cryptography.CspParameters> 对象，并指定密钥容器的名称。  
  
     [!code-csharp[HowToDecryptXMLElementAsymmetric#2](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToDecryptXMLElementAsymmetric/cs/sample.cs#2)]
     [!code-vb[HowToDecryptXMLElementAsymmetric#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToDecryptXMLElementAsymmetric/vb/sample.vb#2)]  
  
2.  使用 <xref:System.Security.Cryptography.RSACryptoServiceProvider> 对象从容器中检索以前生成的非对称密钥。  当将 <xref:System.Security.Cryptography.CspParameters> 对象传递到 <xref:System.Security.Cryptography.RSACryptoServiceProvider> 构造函数中时，将自动从密钥容器中检索到密钥。  
  
     [!code-csharp[HowToDecryptXMLElementAsymmetric#3](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToDecryptXMLElementAsymmetric/cs/sample.cs#3)]
     [!code-vb[HowToDecryptXMLElementAsymmetric#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToDecryptXMLElementAsymmetric/vb/sample.vb#3)]  
  
3.  创建新 <xref:System.Security.Cryptography.Xml.EncryptedXml> 对象以对文档进行解密。  
  
     [!code-csharp[HowToDecryptXMLElementAsymmetric#5](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToDecryptXMLElementAsymmetric/cs/sample.cs#5)]
     [!code-vb[HowToDecryptXMLElementAsymmetric#5](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToDecryptXMLElementAsymmetric/vb/sample.vb#5)]  
  
4.  添加一个密钥\/名称映射，以便 RSA 密钥与应该进行解密的文档中的元素相关联。  必须使用与加密文档时所用密钥名称相同的名称。  请注意，此名称独立于用来标识在步骤 1 中指定的密钥容器中的密钥名称。  
  
     [!code-csharp[HowToDecryptXMLElementAsymmetric#6](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToDecryptXMLElementAsymmetric/cs/sample.cs#6)]
     [!code-vb[HowToDecryptXMLElementAsymmetric#6](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToDecryptXMLElementAsymmetric/vb/sample.vb#6)]  
  
5.  调用 <xref:System.Security.Cryptography.Xml.EncryptedXml.DecryptDocument%2A> 方法以解密 \<`EncryptedData`\> 元素。  此方法使用 RSA 密钥来解密会话密钥，并自动使用会话密钥来解密 XML 元素。  它还会自动将 \<`EncryptedData`\> 元素替换为原始的纯文本。  
  
     [!code-csharp[HowToDecryptXMLElementAsymmetric#7](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToDecryptXMLElementAsymmetric/cs/sample.cs#7)]
     [!code-vb[HowToDecryptXMLElementAsymmetric#7](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToDecryptXMLElementAsymmetric/vb/sample.vb#7)]  
  
6.  保存 XML 文档。  
  
     [!code-csharp[HowToDecryptXMLElementAsymmetric#8](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToDecryptXMLElementAsymmetric/cs/sample.cs#8)]
     [!code-vb[HowToDecryptXMLElementAsymmetric#8](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToDecryptXMLElementAsymmetric/vb/sample.vb#8)]  
  
## 示例  
 此示例假定名为 `test.xml` 的文件与已编译程序存在于同一目录中。  它也假定使用 `test.xml` 包含使用[如何：用非对称密钥对 XML 元素进行加密](../../../docs/standard/security/how-to-encrypt-xml-elements-with-asymmetric-keys.md)中描述的方法进行加密的 XML 元素。  
  
 [!code-csharp[HowToDecryptXMLElementAsymmetric#1](../../../samples/snippets/csharp/VS_Snippets_CLR/HowToDecryptXMLElementAsymmetric/cs/sample.cs#1)]
 [!code-vb[HowToDecryptXMLElementAsymmetric#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/HowToDecryptXMLElementAsymmetric/vb/sample.vb#1)]  
  
## 编译代码  
  
-   若要编译此示例，需要包含对 `System.Security.dll` 的引用。  
  
-   包括以下命名空间：<xref:System.Xml>、<xref:System.Security.Cryptography> 和 <xref:System.Security.Cryptography.Xml>。  
  
## .NET Framework 安全性  
 永远不要以纯文本形式存储对称加密密钥，也不要以纯文本形式在计算机之间传输对称密钥。  此外，绝不存储或传输纯文本形式的非对称密钥的私钥。  有关对称和非对称加密密钥的详细信息，请参阅[生成加密和解密的密钥](../../../docs/standard/security/generating-keys-for-encryption-and-decryption.md)。  
  
 绝不将密钥直接嵌入源代码。  可通过使用 [Ildasm.exe（IL 反汇编程序）](../../../docs/framework/tools/ildasm-exe-il-disassembler.md) 或在文本编辑器（如 Notepad）中打开程序集的方式轻松从程序集中读取嵌入的密钥。  
  
 当你使用加密密钥执行操作后，通过将每个字节设置为零或通过调用托管加密类的 <xref:System.Security.Cryptography.SymmetricAlgorithm.Clear%2A> 方法来将它从内存中清除。  加密密钥有时可从内存由调试器读取，或从硬盘读取（如果内存位置分页到磁盘）。  
  
## 请参阅  
 <xref:System.Security.Cryptography.Xml>   
 [如何：用非对称密钥对 XML 元素进行加密](../../../docs/standard/security/how-to-encrypt-xml-elements-with-asymmetric-keys.md)