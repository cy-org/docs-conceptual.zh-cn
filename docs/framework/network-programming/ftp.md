---
title: FTP
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
helpviewer_keywords:
- FTP
ms.assetid: 9b43f8b4-89d7-46a7-89fc-71aca916dd32
caps.latest.revision: 9
author: mcleblanc
ms.author: markl
manager: markl
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: d2274873140c415a970884389e71163be7f4cba6
ms.contentlocale: zh-cn
ms.lasthandoff: 08/21/2017

---
# <a name="ftp"></a>FTP
.NET Framework 通过 <xref:System.Net.FtpWebRequest> 和 <xref:System.Net.FtpWebResponse> 类为 FTP 协议提供全面支持。 这些类派生自 <xref:System.Net.WebRequest> 和 <xref:System.Net.WebResponse>。 大多数情况下，<xref:System.Net.WebRequest> 和 <xref:System.Net.WebResponse> 类提供发出请求所需的所有事项，但如果需要访问作为属性公开的 FTP 特定功能，可以将这两个类转换为 <xref:System.Net.FtpWebRequest> 或 <xref:System.Net.FtpWebResponse>。  
  
## <a name="examples"></a>示例  
 有关详细信息，请参阅以下主题：[如何使用 FTP 下载文件](../../../docs/framework/network-programming/how-to-download-files-with-ftp.md)、[如何使用 FTP 上传文件](../../../docs/framework/network-programming/how-to-upload-files-with-ftp.md)和[如何使用 FTP 列出目录内容](../../../docs/framework/network-programming/how-to-list-directory-contents-with-ftp.md)。  
  
## <a name="ftp-and-proxies"></a>FTP 和代理  
 如果代理（由 <xref:System.Net.FtpWebRequest.Proxy%2A> 属性指定）为 HTTP 代理，则仅支持 <xref:System.Net.WebRequestMethods.Ftp.DownloadFile>、<xref:System.Net.WebRequestMethods.Ftp.ListDirectory> 和 <xref:System.Net.WebRequestMethods.Ftp.ListDirectoryDetails> 命令。  
  
## <a name="see-also"></a>另请参阅  
 [通过代理访问 Internet](../../../docs/framework/network-programming/accessing-the-internet-through-a-proxy.md)   
 [网络编程示例](../../../docs/framework/network-programming/network-programming-samples.md)   
 [FTP 客户端技术示例](http://go.microsoft.com/fwlink/?LinkID=179557)   
 [FTP 资源管理器技术示例](http://go.microsoft.com/fwlink/?LinkID=179569)   
 [使用应用程序协议](../../../docs/framework/network-programming/using-application-protocols.md)

