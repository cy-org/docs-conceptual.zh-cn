---
title: "MTOM 编码 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 820e316f-4ee1-4eb5-ae38-b6a536e8a14f
caps.latest.revision: 14
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 14
---
# MTOM 编码
此示例演示如何将消息传输优化机制 \(MTOM\) 消息编码与 WSHttpBinding 一起使用。MTOM 是一种机制，用来以原始字节形式传输包含 SOAP 消息的较大二进制附件，从而使所传输的消息较小。  
  
> [!IMPORTANT]
>  您的计算机上可能已安装这些示例。在继续操作之前，请先检查以下（默认）目录。  
>   
>  `<安装驱动器>:\WF_WCF_Samples`  
>   
>  如果此目录不存在，请访问[针对 .NET Framework 4 的 Windows Communication Foundation \(WCF\) 和 Windows Workflow Foundation \(WF\) 示例](http://go.microsoft.com/fwlink/?LinkId=150780)（可能为英文网页），下载所有 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 和 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 示例。此示例位于以下目录：  
>   
>  `<安装驱动器>:\WF_WCF_Samples\WCF\Basic\Binding\WS\MTOM`  
  
 默认情况下，WSHttpBinding 以正常文本 XML 形式发送和接收消息。若要允许发送和接收 MTOM 消息，请在绑定的配置中设置 `messageEncoding` 属性 \(Attribute\)（如下面的示例代码中所示），或者使用 `MessageEncoding` 属性 \(Property\) 直接在绑定中进行设置。服务或客户端现在可以发送和接收 MTOM 消息了。  
  
```  
<wsHttpBinding>  
    <binding name="WSHttpBinding_IUpload" messageEncoding="Mtom"/>  
</wsHttpBinding>  
```  
  
 MTOM 编码器可以优化字节和流的数组。在下面的示例中，操作使用 `Stream` 参数，因此可以进行优化。  
  
```  
[ServiceContract(Namespace="http://Microsoft.ServiceModel.Samples")]  
  public interface IUpload  
  {  
      [OperationContract]  
      int Upload(Stream data);  
  }  
```  
  
 为该示例选择的协定会将二进制数据传输到服务，并将上载的字节数作为返回值接收。在安装服务之后运行客户端时，服务会显示数字 1000，这表示收到了全部 1000 个字节。剩下的输出列出了在各种负载情况下经过优化和未经优化的消息大小。  
  
```  
Output:  
1000  
  
Text encoding with a 100 byte payload: 433  
MTOM encoding with a 100 byte payload: 912  
  
Text encoding with a 1000 byte payload: 1633  
MTOM encoding with a 1000 byte payload: 2080  
  
Text encoding with a 10000 byte payload: 13633  
MTOM encoding with a 10000 byte payload: 11080  
  
Text encoding with a 100000 byte payload: 133633  
MTOM encoding with a 100000 byte payload: 101080  
  
Text encoding with a 1000000 byte payload: 1333633  
MTOM encoding with a 1000000 byte payload: 1001080  
  
Press <ENTER> to terminate client.  
```  
  
 使用 MTOM 的目的在于优化对较大的二进制负载的传输。对于较小的二进制负载来说，使用 MTOM 发送 SOAP 消息会产生显著的开销，但是，当这些负载增大到几千个字节时，该开销会变得微不足道。原因在于，正常文本 XML 使用 Base64 对二进制数据进行编码，这要求每三个字节对应四个字符，从而使得数据的大小增加三分之一。MTOM 能够以原始字节形式传输二进制数据，这会缩短编码\/解码时间并生成较小的消息。与当今的业务文档和数字照片相比，几千个字节的阈值是非常小的。  
  
### 设置、生成和运行示例  
  
1.  使用以下命令安装 [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)] 4.0。  
  
    ```  
    %windir%\Microsoft.NET\Framework\v4.0.XXXXX\aspnet_regiis.exe /i /enable  
  
    ```  
  
2.  请确保已执行 [Windows Communication Foundation 示例的一次性安装过程](../../../../docs/framework/wcf/samples/one-time-setup-procedure-for-the-wcf-samples.md)。  
  
3.  若要生成 C\# 或 Visual Basic .NET 版本的解决方案，请按照[生成 Windows Communication Foundation 示例](../../../../docs/framework/wcf/samples/building-the-samples.md)中的说明进行操作。  
  
4.  若要用单机配置或跨计算机配置来运行示例，请按照[运行 Windows Communication Foundation 示例](../../../../docs/framework/wcf/samples/running-the-samples.md)中的说明进行操作。  
  
## 请参阅