---
title: "改进的强命名"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology:
- dotnet-bcl
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- strong-named assemblies
- strong naming [.NET Framework], enhanced
ms.assetid: 6cf17a82-62a1-4f6d-8d5a-d7d06dec2bb5
caps.latest.revision: 11
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: 429a54340cef6d608692abd71311c012afe9a3d0
ms.contentlocale: zh-cn
ms.lasthandoff: 07/28/2017

---
# <a name="enhanced-strong-naming"></a>改进的强命名
强名称签名是 .NET Framework 中用于识别程序集的识别机制。 它是一个公钥数字签名，通常用于验证发信方（签名方）发送给收信方（验证方）的数据的完整性。 此签名是程序集的唯一标识，可确保对程序集的引用清楚明确。 在生成过程中对程序集进行签名，然后在加载程序集时对其进行验证。  
  
 强名称签名有助于防止恶意方篡改程序集，然后使用原始签名方的密钥对程序集进行重新签名。 但是强名称密钥不包含任何有关发布服务器的可靠信息，也不包含任何证书层次结构。 强名称签名不保证为程序集签名的人员的可信度，也不指示该人员是否为密钥的合法所有者；它仅指示密钥所有者对程序集进行了签名。 因此，不建议使用强名称签名作为判断是否应信任第三方代码的安全验证程序。 建议使用 Microsoft Authenticode 对代码进行身份验证。  
  
## <a name="limitations-of-conventional-strong-names"></a>传统的强名称的限制  
 在早于 [!INCLUDE[net_v45](../../../includes/net-v45-md.md)] 的版本中使用强命名技术有以下缺点：  
  
-   密钥会不断受到攻击，并且技术和硬件的改进让根据公钥推断私钥变得更加容易。 抵御攻击需要使用更大的密钥。 早于 [!INCLUDE[net_v45](../../../includes/net-v45-md.md)] 的 .NET Framework 版本可以使用任意大小的密钥进行签名（默认大小为 1024 位），但是使用新密钥对程序集签名会破坏引用程序集旧标识的所有二进制文件。 因此，如果想要保持兼容性，就很难升级签名密钥的大小。  
  
-   强名称签名仅支持 SHA-1 算法。 人们最近发现 SHA-1 不足以保证哈希应用程序的安全。 因此需要使用更强的算法（SHA-256 或更高）。 SHA-1 可能不再与 FIPS 兼容，这样的话选择只使用与 FIPS 兼容的软件和算法的用户可能会遇到问题。  
  
## <a name="advantages-of-enhanced-strong-names"></a>增强的强名称的优点  
 增强的强名称最主要的优势是与预先存在的强名称兼容，并且能够声明一个标识等效于另一个标识：  
  
-   具有现有已签名程序集的开发人员可以将其标识迁移到 SHA-2 算法，同时兼容引用旧标识的程序集。  
  
-   创建新的程序集并且不考虑已有的强名称签名的开发人员可以使用安全性更高的 SHA-2 算法，并按惯用的方式对程序集签名。  
  
## <a name="using-enhanced-strong-names"></a>使用改进的强名称  
 强名称密钥包含签名密钥和标识密钥。 使用签名密钥对程序集进行签名，使用标识密钥标识该程序集。 在 [!INCLUDE[net_v45](../../../includes/net-v45-md.md)] 之前，这两个密钥相同。 从 [!INCLUDE[net_v45](../../../includes/net-v45-md.md)] 开始，标识密钥与早期 .NET Framework 版本中的相同，但是签名密钥使用了更强的哈希算法进行了改进。 此外，使用标识密钥对签名密钥进行签名以创建副署。  
  
 通过 <xref:System.Reflection.AssemblySignatureKeyAttribute> 属性，程序集元数据可将已有公钥用于程序集标识，让旧程序集引用仍然有效。  <xref:System.Reflection.AssemblySignatureKeyAttribute> 使用副署来确保新签名密钥的所有者同时也是旧标识密钥的所有者。  
  
### <a name="signing-with-sha-2-without-key-migration"></a>使用 SHA-2 签名，但不进行密钥迁移  
 在命令提示符窗口中运行以下命令，在不迁移强名称签名的情况下对程序集签名：  
  
1.  生成新的标识密钥（如有必要）。  
  
    ```  
    sn -k IdentityKey.snk  
    ```  
  
2.  提取标识公钥，并指定使用此密钥进行签名时，须使用 SHA-2 算法。  
  
    ```  
    sn -p IdentityKey.snk IdentityPubKey.snk sha256  
    ```  
  
3.  使用标识公钥文件对程序集进行延迟签名。  
  
    ```  
    csc MyAssembly.cs /keyfile:IdentityPubKey.snk /delaySign+  
    ```  
  
4.  使用完整标识密钥对对程序集进行重新签名。  
  
    ```  
    sn -Ra MyAssembly.exe IdentityKey.snk  
    ```  
  
### <a name="signing-with-sha-2-with-key-migration"></a>使用 SHA-2 签名，并进行密钥迁移  
 在命令提示符窗口中运行以下命令，使用迁移的强名称签名对程序集签名：  
  
1.  生成标识密钥和签名密钥对（如有必要）。  
  
    ```  
    sn -k IdentityKey.snk  
    sn -k SignatureKey.snk  
    ```  
  
2.  提取签名公钥，并指定使用此密钥进行签名时，必须使用 SHA-2 算法。  
  
    ```  
    sn -p SignatureKey.snk SignaturePubKey.snk sha256  
    ```  
  
3.  提取标识公钥，该公钥确定用于生成副署的哈希算法。  
  
    ```  
    sn -p IdentityKey.snk IdentityPubKey.snk  
    ```  
  
4.  生成 <xref:System.Reflection.AssemblySignatureKeyAttribute> 属性的参数，并将该参数附加到程序集。  
  
    ```  
    sn -ac IdentityPubKey.snk IdentityKey.snk SignaturePubKey.snk  
    ```  
  
5.  使用标识公钥延迟对程序集签名。  
  
    ```  
    csc MyAssembly.cs /keyfile:IdentityPubKey.snk /delaySign+  
    ```  
  
6.  使用签名密钥对对程序集进行完整签名。  
  
    ```  
    sn -Ra MyAssembly.exe SignatureKey.snk  
    ```  
  
## <a name="see-also"></a>另请参阅  
 [创建和使用具有强名称的程序集](../../../docs/framework/app-domains/create-and-use-strong-named-assemblies.md)

