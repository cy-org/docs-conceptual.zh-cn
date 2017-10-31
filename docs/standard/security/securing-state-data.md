---
title: "保护状态数据 | Microsoft Docs"
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
  - "代码安全性, 状态数据"
  - "安全编码, 状态数据"
  - "安全性 [.NET Framework], 状态数据"
  - "状态数据安全性"
ms.assetid: 12671309-2877-43fe-a3df-6863507e712d
caps.latest.revision: 9
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 7
---
# 保护状态数据
处理重要数据或做出任何种类的安全决策的应用程序需要将相关的数据保持在自己的控制之下，而不允许其他可能的恶意代码直接访问这些数据。  保护内存中的数据的最好方法就是，将数据声明为私有或内部（范围限定为相同的程序集内）变量。  然而，即使这些数据受到访问权制约，您也应当了解到：  
  
-   通过使用反射机制，那些能够引用您的对象的、高度受信任的代码，可以获取和设置私有成员。  
  
-   使用序列化时，如果高度受信任的代码可以访问对象的序列化格式的相应数据，那么它就可以有效地获取和设置私有成员。  
  
-   调试时，可以读取这些数据。  
  
 千万不要让您自己的任何方法或属性在无意中公开这些值。  
  
 在某些情况下，通过限制对类及其派生类的访问权，可以将数据声明为“受保护的”。  然而，由于会存在其他一些披露情形，您应当采取以下进一步防范措施：  
  
-   通过如下方法控制允许从您的类中派生的代码：将允许派生的代码限制到同一程序集；通过使用在[保护方法访问](../../../docs/framework/misc/securing-method-access.md)中所描述的声明式安全，要求必须提供某些标识或权限才能从您的类进行派生。  
  
-   确保所有派生的类实现类似的保护或被密封。  
  
## 请参阅  
 [代码安全维护指南](../../../docs/standard/security/secure-coding-guidelines.md)