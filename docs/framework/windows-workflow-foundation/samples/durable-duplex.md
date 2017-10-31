---
title: "持久双工 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 4e76d1a1-f3d8-4a0f-8746-4a322cdff6eb
caps.latest.revision: 10
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 10
---
# 持久双工
此示例演示如何使用 [!INCLUDE[wf](../../../../includes/wf-md.md)] 中的消息传递活动来设置和配置持久双工消息交换。持久双工消息交换是一类持续时间较长的双向消息交换。消息交换的生存期可能比通信通道的生存期和服务实例的内存生存期要长一些。  
  
## 示例详细信息  
 在此示例中，将使用 [!INCLUDE[wf2](../../../../includes/wf2-md.md)] 实现的两个 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 服务配置为具有持久双工消息交换。持久双工消息交换由两个单向消息组成，二者通过 MSMQ 发送并使用 [.NET 上下文交换](http://go.microsoft.com/fwlink/?LinkID=166059)（可能为英文网页）进行关联。使用 <xref:System.ServiceModel.Activities.Send> 和 <xref:System.ServiceModel.Activities.Receive> 消息传递活动发送消息。.NET 上下文交换用于指定所发送消息上的回调地址。使用 Windows 进程激活服务 \(WAS\) 承载这两个服务，并将其配置为启用服务实例的持久性。  
  
 第一个服务 \(Service1.xamlx\) 会向第二个服务 \(Service2.xamlx\) 发送执行某项工作的请求。 完成此项工作后，Service2.xamlx 会向 Service1.xamlx 发送通知，以指示工作已完成。工作流控制台应用程序会设置服务正在侦听的队列，并会发送初始启动消息以激活 Service1.xamlx。一旦 Service1.xamlx 收到来自 Service2.xamlx 的有关请求的工作已完成的通知，它就会将结果保存到一个 XML 文件中。在等待回调消息时，Service1.xamlx 会使用默认的 <xref:System.ServiceModel.Activities.Description.WorkflowIdleBehavior> 保持其实例状态。Service2.xamlx 将其实例状态保持为完成 Service1.xamlx 所请求的工作的一部分。  
  
 若要配置服务以通过 MSMQ 使用 .NET 上下文交换，请将这两个服务配置为使用由 <xref:System.ServiceModel.Channels.ContextBindingElement> 和 <xref:System.ServiceModel.Channels.MsmqTransportBindingElement> 组成的自定义绑定。使用 <xref:System.ServiceModel.Channels.ContextBindingElement> 指定一个回调地址，并将该地址包含在带有使用一个自定义绑定发送的所有消息的回调上下文标头中。下面的代码示例定义了该自定义绑定。  
  
```xml  
<configuration>  
     <system.serviceModel>  
          …  
          <bindings>  
               <customBinding>  
                    <binding name="netMsmqContextBinding">  
                         <context clientCallbackAddress="net.msmq://localhost/private/DurableDuplex/Service1.xamlx"/>  
                         <msmqTransport exactlyOnce="False">  
                              <msmqTransportSecurity msmqAuthenticationMode="None" msmqProtectionLevel="None"/>  
                         </msmqTransport>  
                    </binding>  
               </customBinding>  
          </bindings>  
          …  
     </system.serviceModel>  
</configuration>  
  
```  
  
> [!NOTE]
>  此示例使用的绑定并不安全。在部署应用程序时，应按照应用程序的安全要求配置绑定。  
  
> [!NOTE]
>  此示例中使用的队列不是事务性队列。有关演示如何使用事务队列设置 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 消息交换的示例，请参见 [MSMQ 激活](../../../../docs/framework/wcf/samples/msmq-activation.md)示例。  
  
 使用一个客户端终结点发送已由 Service1.xamlx 发送给 Service2.xamlx 的消息，该客户端终结点是使用 Service2.xamlx 的地址和之前定义的自定义绑定配置的。使用一个客户端终结点发送从 Service2.xamlx 到 Service1.xamlx 的回调，该客户端终结点没有显式配置的地址，因为此地址取自由 Service1.xamlx 发送的回调上下文。下面的代码示例定义了这些客户端终结点。  
  
```xml  
<?xml version="1.0"?>  
<configuration>  
     <system.serviceModel>  
          …  
          <client>  
               <endpoint address="net.msmq://localhost/private/DurableDuplex/Service2.xamlx" binding="customBinding" bindingConfiguration="netMsmqContextBinding" contract="IDoWork"/>  
               <endpoint binding="customBinding" bindingConfiguration="netMsmqContextBinding" contract="INotify"/>  
          </client>  
          …  
     </system.serviceModel>  
</configuration>  
  
```  
  
 下面的代码示例通过将 net.msmq 基地址的默认协议映射更改为使用此自定义绑定，来公开使用此自定义绑定的终结点。  
  
```  
<configuration>  
     <system.serviceModel>  
          <protocolMapping>  
               <add scheme="net.msmq" binding="customBinding" bindingConfiguration="netMsmqContextBinding"/>  
          </protocolMapping>  
          …  
     </system.serviceModel>  
</configuration>  
  
```  
  
 下面的代码示例通过将 <xref:System.ServiceModel.Activities.Description.SqlWorkflowInstanceStoreBehavior> 行为添加到这两个服务并指定持久性数据库的连接字符串，为这两个服务启用持久性。  
  
```xml  
<?xml version="1.0"?>  
<configuration>  
    <system.serviceModel>  
          …  
          <behaviors>  
               <serviceBehaviors>  
                    <behavior>  
                         <serviceDebug includeExceptionDetailInFaults="True"/>  
                         <serviceMetadata httpGetEnabled="True"/>  
                         <sqlWorkflowInstanceStore connectionString="Data Source=.\SQLEXPRESS;Initial Catalog=DefaultSampleStore;Integrated Security=True"/>  
                    </behavior>  
               </serviceBehaviors>  
          </behaviors>  
     </system.serviceModel>  
</configuration>  
  
```  
  
## 系统要求  
 此示例需要以下组件。  
  
1.  Internet 信息服务。  
  
2.  Internet 信息服务 \-\> IIS 6.0 管理兼容性 \-\> IIS 元数据库与 IIS 6.0 配置的兼容性。  
  
3.  万维网服务 \-\> 应用程序开发功能 \-\> ASP.NET。  
  
4.  Microsoft Message Queues \(MSMQ\) Server。  
  
#### 使用此示例  
  
1.  设置持久性数据库和结果目录。  
  
    1.  打开 [!INCLUDE[vs2010](../../../../includes/vs2010-md.md)] 命令提示符。  
  
    2.  导航到此示例所在的文件夹并运行 Setup.cmd。  
  
2.  设置虚拟应用程序。  
  
    1.  在 [!INCLUDE[vs2010](../../../../includes/vs2010-md.md)] 命令提示符下，通过运行以下命令来注册 ASP.NET。  
  
        ```  
        aspnet_regiis -i  
        ```  
  
    2.  通过右击 [!INCLUDE[vs2010](../../../../includes/vs2010-md.md)] 并选择**“以管理员身份运行”**，使用管理员权限运行 [!INCLUDE[vs2010](../../../../includes/vs2010-md.md)]。  
  
    3.  使用 [!INCLUDE[vs2010](../../../../includes/vs2010-md.md)] 打开 DurableDuplex.sln 文件。  
  
3.  设置服务队列。  
  
    1.  若要运行 DurableDuplex 客户端，请按 F5。  
  
    2.  通过从命令提示符运行 `Compmgmt.msc` 打开**“计算机管理”**控制台。  
  
    3.  依次展开**“服务和应用程序”**、**“消息队列”**和**“专用队列”**。  
  
    4.  右击 durableduplex\/service1.xamlx 和 durableduplex\/service2.xamlx 队列，然后选择**“属性”**。  
  
    5.  选择**“安全性”**选项卡，并允许这两个队列具有**“每个人接收消息”\[Everyone Receive Message\]**、**“查看消息”**和**“发送消息”**权限。  
  
    6.  打开 Internet 信息服务 \(IIS\) 管理器。  
  
    7.  浏览到 **“服务器”**\-\>**“站点”**\-\>**“默认网站”**\-\>**“专用”**\-\>**“Durable Duplex”（持久双工）**，然后选择**“高级选项”**。  
  
    8.  将**“已启用的协议”**更改为**“http,net.msmq”**。  
  
4.  运行示例。  
  
    1.  浏览到 http:\/\/localhost\/private\/durableduplex\/service1.xamlx 和 http:\/\/localhost\/private\/durableduplex\/service2.xamlx 以确保这两个服务正在运行。  
  
    2.  按 F5 运行 DurableDuplexClient。  
  
         在持久双工消息交换完成后时，会将一个 result.xml 文件将保存到 C:\\Inbox 文件夹中，此文件包含消息交换的结果。  
  
#### 清理（可选）  
  
1.  运行 Cleanup.cmd。  
  
    1.  打开 [!INCLUDE[vs2010](../../../../includes/vs2010-md.md)] 命令提示符。  
  
    2.  导航到此示例所在的文件夹并运行 Cleanup.cmd。  
  
2.  移除服务的虚拟应用程序。  
  
    1.  通过从命令提示符运行 `Inetmgr.exe` 打开 Internet 信息服务 \(IIS\) 管理器。  
  
    2.  浏览到默认网站，然后移除 **private** 虚拟目录。  
  
3.  移除为此示例设置的队列。  
  
    1.  通过从命令提示符运行 `Compmgmt.msc` 打开“计算机管理”控制台。  
  
    2.  依次展开**“服务和应用程序”**、**“消息队列”**和**“专用队列”**。  
  
    3.  删除 durableduplex\/service1.xamlx 和 durableduplex\/service2.xamlx 队列。  
  
4.  移除 C:\\Inbox 目录。  
  
> [!IMPORTANT]
>  您的计算机上可能已安装这些示例。在继续操作之前，请先检查以下（默认）目录：  
>   
>  `<安装驱动器>:\WF_WCF_Samples`  
>   
>  如果此目录不存在，请访问[针对 .NET Framework 4 的 Windows Communication Foundation \(WCF\) 和 Windows Workflow Foundation \(WF\) 示例](http://go.microsoft.com/fwlink/?LinkId=150780)（可能为英文网页），下载所有 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 和 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 示例。此示例位于以下目录：  
>   
>  `<安装驱动器>:\WF_WCF_Samples\WF\Basic\Services\DurableDuplex`  
  
## 请参阅