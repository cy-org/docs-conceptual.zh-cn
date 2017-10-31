---
title: "Windows Communication Foundation 示例的一次性安装过程 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: a5848ffd-3eb5-432d-812e-bd948ccb6bca
caps.latest.revision: 83
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 83
---
# Windows Communication Foundation 示例的一次性安装过程
大多数 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 示例均承载于 Internet 信息服务 \(IIS\) 中，并从公共虚拟目录中运行。此一次性安装过程在磁盘上创建一个文件夹；还将向 IIS 添加一个名为**“ServiceModelSamples”**的虚拟目录。  
  
 **“ServiceModelSamples”**虚拟目录用于生成和运行使用 IIS 承载的服务的所有示例。这是运行示例所需的唯一虚拟目录。绑定示例将替换以前在此虚拟目录部署的所有服务；只有最近生成的示例将在此虚拟目录中部署并可用。  
  
> [!NOTE]
>  必须在本地管理员帐户下运行所有命令。如果使用的是 Windows 7、[!INCLUDE[windowsver](../../../../includes/windowsver-md.md)] 或 Windows Server 2008 R2，则还必须用提升的特权运行命令提示。为此，请右击命令提示图标，然后单击**“以管理员身份运行”**。本主题中的所有命令都必须在具有合适路径设置的命令提示中运行。确保这一点的最简单方法是使用 Visual Studio 命令提示。若要打开此提示，请单击“开始”，选择**“所有程序”**，向下滚动到**“Visual Studio 2010”**，选择**“Visual Studio工具”**，右击**“Visual Studio 命令提示\(2010\)”**然后单击**“以管理员身份运行”**。如果安装了 Visual Studio 学习版，但此命令提示不可用，则必须向系统路径添加“C:\\Windows\\Microsoft.Net\\Framework\\v4.0”。  
  
### WCF 示例的一次性安装过程  
  
1.  确保已安装 [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)]。[!INCLUDE[crabout](../../../../includes/crabout-md.md)]如何安装 [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)] 的更多信息，请参见[Internet 信息服务承载说明](../../../../docs/framework/wcf/samples/internet-information-service-hosting-instructions.md)。  
  
2.  确保已安装 [!INCLUDE[netfx40_long](../../../../includes/netfx40-long-md.md)]。搜索 v4.0（或更高版本）的以下目录：**\\Windows\\Microsoft.NET\\Framework**  
  
3.  如果未安装 [!INCLUDE[vs_current_long](../../../../includes/vs-current-long-md.md)] 并且操作系统不是 Windows Server 2008 SP2 或更高版本，请安装[修补程序 251798](http://go.microsoft.com/fwlink/?LinkId=184693)（可能为英文网页）。  
  
4.  运行以下命令。有关必须运行这些命令的原因的更多信息，请参见 [IIS Hosted Service Fails](http://msdn.microsoft.com/zh-cn/ee5499fc-1b10-4cda-a9b1-13dba70f05f8)。  
  
    > [!WARNING]
    >  如果重新安装 IIS，则需要再次运行以下命令。  
  
    ```  
    "%WINDIR%\Microsoft.Net\Framework\v4.0.30319\aspnet_regiis" –i –enable  
    "%WINDIR%\Microsoft.Net\Framework\v4.0.30319\ServiceModelReg.exe" -r  
    ```  
  
    > [!WARNING]
    >  运行命令 `aspnet_regiis –i –enable` 会使默认应用程序池使用 [!INCLUDE[netfx40_short](../../../../includes/netfx40-short-md.md)] 运行，这可能会对同一台计算机上的其他应用程序产生不兼容问题。  
  
5.  按照[防火墙说明](../../../../docs/framework/wcf/samples/firewall-instructions.md)启用示例使用的端口。  
  
6.  检查以下默认目录：\<安装驱动器\>:**\\WF\_WCF\_Samples**。如果之前已安装这些示例，则该目录为默认目录。  
  
7.  如果未安装示例，则可以从 [Visual C\#](http://go.microsoft.com/fwlink/?LinkId=190939) 或 [Visual Basic](http://go.microsoft.com/fwlink/?LinkID=193373)（可能为英文网页）的示例下载位置进行安装。  
  
8.  安装这些示例后，转到：\<安装驱动器\>:**\\WF\_WCF\_Samples\\WCF\\Setup\\**  
  
9. 运行 **Setupvroot.bat** 批处理文件。将执行以下步骤：  
  
    -   将在 IIS 中创建一个名为 ServiceModelSamples 的虚拟目录。  
  
    -   新建名为 %SystemDrive%\\Inetpub\\wwwroot\\ServiceModelSamples 和 %SystemDrive%\\Inetpub\\wwwroot\\ServiceModelSamples\\bin 的磁盘目录。  
  
     如果想要手动设置这些目录，请参见[虚拟目录设置说明](../../../../docs/framework/wcf/samples/virtual-directory-setup-instructions.md)。若要恢复此步骤中所进行的所有更改，请在使用完示例后运行一次 cleanupvroot.bat。  
  
    > [!NOTE]
    >  除非运行 cleanupvroot.bat，否则此过程只能在计算机上执行一次。  
  
10. 您必须向在其下生成示例的帐户和 Network Service 用户授予对 %SystemDrive%\\inetpub\\wwwroot 的修改权限。在生成过程中，某些 Web 承载的示例可能会尝试将已编译的二进制文件复制到上述位置，如果您没有设置相应权限，则生成过程将中断。另外，也可以保持权限不变，并以管理员身份运行 SDK 命令提示或 Visual Studio 命令提示 \(2012\)，或在 [!INCLUDE[vs_current_long](../../../../includes/vs-current-long-md.md)] 中生成示例（也以管理员身份运行）。  
  
    > [!NOTE]
    >  如果未完成此步骤，IIS 承载的所有示例都将在生成时失败。确保正确设置权限，或者同时以管理员身份运行 SDK 命令提示和 Visual Studio 命令提示 \(2012\)。  
  
11. 在计算机上创建一个 C:\\logs 目录；某些示例可能需要此目录。确保向合适的帐户授予了对此文件夹的写访问权限。对于 Windows 7、[!INCLUDE[wv](../../../../includes/wv-md.md)] 和 Windows Server 2008 R2，此帐户为 **Network Service**。对于 [!INCLUDE[lserver](../../../../includes/lserver-md.md)]，该帐户为 NT Authority\\Network Service。对于 [!INCLUDE[wxp](../../../../includes/wxp-md.md)] 和 [!INCLUDE[ws2003](../../../../includes/ws2003-md.md)]，该帐户为 ASPNET。  
  
12. 运行 Setupcerttool.bat 文件。此文件位于 \<安装路径\>\\WF\_WCF\_Samples\\WCF\\Setup\\ 文件夹中。此脚本将执行以下任务：  
  
    -   生成 FindPrivateKey 工具。  
  
    -   创建一个名为 %ProgramFiles%\\ServiceModelSampleTools 的目录。  
  
    -   将新的 FindPrivateKey 工具复制到此目录。  
  
     使用证书且承载于 IIS 中的示例需要使用此工具。  
  
    > [!NOTE]
    >  出于安全方面的考虑，请记住在完成这些示例后，通过运行名为 Cleanupvroot.bat 的批处理文件来移除虚拟目录定义和在上面的设置步骤中授予的权限。  
  
13. 自承载（不承载于 IIS 中）的示例需要在计算机上注册要侦听的 HTTP 地址的权限。用于 HTTP 命名空间保留的权限由用于运行该示例的用户帐户提供。默认情况下，管理员帐户具有注册任何 HTTP 地址的权限。必须授予非管理员帐户对示例使用的 HTTP 命名空间的权限。[!INCLUDE[crabout](../../../../includes/crabout-md.md)]如何配置命名空间保留的更多信息，请参见[配置 HTTP 和 HTTPS](../../../../docs/framework/wcf/feature-details/configuring-http-and-https.md)。  
  
14. 有些示例需要使用消息队列。有关安装说明，请参见[安装“消息队列 \(MSMQ\)”](../../../../docs/framework/wcf/samples/installing-message-queuing-msmq.md)。  
  
    > [!NOTE]
    >  确保在运行需要消息队列的任何示例之前启动 MSMQ 服务。  
  
15. 有些示例需要使用证书。请参见 [Internet Information Services \(IIS\) 服务器证书安装说明](../../../../docs/framework/wcf/samples/iis-server-certificate-installation-instructions.md)。  
  
## 请参阅