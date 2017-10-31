---
title: "如何：使用 Svcutil.exe 下载元数据文档 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 15524274-3167-4627-b722-d6cedb9fa8c6
caps.latest.revision: 12
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 12
---
# 如何：使用 Svcutil.exe 下载元数据文档
您可以使用 Svcutil.exe 从正在运行的服务中下载元数据并将元数据保存到本地文件。对于 HTTP 和 HTTPS URL 架构，Svcutil.exe 会尝试使用 WS\-MetadataExchange 和 [XML Web 服务发现](http://go.microsoft.com/fwlink/?LinkId=94950)（可能为英文网页）检索元数据。对于所有其他 URL 架构，Svcutil.exe 仅使用 WS\-MetadataExchange。  
  
 默认情况下，Svcutil.exe 使用 <xref:System.ServiceModel.Description.MetadataExchangeBindings> 类中定义的绑定。若要配置用于 WS\-MetadataExchange 的绑定，必须在 Svcutil.exe 的配置文件 \(svcutil.exe.config\) 中定义一个客户端终结点，使该终结点使用 `IMetadataExchange` 约定，并具有与元数据终结点地址的统一资源标识符 \(URI\) 架构相同的名称。  
  
> [!CAUTION]
>  当运行 Svcutil.exe 以获取公开两个不同服务协定（两个服务协定包含具有相同名称的操作）的服务的元数据时，Svcutil.exe 将显示一条错误消息“无法从 .... 获取元数据”。例如，如果有一个服务公开了一个名为 ICarService 的服务协定，该服务协定具有一个 Get\(Car c\) 操作，且同一服务还公开了一个名为 IBookService 的服务协定，该服务协定具有一个 Get\(Book b\) 操作。若要解决此问题，请执行下列操作之一：  
>   
>  -   重命名其中的一项操作  
> -   将 <xref:System.ServiceModel.OperationContractAttribute.Name%2A> 设置为其他名称。  
> -   使用 <xref:System.ServiceModel.ServiceContractAttribute.Namespace%2A> 属性将其中一项操作的命名空间设置为其他命名空间。  
  
### 使用 Svcutil.exe 下载元数据  
  
1.  在以下位置找到 Svcutil.exe 工具：  
  
     C:\\Program Files\\Microsoft SDKs\\Windows\\v1.0.\\bin  
  
2.  在命令提示符处，使用下面的格式启动该工具。  
  
    ```  
    svcutil.exe /t:metadata  <url>* | <epr>  
    ```  
  
     您必须指定 `/t:metadata` 选项才能下载元数据。否则，会生成客户端代码和配置。  
  
3.  \<`url`\>参数指定到提供元数据的服务终结点或到联机承载的元数据文档的 URL。\<`epr`\> 参数指定到 XML 文件的路径，该文件包含支持 WS\-MetadataExchange 的服务终结点的 WS\-Addressing `EndpointAddress`。  
  
 有关使用此工具进行元数据下载的更多选项，请参见 [ServiceModel 元数据实用工具 \(Svcutil.exe\)](../../../../docs/framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md)。  
  
## 示例  
 下面的命令从正在运行的服务中下载元数据文档。  
  
```  
svcutil /t:metadata http://service/metadataEndpoint  
```  
  
## 请参阅  
 [ServiceModel 元数据实用工具 \(Svcutil.exe\)](../../../../docs/framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md)