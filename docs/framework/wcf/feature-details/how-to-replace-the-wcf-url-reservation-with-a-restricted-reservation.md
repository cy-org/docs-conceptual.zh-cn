---
title: "如何：用受限保留项替换 WCF URL 保留项 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 2754d223-79fc-4e2b-a6ce-989889f2abfa
caps.latest.revision: 6
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 6
---
# 如何：用受限保留项替换 WCF URL 保留项
URL 保留项使您能够限制谁可以接收来自某个 URL 或某一组 URL 的消息。保留项由一个 URL 模板、一个访问控制列表 \(ACL\) 和一组标志组成。URL 模板定义了受保留项影响的 URL。[!INCLUDE[crabout](../../../../includes/crabout-md.md)]如何处理 URL 模板的更多信息，请参见 [Routing Incoming Requests](http://go.microsoft.com/fwlink/?LinkId=136764)（路由传入的请求）。ACL 控制哪个用户或用户组允许接收来自指定 URL 的消息。标志指示保留项是赋予用户或用户组直接侦听 URL 的权限，还是将侦听权限委托给其他进程。  
  
 在默认的操作系统配置中，[!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 为端口 80 创建可全局访问的保留项，使所有用户都能够运行应用程序，在该应用程序中使用双向 HTTP 绑定来进行双工通信。由于此保留项的 ACL 适用于所有用户，因此管理员不能显式允许或禁止侦听某个 URL 或某一组 URL 的权限。本主题介绍如何删除此保留项，以及如何重新创建具有受限 ACL 的保留项。  
  
 在 [!INCLUDE[wv](../../../../includes/wv-md.md)] 或 [!INCLUDE[lserver](../../../../includes/lserver-md.md)] 上键入 `netsh http show urlacl`，就可以在具有提升权限的命令提示符中查看所有 HTTP URL 保留项。下面的示例演示 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] URL 保留项的形式。  
  
```  
Reserved URL : http://+:80/Temporary_Listen_Addresses/  
        User: \Everyone  
            Listen: Yes  
            Delegate: No  
            SDDL: D:(A;;GX;;;WD)  
```  
  
 该保留项包含的 URL 模板在 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 应用程序使用 HTTP 双向绑定进行双工通信时使用。这种 URL 由 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 服务用于在通过 HTTP 双向绑定进行通信时将消息发送回 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 客户端。向每个用户授予侦听该 URL 的权限，而不将侦听权限委托给另一个进程。最后，安全描述符定义语言 \(SSDL\) 中介绍了该 ACL。[!INCLUDE[crabout](../../../../includes/crabout-md.md)] SSDL 的更多信息，请参见 [SSDL](http://go.microsoft.com/fwlink/?LinkId=136789)  
  
### 删除 WCF URL 保留项  
  
1.  单击**“开始”**，指向**“所有程序”**，单击**“附件”**，右键单击**“命令提示符”**，然后在显示的上下文菜单中单击**“以管理员身份运行”**。如果“用户帐户控制”\(UAC\) 窗口请求您允许其继续，请单击**“继续”**。  
  
2.  在命令提示符窗口中键入 **netsh http delete urlacl url\=http:\/\/\+:80\/Temporary\_Listen\_Addresses\/**。  
  
3.  如果成功删除了保留项，将显示以下消息。**URL reservation successfully deleted**  
  
## 创建新的安全组和新的受限 URL 保留项  
 若要用受限保留项替换 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] URL 保留项，必须先创建新的安全组。可以通过两种方法执行此操作：从命令提示符或从计算机管理控制台。您只需要执行一次。  
  
#### 从命令提示符创建新的安全组  
  
1.  单击**“开始”**，指向**“所有程序”**，单击**“附件”**，右键单击**“命令提示符”**，然后在显示的上下文菜单中单击**“以管理员身份运行”**。如果“用户帐户控制”\(UAC\) 窗口请求您允许其继续，请单击**“继续”**。  
  
2.  在命令提示符处键入 **net localgroup "\<security group name\>" \/comment:"\<security group description\>" \/add**。请将 **\<security group name\>** 替换为要创建的安全组名称，并将 **\<security group description\>** 安全组说明替换为适当的安全组说明。  
  
3.  如果成功创建了安全组，将显示以下消息。**The command completed successfully.**  
  
#### 从计算机管理控制台创建新的安全组  
  
1.  依次单击**“开始”**、**“控制面板”**、**“管理工具”**和**“计算机管理”**，以打开计算机管理控制台。如果“用户帐户控制”\(UAC\) 窗口请求您允许其继续，请单击**“继续”**。  
  
2.  依次单击**“系统工具”**、**“本地用户和组”**，右键单击**“组”**文件夹，然后在显示的上下文菜单中单击**“新建组”**。键入新安全组所需的**“组名称”**、**“说明”**和其他详情，然后单击**“创建”**按钮创建安全组。  
  
#### 创建受限 URL 保留项  
  
1.  单击**“开始”**，指向**“所有程序”**，单击**“附件”**，右键单击**“命令提示符”**，然后在显示的上下文菜单中单击**“以管理员身份运行”**。如果“用户帐户控制”\(UAC\) 窗口请求您允许其继续，请单击**“继续”**。  
  
2.  在命令提示符处键入 **netsh http add urlacl url\=http:\/\/\+:80\/Temporary\_Listen\_Addresses\/ user\="\<machine name\>\\\<security group name\>**。请将 **\<machine name\>** 替换为必须创建的组的计算机名称，并将 **\<security group name\>** 替换为前面创建的安全组的名称。  
  
3.  如果成功创建了保留项，将显示以下消息。**URL reservation successfully added**.