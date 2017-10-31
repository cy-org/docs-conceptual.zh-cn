---
title: "将算法名称映射到加密类 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - "加密算法"
  - "密码系统, 映射算法名称"
  - "映射算法名称"
  - "名称 [.NET Framework], 算法映射"
ms.assetid: 01327c69-c5e1-4ef6-b73f-0a58351f0492
caps.latest.revision: 11
author: "mcleblanc"
ms.author: "markl"
manager: "markl"
caps.handback.revision: 10
---
# 将算法名称映射到加密类
开发人员可以通过四种方式使用 [!INCLUDE[winsdklong](../../../includes/winsdklong-md.md)] 创建加密对象：  
  
-   通过使用 **new** 运算符创建对象。  
  
-   通过调用特定加密算法的抽象类上的 **Create** 方法，创建实现特定加密算法的对象。  
  
-   通过调用 [System.Security.Cryptography.CryptoConfig.CreateFromName](frlrfSystemSecurityCryptographyCryptoConfigClassCreateFromNameTopic) 方法，创建实现特定加密算法的对象。  
  
-   通过对某类型的算法（如 <xref:System.Security.Cryptography.SymmetricAlgorithm>）的抽象类调用 **Create** 方法，创建实现加密算法的类（如对称分组加密）的对象。  
  
 例如，假设开发人员要计算一组字节的 SHA1 哈希。  <xref:System.Security.Cryptography> 命名空间包含 SHA1 算法的两个实现，一个是纯粹的托管实现，另一个包装 CryptoAPI。  开发人员可以通过调用 **new** 运算符来选择实例化特定的 SHA1 实现（如 [SHA1Managed 类](frlrfSystemSecurityCryptographySHA1ManagedClassTopic)）。  但是，如果公共语言运行时加载哪一个类无关紧要，只要该类实现 SHA1 哈希算法，那么开发人员就可以通过调用 [System.Security.Cryptography.SHA1.Create](frlrfSystemSecurityCryptographySHA1ClassCreateTopic) 方法来创建对象。  该方法调用 **System.Security.Cryptography.CryptoConfig.CreateFromName\("System.Security.Cryptography.SHA1"\)**，它必须返回 SHA1 哈希算法的实现。  
  
 开发人员还可以调用 **System.Security.Cryptography.CryptoConfig.CreateFromName\("SHA1"\)**，因为在默认情况下，加密配置包括 .NET Framework 中提供的算法的简短名称。  
  
 如果使用哪一种哈希算法无关紧要，那么开发人员就可以调用 [System.Security.Cryptography.HashAlgorithm.Create](frlrfSystemSecurityCryptographyHashAlgorithmClassCreateTopic) 方法，它返回一个对象，该对象实现哈希转换。  
  
## 在配置文件中映射算法名称  
 默认情况下，运行时为所有四种方案返回 [System.Security.Cryptography.SHA1CryptoServiceProvider class](frlrfSystemSecurityCryptographySHA1CryptoServiceProviderClassTopic) 对象。  但是，计算机管理员可以更改最后两种方案中的方法返回的对象的类型。  为此，必须在计算机配置文件 \(Machine.config\) 中将友好算法名称映射到要使用的类。  
  
 下面的示例说明如何配置运行时，以使 **System.Security.Cryptography.SHA1.Create**、**System.Security.CryptoConfig.CreateFromName\("SHA1"\)** 和 **System.Security.Cryptography.HashAlgorithm.Create** 返回 `MySHA1HashClass` 对象。  
  
```  
<configuration>  
   <!-- Other configuration settings. -->  
   <mscorlib>  
      <cryptographySettings>  
         <cryptoNameMapping>  
            <cryptoClasses>  
               <cryptoClass MySHA1Hash="MySHA1HashClass, MyAssembly  
                  Culture='en', PublicKeyToken=a5d015c7d5a0b012,  
                  Version=1.0.0.0"/>  
            </cryptoClasses>  
            <nameEntry name="SHA1" class="MySHA1Hash"/>  
            <nameEntry name="System.Security.Cryptography.SHA1"  
                       class="MySHA1Hash"/>  
            <nameEntry name="System.Security.Cryptography.HashAlgorithm"  
                       class="MySHA1Hash"/>  
         </cryptoNameMapping>  
      </cryptographySettings>  
   </mscorlib>  
</configuration>  
```  
  
 你可以在[\<cryptoClass\> element](../../../docs/framework/configure-apps/file-schema/cryptography/cryptoclass-element.md) \(原来的例子把这个属性命名为`MySHA1Hash`\)中，指定属性的名字。  **\<cryptoClass\>**元素中的属性值是公共语言运行时用来查找类的字符串。  可以使用满足[指定完全限定的类型名称](../../../docs/framework/reflection-and-codedom/specifying-fully-qualified-type-names.md)中指定的要求的任何字符串。  
  
 许多算法名称可以映射到同一个类。  The [\<nameEntry\> element](../../../docs/framework/configure-apps/file-schema/cryptography/nameentry-element.md)将类映射到一个友好算法名称。  **name** 特性可以是在调用 **System.Security.Cryptography.CryptoConfig.CreateFromName** 方法时使用的字符串或是 <xref:System.Security.Cryptography> 命名空间中的抽象加密类的名称。  **class**属性的值是**\<cryptoClass\>**元素中的属性的名称。  
  
> [!NOTE]
>  可以通过调用 [System.Security.Cryptography.SHA1.Create](frlrfSystemSecurityCryptographySHA1ClassCreateTopic) 或 **Security.CryptoConfig.CreateFromName\("SHA1"\)** 方法来获取 SHA1 算法。  每一个方法只保证它返回能实现 SHA1 算法的对象。  没有必要在配置文件中将算法的每一个友好名称都映射到同一个类。  
  
 有关默认名称以及它们所映射到的类的列表，请参见 [CryptoConfig 类](frlrfSystemSecurityCryptographyCryptoConfigClassTopic)。  
  
## 请参阅  
 [加密服务](../../../docs/standard/security/cryptographic-services.md)   
 [配置加密类](../../../docs/framework/configure-apps/configure-cryptography-classes.md)