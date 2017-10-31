---
title: "如何：启用 Net.TCP 端口共享服务 | Microsoft Docs"
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
  - "端口共享 [WCF]"
  - "激活服务 [WCF]"
ms.assetid: c9175af4-c27c-4765-bf45-b8f7528a7282
caps.latest.revision: 12
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 12
---
# 如何：启用 Net.TCP 端口共享服务
[!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 使用一个名为 Net.TCP 端口共享服务的 Windows 服务，以方便在多个进程之间共享 TCP 端口。 此服务作为 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 的一部分进行安装，但作为一项安全预防措施，默认情况下不会启用该服务，因此必须在首次使用它之前手动启用。 本主题描述如何使用 Microsoft 管理控制台 (MMC) 管理单元配置 Net TCP 端口共享服务。  
  
 启用 Net.TCP Port Sharing Service 并手动启动后，请参阅[如何︰ 配置 WCF 服务以使用端口共享](../../../../docs/framework/wcf/feature-details/how-to-configure-a-wcf-service-to-use-port-sharing.md)有关如何配置你的服务以使用此服务的信息。  
  
 有关使用 net.tcp:// 端口共享的示例，请参阅[Net.TCP 端口共享示例](../../../../docs/framework/wcf/samples/net-tcp-port-sharing-sample.md)。  
  
### <a name="to-enable-the-nettcp-port-sharing-service-using-mmc"></a>使用 MMC 启用 Net.TCP 端口共享服务  
  
1.  从开始菜单中，打开服务管理控制台通过打开命令提示符窗口并键入`services.msc`或通过打开运行并键入`services.msc`到打开框。  
  
2.  在**名称**服务列表的列中用鼠标右键单击**Net.Tcp Port Sharing Service**，然后选择**属性**从菜单。  
  
3.  若要启用该服务的手动启动在**属性**窗口中选择**常规**选项卡上，然后在**启动类型**框中选择手动，然后再单击**应用**。  
  
4.  若要启动服务，服务状态区域中，请单击**启动**按钮。 现在，服务状态区域应显示为“已启动”。  
  
5.  若要返回到服务的列表，请单击**确定**，并退出 MMC 控制台。  
  
## <a name="example"></a>示例  
<!-- TODO: review snippet reference  [!CODE [Microsoft.Win32.RegistryKey#4](Microsoft.Win32.RegistryKey#4)]  -->  
  
## <a name="see-also"></a>另请参阅  
 [Net.TCP 端口共享](../../../../docs/framework/wcf/feature-details/net-tcp-port-sharing.md)   
 [配置 Net.TCP 端口共享服务](../../../../docs/framework/wcf/feature-details/configuring-the-net-tcp-port-sharing-service.md)