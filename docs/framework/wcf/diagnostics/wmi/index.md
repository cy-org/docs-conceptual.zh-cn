---
title: "使用 Windows Management Instrumentation 进行诊断 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: fe48738d-e31b-454d-b5ec-24c85c6bf79a
caps.latest.revision: 24
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 24
---
# 使用 Windows Management Instrumentation 进行诊断
[!INCLUDE[indigo1](../../../../../includes/indigo1-md.md)] 通过 [!INCLUDE[indigo2](../../../../../includes/indigo2-md.md)] Windows Management Instrumentation \(WMI\) 提供程序在运行时公开服务的检测数据。  
  
## 启用 WMI  
 WMI 是 Microsoft 基于 Web 的企业管理 \(WBEM\) 标准的实现。  [!INCLUDE[crabout](../../../../../includes/crabout-md.md)] WMI SDK 的更多信息，请参见 MSDN 库。  \(http:\/\/msdn.microsoft.com\/library\/default.asp?url\=\/library\/wmisdk\/wmi\/wmi\_start\_page.asp\)。  WBEM 是有关应用程序如何向外部管理工具公开管理规范的行业标准。  
  
 WMI 提供程序是一个在运行时通过 WBEM 兼容接口公开规范的组件。  它由一组包含属性\/值对的 WMI 对象组成。  这些对可以是多个简单类型。  管理工具可以在运行时通过接口连接至服务。  [!INCLUDE[indigo2](../../../../../includes/indigo2-md.md)] 公开服务的特性，如地址、绑定、行为和侦听器。  
  
 您可以在应用程序的配置文件中激活内置 WMI 提供程序。  这可以通过 [\<system.serviceModel\>](../../../../../docs/framework/configure-apps/file-schema/wcf/system-servicemodel.md)一节中的 [\<诊断\>](../../../../../docs/framework/configure-apps/file-schema/wcf/diagnostics.md)的 `wmiProviderEnabled` 特性完成，如以下示例配置所示。  
  
```  
<system.serviceModel>  
    …  
    <diagnostics wmiProviderEnabled="true" />  
    …  
</system.serviceModel>  
  
```  
  
 此配置项公开 WMI 接口。  现在，您可以通过此接口连接管理应用程序并访问应用程序的管理规范。  
  
## 访问 WMI 数据  
 可以采用多种不同方式访问 WMI 数据。  Microsoft 提供用于脚本的 WMI API、[!INCLUDE[vbprvb](../../../../../includes/vbprvb-md.md)] 应用程序、C\+\+ 应用程序和 [!INCLUDE[dnprdnshort](../../../../../includes/dnprdnshort-md.md)]。  有关更多信息，请参见[使用 WMI](http://go.microsoft.com/fwlink/?LinkId=95183)（可能为英文网页）。  
  
> [!CAUTION]
>  如果您使用 .NET Framework 提供的方法以编程方式访问 WMI 数据，您应注意此类方法可能会在建立连接时引发异常。  连接并不是在构建 <xref:System.Management.ManagementObject> 实例的过程中建立的，而是在涉及实际数据交换的第一次请求时建立的。  因此，您应该使用 `try..catch` 块来捕捉可能的异常。  
  
 您可以在 WMI 中更改 `System.ServiceModel` 跟踪源的跟踪和消息日志记录级别以及消息日志记录选项。  这可以通过访问 [AppDomainInfo](../../../../../docs/framework/wcf/diagnostics/wmi/appdomaininfo.md) 实例实现，该实例将公开下列布尔属性：`LogMessagesAtServiceLevel`、`LogMessagesAtTransportLevel`、`LogMalformedMessages` 和 `TraceLevel`。  因此，如果为消息日志记录配置了跟踪侦听器，但是在配置中将这些选项设置为 `false`，那么可以在以后运行应用程序时将它们更改为 `true`。  这将在运行时有效地启用消息日志记录。  同样，如果在配置文件中启用了消息日志记录，可以在运行时使用 WMI 将其禁用。  
  
 您应该注意如果没有用于消息日志记录的消息日志记录跟踪侦听器，或者配置文件中没有指定用于跟踪的 `System.ServiceModel` 跟踪侦听器，您所执行的任何更改都将无效，即使已被 WMI 接受的更改也不例外。  有关正确设置各侦听器的详细信息，请参阅[配置消息日志记录](../../../../../docs/framework/wcf/diagnostics/configuring-message-logging.md)和[配置跟踪](../../../../../docs/framework/wcf/diagnostics/tracing/configuring-tracing.md)。  应用程序启动时，由配置指定的所有其他跟踪源的跟踪级别均有效，而且不能更改。  
  
 [!INCLUDE[indigo2](../../../../../includes/indigo2-md.md)] 公开 `GetOperationCounterInstanceName` 方法以编写脚本。  如果您为其提供了一个操作名称，此方法将返回一个性能计数器实例名称。  但是，它不会验证您的输入。  因此，如果您提供了一个不正确的操作名称，将返回不正确的计数器名称。  
  
 如果没有在 `OutgoingChannel` 方法中创建目标服务的 `Service` 客户端，则 [!INCLUDE[indigo2](../../../../../includes/indigo2-md.md)] 实例的 `Service` 属性将不会计算由某项服务打开以连接至其他服务的通道数量。  
  
 **警告** WMI 仅支持最多 3 位小数的 <xref:System.TimeSpan> 值。  例如，如果您的服务将其中一个属性设置为 <xref:System.TimeSpan.MaxValue>，当通过 WMI 查看时，它的值将保留 3 位小数。  
  
## 安全性  
 因为 [!INCLUDE[indigo2](../../../../../includes/indigo2-md.md)] WMI 提供程序允许在某个环境中发现服务，您应该在为其授予访问权限时特别小心。  如果您放宽了默认的仅管理员访问，就可能允许不完全受信任方访问您的环境中的敏感数据。  特别是，如果您放宽了对远程 WMI 访问的权限，可能会发生洪泛攻击。  如果某个进程被大量 WMI 请求溢满，其性能将有所下降。  
  
 此外，如果您放宽了对 MOF 文件的访问权限，不完全受信任方可以控制 WMI 的行为并更改加载到 WMI 架构中的对象。  例如，不完全受信任方可以移除字段，这样，管理员将无法看到关键数据，或者未填充或导致异常的字段将添加到文件中。  
  
 默认情况下，[!INCLUDE[indigo2](../../../../../includes/indigo2-md.md)] WMI 提供程序将对管理员授予“执行方法”、“提供程序编写”和“启用帐户”权限，并对 ASP.NET、本地服务和网络服务授予“启用帐户”权限。  尤其是，在非 [!INCLUDE[wv](../../../../../includes/wv-md.md)] 平台中，ASP.NET 帐户对 WMI ServiceModel 命名空间具有读访问权限。  如果您不希望对特定用户组授予这些特权，就应该停用 WMI 提供程序（默认状态为禁用），或者是禁用对特定用户组的访问。  
  
 此外，当您尝试通过配置启用 WMI 时，WMI 可能会因用户特权不足而无法启用。  但是，并不会将任何事件写入事件日志用于记录此次失败。  
  
 若要修改用户特权级别，请使用下列步骤。  
  
1.  单击“开始”，然后单击“运行”并键入 **compmgmt.msc**。  
  
2.  右击**“服务和应用程序\/WMI 控制”**以选择**“属性”**。  
  
3.  选择**“安全性”**选项卡，然后定位到**“Root\/ServiceModel”**命名空间。  单击**“安全性”**按钮。  
  
4.  选择您希望控制访问权限的特定组或用户，并使用**“允许”**或**“拒绝”**复选框配置权限。  
  
## 向其他用户授予 WCF WMI 注册权限  
 WCF 将管理数据公开到 WMI。  它通过承载进程内 WMI 提供程序（有时称为“分离的提供程序”）来完成此操作。  对于要公开的管理数据，注册此提供程序的帐户必须具有适当的权限。  在 Windows 中，默认情况下只有一小组特权帐户可以注册分离的提供程序。这是一个问题，因为用户通常要从不在默认集中的帐户下运行的 WCF 服务公开 WMI 数据。  
  
 若要提供此访问权，管理员必须按以下顺序向其他帐户授予以下权限：  
  
1.  用于访问 WCF WMI 命名空间的权限。  
  
2.  用于注册 WCF 分离 WMI 提供程序的权限。  
  
#### 授予 WMI 命名空间访问权限  
  
1.  运行下面的 PowerShell 脚本。  
  
    ```powershell  
    write-host “”  
    write-host “Granting Access to root/servicemodel WMI namespace to built in users group”  
    write-host “”  
  
    # Create the binary representation of the permissions to grant in SDDL  
    $newPermissions = "O:BAG:BAD:P(A;CI;CCDCLCSWRPWPRCWD;;;BA)(A;CI;CC;;;NS)(A;CI;CC;;;LS)(A;CI;CC;;;BU)"  
    $converter = new-object system.management.ManagementClass Win32_SecurityDescriptorHelper  
    $binarySD = $converter.SDDLToBinarySD($newPermissions)  
    $convertedPermissions = ,$binarySD.BinarySD  
  
    # Get the object used to set the permissions  
    $security = gwmi -namespace root/servicemodel -class __SystemSecurity  
  
    # Get and output the current settings  
    $binarySD = @($null)  
    $result = $security.PsBase.InvokeMethod("GetSD",$binarySD)  
  
    $outsddl = $converter.BinarySDToSDDL($binarySD[0])  
    write-host "Previous ACL: "$outsddl.SDDL  
  
    # Change the Access Control List (ACL) using SDDL  
    $result = $security.PsBase.InvokeMethod("SetSD",$convertedPermissions)   
  
    # Get and output the current settings  
    $binarySD = @($null)  
    $result = $security.PsBase.InvokeMethod("GetSD",$binarySD)  
  
    $outsddl = $converter.BinarySDToSDDL($binarySD[0])  
    write-host "New ACL:      "$outsddl.SDDL  
    write-host “”  
  
    ```  
  
     此 PowerShell 脚本使用安全描述符定义语言 \(SDDL\) 向 Built\-In Users 组授予对“root\/servicemodel”WMI 命名空间的访问权。  它指定了以下 ACL：  
  
    -   内置管理员 \(BA\) \- 已经具有访问权。  
  
    -   网络服务 \(NS\) \- 已经具有访问权。  
  
    -   本地系统 \(LS\) \- 已经具有访问权。  
  
    -   Built\-In Users \- 向其授予访问权的组。  
  
#### 向提供程序授予注册访问权  
  
1.  运行下面的 PowerShell 脚本。  
  
    ```powershell  
    write-host “”  
    write-host “Granting WCF provider registration access to built in users group”  
    write-host “”  
    # Set security on ServiceModel provider  
    $provider = get-WmiObject -namespace "root\servicemodel" __Win32Provider  
  
    write-host "Previous ACL: "$provider.SecurityDescriptor  
    $result = $provider.SecurityDescriptor = "O:BUG:BUD:(A;;0x1;;;BA)(A;;0x1;;;NS)(A;;0x1;;;LS)(A;;0x1;;;BU)"  
  
    # Commit the changes and display it to the console  
    $result = $provider.Put()  
    write-host "New ACL:      "$provider.SecurityDescriptor  
    write-host “”  
  
    ```  
  
### 向任意用户或组授予访问权  
 本节中的示例向所有本地用户授予 WMI 提供程序注册特权。  如果您希望向非内置的用户或组授予访问权，则必须获取该用户或组的安全标识符 \(SID\)。  获取任意用户的 SID 没有简单方法。  一个方法是以所需的用户身份登录，然后发出以下 shell 命令。  
  
```  
Whoami /user  
```  
  
 此方法提供了当前用户的 SID，但是此方法不能用于获取任意用户的 SID。  另一个获取 SID 的方法是使用 [Windows 2000 资源工具包对于管理任务](http://go.microsoft.com/fwlink/?LinkId=178660)（可能为英文网页）中的 [getsid.exe](http://go.microsoft.com/fwlink/?LinkId=186467) 工具。  此工具比较两个用户（本地用户或域用户）的 SID，其副功能是将两个 SID 显示到命令行。  [!INCLUDE[crdefault](../../../../../includes/crdefault-md.md)][常见 SID](http://go.microsoft.com/fwlink/?LinkId=186468)（可能为英文网页）。  
  
## 访问远程 WMI 对象实例  
 如果您需要访问远程计算机上的 [!INCLUDE[indigo2](../../../../../includes/indigo2-md.md)] WMI 实例，就必须对您用于访问的工具启用数据包保密性。  以下部分描述如何通过使用 WMI CIM Studio、Windows Management Instrumentation 测试器以及 .NET SDK 2.0 实现这些目标。  
  
### WMI CIM Studio  
 如果安装了 [WMI 管理工具](http://go.microsoft.com/fwlink/?LinkId=95185)（可能为英文网页），即可使用 WMI CIM Studio 访问 WMI 实例。  这些工具位于以下文件夹中  
  
 **%windir%\\Program Files\\WMI Tools\\**  
  
1.  在**“连接到命名空间:”**窗口中，键入 root\\ServiceModel，然后单击**“确定”**。  
  
2.  在**“WMI CIM Studio 登录”**窗口中，单击**“选项 \>\>”**按钮展开该窗口。  对**“身份验证级别”**选择**“数据包保密性”**，然后单击**“确定”**。  
  
### Windows Management Instrumentation 测试器  
 此工具由 Windows 安装。  若要运行它，请通过在**“开始\/运行”**对话框中键入 cmd.exe 然后单击**“确定”**来启动命令控制台。  然后，在命令窗口中键入 wbemtest.exe。  Windows Management Instrumentation 测试器工具随即启动。  
  
1.  单击窗口右上角的**“连接”**按钮。  
  
2.  在新窗口中，对于**“命名空间”**字段，输入 root\\ServiceModel，对于**“身份验证级别”**，选择**“数据包隐私性”**。  单击**“连接”**。  
  
### 使用托管代码  
 您还可以通过使用由 <xref:System.Management> 命名空间提供的类以编程方式访问远程 WMI 实例。  下面的代码示例演示如何实现此操作。  
  
```  
String wcfNamespace = String.Format(@"\\{0}\Root\ServiceModel",      
   this.serviceMachineName);  
  
ConnectionOptions connection = new ConnectionOptions();  
connection.Authentication = AuthenticationLevel.PacketPrivacy;  
ManagementScope scope = new ManagementScope(this.wcfNamespace, connection);  
```