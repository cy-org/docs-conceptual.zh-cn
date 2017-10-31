---
title: "配置 Net.TCP 端口共享服务 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: b6dd81fa-68b7-4e1b-868e-88e5901b7ea0
caps.latest.revision: 20
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 20
---
# 配置 Net.TCP 端口共享服务
使用 Net.TCP 传输协议的自承载服务可以控制某些高级设置，如 `ListenBacklog` 和 `MaxPendingAccepts`，这些设置控制用作网络通信的基础 TCP 套接字的行为。  但是，如果传输绑定已禁用端口共享（默认情况下是启用的），则这些针对每个套接字的设置将仅在绑定级别适用。  
  
 当 net.tcp 绑定启用端口共享时（通过在传输绑定元素上设置 `portSharingEnabled =true` 来实现），该绑定隐式允许外部进程（即承载 Net.TCP 端口共享服务的 SMSvcHost.exe）代表它来管理 TCP 套接字。  例如，使用 TCP 时指定：  
  
```  
    <tcpTransport   
        portSharingEnabled="true"  
/>  
```  
  
 如果按这种方式进行配置，则会忽略在服务的传输绑定元素上指定的任何套接字设置，而代之以由 SMSvcHost.exe 指定的套接字设置。  
  
 若要配置 SMSvcHost.exe，请创建一个名为 SmSvcHost.exe.config 的 XML 配置文件，并将其与 SMSvcHost.exe 可执行文件放在同一个物理目录中（例如，C:\\Windows\\Microsoft.NET\\Framework\\v4.5）。  
  
 下面的示例阐释了示例 SMSvcHost.exe.config 并对所有显式指定的可配置值使用默认设置。  
  
```  
<configuration>  
   <system.serviceModel.activation>  
       <net.tcp listenBacklog="16" <!—16 * # of processors -->  
          maxPendingAccepts="4"<!— 4 * # of processors -->  
          maxPendingConnections="100"  
          receiveTimeout="00:00:30" <!—30 seconds -->  
          teredoEnabled="false">  
          <allowAccounts>  
             <!-- LocalSystem account -->  
             <add securityIdentifier="S-1-5-18"/>  
             <!-- LocalService account -->  
             <add securityIdentifier="S-1-5-19"/>  
             <!-- Administrators account -->  
             <add securityIdentifier="S-1-5-20"/>  
             <!-- Network Service account -->  
             <add securityIdentifier="S-1-5-32-544" />  
             <!-- IIS_IUSRS account (Vista only) -->  
             <add securityIdentifier="S-1-5-32-568"/>  
           </allowAccounts>  
       </net.tcp>  
</configuration>  
```  
  
## 何时修改 SMSvcHost.exe.config  
 通常，修改 SMSvcHost.exe.config 文件的内容时应当小心，原因是此文件中指定的任何配置设置都会影响使用 Net.TCP 端口共享服务的计算机上的所有服务。  这包括 [!INCLUDE[wv](../../../../includes/wv-md.md)] 上使用 Windows 进程激活服务 \(WAS\) 的 TCP 激活功能的应用程序。  
  
 但是，有时可能需要更改 Net.TCP 端口共享服务的默认配置。  例如，`maxPendingAccepts` 的默认值为 4 \* 处理器数。  承载大量使用端口共享的服务的服务器可以增加此值，以实现最大的吞吐量。  `maxPendingConnections` 的默认值为 100。  如果有多个并发客户端调用服务，并且此服务正在丢弃客户端连接，您还应该考虑增加此值。  
  
 SMSvcHost.exe.config 还包含有关可以使用端口共享服务的进程标识的信息。  当进程连接到端口共享服务以使用共享的 TCP 端口时，将根据允许使用端口共享服务的标识列表来检查连接进程的进程标识。  这些标识在 SMSvcHost.exe.config 文件的 \<allowAccounts\> 节中将作为安全标识符 \(SID\) 指定。  默认情况下，将授予系统帐户（LocalService、LocalSystem 和 NetworkService）和 Administrators 组的成员使用端口共享服务的权限。  允许作为另一个标识（例如，用户标识）运行的进程连接到端口共享服务的应用程序必须将适当的 SID 显式添加到 SMSvcHost.exe.config 中（在重新启动 SMSvc.exe 进程之前不会应用这些更改）。  
  
> [!NOTE]
>  在启用用户帐户控制 \(UAC\) 的 [!INCLUDE[wv](../../../../includes/wv-md.md)] 系统上，即使本地用户的帐户是 Administrators 组成员，本地用户也需要提升的权限。  若要允许这些用户不用提升权限也能使用端口共享服务，则必须将用户的 SID（或用户所属的成员组的 SID）显式添加到 SMSvcHost.exe.config 的 \<allowAccounts\> 节中。  
  
> [!WARNING]
>  默认 SMSvcHost.exe.config 文件指定自定义 `etwProviderId` 以阻止 SMSvcHost.exe 跟踪干扰服务跟踪。  
  
## 请参阅  
 [\<net.tcp\>](../../../../docs/framework/configure-apps/file-schema/wcf/net-tcp.md)