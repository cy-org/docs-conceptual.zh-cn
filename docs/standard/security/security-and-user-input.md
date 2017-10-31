---
title: "安全性和用户输入 | Microsoft Docs"
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
  - "代码安全性, 用户输入"
  - "安全编码, 用户输入"
  - "安全性 [.NET Framework], 用户输入"
  - "用户输入, 安全性"
ms.assetid: 9141076a-96c9-4b01-93de-366bb1d858bc
caps.latest.revision: 7
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 5
---
# 安全性和用户输入
用户数据是指任何种类的输入（来自 Web 请求或 URL 的数据、对 Microsoft Windows Forms 应用程序控件输入的数据等等），它可能会对代码产生负面影响，因为这些数据通常直接用作参数来调用其他代码。  这种情况类似于恶意代码使用奇特参数调用您的代码，因而必须采取同样的防范措施。  用户输入实际上更难以保证安全性，因为没有堆栈帧来跟踪可能不受信任的代码的存在。  
  
 它们属于最为微妙、最难于发现的安全 bug，因为，虽然它们位于表面上与安全性不相关的代码中，但它们是将有害代码传递到其他代码的通道。  要查找这些 bug，请跟随任意一种输入数据，设想可能的值的范围，并考虑看到这一数据的代码是否能够处理所有这些情形。  通过范围检查和拒绝任何无法由代码处理的输入，可以纠正这些 bug。  
  
 涉及用户数据的重要注意事项包括以下几个方面：  
  
-   服务器响应中的任何用户数据在客户端上的服务器站点的上下文中运行。  如果您的 Web 服务器获得了用户数据，并将这些数据插入到返回的网页中，那么它可能会包含诸如 **\<\<script\>\>** 的标记，而且这些数据的运行好像是从服务器进行的。  
  
-   记住客户端可以请求任何 URL。  
  
-   考虑欺骗性的或无效的路径：  
  
    -   ..\\ ，非常长的路径。  
  
    -   使用通配符 \(\*\)。  
  
    -   标记展开 \(%token%\)。  
  
    -   具有特殊意义的奇特路径形式。  
  
    -   备用文件系统流名称，如 `filename::$DATA`。  
  
    -   文件名的简称，例如 `longfilename` 简称为 `longfi~1`。  
  
-   请记住，Eval\(userdata\) 可以执行任何操作。  
  
-   在后期绑定到包含某些用户数据的名称时要多加小心。  
  
-   如果您正在处理 Web 数据，请考虑所允许的各种转义形式，包括：  
  
    -   十六进制转义 \(%nn\)。  
  
    -   Unicode 转义 \(%nnn\)。  
  
    -   超长 UTF\-8 转义 \(%nn%nn\)。  
  
    -   双转义 \(%nn 成为 %mmnn，其中 %mm 是 '%' 的转义\)。  
  
-   请注意，用户名可能不止有一种规范格式。  例如，在 Microsoft Windows 2000 中，您经常可以使用 MYDOMAIN\\*username* 形式或 *username*@mydomain.example.com 形式。  
  
## 请参阅  
 [代码安全维护指南](../../../docs/standard/security/secure-coding-guidelines.md)