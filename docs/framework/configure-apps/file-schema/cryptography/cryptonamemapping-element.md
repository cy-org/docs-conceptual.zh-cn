---
title: "&lt;cryptoNameMapping&gt; 元素 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "http://schemas.microsoft.com/.NetConfiguration/v2.0#cryptoNameMapping"
  - "http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/mscorlib/cryptographySettings/cryptoNameMapping"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - "<cryptoNameMapping> 元素"
  - "cryptoNameMapping 元素"
ms.assetid: c59c9494-149b-4ce6-b38d-371f896ae85c
caps.latest.revision: 12
author: "mcleblanc"
ms.author: "markl"
manager: "markl"
caps.handback.revision: 12
---
# &lt;cryptoNameMapping&gt; 元素
包含类到友好名称的映射。  
  
## 语法  
  
```  
  
      <cryptoNameMapping>   
</cryptoNameMapping>  
```  
  
## 特性和元素  
 下列各节描述了特性、子元素和父元素。  
  
### 特性  
 无。  
  
### 子元素  
  
|元素|说明|  
|--------|--------|  
|`cryptoClasses`|包含密码类的列表，这些类具有到**\<nameEntry\>**元素中的友好名称的映射。|  
|`nameEntry`|将类名映射为友好算法名称，这样允许一个类具有多个友好名称。|  
  
### 父元素  
  
|元素|说明|  
|--------|--------|  
|`configuration`|公共语言运行时和 .NET Framework 应用程序所使用的每个配置文件中的根元素。|  
|`cryptographySettings`|包含密码设置。|  
|`cryptoNameMapping`|包含类到友好名称的映射。|  
|`mscorlib`|包含\<cryptographySettings\>元素。|  
  
## 示例  
 下面的示例演示如何使用**\<cryptoNameMapping\>**元素来引用密码类和配置运行时。  然后，您就可以将字符串“RSA”传递到 <xref:System.Security.Cryptography.CryptoConfig.CreateFromName%2A?displayProperty=fullName> 方法并使用 <xref:System.Security.Cryptography.AsymmetricAlgorithm.Create%2A> 方法返回一个 `MyCryptoRSAClass` 对象。  
  
```  
<configuration>  
   <mscorlib>  
      <cryptographySettings>  
         <cryptoNameMapping>  
            <cryptoClasses>  
               <cryptoClass   MyCryptoRSA="MyCryptoRSAClass, MyAssembly  
                  Culture=neutral, PublicKeyToken=a5d015c7d5a0b012,  
                  Version=1.0.0.0"/>  
            </cryptoClasses>  
            <nameEntry name="RSA" class="MyCryptoRSA"/>  
            <nameEntry name="System.Security.Cryptography.AsymmetricAlgorithm"  
                       class="MyCryptoRSA"/>  
         </cryptoNameMapping>  
      </cryptographySettings>  
   </mscorlib>  
</configuration>  
```  
  
## 请参阅  
 [配置文件架构](../../../../../docs/framework/configure-apps/file-schema/index.md)   
 [密码设置架构](../../../../../docs/framework/configure-apps/file-schema/cryptography/index.md)   
 [加密服务](../../../../../docs/standard/security/cryptographic-services.md)   
 [配置加密类](../../../../../docs/framework/configure-apps/configure-cryptography-classes.md)