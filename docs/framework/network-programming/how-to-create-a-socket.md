---
title: "如何：创建套接字"
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
- Networking
- sending data, sockets
- data requests, sockets
- requesting data from Internet, sockets
- Socket class, creating sockets
- Network Resources
- receiving data, sockets
- protocols, sockets
- Internet, sockets
- sockets, creating
ms.assetid: c64a049c-5981-43bc-a2dc-1851473589c7
caps.latest.revision: 7
author: mcleblanc
ms.author: markl
manager: markl
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: 02b02b2fbc5398d7afda8884a04eafdaee12aef4
ms.contentlocale: zh-cn
ms.lasthandoff: 08/21/2017

---
# <a name="how-to-create-a-socket"></a>如何：创建套接字
必须先使用协议和网络地址信息初始化套接字，然后才能使用套接字与远程设备进行通信。 <xref:System.Net.Sockets.Socket> 类的构造函数包含的参数可以指定地址系列、套接字类型，以及套接字用于建立连接的协议类型。  
  
## <a name="example"></a>示例  
 下例创建的套接字可用于与基于 TCP/IP 的网络（例如 Internet）进行通信。  
  
```csharp  
Socket s = new Socket(AddressFamily.InterNetwork,   
   SocketType.Stream, ProtocolType.Tcp);  
```  
  
```vb  
Dim s as New Socket(AddressFamily.InterNetwork, _  
   SocketType.Stream, ProtocolType.Tcp)  
```  
  
 使用 UDP 而不是 TCP更改协议类型，如以下示例所示：  
  
```csharp  
Socket s = new Socket(AddressFamily.InterNetwork,   
   SocketType.Dgram, ProtocolType.Udp);  
```  
  
```vb  
Dim s as New Socket(AddressFamily.InterNetwork, _  
   SocketType.Dgram, ProtocolType.Udp)  
```  
  
 <xref:System.Net.Sockets.AddressFamily> 枚举指定 Socket 类用其解析网络地址的标准地址系列（例如，AddressFamily.InterNetwork 成员指定 IP 版本 4 地址系列）。  
  
 <xref:System.Net.Sockets.SocketType> 枚举指定套接字的类型（例如，SocketType.Stream 成员指定用流控制来发送和接收数据的标准套接字）。  
  
 <xref:System.Net.Sockets.ProtocolType> 枚举指定通信时套接字使用的网络协议（例如：ProtocolType.Tcp 表示套接字使用 TCP；ProtocolType.Udp 表示套接字使用 UDP）。  
  
 套接字创建完成后，可启动与远程终结点的连接或接收来自远程设备的连接。  
  
## <a name="see-also"></a>另请参阅  
 [使用客户端套接字](../../../docs/framework/network-programming/using-client-sockets.md)   
 [使用套接字侦听](../../../docs/framework/network-programming/listening-with-sockets.md)

