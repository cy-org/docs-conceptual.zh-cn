---
title: "如何：在 .NET Framework 中执行基本字符串操作 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-standard"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "字符串 [.NET Framework], 示例"
ms.assetid: 121d1eae-251b-44c0-8818-57da04b8215e
caps.latest.revision: 7
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 7
---
# 如何：在 .NET Framework 中执行基本字符串操作
下面的示例使用在[基本字符串运算](../../../docs/standard/base-types/basic-string-operations.md)主题中讨论的一些方法来构造一个类，该类执行字符串操纵的方式在现实应用程序中也可以找到。  `MailToData` 类将个人的姓名和地址存储在单独的属性中，并提供了一种将 `City`、`State` 和 `Zip` 字段合并成单个字符串的方法，以便将它们显示给用户。  此外，该类允许用户将城市、省\/市\/自治区和邮政编码信息作为单个字符串输入；应用程序自动分析此单个字符串并将正确的信息输入到相应的属性中。  
  
 为简单起见，此示例使用带有命令行接口的控制台应用程序。  
  
## 示例  
 [!code-csharp[Conceptual.String.BasicOps#1](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.string.basicops/cs/basicops.cs#1)]
 [!code-vb[Conceptual.String.BasicOps#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.string.basicops/vb/basicops.vb#1)]  
  
 当执行以上的代码时，将要求用户输入他或她的用户名和地址。  应用程序将这些信息放入相应的属性中，并将这些信息回显给用户，同时创建显示城市、省\/市\/自治区和邮政编码信息的单个字符串。  
  
## 请参阅  
 [基本字符串操作](../../../docs/standard/base-types/basic-string-operations.md)