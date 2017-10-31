---
title: "解密数据 | Microsoft Docs"
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
  - "不对称解密"
  - "数据 [.NET Framework], 解密"
  - "解密"
  - "对称解密"
ms.assetid: 9b266b6c-a9b2-4d20-afd8-b3a0d8fd48a0
caps.latest.revision: 15
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 15
---
# 解密数据
解密是加密的反向操作。 对于私钥加密，必须知道用于加密数据的密钥和 IV。 对于公钥加密，必须知道公钥（如果使用了私钥来加密数据）或私钥（如果使用了公钥来加密数据）。  
  
## 对称解密  
 解密用对称算法加密的数据类似于用对称算法加密数据的过程。 若要对从任何托管流对象中读取的数据进行解密，应将 <xref:System.Security.Cryptography.CryptoStream> 与 .NET Framework 提供的对称加密类一起使用。  
  
 下面的示例演示如何创建 <xref:System.Security.Cryptography.RijndaelManaged> 类的新实例，并使用该实例对 <xref:System.Security.Cryptography.CryptoStream> 对象执行解密。 此示例首先创建 **RijndaelManaged** 类的一个新实例。 接下来，它创建一个 **CryptoStream** 对象并将其初始化为称作 `MyStream` 的托管流的值。 随后，将用于加密的同一个密钥和 IV 传递给 **RijndaelManaged** 类的 **CreateDecryptor** 方法，然后将该方法传递给 **CryptoStream** 构造函数。 最后，将 **CryptoStreamMode.Read** 枚举传递给 **CryptoStream** 构造函数，以指定对流的读取访问权限。  
  
```vb  
Dim RMCrypto As New RijndaelManaged() Dim CryptStream As New CryptoStream(MyStream, RMCrypto.CreateDecryptor(RMCrypto.Key, RMCrypto.IV), CryptoStreamMode.Read)  
  
```  
  
```csharp  
RijndaelManaged RMCrypto = new RijndaelManaged(); CryptoStream CryptStream = new CryptoStream(MyStream, RMCrypto.CreateDecryptor(Key, IV), CryptoStreamMode.Read);  
```  
  
 下面的示例显示创建流、解密流、从流中读取和关闭流的整个过程。 创建一个 <xref:System.Net.Sockets.TcpListener> 对象，它在建立到侦听对象的连接时初始化一个网络流。 然后，使用 **CryptoStream** 类和 **RijndaelManaged** 类解密该网络流。 此示例假定已成功传输或已预先商定密钥和 IV。 它不会显示加密和传输这些值所需的代码。  
  
```vb  
Imports System Imports System.Net.Sockets Imports System.Threading Imports System.IO Imports System.Net Imports System.Security.Cryptography Module Module1 Sub Main() 'The key and IV must be the same values that were used 'to encrypt the stream. Dim Key As Byte() = {&H1, &H2, &H3, &H4, &H5, &H6, &H7, &H8, &H9, &H10, &H11, &H12, &H13, &H14, &H15, &H16} Dim IV As Byte() = {&H1, &H2, &H3, &H4, &H5, &H6, &H7, &H8, &H9, &H10, &H11, &H12, &H13, &H14, &H15, &H16} Try 'Initialize a TCPListener on port 11000 'using the current IP address. Dim TCPListen As New TcpListener(IPAddress.Any, 11000) 'Start the listener. TCPListen.Start() 'Check for a connection every five seconds. While Not TCPListen.Pending() Console.WriteLine("Still listening. Will try in 5 seconds.") Thread.Sleep(5000) End While 'Accept the client if one is found. Dim TCP As TcpClient = TCPListen.AcceptTcpClient() 'Create a network stream from the connection. Dim NetStream As NetworkStream = TCP.GetStream() 'Create a new instance of the RijndaelManaged class 'and decrypt the stream. Dim RMCrypto As New RijndaelManaged() 'Create an instance of the CryptoStream class, pass it the NetworkStream, and decrypt 'it with the Rijndael class using the key and IV. Dim CryptStream As New CryptoStream(NetStream, RMCrypto.CreateDecryptor(Key, IV), CryptoStreamMode.Read) 'Read the stream. Dim SReader As New StreamReader(CryptStream) 'Display the message. Console.WriteLine("The decrypted original message: {0}", SReader.ReadToEnd()) 'Close the streams. SReader.Close() NetStream.Close() TCP.Close() 'Catch any exceptions. Catch Console.WriteLine("The Listener Failed.") End Try End Sub End Module  
  
```  
  
```csharp  
using System; using System.Net.Sockets; using System.Threading; using System.IO; using System.Net; using System.Security.Cryptography; class Class1 { static void Main(string[] args) { //The key and IV must be the same values that were used //to encrypt the stream. byte[] Key = {0x01, 0x02, 0x03, 0x04, 0x05, 0x06, 0x07, 0x08, 0x09, 0x10, 0x11, 0x12, 0x13, 0x14, 0x15, 0x16}; byte[] IV = {0x01, 0x02, 0x03, 0x04, 0x05, 0x06, 0x07, 0x08, 0x09, 0x10, 0x11, 0x12, 0x13, 0x14, 0x15, 0x16}; try { //Initialize a TCPListener on port 11000 //using the current IP address. TcpListener TCPListen = new TcpListener(IPAdress.Any, 11000); //Start the listener. TCPListen.Start(); //Check for a connection every five seconds. while(!TCPListen.Pending()) { Console.WriteLine("Still listening. Will try in 5 seconds."); Thread.Sleep(5000); } //Accept the client if one is found. TcpClient TCP = TCPListen.AcceptTcpClient(); //Create a network stream from the connection. NetworkStream NetStream = TCP.GetStream(); //Create a new instance of the RijndaelManaged class // and decrypt the stream. RijndaelManaged RMCrypto = new RijndaelManaged(); //Create a CryptoStream, pass it the NetworkStream, and decrypt //it with the Rijndael class using the key and IV. CryptoStream CryptStream = new CryptoStream(NetStream, RMCrypto.CreateDecryptor(Key, IV), CryptoStreamMode.Read); //Read the stream. StreamReader SReader = new StreamReader(CryptStream); //Display the message. Console.WriteLine("The decrypted original message: {0}", SReader.ReadToEnd()); //Close the streams. SReader.Close(); NetStream.Close(); TCP.Close(); } //Catch any exceptions. catch { Console.WriteLine("The Listener Failed."); } } }  
```  
  
 为使上面的示例正常运行，必须建立一个到侦听器的加密连接。 该连接必须使用侦听器中所用的相同的密钥、IV 和算法。 如果建立了这样的连接，则会将消息解密并显示到控制台上。  
  
## 不对称解密  
 通常，一方（A 方）同时生成公钥和私钥，并将其存储在内存或加密密钥容器中。  然后 A 方将公钥发送到另一方（B 方）。  B 方使用此公钥将数据加密后发送回 A 方。接收到数据后，A 方使用对应的私钥将其解密。  A 方只有使用与 B 方用于加密数据的公钥相对应的私钥，解密才能成功。  
  
 有关如何将非对称密钥存储在安全加密密钥容器中以及随后如何获取非对称密钥的信息，请参阅[如何：将非对称密钥存储在密钥容器中](../../../docs/standard/security/how-to-store-asymmetric-keys-in-a-key-container.md)。  
  
 下面的示例阐释如何对表示一个对称密钥和 IV 的两个字节数组进行解密。  有关如何以可方便地发送到第三方的格式从 <xref:System.Security.Cryptography.RSACryptoServiceProvider> 对象提取非对称公钥的信息，请参阅[加密数据](../../../docs/standard/security/encrypting-data.md)。  
  
```vb  
'Create a new instance of the RSACryptoServiceProvider class. Dim RSA As New RSACryptoServiceProvider() ' Export the public key information and send it to a third party. ' Wait for the third party to encrypt some data and send it back. 'Decrypt the symmetric key and IV. SymmetricKey = RSA.Decrypt(EncryptedSymmetricKey, False) SymmetricIV = RSA.Decrypt(EncryptedSymmetricIV, False)  
  
```  
  
```csharp  
//Create a new instance of the RSACryptoServiceProvider class. RSACryptoServiceProvider RSA = new RSACryptoServiceProvider(); // Export the public key information and send it to a third party. // Wait for the third party to encrypt some data and send it back. //Decrypt the symmetric key and IV. SymmetricKey = RSA.Decrypt( EncryptedSymmetricKey, false); SymmetricIV = RSA.Decrypt( EncryptedSymmetricIV , false);  
```  
  
## 请参阅  
 [生成加密和解密的密钥](../../../docs/standard/security/generating-keys-for-encryption-and-decryption.md)   
 [加密数据](../../../docs/standard/security/encrypting-data.md)   
 [加密服务](../../../docs/standard/security/cryptographic-services.md)