---
title: "将对象标识符映射到加密算法 | Microsoft Docs"
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
  - "密码系统, 映射对象标识符"
  - "数字签名"
  - "标识符, 映射对象标识符"
  - "映射对象标识符"
ms.assetid: c9673f81-bf9e-47fd-bc6f-6bc1c1c4c15e
caps.latest.revision: 8
author: "mcleblanc"
ms.author: "markl"
manager: "markl"
caps.handback.revision: 8
---
# 将对象标识符映射到加密算法
数字签名能确保数据在从一个程序发送到另一个程序时不被篡改。  通常数字签名通过将数学函数应用到要签名的数据的哈希来计算。  在设置要签名的哈希值格式时，作为格式操作的组成部分，一些数字签名算法会追加一个 ASN.1 对象标识符 \(OID\)。  OID 标识用于计算哈希的算法。  可以将算法映射到对象标识符，以扩展加密机制，以便使用自定义算法。  下面的示例演示如何将对象标识符映射到新的哈希算法。  
  
```  
<configuration>  
   <mscorlib>  
      <cryptographySettings>  
         <cryptoNameMapping>  
            <cryptoClasses>  
               <cryptoClass MyNewHash="MyNewHashClass, MyAssembly  
                  Culture='en', PublicKeyToken=a5d015c7d5a0b012,  
                  Version=1.0.0.0"/>  
            </cryptoClasses>  
            <nameEntry name="NewHash" class="MyNewHash"/>  
         </cryptoNameMapping>  
         <oidMap>  
            <oidEntry OID="1.3.14.33.42.46"  name="NewHash"/>  
         </oidMap>  
      </cryptographySettings>  
   </mscorlib>  
</configuration>  
```  
  
 [\<oidEntry\> 元素](../../../docs/framework/configure-apps/file-schema/cryptography/oidentry-element.md)包含两个特性。  **OID** 特性是对象标识符号码。  **name** 特性是[\<nameEntry\> element](../../../docs/framework/configure-apps/file-schema/cryptography/nameentry-element.md)中的**name**特性的值。  在对象标识符可以映射到简单名称之前，必须存在从算法名称到类的映射。  
  
## 请参阅  
 [配置加密类](../../../docs/framework/configure-apps/configure-cryptography-classes.md)   
 [加密服务](../../../docs/standard/security/cryptographic-services.md)