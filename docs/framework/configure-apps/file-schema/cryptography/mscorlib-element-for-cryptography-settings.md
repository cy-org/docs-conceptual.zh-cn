---
title: "加密设置的 &lt;mscorlib&gt; 元素 | Microsoft Docs"
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
  - "http://schemas.microsoft.com/.NetConfiguration/v2.0#mscorlib"
  - "http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/mscorlib"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - "<mscorlib> 元素"
  - "mscorlib 元素"
ms.assetid: d549668f-31f1-4b92-8021-a9135c09ca3c
caps.latest.revision: 13
author: "mcleblanc"
ms.author: "markl"
manager: "markl"
caps.handback.revision: 13
---
# 加密设置的 &lt;mscorlib&gt; 元素
包含[\<cryptographySettings\> element](../../../../../docs/framework/configure-apps/file-schema/cryptography/cryptographysettings-element.md)。  
  
## 语法  
  
```  
  
      <mscorlib>   
</mscorlib>  
```  
  
## 特性和元素  
 下列各节描述了特性、子元素和父元素。  
  
### 特性  
 无。  
  
### 子元素  
  
|元素|说明|  
|--------|--------|  
|`cryptographySettings`|包含密码设置。|  
  
### 父元素  
  
|元素|说明|  
|--------|--------|  
|`configuration`|公共语言运行时和 .NET Framework 应用程序所使用的每个配置文件中的根元素。|  
  
## 示例  
 下面的示例演示如何使用**\<mscorlib\>**元素来引用密码类和配置运行时。  然后，您就可以将字符串“RSA”传递到 <xref:System.Security.Cryptography.CryptoConfig.CreateFromName%2A?displayProperty=fullName> 方法并使用 <xref:System.Security.Cryptography.AsymmetricAlgorithm.Create%2A> 方法返回一个 `MyCryptoRSAClass` 对象。  
  
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
 <xref:System.Security.Cryptography.CryptoConfig.CreateFromName%2A>   
 <xref:System.Security.Cryptography>   
 [配置文件架构](../../../../../docs/framework/configure-apps/file-schema/index.md)   
 [密码设置架构](../../../../../docs/framework/configure-apps/file-schema/cryptography/index.md)   
 [加密服务](../../../../../docs/standard/security/cryptographic-services.md)   
 [配置加密类](../../../../../docs/framework/configure-apps/configure-cryptography-classes.md)