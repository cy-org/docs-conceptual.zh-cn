---
title: "扩展保护身份验证示例自述文件 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 80bf2e97-398d-4db5-9040-d96478a2ccab
caps.latest.revision: 3
author: "BrucePerlerMS"
ms.author: "bruceper"
manager: "mbaldwin"
caps.handback.revision: 3
---
# 扩展保护身份验证示例自述文件
扩展保护是一种用于抵御中间人 \(MITM\) 攻击的安全计划，在此类攻击中，攻击者（称为“中间人”）截获客户端凭据并使用这些凭据访问客户端目标服务器上的安全资源。  
  
 有关更多信息，请参见[身份验证的扩展保护概述](../../../../docs/framework/wcf/feature-details/extended-protection-for-authentication-overview.md)。  
  
> [!NOTE]
>  仅当承载于 IIS 上时，此示例才有效。它不适用于 Visual Studio 开发服务器，原因是此服务器不支持 HTTPS。  
  
## 设置、生成和运行示例  
  
1.  在计算机上，从“添加\/删除程序”\-\>“Windows 功能”安装 IIS。  
  
2.  在 Windows 功能中打开“Windows 身份验证”：“Internet 信息服务”\-\>“万维网服务”\-\>“安全”\-\>“Windows 身份验证”。  
  
3.  在 Windows 功能中打开“HTTP 激活”：“Microsoft .NET Framework 3.5.1”\-\>“Windows Communication Foundation HTTP 激活”。  
  
4.  此示例要求客户端与服务器建立一个安全通道，因此它要求存在服务器证书，此证书可从 Internet 信息服务 \(IIS\) 管理器进行安装。  
  
    1.  打开“IIS 管理器”\-\>“服务器证书”（从“功能视图”选项卡）。  
  
    2.  为了测试此示例，您可以创建一个自签名证书。（如果不希望 Internet Explorer 提示证书不安全，可将证书安装到受信任的证书根颁发机构存储区中）。  
  
5.  转至默认网站的“操作”窗格。单击“编辑站点”\-\>“绑定”。如果 HTTPS 不存在，则将其作为一种类型添加，端口号为 443，并分配在上一步中创建的 SSL 证书。  
  
6.  生成服务。这会在 IIS 中为您创建一个虚拟目录（从在项目属性中指定的生成后操作），并根据需要为要进行 Web 承载的服务复制 dll、.svc 和配置文件。  
  
7.  打开 IIS 管理器。右击在上一步中创建的虚拟目录 \(ExtendedProtection\)，然后选择“转换为应用程序”。  
  
8.  在 IIS 管理器中为此虚拟目录打开“身份验证”模块，并启用“Windows 身份验证”。  
  
9. 为此虚拟目录打开“Windows 身份验证”的“高级设置”，然后将其设置为“必选”，因为在此示例中，相应的 ExtendedProtection 设置已设置为“始终”。  
  
10. 通过从浏览器窗口访问 URL 可测试此服务。如果想要跨计算机访问此 URL，请确保为所有传入 HTTP 和 HTTPS 连接打开了防火墙。  
  
11. 打开客户端配置文件，并为 \<client\> \- \<endpoint\> \- address 特性提供完整的计算机名称，取代“\<\<\>\>full\_machine\_name”。  
  
12. 运行客户端。客户端通过建立安全通道并使用扩展保护与服务进行通信。