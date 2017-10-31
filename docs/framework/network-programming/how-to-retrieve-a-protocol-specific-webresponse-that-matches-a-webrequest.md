---
title: "如何：检索与 WebRequest 匹配的特定于协议的 WebResponse"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- VB
- CSharp
- C++
- jsharp
ms.assetid: d8c90785-f16b-42a5-8439-ed2f731b2ba8
caps.latest.revision: 8
author: mcleblanc
ms.author: markl
manager: markl
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: 7a6d3fbb7fe336487553a70f40478a022e6b5552
ms.contentlocale: zh-cn
ms.lasthandoff: 08/21/2017

---
# 如何：检索与 WebRequest 匹配的特定于协议的 WebResponse
此示例演示如何检索与 WebRequest 匹配的特定于协议的 WebResponse。  
  
## 示例  
  
```csharp  
WebRequest req = WebRequest.Create("http://www.contoso.com/");  
WebResponse resp = req.GetResponse();  
```  
  
```vb  
Dim req As WebRequest = WebRequest.Create("http://www.contoso.com")  
Dim resp As WebResponse = req.GetResponse()  
```  
  
## 编译代码  
 此示例需要：  
  
-   引用 System.Net 命名空间。  
  
## 另请参阅  
 [请求数据](../../../docs/framework/network-programming/requesting-data.md)

