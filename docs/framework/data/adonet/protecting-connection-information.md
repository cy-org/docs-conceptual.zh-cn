---
title: "保护连接信息 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 1471f580-bcd4-4046-bdaf-d2541ecda2f4
caps.latest.revision: 4
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 4
---
# 保护连接信息
保护应用程序时，最重要的目标之一是保护对数据源的访问。  如果连接字符串未受保护，那么它就是一个潜在漏洞。  如果以纯文本形式存储连接信息或者使连接信息持续位于内存中，则可能会损害整个系统。  可以使用 [Ildasm.exe（IL 反汇编程序）](../../../../docs/framework/tools/ildasm-exe-il-disassembler.md) 读取嵌入在源代码中的连接字符串，以查看已编译的程序集中的 Microsoft 中间语言 \(MSIL\)。  
  
 根据以下因素可能会出现与连接字符串有关的安全漏洞：所使用的身份验证类型，连接字符串持久地位于内存和磁盘中的方式，以及在运行时构造连接字符串所采用的技术。  
  
## 使用 Windows 身份验证  
 为了帮助限制对数据源的访问，必须保护诸如用户 ID、密码和数据源名称等连接信息的安全。  为避免公开用户信息，建议尽可能使用 Windows 身份验证（有时也称为“集成安全性”）。  使用 `Integrated Security` 或 `Trusted_Connection` 关键字在连接字符串中指定 Windows 身份验证后，不必再使用用户 ID 和密码。  在使用 Windows 身份验证时，用户由 Windows 进行身份验证，通过对 Windows 用户和组授予权限来确定他们是否可访问服务器和数据库资源。  
  
 在不能使用 Windows 身份验证的情况下必须格外小心，因为此时用户凭据在连接字符串中是公开的。  在 ASP.NET 应用程序中，您可以将 Windows 帐户配置为用于连接到数据库和其他网络资源的固定标识。  您可以在 **web.config** 文件中的标识元素中启用模拟，并指定用户名和密码。  
  
```  
<identity impersonate="true"   
        userName="MyDomain\UserAccount"   
        password="*****" />  
```  
  
 固定标识帐户应是低权限帐户，仅被授予数据库中的必要权限。  此外，您还应该加密配置文件，从而使用户名和密码不会以明文形式公开。  
  
## 不要使用通用数据链接 \(UDL\) 文件  
 不要在通用数据链接 \(UDL\) 文件中存储 <xref:System.Data.OleDb.OleDbConnection> 的连接字符串。  UDL 以明文形式存储，无法加密。  因为 UDL 文件对您的应用程序来说是一个基于文件的外部资源，所以无法使用 .NET Framework 保护或加密该文件。  
  
## 利用连接字符串生成器避免注入攻击  
 当动态字符串串联根据用户输入的内容构建连接字符串时，会发生连接字符串注入攻击。  如果用户输入的内容未经验证，并且恶意文本或字符串未被转义，则攻击者可能会访问敏感数据或服务器上的其他资源。  为解决此问题，ADO.NET 2.0 引入了新的连接字符串生成器类，以验证连接字符串语法并确保不会引入附加参数。  有关详细信息，请参阅[连接字符串生成器](../../../../docs/framework/data/adonet/connection-string-builders.md)。  
  
## 使用 Persist Security Info\=False  
 `Persist Security Info` 的默认值为 false；建议在所有连接字符串中使用此默认值。  如果将 `Persist Security Info` 设置为 `true` 或 `yes`，则允许在打开连接后通过连接获取安全敏感信息（包括用户 ID 和密码）。  如果将 `Persist Security Info` 设置为 `false` 或 `no`，则在使用安全信息打开连接后会丢弃安全信息，这可确保不受信任的来源不能访问安全敏感信息。  
  
## 加密配置文件  
 您还可以在配置文件中存储连接字符串，从而不必将它们嵌入到应用程序的代码中。  配置文件是标准 XML 文件，.NET Framework 已为这些文件定义了一组常用的元素。  配置文件中的连接字符串通常存储在 Windows 应用程序的 **app.config** 的 **\<connectionStrings\>** 元素中，或存储在 ASP.NET 应用程序的 **web.config** 文件中。  有关在配置文件中存储、检索和加密连接字符串的基本知识的更多信息，请参见[连接字符串和配置文件](../../../../docs/framework/data/adonet/connection-strings-and-configuration-files.md)。  
  
## 请参阅  
 [保证 ADO.NET 应用程序的安全](../../../../docs/framework/data/adonet/securing-ado-net-applications.md)   
 [Encrypting Configuration Information Using Protected Configuration](../Topic/Encrypting%20Configuration%20Information%20Using%20Protected%20Configuration.md)   
 [PAVE Security in Native and .NET Framework Code](http://msdn.microsoft.com/zh-cn/bd61be84-c143-409a-a75a-44253724f784)   
 [ADO.NET 托管提供程序和数据集开发人员中心](http://go.microsoft.com/fwlink/?LinkId=217917)