---
title: "加密签名 | Microsoft Docs"
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
  - "密码系统 [.NET Framework], 签名"
  - "数字签名"
  - "数字签名, 关于"
  - "数字签名, 生成"
  - "数字签名, 验证"
  - "数字签名, XML 签名"
  - "加密 [.NET Framework], 签名"
  - "生成签名"
  - "安全性 [.NET Framework], 签名"
  - "签名, 加密"
  - "签名 XML"
  - "验证签名"
  - "XML 签名"
ms.assetid: aa87cb7f-e608-4a81-948b-c9b8a1225783
caps.latest.revision: 17
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 17
---
# 加密签名
<a name="top"></a> 加密数字签名使用公钥算法提供数据完整性。 如果使用数字签名对数据进行签名，则其他人可验证该签名，并且可证明这些数据确实是你发出的，并且在你签名之后未被更改。 有关数字签名的详细信息，请参阅[加密服务](../../../docs/standard/security/cryptographic-services.md)。  
  
 本主题说明如何使用 <xref:System.Security.Cryptography?displayProperty=fullName> 命名空间中的类来生成和验证数字签名。  
  
-   [生成签名](#generate)  
  
-   [验证签名](#verify)  
  
<a name="generate"></a>   
## 生成签名  
 数字签名通常应用于表示较大数据的哈希值。 下面的示例将数字签名应用于哈希值。 首先，创建 <xref:System.Security.Cryptography.RSACryptoServiceProvider> 类的新实例以生成公钥\/私钥对。 然后，将 <xref:System.Security.Cryptography.RSACryptoServiceProvider> 传递到 <xref:System.Security.Cryptography.RSAPKCS1SignatureFormatter> 类的新实例。 这将私钥传输给了实际执行数字签名的 <xref:System.Security.Cryptography.RSAPKCS1SignatureFormatter>。 必须先指定要使用的哈希算法。然后才可以对哈希代码进行签名。 本示例使用 SHA1 算法。 最后，调用 <xref:System.Security.Cryptography.AsymmetricSignatureFormatter.CreateSignature%2A> 方法以执行签名。  
  
```vb  
Imports System Imports System.Security.Cryptography Module Module1 Sub Main() 'The hash value to sign. Dim HashValue As Byte() = {59, 4, 248, 102, 77, 97, 142, 201, 210, 12, 224, 93, 25, 41, 100, 197, 213, 134, 130, 135} 'The value to hold the signed value. Dim SignedHashValue() As Byte 'Generate a public/private key pair. Dim RSA As New RSACryptoServiceProvider() 'Create an RSAPKCS1SignatureFormatter object and pass it 'the RSACryptoServiceProvider to transfer the private key. Dim RSAFormatter As New RSAPKCS1SignatureFormatter(RSA) 'Set the hash algorithm to SHA1. RSAFormatter.SetHashAlgorithm("SHA1") 'Create a signature for HashValue and assign it to 'SignedHashValue. SignedHashValue = RSAFormatter.CreateSignature(HashValue) End Sub End Module using System; using System.Security.Cryptography;  
  
```  
  
```csharp  
class Class1 { static void Main() { //The hash value to sign. byte[] HashValue = {59,4,248,102,77,97,142,201,210,12,224,93,25,41,100,197,213,134,130,135}; //The value to hold the signed value. byte[] SignedHashValue; //Generate a public/private key pair. RSACryptoServiceProvider RSA = new RSACryptoServiceProvider(); //Create an RSAPKCS1SignatureFormatter object and pass it the //RSACryptoServiceProvider to transfer the private key. RSAPKCS1SignatureFormatter RSAFormatter = new RSAPKCS1SignatureFormatter(RSA); //Set the hash algorithm to SHA1. RSAFormatter.SetHashAlgorithm("SHA1"); //Create a signature for HashValue and assign it to //SignedHashValue. SignedHashValue = RSAFormatter.CreateSignature(HashValue); } }  
```  
  
### 对 XML 文件进行签名  
 .NET Framework 提供可实现 XML 签名的 <xref:System.Security.Cryptography.Xml> 命名空间。 当想要验证 XML 是否源自某个源时，对 XML 进行签名就变得非常重要。 例如，如果你正在利用使用 XML 的股票报价服务，则如果已对 XML 签名，你就可以验证该 XML 的源。  
  
 此命名空间中的类遵循来自万维网联合会的 [XML 签名语法和处理建议](http://go.microsoft.com/fwlink/?LinkId=136777)。  
  
 [返回页首](#top)  
  
<a name="verify"></a>   
## 验证签名  
 若要验证数据是否是由特定方进行签名的，则必须具有以下信息：  
  
-   对数据进行签名的一方的公钥。  
  
-   数字签名。  
  
-   已签名的数据。  
  
-   签名方使用的哈希算法。  
  
 若要验证由 <xref:System.Security.Cryptography.RSAPKCS1SignatureFormatter> 类签署的签名，请使用 <xref:System.Security.Cryptography.RSAPKCS1SignatureDeformatter> 类。 必须向 <xref:System.Security.Cryptography.RSAPKCS1SignatureDeformatter> 类提供签名者的公钥。 将需要模数和指数的值以指定公钥。 （生成公钥\/私钥对的一方应提供这些值）。 首先创建一个 <xref:System.Security.Cryptography.RSACryptoServiceProvider> 对象以保存将验证签名的公钥，然后将 <xref:System.Security.Cryptography.RSAParameters> 结构初始化为指定该公钥的模数值和指数值。  
  
 下面的代码显示 <xref:System.Security.Cryptography.RSAParameters> 结构的创建。`Modulus` 属性设置为名为 `ModulusData` 的字节数组的值，`Exponent` 属性设置为名为 `ExponentData` 的字节数组的值。  
  
```vb  
Dim RSAKeyInfo As RSAParameters RSAKeyInfo.Modulus = ModulusData RSAKeyInfo.Exponent = ExponentData  
  
```  
  
```csharp  
RSAParameters RSAKeyInfo; RSAKeyInfo.Modulus = ModulusData; RSAKeyInfo.Exponent = ExponentData;  
```  
  
 创建 <xref:System.Security.Cryptography.RSAParameters> 对象后，可将 <xref:System.Security.Cryptography.RSACryptoServiceProvider> 类的新实例初始化为 <xref:System.Security.Cryptography.RSAParameters> 中指定的值。 然后将 <xref:System.Security.Cryptography.RSACryptoServiceProvider> 传递到 <xref:System.Security.Cryptography.RSAPKCS1SignatureDeformatter> 的构造函数以传输密钥。  
  
 下面的示例阐释此过程。 在本示例中，`HashValue` 和 `SignedHashValue` 是由远程方提供的字节数组。 远程方已使用 SHA1 算法对 `HashValue` 进行了签名，从而生成了数字签名 `SignedHashValue`。 新任务将观察的  
  
 <xref:System.Security.Cryptography.RSAPKCS1SignatureDeformatter.VerifySignature%2A?displayProperty=fullName> 方法验证数字签名是否有效，并且是否已用于对 `HashValue` 进行签名。  
  
```vb  
Dim RSA As New RSACryptoServiceProvider() RSA.ImportParameters(RSAKeyInfo) Dim RSADeformatter As New RSAPKCS1SignatureDeformatter(RSA) RSADeformatter.SetHashAlgorithm("SHA1") If RSADeformatter.VerifySignature(HashValue, SignedHashValue) Then Console.WriteLine("The signature is valid.") Else Console.WriteLine("The signture is not valid.") End If  
  
```  
  
```csharp  
RSACryptoServiceProvider RSA = new RSACryptoServiceProvider(); RSA.ImportParameters(RSAKeyInfo); RSAPKCS1SignatureDeformatter RSADeformatter = new RSAPKCS1SignatureDeformatter(RSA); RSADeformatter.SetHashAlgorithm("SHA1"); if(RSADeformatter.VerifySignature(HashValue, SignedHashValue)) { Console.WriteLine("The signature is valid."); } else { Console.WriteLine("The signature is not valid."); }  
```  
  
 如果签名有效，则此代码段将显示“`The signature is valid`”，如果无效，则显示“`The signature is not valid`”。  
  
## 请参阅  
 [加密服务](../../../docs/standard/security/cryptographic-services.md)