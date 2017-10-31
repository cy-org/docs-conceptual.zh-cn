---
title: "使用同步服务器套接字"
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
- synchronous server sockets
- sending data, sockets
- data requests, sockets
- requesting data from Internet, sockets
- server sockets
- receiving data, sockets
- Socket class, synchronous server sockets
- protocols, sockets
- sockets, synchronous server sockets
- Internet, sockets
ms.assetid: d1ce882e-653e-41f5-9289-844ec855b804
caps.latest.revision: 9
author: mcleblanc
ms.author: markl
manager: markl
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: c4ecba2d6c5026a3b2f7d65540fcf40dd71ba3d7
ms.contentlocale: zh-cn
ms.lasthandoff: 08/21/2017

---
# <a name="using-a-synchronous-server-socket"></a>使用同步服务器套接字
同步服务器套接字会挂起应用程序的执行，直到在套接字上收到连接请求。 同步服务器套接字不适用于在其操作中大量使用网络的应用程序，但它们可能适用于简单的网络应用程序。  
  
 使用 <xref:System.Net.Sockets.Socket.Bind%2A> 和 <xref:System.Net.Sockets.Socket.Listen%2A> 方法将 <xref:System.Net.Sockets.Socket> 设置为侦听终结点之后，便可以开始使用 <xref:System.Net.Sockets.Socket.Accept%2A> 方法接受传入的连接请求。 调用 Accept 方法时，应用程序将处于挂起状态，直到收到连接请求。  
  
 在收到连接请求时，Accept 会返回一个与连接客户端关联的新 Socket 实例。 下面的示例从客户端读取数据，并在控制台上显示该数据，然后将数据回显到客户端。 Socket 不指定任何消息协议，因此字符串“\<EOF>”标记消息数据的结尾。 它假定名为 `listener` 的 Socket 已初始化并绑定到终结点。  
  
```vb  
Console.WriteLine("Waiting for a connection...")  
Dim handler As Socket = listener.Accept()  
Dim data As String = Nothing  
  
While True  
    bytes = New Byte(1024) {}  
    Dim bytesRec As Integer = handler.Receive(bytes)  
    data += Encoding.ASCII.GetString(bytes, 0, bytesRec)  
    If data.IndexOf("<EOF>") > - 1 Then  
        Exit While  
    End If  
End While  
  
Console.WriteLine("Text received : {0}", data)  
  
Dim msg As Byte() = Encoding.ASCII.GetBytes(data)  
handler.Send(msg)  
handler.Shutdown(SocketShutdown.Both)  
handler.Close()  
```  
  
```csharp  
Console.WriteLine("Waiting for a connection...");  
Socket handler = listener.Accept();  
String data = null;  
  
while (true) {  
    bytes = new byte[1024];  
    int bytesRec = handler.Receive(bytes);  
    data += Encoding.ASCII.GetString(bytes,0,bytesRec);  
    if (data.IndexOf("<EOF>") > -1) {  
        break;  
    }  
}  
  
Console.WriteLine( "Text received : {0}", data);  
  
byte[] msg = Encoding.ASCII.GetBytes(data);  
handler.Send(msg);  
handler.Shutdown(SocketShutdown.Both);  
handler.Close();  
```  
  
## <a name="see-also"></a>另请参阅  
 [使用异步服务器套接字](../../../docs/framework/network-programming/using-an-asynchronous-server-socket.md)   
 [同步服务器套接字示例](../../../docs/framework/network-programming/synchronous-server-socket-example.md)   
 [使用套接字侦听](../../../docs/framework/network-programming/listening-with-sockets.md)

