---
title: "“查找私钥”工具 (FindPrivateKey.exe) | Microsoft Docs"
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
ms.assetid: b8846a95-3fcc-4e8c-b9c0-128d975a6307
caps.latest.revision: 13
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 13
---
# “查找私钥”工具 (FindPrivateKey.exe)
可以使用此命令行工具从证书存储区中检索私钥。  例如，可以使用 FindPrivateKey.exe 来查找与证书存储区中特定 X.509 证书关联的私钥文件的位置和名称。  
  
> [!IMPORTANT]
>  FindPrivateKey 工具附带作为一个 WCF 示例。  有关在何处找到此示例以及如何构建此示例的更多信息，请参见  
  
## 语法  
  
```  
FindPrivateKey <storeName> <storeLocation> [{ {-n <subjectName>} | {-t <thumbprint>} } [-f | -d | -a]]  
```  
  
## 备注  
 下表介绍了可用于“查找私钥”工具 \(FindPrivateKey.exe\) 的参数和选项。  
  
|参数|描述|  
|--------|--------|  
|`storeName`|证书存储区的名称。|  
|`storeLocation`|证书存储区的位置。|  
  
|选项|描述|  
|--------|--------|  
|`/n <` *主题名称* `>`|指定证书的主题名称。|  
|`/t <` *指纹* `>`|指定证书的指纹。  使用 Certmgr.exe 来检索证书的指纹。|  
|`/f`|只输出文件名。|  
|`/d`|只输出目录。|  
|`/a`|输出绝对文件名。|  
  
## 示例  
 下面的命令检索 John Doe 的私钥。  
  
```  
FindPrivateKey My CurrentUser -n "CN=John Doe"  
```  
  
 下面的命令检索本地计算机的私钥。  
  
```  
FindPrivateKey My LocalMachine -t "03 33 98 63 d0 47 e7 48 71 33 62 64 76 5c 4c 9d 42 1d 6b 52" –a  
```