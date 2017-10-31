---
title: "配置 HTTP 和 HTTPS | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "配置 HTTP [WCF]"
ms.assetid: b0c29a86-bc0c-41b3-bc1e-4eb5bb5714d4
caps.latest.revision: 17
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 17
---
# 配置 HTTP 和 HTTPS
WCF 服务和客户端可以通过 HTTP 和 HTTPS 通信。  通过使用 Internet Information Services \(IIS\) 或命令行工具可以配置 HTTP\/HTTPS 设置。  当某个 WCF 服务承载于 IIS 之下时，可以在 IIS 中配置 HTTP 或 HTTPS 设置（使用 inetmgr.exe 工具）。  如果 WCF 服务是自承载的，则可使用命令行工具配置 HTTP 或 HTTPS 设置。  
  
 至少您需要配置 URL 注册，并为您的服务将使用的 URL 添加防火墙例外。  
  
 用于配置 HTTP 设置的工具取决于计算机所运行的操作系统。  
  
 在运行 [!INCLUDE[ws2003](../../../../includes/ws2003-md.md)] 或 [!INCLUDE[wxp](../../../../includes/wxp-md.md)] 时，应使用 HttpCfg.exe 工具。  [!INCLUDE[ws2003](../../../../includes/ws2003-md.md)] 会自动安装此工具。  运行 [!INCLUDE[wxp](../../../../includes/wxp-md.md)] 时，可以在 [Windows XP Service Pack 2 支持工具](http://go.microsoft.com/fwlink/?LinkId=88606)中下载该工具。  [!INCLUDE[crdefault](../../../../includes/crdefault-md.md)] [Httpcfg 概述](http://go.microsoft.com/fwlink/?LinkId=88605)。  
  
 如果运行的是 [!INCLUDE[wv](../../../../includes/wv-md.md)] 或 Windows 7，则可以使用 Netsh.exe 工具配置这些设置。  
  
## 配置命名空间保留  
 命名空间保留将 HTTP URL 命名空间的一部分的权限分配给特定的用户组。  保留提供给这些用户创建用于侦听命名空间的相应部分的服务的权限。  保留是 URL 前缀，这意味着保留涵盖保留路径的所有子路径。  命名空间保留允许以两种方式使用通配符。  HTTP Server API 文档描述了[涉及通配符的命名空间声明之间的解析顺序](http://go.microsoft.com/fwlink/?LinkId=94841)。  
  
 运行的应用程序可以创建一个类似请求来添加命名空间注册。  注册和保留会竞争命名空间的某些部分。  根据[涉及通配符的命名空间声明之间的解析顺序](http://go.microsoft.com/fwlink/?LinkId=94841)中给定的解析顺序，保留可能优先于注册。  在此情况下，保留会阻止运行的应用程序接收请求。  
  
### 运行 Windows XP 或 Server 2003  
 使用 `httpcfg.exe set urlacl` 命令更改命名空间保留。  [Windows 支持工具文档](http://go.microsoft.com/fwlink/?LinkId=94840)（可能为英文网页）说明了 Httpcfg.exe 工具的语法。  若要修改命名空间的一部分的保留权限，需要管理特权或命名空间的相应部分的所有权。  最初，整个 HTTP 命名空间属于本地管理员。  
  
 下面演示的是带有 `set urlacl` 选项的 Httpcfg 命名的语法。  
  
```  
httpcfg set urlacl /u {http://URL:Port/ | https://URL:Port/} /aACL  
  
```  
  
 使用 `/u` 时需要 `set urlacl` 参数。  该参数接受一个包含完全限定的 URL 的字符串，该 URL 用作所要生成的保留的记录密钥。  
  
 使用 `/a` 时还需要 `set urlacl` 参数。  该参数接受一个字符串，其中包含安全描述符定义语言 \(SDDL\) 字符串格式的访问控制列表 \(ACL\)。  
  
 下面演示的是一个使用此命令的示例。  
  
```  
httpcfg.exe set urlacl /u http://myhost:8000/ /a "O:AOG:DAD:(A;;RPWPCCDCLCSWRCWDWOGA;;;S-1-0-0)"  
  
```  
  
### 运行 Windows Vista、Windows Server 2008 R2 或 Windows 7  
 如果在 [!INCLUDE[wv](../../../../includes/wv-md.md)]、Windows Server 2008 R2 或 Windows 7 上运行，则使用 Netsh.exe 工具。  下面演示的是一个使用此命令的示例。  
  
```  
netsh http add urlacl url=http://+:80/MyUri user=DOMAIN\user  
  
```  
  
 该命令为 DOMAIN\\用户帐户的指定 URL 命名空间添加一个 URL 保留项。  有关使用 netsh 命令的更多信息，请在命令提示符下键入“netsh http add urlacl”并按 Enter。  
  
## 配置防火墙例外  
 当自承载通过 HTTP 进行通信的 WCF 服务时，必须向防火墙配置添加一个例外，以允许使用特定 URL 的入站连接。  有关更多信息，请参见[在 Windows 防火墙中打开端口 \(Windows 7\)](http://go.microsoft.com/fwlink/?LinkId=239961)  
  
## 配置 SSL 证书  
 安全套接字层 \(SSL\) 协议在客户端和服务器上使用证书来存储加密密钥。  在建立连接时，服务器会提供其 SSL 证书，以便客户端验证服务器标识。  服务器还可以从客户端请求证书以提供连接双方的相互身份验证。  
  
 证书将根据连接的 IP 地址和端口号存储在一个中央存储区中。  特殊的 IP 地址 0.0.0.0 可以与本地计算机的任何 IP 地址相匹配。  请注意，证书存储区不会基于路径区分 URL。  即使服务的 URL 中的路径不同，带有相同 IP 地址和端口组合的服务也必须共享证书。  
  
 有关分步说明，请参见[如何：使用 SSL 证书配置端口](../../../../docs/framework/wcf/feature-details/how-to-configure-a-port-with-an-ssl-certificate.md)。  
  
## 配置 IP 侦听列表  
 在用户注册一个 URL 之后，HTTP 服务器 API 只绑定到一个 IP 地址和端口。  默认情况下，对于计算机的所有 IP 地址，HTTP 服务器 API 将绑定到所注册的 URL 中的端口。  如果不使用 HTTP 服务器 API 的应用程序先前已经绑定到该 IP 地址和端口的组合，则会引起冲突。  IP 侦听列表允许 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 服务与使用计算机的一些 IP 地址的端口的应用程序共存。  如果 IP 侦听列表包含任何项，则 HTTP 服务器 API 只绑定到该列表指定的那些 IP 地址。  修改 IP 侦听列表需要管理特权。  
  
### 运行 Windows XP 或 Server 2003  
 使用 httpcfg 工具修改 IP 侦听列表，如下面的示例所示。  [Windows 支持工具文档](http://go.microsoft.com/fwlink/?LinkId=94840)说明了 httpcfg.exe 工具的语法。  
  
```  
httpcfg.exe set iplisten -i 0.0.0.0:8000  
```  
  
### 运行 Windows Vista 或 Windows 7  
 使用 netsh 工具修改 IP 侦听列表，如下面的示例所示。  
  
```  
netsh http add iplisten ipaddress=0.0.0.0:8000  
```  
  
## 其他配置设置  
 使用 <xref:System.ServiceModel.WsDualHttpBinding> 时，客户端连接使用与命名空间保留和 Windows 防火墙兼容的默认设置。  如果选择自定义双向连接的客户端基址，则还必须配置这些客户端上的 HTTP 设置以与新地址相匹配。  
  
 HTTP 服务器 API 具有一些不可通过 HttpCfg 使用的高级配置设置。  这些设置保留在注册表中并应用于在使用 HTTP 服务器 API 的系统上运行的所有应用程序。  有关这些设置的信息，请参见[用于 IIS 的 Http.sys 注册表设置](http://go.microsoft.com/fwlink/?LinkId=94843)。  大多数用户应该不需要更改这些设置。  
  
## Windows XP 特有的问题  
 IIS 在 [!INCLUDE[wxp](../../../../includes/wxp-md.md)] 上不支持端口共享。  如果 IIS 正在运行并且 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 服务尝试通过相同端口来使用某个命名空间，则 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 服务将无法启动。  IIS 和 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 均默认设置使用端口 80。  请更改其中一个服务的端口分配或使用 IP 侦听列表将 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 服务分配到 IIS 未使用的网络适配器。  IIS 6.0 和更高版本已经过重新设计，可以使用 HTTP 服务器 API。  
  
## 请参阅  
 <xref:System.ServiceModel.WsDualHttpBinding>   
 [如何：使用 SSL 证书配置端口](../../../../docs/framework/wcf/feature-details/how-to-configure-a-port-with-an-ssl-certificate.md)