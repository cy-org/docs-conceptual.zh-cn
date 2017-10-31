---
title: "创建 Internet 请求"
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
- WebRequest class, sending and receiving data
- Networking
- HttpWebResponse class, sending and receiving data
- requesting data from Internet, creating requests
- Network Resources
- Internet, requesting data
- data requests, creating requests
ms.assetid: faab683e-3f1e-4eee-b5e9-59f7245033d5
caps.latest.revision: 8
author: mcleblanc
ms.author: markl
manager: markl
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: d5bc99f08542718ccd449c069c91082d8227f9a4
ms.contentlocale: zh-cn
ms.lasthandoff: 08/21/2017

---
# <a name="creating-internet-requests"></a>创建 Internet 请求
应用程序通过 <xref:System.Net.WebRequest.Create%2A?displayProperty=fullName> 方法创建 <xref:System.Net.WebRequest> 实例。 这是一种基于传递给它的 URI 方案创建从 WebRequest 派生的类的静态方法。  
  
## <a name="web-file-and-ftp-requests"></a>Web、文件和 FTP 请求  
 .NET Framework 提供从 WebRequest 派生的 <xref:System.Net.HttpWebRequest> 类，用以处理 HTTP 和 HTTPS 请求。 在大多数情况下，WebRequest 类提供提出请求所需的所有属性；但是，如有必要，将 WebRequest.Create 方法创建的 WebRequest 对象转换为 HttpWebRequest 类型，即可访问该请求特定于 HTTP 的属性。 同样，HttpWebResponse 对象可处理来自 HTTP 和 HTTPS 请求的响应。 要访问 HttpWebResponse 对象特定于 HTTP 的属性，需将 WebResponse 对象转换为 HttpWebResponse 类型。  
  
 .NET Framework 还提供 <xref:System.Net.FileWebRequest> 和 <xref:System.Net.FileWebResponse> 类来处理使用“file:”URI 方案的资源请求。 同样，提供的 <xref:System.Net.FtpWebRequest> 和 <xref:System.Net.FtpWebResponse> 类可处理使用“ftp:”方案的资源请求。 如果请求的是使用上述任一方案的资源，则可使用 WebRequest.Create 方法获取用于发出请求的对象。  
  
 要处理使用其他应用程序级协议的请求，需实现从 WebRequest 和 WebResponse 派生的协议特定的类。 有关详细信息，请参阅[对可插入协议进行编程](../../../docs/framework/network-programming/programming-pluggable-protocols.md)。  
  
## <a name="see-also"></a>另请参阅  
 [如何：使用 WebRequest 类请求数据](../../../docs/framework/network-programming/how-to-request-data-using-the-webrequest-class.md)   
 [请求数据](../../../docs/framework/network-programming/requesting-data.md)

