---
title: "自定义消息编码器：自定义文本编码器 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 68ff5c74-3d33-4b44-bcae-e1d2f5dea0de
caps.latest.revision: 28
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 28
---
# 自定义消息编码器：自定义文本编码器
本示例演示如何使用 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 实现自定义文本消息编码器。  
  
> [!WARNING]
>  您的计算机上可能已安装这些示例。在继续操作之前，请先检查以下（默认）目录。  
>   
>  `<安装驱动器>:\WF_WCF_Samples`  
>   
>  如果此目录不存在，请访问[针对 .NET Framework 4 的 Windows Communication Foundation \(WCF\) 和 Windows Workflow Foundation \(WF\) 示例](http://go.microsoft.com/fwlink/?LinkId=150780)（可能为英文网页），下载所有 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 和 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 示例。此示例位于以下目录。  
>   
>  `<安装驱动器>:\WF_WCF_Samples\WCF\Extensibility\MessageEncoder\Text`  
  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 的 <xref:System.ServiceModel.Channels.TextMessageEncodingBindingElement> 仅支持 UTF\-8、UTF\-16 和 Big Endean Unicode 编码。本示例中的自定义文本消息编码器支持所有平台支持的字符编码，这可能是互操作性所要求的。本示例包括客户端控制台程序 \(.exe\)、Internet 信息服务 \(IIS\) 承载的服务库 \(.dll\) 和文本消息编码器库 \(.dll\)。该服务实现定义“请求\-答复”通信模式的协定。该协定由 `ICalculator` 接口定义，此接口公开数学运算（加、减、乘和除）。客户端向给定的数学运算发出同步请求，服务使用结果进行回复。客户端和服务都使用 `CustomTextMessageEncoder`，而不是使用默认的 <xref:System.ServiceModel.Channels.TextMessageEncodingBindingElement>。  
  
 自定义编码器实现由消息编码器工厂、消息编码器、消息编码绑定元素和配置处理程序组成，演示如下：  
  
-   生成自定义编码器和编码器工厂。  
  
-   为自定义编码器创建绑定元素。  
  
-   使用自定义绑定配置集成自定义绑定元素。  
  
-   开发自定义配置处理程序以允许对自定义绑定元素进行文件配置。  
  
### 设置、生成和运行示例  
  
1.  使用以下命令安装 [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)] 4.0。  
  
    ```  
    %windir%\Microsoft.NET\Framework\v4.0.XXXXX\aspnet_regiis.exe /i /enable  
  
    ```  
  
2.  请确保已执行 [Windows Communication Foundation 示例的一次性安装过程](../../../../docs/framework/wcf/samples/one-time-setup-procedure-for-the-wcf-samples.md)。  
  
3.  若要生成解决方案，请按照[生成 Windows Communication Foundation 示例](../../../../docs/framework/wcf/samples/building-the-samples.md)中的说明进行操作。  
  
4.  若要用单机配置或跨计算机配置来运行示例，请按照[运行 Windows Communication Foundation 示例](../../../../docs/framework/wcf/samples/running-the-samples.md)中的说明进行操作。  
  
## 消息编码器工厂和消息编码器  
 当 <xref:System.ServiceModel.ServiceHost> 或客户端通道打开时，设计时组件 `CustomTextMessageBindingElement` 可创建 `CustomTextMessageEncoderFactory`。该工厂创建 `CustomTextMessageEncoder`。消息编码器运行在流模式和缓冲模式中。它分别使用 <xref:System.Xml.XmlReader> 和 <xref:System.Xml.XmlWriter> 读写消息。相对于仅支持 UTF\-8、UTF\-16 和 Big\-Endean Unicode 的 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] XML 读取器和编写器，这些读取器和编写器支持所有平台支持的编码。  
  
 下面的代码示例演示 CustomTextMessageEncoder。  
  
```csharp  
  
public class CustomTextMessageEncoder : MessageEncoder  
{  
    private CustomTextMessageEncoderFactory factory;  
    private XmlWriterSettings writerSettings;  
    private string contentType;  
  
    public CustomTextMessageEncoder(CustomTextMessageEncoderFactory factory)  
    {  
        this.factory = factory;  
  
        this.writerSettings = new XmlWriterSettings();  
        this.writerSettings.Encoding = Encoding.GetEncoding(factory.CharSet);  
        this.contentType = string.Format("{0}; charset={1}",   
            this.factory.MediaType, this.writerSettings.Encoding.HeaderName);  
    }  
  
    public override string ContentType  
    {  
        get  
        {  
            return this.contentType;  
        }  
    }  
  
    public override string MediaType  
    {  
        get   
        {  
            return factory.MediaType;  
        }  
    }  
  
    public override MessageVersion MessageVersion  
    {  
        get   
        {  
            return this.factory.MessageVersion;  
        }  
    }  
  
    public override Message ReadMessage(ArraySegment<byte> buffer, BufferManager bufferManager, string contentType)  
    {     
        byte[] msgContents = new byte[buffer.Count];  
        Array.Copy(buffer.Array, buffer.Offset, msgContents, 0, msgContents.Length);  
        bufferManager.ReturnBuffer(buffer.Array);  
  
        MemoryStream stream = new MemoryStream(msgContents);  
        return ReadMessage(stream, int.MaxValue);  
    }  
  
    public override Message ReadMessage(Stream stream, int maxSizeOfHeaders, string contentType)  
    {  
        XmlReader reader = XmlReader.Create(stream);  
        return Message.CreateMessage(reader, maxSizeOfHeaders, this.MessageVersion);  
    }  
  
    public override ArraySegment<byte> WriteMessage(Message message, int maxMessageSize, BufferManager bufferManager, int messageOffset)  
    {  
        MemoryStream stream = new MemoryStream();  
        XmlWriter writer = XmlWriter.Create(stream, this.writerSettings);  
        message.WriteMessage(writer);  
        writer.Close();  
  
        byte[] messageBytes = stream.GetBuffer();  
        int messageLength = (int)stream.Position;  
        stream.Close();  
  
        int totalLength = messageLength + messageOffset;  
        byte[] totalBytes = bufferManager.TakeBuffer(totalLength);  
        Array.Copy(messageBytes, 0, totalBytes, messageOffset, messageLength);  
  
        ArraySegment<byte> byteArray = new ArraySegment<byte>(totalBytes, messageOffset, messageLength);  
        return byteArray;  
    }  
  
    public override void WriteMessage(Message message, Stream stream)  
    {  
        XmlWriter writer = XmlWriter.Create(stream, this.writerSettings);  
        message.WriteMessage(writer);  
        writer.Close();  
    }  
}  
```  
  
 下面的代码示例演示如何生成消息编码器工厂。  
  
```csharp  
public class CustomTextMessageEncoderFactory : MessageEncoderFactory  
{  
    private MessageEncoder encoder;  
    private MessageVersion version;  
    private string mediaType;  
    private string charSet;  
  
    internal CustomTextMessageEncoderFactory(string mediaType, string charSet,  
        MessageVersion version)  
    {  
        this.version = version;  
        this.mediaType = mediaType;  
        this.charSet = charSet;  
        this.encoder = new CustomTextMessageEncoder(this);  
    }  
  
    public override MessageEncoder Encoder  
    {  
        get   
        {   
            return this.encoder;  
        }  
    }  
  
    public override MessageVersion MessageVersion  
    {  
        get   
        {   
            return this.version;  
        }  
    }  
  
    internal string MediaType  
    {  
        get  
        {  
            return this.mediaType;  
        }  
    }  
  
    internal string CharSet  
    {  
        get  
        {  
            return this.charSet;  
        }  
    }  
}  
```  
  
## 消息编码绑定元素  
 绑定元素允许配置 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 运行时堆栈。若要在 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 应用程序中使用自定义消息编码器，则需要一个绑定元素，该元素在运行时堆栈中的相应级别使用相应的设置创建消息编码器工厂。  
  
 `CustomTextMessageBindingElement` 从 <xref:System.ServiceModel.Channels.BindingElement> 基类派生并从 <xref:System.ServiceModel.Channels.MessageEncodingBindingElement> 类继承。这允许其他 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 组件将此绑定元素识别为消息编码绑定元素。<xref:System.ServiceModel.Channels.MessageEncodingBindingElement.CreateMessageEncoderFactory%2A> 的实现返回与相应设置匹配的消息编码器工厂的实例。  
  
 `CustomTextMessageBindingElement` 通过属性公开 `MessageVersion`、`ContentType` 和 `Encoding` 的设置。编码器支持 Soap11Addressing 和 Soap12Addressing1 版本。默认值为 Soap11Addressing1。`ContentType` 的默认值为“text\/xml”。使用 `Encoding` 属性可以将该值设置为所需的字符编码。示例客户端和服务使用 ISO\-8859\-1 \(Latin1\) 字符编码，[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 的 <xref:System.ServiceModel.Channels.TextMessageEncodingBindingElement> 不支持该编码。  
  
 下面的代码演示如何使用自定义文本消息编码器以编程方式创建绑定。  
  
```  
ICollection<BindingElement> bindingElements = new List<BindingElement>();  
HttpTransportBindingElement httpBindingElement = new HttpTransportBindingElement();  
CustomTextMessageBindingElement textBindingElement = new CustomTextMessageBindingElement();  
bindingElements.Add(textBindingElement);  
bindingElements.Add(httpBindingElement);  
CustomBinding binding = new CustomBinding(bindingElements);  
```  
  
## 将元数据支持添加到消息编码绑定元素  
 从 <xref:System.ServiceModel.Channels.MessageEncodingBindingElement> 派生的任何类型负责更新为服务生成的 WSDL 文档中 SOAP 绑定的版本。这是通过实现 <xref:System.ServiceModel.Description.IWsdlExportExtension> 接口上的 `ExportEndpoint` 方法，然后修改生成的 WSDL 来实现的。在本示例中，`CustomTextMessageBindingElement` 使用来自 `TextMessageEncodingBinidngElement` 的 WSDL 导出逻辑。  
  
 对于本示例，客户端配置是手动配置的。无法使用 Svcutil.exe 生成客户端配置，因为 `CustomTextMessageBindingElement` 未导出策略断言来描述其行为。通常应该实现自定义绑定元素上的 <xref:System.ServiceModel.Description.IPolicyExportExtension> 接口，以导出描述绑定元素实现的行为或功能的自定义策略断言。有关如何导出自定义绑定元素的策略断言的示例，请参见[传输：UDP](../../../../docs/framework/wcf/samples/transport-udp.md) 示例。  
  
## 消息编码绑定配置处理程序  
 上一节演示如何以编程方式使用自定义文本消息编码器。`CustomTextMessageEncodingBindingSection` 实现配置处理程序，使用该程序可以在配置文件中指定自定义文本消息编码器的用法。`CustomTextMessageEncodingBindingSection` 类是从 <xref:System.ServiceModel.Configuration.BindingElementExtensionElement> 类派生的。`BindingElementType` 属性通知配置系统要为此节创建的绑定元素的类型。  
  
 由 `CustomTextMessageBindingElement` 定义的所有设置作为 `CustomTextMessageEncodingBindingSection` 中的属性公开。<xref:System.Configuration.ConfigurationPropertyAttribute> 有助于将配置元素属性映射到属性并在未设置属性的情况下设置默认值。在配置中的值加载并应用到该类型的属性之后，将调用 <xref:System.ServiceModel.Configuration.BindingElementExtensionElement.CreateBindingElement%2A> 方法，该方法将属性转换成绑定元素的具体实例。  
  
 此配置处理程序映射到服务或客户端的 App.config 或 Web.config 中的以下表示形式。  
  
```  
<customTextMessageEncoding encoding="utf-8" contentType="text/xml" messageVersion="Soap11Addressing1" />  
  
```  
  
 本示例使用 ISO\-8859\-1 编码。  
  
 若要使用此配置处理程序，它必须使用下面的配置元素注册。  
  
```  
<extensions>  
    <bindingElementExtensions>  
        <add name="customTextMessageEncoding" type="   
Microsoft.ServiceModel.Samples.CustomTextMessageEncodingBindingSection,   
                  CustomTextMessageEncoder" />  
    </bindingElementExtensions>  
</extensions>  
  
```  
  
## 请参阅