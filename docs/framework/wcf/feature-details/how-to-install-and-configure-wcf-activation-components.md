---
title: "如何：安装和配置 WCF 激活组件 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "HTTP 激活 [WCF]"
ms.assetid: 33a7054a-73ec-464d-83e5-b203aeded658
caps.latest.revision: 16
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 16
---
# 如何：安装和配置 WCF 激活组件
本主题描述了在 [!INCLUDE[wv](../../../../includes/wv-md.md)] 上设置 Windows 进程激活服务（也称为 WAS）以承载不通过 HTTP 网络协议进行通信的 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 服务所需步骤。下面的部分略述此配置的步骤：  
  
-   安装（或确认安装）[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 激活组件。  
  
-   配置 WAS 以支持非 HTTP 协议。下面的过程对 [!INCLUDE[wv](../../../../includes/wv-md.md)] 进行 TCP 激活配置。  
  
 在安装和配置 WAS 之后，请参见 [如何：在 WAS 中承载 WCF 服务](../../../../docs/framework/wcf/feature-details/how-to-host-a-wcf-service-in-was.md) 以了解创建公开使用 WAS 的非 HTTP 终结点的 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 服务的过程。  
  
### 安装 WCF 非 HTTP 激活组件  
  
1.  单击**“开始”**按钮，再单击**“控制面板”**。  
  
2.  单击**“程序”**，再单击**“程序和功能”**。  
  
3.  在**“任务”**菜单上，单击**“打开或关闭 Windows 功能”**。  
  
4.  查找 [!INCLUDE[vstecwinfx](../../../../includes/vstecwinfx-md.md)] 节点，选中该节点然后将其展开。  
  
5.  选中**“WCF 非 HTTP 激活组件”**框并保存设置。  
  
### 配置 WAS 以支持 TCP 激活  
  
1.  若要支持 net.tcp 激活，必须首先将默认的网站绑定到一个 net.tcp 端口。可以通过使用随 [!INCLUDE[iisver](../../../../includes/iisver-md.md)] 管理工具集安装的 Appcmd.exe 来执行此操作。在管理员级别命令提示符窗口中，运行以下命令。  
  
    ```  
    %windir%\system32\inetsrv\appcmd.exe set site "Default Web Site" -+bindings.[protocol='net.tcp',bindingInformation='808:*']  
    ```  
  
    > [!NOTE]
    >  此命令是单行文本。此命令将 net.tcp 网站绑定添加到以任何主机名侦听 TCP 端口 808 的默认网站。  
  
2.  尽管网站内的所有应用程序共享一个公共 net.tcp 绑定，但是每个应用程序可以单独启用 net.tcp 支持。若要启用应用程序的 net.tcp，请从管理员级别命令提示符运行以下命令。  
  
    ```  
    %windir%\system32\inetsrv\appcmd.exe set app   
    "Default Web Site/<WCF Application>" /enabledProtocols:http,net.tcp  
    ```  
  
    > [!NOTE]
    >  此命令是单行文本。此命令使 \/\<*WCF Application*\> 应用程序可以通过 http:\/\/localhost*\/\<WCF Application\>* 和 net.tcp:\/\/localhost\/*\<WCF Application\>* 来进行访问。  
  
     移除为此示例添加的 net.tcp 站点绑定。  
  
     为方便起见，在位于示例目录中名为 RemoveNetTcpSiteBinding.cmd 的批处理文件中实现以下两个步骤。  
  
    1.  通过在管理员级别命令提示符窗口中运行以下命令，从启用的协议列表移除 net.tcp。  
  
        ```  
        %windir%\system32\inetsrv\appcmd.exe set app   
        "Default Web Site/servicemodelsamples<WCF Application>" " /enabledProtocols:http  
        ```  
  
        > [!NOTE]
        >  此命令是单行文本。  
  
    2.  通过在提升的命令提示符窗口中运行以下命令移除 net.tcp 网站绑定：  
  
        ```  
        %windir%\system32\inetsrv\appcmd.exe set site "Default Web Site"   
        --bindings.[protocol='net.tcp',bindingInformation='808:*']  
        ```  
  
        > [!NOTE]
        >  此命令是单行文本。  
  
### 从启用的协议列表中移除 net.tcp  
  
1.  若要从启用的协议列表中移除 net.tcp，请在管理员级别命令提示符窗口中运行以下命令。  
  
    ```  
    %windir%\system32\inetsrv\appcmd.exe set app "Default Web Site/servicemodelsamples<WCF Application>" " /enabledProtocols:http  
    ```  
  
    > [!NOTE]
    >  此命令是单行文本。  
  
### 移除 net.tcp 网站绑定  
  
1.  要移除 net.tcp 网站绑定，请在管理员级别命令提示窗口中运行以下命令。  
  
    ```  
    %windir%\system32\inetsrv\appcmd.exe set site "Default Web Site"   
    -bindings.[protocol='net.tcp',bindingInformation='808:*']  
    ```  
  
    > [!NOTE]
    >  此命令是单行文本。  
  
## 请参阅  
 [TCP 激活](../../../../docs/framework/wcf/samples/tcp-activation.md)   
 [MSMQ 激活](../../../../docs/framework/wcf/samples/msmq-activation.md)   
 [NamedPipe 激活](../../../../docs/framework/wcf/samples/namedpipe-activation.md)   
 [Windows Server App Fabric 承载功能](http://go.microsoft.com/fwlink/?LinkId=201276)