---
title: "套接字"
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
- application protocols, sockets
- sending data, sockets
- data requests, sockets
- Windows Sockets
- sockets, about sockets
- Socket class, about Socket class
- sockets
- requesting data from Internet, sockets
- network, sockets
- receiving data, sockets
- protocols, sockets
- Internet, sockets
ms.assetid: 10d22735-bd37-42c1-a2be-c1932f979a7d
caps.latest.revision: 8
author: mcleblanc
ms.author: markl
manager: markl
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: 9ddf506ee82d90c8a4d363c1ecc3abd1a8f9dbca
ms.contentlocale: zh-cn
ms.lasthandoff: 08/21/2017

---
# <a name="sockets"></a>套接字
<xref:System.Net.Sockets> 命名空间包含 Windows 套接字接口的托管实现。 <xref:System.Net> 命名空间中的所有其他网络访问类均建立在套接字的此实现之上。  
  
 .NET Framework <xref:System.Net.Sockets.Socket> 类是由 Winsock32 API 提供的套接字服务的托管代码版本。 大多数情况下，Socket 类方法只是将数据封送到其本机 Win32 对等体中，并负责任何必要的安全检查。  
  
 Socket 类支持同步和异步两种基本模式。 在同步模式下，对执行网络操作（例如 <xref:System.Net.Sockets.Socket.Send%2A> 和 <xref:System.Net.Sockets.Socket.Receive%2A>）的函数的调用等待操作完成，再将控制权返回给调用程序。 在异步模式下，这些调用立即返回。  
  
## <a name="see-also"></a>另请参阅  
 [如何：创建套接字](../../../docs/framework/network-programming/how-to-create-a-socket.md)   
    
 [使用应用程序协议](../../../docs/framework/network-programming/using-application-protocols.md)

