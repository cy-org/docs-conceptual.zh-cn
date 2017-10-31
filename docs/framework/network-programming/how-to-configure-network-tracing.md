---
title: "如何：配置网络跟踪"
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
- formatting [.NET Framework], network tracing
- network tracing, configuring
- level attribute
- app.config files, network tracing
- configuration files [.NET Framework], network tracing
- protocol-level trace output
- application configuration files, network tracing
- sockets, trace output
ms.assetid: 5ef9fe4b-8d3d-490e-9259-1d014b2181af
caps.latest.revision: 23
author: mcleblanc
ms.author: markl
manager: markl
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: 3a713b9b2d76d6198d035226aaa55be7345b87f1
ms.contentlocale: zh-cn
ms.lasthandoff: 08/21/2017

---
# <a name="how-to-configure-network-tracing"></a>如何：配置网络跟踪
应用程序或计算机配置文件可保存用于确定网络跟踪的格式和内容的设置。 在执行此过程之前，请确保启用跟踪。 有关如何启用跟踪的信息，请参阅[启用网络跟踪](../../../docs/framework/network-programming/enabling-network-tracing.md)。  
  
 计算机配置文件 machine.config 存储在 Windows 安装目录的 %Windir%\Microsoft.NET\Framework 文件夹中。 对于在计算机上安装的每个 .NET Framework 版本，%Windir%\Microsoft.NET\Framework 下的文件夹中分别有一个单独的 machine.config 文件（例如，C:\WINDOWS\Microsoft.NET\Framework\v2.0.50727\machine.config）。  
  
 也可以在应用程序的配置文件中做出这些设置，其优先级别高于计算机配置文件。  
  
### <a name="to-configure-network-tracing"></a>配置网络跟踪  
  
-   将下面的代码行添加到相应的配置文件。 这些设置的值和选项已在下表中予以说明。  
  
    ```xml  
    <configuration>  
      <system.diagnostics>  
        <sources>  
          <source name="System.Net" tracemode="includehex" maxdatasize="1024">  
            <listeners>  
              <add name="System.Net"/>  
            </listeners>  
          </source>  
          <source name="System.Net.Cache">  
            <listeners>  
              <add name="System.Net"/>  
            </listeners>  
          </source>  
          <source name="System.Net.Http">  
            <listeners>  
              <add name="System.Net"/>  
            </listeners>  
          </source>  
          <source name="System.Net.Sockets">  
            <listeners>  
              <add name="System.Net"/>  
            </listeners>  
          </source>  
          <source name="System.Net.WebSockets">  
            <listeners>  
              <add name="System.Net"/>  
            </listeners>  
          </source>  
        </sources>  
        <switches>  
          <add name="System.Net" value="Verbose"/>  
          <add name="System.Net.Cache" value="Verbose"/>  
          <add name="System.Net.Http" value="Verbose"/>  
          <add name="System.Net.Sockets" value="Verbose"/>  
          <add name="System.Net.WebSockets" value="Verbose"/>  
        </switches>  
        <sharedListeners>  
          <add name="System.Net"  
            type="System.Diagnostics.TextWriterTraceListener"  
            initializeData="network.log"  
          />  
        </sharedListeners>  
        <trace autoflush="true"/>  
      </system.diagnostics>  
    </configuration>  
    ```  
  
 当你将一个名称添加到 `<switches>` 块后，跟踪输出中将包括来自与该名称相关的一些方法的信息。 下表对输出进行了说明。  
  
|名称|输出来自|  
|----------|-----------------|  
|`System.Net.Sockets`|<xref:System.Net.Sockets.Socket>、<xref:System.Net.Sockets.TcpListener>、<xref:System.Net.Sockets.TcpClient> 和 <xref:System.Net.Dns> 类的一些公共方法|  
|`System.Net`|<xref:System.Net.HttpWebRequest>、<xref:System.Net.HttpWebResponse>、<xref:System.Net.FtpWebRequest> 和 <xref:System.Net.FtpWebResponse> 类的一些公共方法，以及 SSL 调试信息（证书无效、缺少颁发机构列表以及客户端证书错误）。|  
|`System.Net.HttpListener`|<xref:System.Net.HttpListener>、<xref:System.Net.HttpListenerRequest> 和 <xref:System.Net.HttpListenerResponse> 类的一些公共方法。|  
|`System.Net.Cache`|`System.Net.Cache` 中的一些私有方法和内部方法。|  
|`System.Net.Http`|<xref:System.Net.Http.HttpClient>、<xref:System.Net.Http.DelegatingHandler>、<xref:System.Net.Http.HttpClientHandler>、<xref:System.Net.Http.HttpMessageHandler>、<xref:System.Net.Http.MessageProcessingHandler> 和 <xref:System.Net.Http.WebRequestHandler> 类的一些公共方法。|  
|`System.Net.WebSockets.WebSocket`|<xref:System.Net.WebSockets.ClientWebSocket> 和 <xref:System.Net.WebSockets.WebSocket> 类的一些公共方法。|  
  
 下表中列出的特性用于配置跟踪输出。  
  
|特性名|特性值|  
|--------------------|---------------------|  
|`Value`|必选的 <xref:System.String> 特性。 设置输出的详细程度。 合法值为 `Critical`、`Error`、`Verbose`、`Warning` 和 `Information`。<br /><br /> 如此示例所示，此特性必须在 \<switches> 元素的 \<add name> 元素上进行设置。 如果此特性是在 \<source> 元素上设置的，则会引发异常。|  
|`maxdatasize`|可选的 <xref:System.Int32> 特性。 设置每行跟踪中包含的最大网络数据字节数。 默认值为 1024。<br /><br /> 如此示例所示，此特性必须在 \<source> 元素上进行设置。 如果此特性是在 \<switches> 元素下的一个元素上设置的，则会引发异常。|  
|`Tracemode`|可选的 <xref:System.String> 特性。 设置为 `includehex` 将会以十六进制和文本格式显示协议跟踪。 设置为 `protocolonly` 将会仅显示文本。 默认值为 `includehex`。<br /><br /> 如此示例所示，此特性必须在 \<switches> 元素上进行设置。 如果此特性是在 \<source> 元素下的一个元素上设置的，则会引发异常。|  
  
## <a name="see-also"></a>另请参阅  
 [解释网络跟踪](../../../docs/framework/network-programming/interpreting-network-tracing.md)   
 [.NET Framework 中的网络跟踪](../../../docs/framework/network-programming/network-tracing.md)   
 [启用网络跟踪](../../../docs/framework/network-programming/enabling-network-tracing.md)   
 [检测和跟踪简介](http://msdn.microsoft.com/en-us/e924e57c-33cf-4b0e-9e7f-a45d13e38f2c)

