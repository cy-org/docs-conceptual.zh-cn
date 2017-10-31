---
title: "WS-AtomicTransaction 配置 MMC 管理单元 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 23592973-1d51-44cc-b887-bf8b0d801e9e
caps.latest.revision: 17
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 17
---
# WS-AtomicTransaction 配置 MMC 管理单元
WS\-AtomicTransaction 配置 MMC 管理单元用于在本地计算机和远程计算机上配置一部分 WS\-AtomicTransaction 设置。  
  
## 备注  
 如果运行的是 [!INCLUDE[wxp](../../../includes/wxp-md.md)] 或 [!INCLUDE[ws2003](../../../includes/ws2003-md.md)]，则可通过以下方式找到该 MMC 管理单元：定位到**“控制面板”\/“管理工具”\/“组件服务”\/**，右击**“我的电脑”**，并选择**“属性”**。这与可在其中配置 MSDTC 的位置相同。可用于配置的选项分组显示在**“WS\-AT”**选项卡下。  
  
 如果运行的是 Windows Vista 或 [!INCLUDE[lserver](../../../includes/lserver-md.md)]，可以通过单击**“开始”**按钮，然后在**“搜索”**框中键入 `dcomcnfg.exe` 找到 MMC 管理单元。MMC 打开后，定位到**“我的电脑”\\“分布式事务处理协调器”\\“本地 DTC”**节点，右击并选择**“属性”**。可用于配置的选项分组显示在**“WS\-AT”**选项卡下。  
  
 使用前面的步骤来启动用于配置本地计算机的管理单元。如果要配置远程计算机，您应在**“控制面板”\/“管理工具”\/“组件服务”\/**中找到远程计算机的名称，然后执行类似的步骤（如果运行的是 [!INCLUDE[wxp](../../../includes/wxp-md.md)] 或 [!INCLUDE[ws2003](../../../includes/ws2003-md.md)]）。如果运行的是 Windows Vista 或 [!INCLUDE[lserver](../../../includes/lserver-md.md)]，请执行前面适用于 Vista 和 [!INCLUDE[lserver](../../../includes/lserver-md.md)] 的步骤，但要使用远程计算机节点下的**“分布式事务处理协调器”\\“本地 DTC”**节点。  
  
 若要使用工具提供的用户界面，您必须注册 WsatUI.dll 文件，该文件位于以下路径中：  
  
 **%PROGRAMFILES%\\Microsoft SDKs\\Windows\\v6.0\\Bin\\WsatUI.dll**  
  
 可通过以下命令完成注册。  
  
```Output  
regasm.exe /codebase WsatUI.dll  
```  
  
 您可以使用此工具来修改基本 WS\-AtomicTransaction 设置。例如，您可以启用和禁用 WS\-AtomicTransaction 协议支持、为 WS\-AT 配置 HTTP 端口、将 SSL 证书绑定到 HTTP 端口、通过指定证书主题名称来配置证书、选择跟踪模式以及设置默认和最大超时。  
  
 如果比粗在本地计算机上配置 WS\-AtomicTransaction 支持，您可以使用此工具的命令行版本。[!INCLUDE[crabout](../../../includes/crabout-md.md)]命令行工具的更多信息，请参见[WS\-AtomicTransaction 配置实用工具 \(wsatConfig.exe\)](../../../docs/framework/wcf/ws-atomictransaction-configuration-utility-wsatconfig-exe.md) 主题。  
  
 应该注意，MMC 管理单元和命令行工具都不支持配置所有 WS\-AT 设置。只能通过直接修改注册表来编辑这些设置。[!INCLUDE[crabout](../../../includes/crabout-md.md)]这些注册表设置的更多信息，请参见 [配置 WS\-Atomic 事务支持](../../../docs/framework/wcf/feature-details/configuring-ws-atomic-transaction-support.md)。  
  
### 用户界面说明  
 **“启用 WS\-AtomicTransaction 网络支持”**：  
  
 切换选择此复选框将启用或禁用此管理单元的所有 GUI 组件。  
  
 在选中此框之前，应确保为入站和\/或出站通信启用了“网络 DTC 访问”。可以在 MSDTC 管理单元的**“安全性”**选项卡中验证此值。  
  
#### “网络”分组框  
 您可以在“网络”组中指定 HTTPS 端口和其他安全设置（比如 SSL 加密）。如果未启用 DTC 网络事务处理，则此组处于禁用状态（显示为灰色）。  
  
 **HTTPS 端口**  
  
 这是用于 WS\-AT 的 HTTPS 端口的值。该值必须是 1\-65535 范围内的数字（以便表示有效的端口）。如果更改 HTTP 端口，将会修改 HTTP 服务配置，这意味着将会释放以前使用的 WS\-AT 服务地址，并基于新端口注册一个新的 WS\-AT 服务地址。此外，将使用当前为 SSL 加密选择的证书对新选择的端口进行加密。  
  
> [!NOTE]
>  如果在运行此工具之前已启用了防火墙，则会在例外列表中自动注册该端口。如果在运行此工具之前防火墙处于禁用状态，将不会对防火墙进行任何其他配置。  
  
 如果在配置 WS\-AT 之后启用防火墙，您必须再次运行此工具并使用此参数提供端口号。如果在配置之后禁用防火墙，WS\-AT 将继续工作，而无需附加输入。  
  
 **终结点证书**  
  
 单击**“选择”**按钮显示本地计算机上当前可用证书的列表，从而允许用户选择可用于 SSL 加密的证书。证书必须具有私钥。否则会收到一条错误消息。  
  
> [!NOTE]
>  为选定端口设置 SSL 证书时，将覆盖与该端口关联的原始 SSL 证书（如果有）。  
  
 **授权的帐户**  
  
 单击**“选择”**按钮调用 Windows 访问控制列表编辑器，通过选中**“参加”**权限组中的**“允许”**或**“拒绝”**框，您可以在该编辑器中指定可参与 WS\-Atomic 事务处理的用户或组。  
  
 **授权的证书**  
  
 单击**“选择”**按钮可显示本地计算机上当前可用证书的列表。然后，您可以选择允许哪些证书标识参与 WS\-Atomic 事务处理。  
  
#### “超时”分组框  
 **“超时”**分组框允许您为 WS\-Atomic 事务处理指定默认和最大超时。传出超时的有效值介于 1 和 3600 之间。传入超时的有效值介于 0 和 3600 之间。  
  
#### “跟踪和日志记录”分组框  
 **“跟踪和日志记录”**分组框允许您配置所需的跟踪和日志记录级别。  
  
 单击**“选项”**按钮将调用一个页面，您可在其中指定附加设置。  
  
 利用**“跟踪级别”**组合框，您可以从 <xref:System.Diagnostics.TraceLevel> 枚举的任何有效值中进行选择。您也可以使用这些复选框来指定是否要执行活动跟踪、活动传播或收集个人身份信息。  
  
 还可以在**“日志记录会话”**分组框中指定日志记录会话。  
  
> [!NOTE]
>  如果另一个跟踪使用者正在使用 WS\-AT 跟踪提供程序，则您无法为跟踪事件创建新的日志记录会话。任何试图在此时配置日志记录的操作都会导致错误消息“无法启用提供程序。错误代码: 1”。  
  
 [!INCLUDE[crabout](../../../includes/crabout-md.md)]跟踪和日志记录的更多信息，请参见[管理和诊断](../../../docs/framework/wcf/diagnostics/index.md)。  
  
## 请参阅  
 [配置 WS\-Atomic 事务支持](../../../docs/framework/wcf/feature-details/configuring-ws-atomic-transaction-support.md)   
 [WS\-AtomicTransaction 配置实用工具 \(wsatConfig.exe\)](../../../docs/framework/wcf/ws-atomictransaction-configuration-utility-wsatconfig-exe.md)   
 [管理和诊断](../../../docs/framework/wcf/diagnostics/index.md)