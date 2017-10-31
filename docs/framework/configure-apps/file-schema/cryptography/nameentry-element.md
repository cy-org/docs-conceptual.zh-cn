---
title: "&lt;nameEntry&gt; 元素 | Microsoft Docs"
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
  - "http://schemas.microsoft.com/.NetConfiguration/v2.0#nameEntry"
  - "http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/mscorlib/cryptographySettings/cryptoNameMapping/nameEntry"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - "<nameEntry> 元素"
  - "nameEntry 元素"
ms.assetid: 7d7535e9-4b4a-4b8c-82e2-e40dff5a7821
caps.latest.revision: 14
author: "mcleblanc"
ms.author: "markl"
manager: "markl"
caps.handback.revision: 13
---
# &lt;nameEntry&gt; 元素
将类名映射为友好算法名称，这样允许一个类具有多个友好名称。  
  
## 语法  
  
```  
<nameEntry name="friendly name" Class="class name" />  
```  
  
## 特性和元素  
 下列各节描述了特性、子元素和父元素。  
  
### 特性  
  
|特性|说明|  
|--------|--------|  
|**name**|必需的特性。<br /><br /> 指定密码类实现的算法的友好名称。|  
|**类**|必需的特性。<br /><br /> 为[\<cryptoClass\>](../../../../../docs/framework/configure-apps/file-schema/cryptography/cryptoclass-element.md)元素中的**name** 属性指定值。|  
  
### 子元素  
 无。  
  
### 父元素  
  
|元素|说明|  
|--------|--------|  
|`configuration`|公共语言运行时和 .NET Framework 应用程序所使用的每个配置文件中的根元素。|  
|`system.web`|为 ASP.NET 配置节指定根元素。|  
  
## 备注  
 **name** 特性可以是位于 <xref:System.Security.Cryptography> 命名空间中的某个抽象类的名称。  在抽象密码类上调用 **Create** 方法时，抽象类名称被传递给 [Security.CryptoConfig.CreateFromName](frlrfSystemSecurityCryptographyCryptoConfigClassCreateFromNameTopic) 方法。  **CreateFromName** 返回由 **class** 特性指示的类型的实例。  如果 **name** 特性是简称（如 RSA），则可以在调用 **CreateFromName** 方法时使用该名称。  
  
## 示例  
 下面的例子演示了如何使用**\<nameEntry\>**元素来引用一个密码类来配置这个运行时。  然后，您就可以将字符串“RSA”传递到 <xref:System.Security.Cryptography.CryptoConfig.CreateFromName%2A?displayProperty=fullName> 方法并使用 <xref:System.Security.Cryptography.AsymmetricAlgorithm.Create%2A> 方法返回一个 `MyCryptoRSAClass` 对象。  
  
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