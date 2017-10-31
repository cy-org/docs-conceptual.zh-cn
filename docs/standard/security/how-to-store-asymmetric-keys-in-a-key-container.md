---
title: "如何：将非对称密钥存储在密钥容器中 | Microsoft Docs"
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
  - "非对称密钥 [.NET Framework]"
  - "密码系统 [.NET Framework], 非对称密钥"
  - "解密密钥"
  - "加密 [.NET Framework], 非对称密钥"
  - "加密密钥"
  - "键, 不对称"
  - "键, 存储在密钥容器中"
  - "存储非对称密钥"
ms.assetid: 0dbcbd8d-0dcf-40e9-9f0c-e3f162d35ccc
caps.latest.revision: 20
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 17
---
# 如何：将非对称密钥存储在密钥容器中
非对称私钥永远不应以原义或纯文本形式存储在本地计算机上。  如果需要存储私钥，则应使用密钥容器。  有关密钥容器的详细信息，请参阅[Understanding Machine\-Level and User\-Level RSA Key Containers](../Topic/Understanding%20Machine-Level%20and%20User-Level%20RSA%20Key%20Containers.md)。  
  
### 创建非对称密钥并且将它保存在密钥容器中  
  
1.  创建 <xref:System.Security.Cryptography.CspParameters> 类的一个新实例，并将你想让密钥容器使用的名称传递给 <xref:System.Security.Cryptography.CspParameters.KeyContainerName?displayProperty=fullName> 字段。  
  
2.  为从 <xref:System.Security.Cryptography.AsymmetricAlgorithm> 类派生的一个类（通常是 **RSACryptoServiceProvider** 或 **DSACryptoServiceProvider**）创建一个新实例，并将先前创建的 **CspParameters** 对象传递给其构造函数。  
  
### 从密钥容器删除密钥  
  
1.  创建 **CspParameters** 类的一个新实例，并将你想让密钥容器使用的名称传递给 **CspParameters.KeyContainerName** 字段。  
  
2.  为从 **AsymmetricAlgorithm** 类派生的一个类（通常是 **RSACryptoServiceProvider** 或 **DSACryptoServiceProvider**）创建一个新实例，并将先前创建的 **CspParameters** 对象传递给其构造函数。  
  
3.  将从 **AsymmetricAlgorithm** 中派生的类的 **PersistKeyInCSP** 属性设置为 **false**（在 Visual Basic 中为 **False**）。  
  
4.  调用从 **AsymmetricAlgorithm** 派生的类的 **Clear** 方法。  该方法释放该类所有的资源并清除密钥容器。  
  
## 示例  
 下面的示例说明下面这一过程：创建一个非对称密钥，将其保存在密钥容器中，以后检索此密钥，最后从该容器中删除此密钥。  
  
 请注意，`GenKey_SaveInContainer` 方法和 `GetKeyFromContainer` 方法的代码相似。  当为 <xref:System.Security.Cryptography.CspParameters> 对象指定密钥容器名称并将其传递给 <xref:System.Security.Cryptography.AsymmetricAlgorithm> 属性或 <xref:System.Security.Cryptography.RSACryptoServiceProvider.PersistKeyInCsp%2A> 属性设置为 true 的 <xref:System.Security.Cryptography.DSACryptoServiceProvider.PersistKeyInCsp%2A> 对象时，将会发生以下情况。  如果附带指定名称的密钥容器不存在，那么将创建一个并且该密钥保持不变。  如果确实存在具有指定名称的密钥容器，则将此容器中的密钥自动加载到当前 <xref:System.Security.Cryptography.AsymmetricAlgorithm> 对象中。  因此，`GenKey_SaveInContainer` 方法中的代码保持密钥不变，因为它首先运行；而 `GetKeyFromContainer` 方法中的代码加载此密钥，因为它随后运行。  
  
```vb  
Imports System  
Imports System.IO  
Imports System.Security.Cryptography  
 _  
  
Public Class StoreKey  
  
    Public Shared Sub Main()  
        Try  
            ' Create a key and save it in a container.  
            GenKey_SaveInContainer("MyKeyContainer")  
  
            ' Retrieve the key from the container.  
            GetKeyFromContainer("MyKeyContainer")  
  
            ' Delete the key from the container.  
            DeleteKeyFromContainer("MyKeyContainer")  
  
            ' Create a key and save it in a container.  
            GenKey_SaveInContainer("MyKeyContainer")  
  
            ' Delete the key from the container.  
            DeleteKeyFromContainer("MyKeyContainer")  
        Catch e As CryptographicException  
            Console.WriteLine(e.Message)  
        End Try  
    End Sub  
  
    Public Shared Sub GenKey_SaveInContainer(ByVal ContainerName As String)  
        ' Create the CspParameters object and set the key container   
        ' name used to store the RSA key pair.  
        Dim cp As New CspParameters()  
        cp.KeyContainerName = ContainerName  
  
        ' Create a new instance of RSACryptoServiceProvider that accesses  
        ' the key container MyKeyContainerName.  
        Dim rsa As New RSACryptoServiceProvider(cp)  
  
        ' Display the key information to the console.  
        Console.WriteLine("Key added to container:  {0}", rsa.ToXmlString(True))  
    End Sub  
  
    Public Shared Sub GetKeyFromContainer(ByVal ContainerName As String)  
        ' Create the CspParameters object and set the key container   
        '  name used to store the RSA key pair.  
        Dim cp As New CspParameters()  
        cp.KeyContainerName = ContainerName  
  
        ' Create a new instance of RSACryptoServiceProvider that accesses  
        ' the key container MyKeyContainerName.  
        Dim rsa As New RSACryptoServiceProvider(cp)  
  
        ' Display the key information to the console.  
        Console.WriteLine("Key retrieved from container : {0}", rsa.ToXmlString(True))  
    End Sub  
  
    Public Shared Sub DeleteKeyFromContainer(ByVal ContainerName As String)  
        ' Create the CspParameters object and set the key container   
        '  name used to store the RSA key pair.  
        Dim cp As New CspParameters()  
        cp.KeyContainerName = ContainerName  
  
        ' Create a new instance of RSACryptoServiceProvider that accesses  
        ' the key container.  
        Dim rsa As New RSACryptoServiceProvider(cp)  
  
        ' Delete the key entry in the container.  
        rsa.PersistKeyInCsp = False  
  
        ' Call Clear to release resources and delete the key from the container.  
        rsa.Clear()  
  
        Console.WriteLine("Key deleted.")  
    End Sub  
End Class  
  
```  
  
```csharp  
using System;  
using System.IO;  
using System.Security.Cryptography;  
  
public class StoreKey  
  
{  
    public static void Main()  
    {  
        try  
        {  
            // Create a key and save it in a container.  
            GenKey_SaveInContainer("MyKeyContainer");  
  
            // Retrieve the key from the container.  
            GetKeyFromContainer("MyKeyContainer");  
  
            // Delete the key from the container.  
            DeleteKeyFromContainer("MyKeyContainer");  
  
            // Create a key and save it in a container.  
            GenKey_SaveInContainer("MyKeyContainer");  
  
            // Delete the key from the container.  
            DeleteKeyFromContainer("MyKeyContainer");  
        }  
        catch(CryptographicException e)  
        {  
            Console.WriteLine(e.Message);  
        }  
  
    }  
  
    public static void GenKey_SaveInContainer(string ContainerName)  
    {  
        // Create the CspParameters object and set the key container   
        // name used to store the RSA key pair.  
        CspParameters cp = new CspParameters();  
        cp.KeyContainerName = ContainerName;  
  
        // Create a new instance of RSACryptoServiceProvider that accesses  
        // the key container MyKeyContainerName.  
        RSACryptoServiceProvider rsa = new RSACryptoServiceProvider(cp);  
  
        // Display the key information to the console.  
        Console.WriteLine("Key added to container: \n  {0}", rsa.ToXmlString(true));  
    }  
  
    public static void GetKeyFromContainer(string ContainerName)  
    {  
        // Create the CspParameters object and set the key container   
        // name used to store the RSA key pair.  
        CspParameters cp = new CspParameters();  
        cp.KeyContainerName = ContainerName;  
  
        // Create a new instance of RSACryptoServiceProvider that accesses  
        // the key container MyKeyContainerName.  
        RSACryptoServiceProvider rsa = new RSACryptoServiceProvider(cp);  
  
        // Display the key information to the console.  
        Console.WriteLine("Key retrieved from container : \n {0}", rsa.ToXmlString(true));  
    }  
  
    public static void DeleteKeyFromContainer(string ContainerName)  
    {  
        // Create the CspParameters object and set the key container   
        // name used to store the RSA key pair.  
        CspParameters cp = new CspParameters();  
        cp.KeyContainerName = ContainerName;  
  
        // Create a new instance of RSACryptoServiceProvider that accesses  
        // the key container.  
        RSACryptoServiceProvider rsa = new RSACryptoServiceProvider(cp);  
  
        // Delete the key entry in the container.  
        rsa.PersistKeyInCsp = false;  
  
        // Call Clear to release resources and delete the key from the container.  
        rsa.Clear();  
  
        Console.WriteLine("Key deleted.");  
    }  
}  
```  
  
```Output  
  
            已添加到容器中的密钥：  
<RSAKeyValue>密钥信息 A</RSAKeyValue>  
从容器中检索到的密钥：  
<RSAKeyValue>密钥信息 A</RSAKeyValue>  
已删除的密钥。  已添加到容器中的密钥：  
<RSAKeyValue>密钥信息 B</RSAKeyValue>  
已删除的密钥。    
```  
  
## 请参阅  
 [生成加密和解密的密钥](../../../docs/standard/security/generating-keys-for-encryption-and-decryption.md)   
 [加密数据](../../../docs/standard/security/encrypting-data.md)   
 [解密数据](../../../docs/standard/security/decrypting-data.md)   
 [加密服务](../../../docs/standard/security/cryptographic-services.md)