---
title: "流处理源示例 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 1f1228c0-daaa-45f0-b93e-c4a158113744
caps.latest.revision: 16
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 16
---
# 流处理源示例
此示例演示如何管理包含大量项的联合源。在服务器上，该示例演示如何在源中延迟创建各个 <xref:System.ServiceModel.Syndication.SyndicationItem> 对象，直至就在将该项写入网络流之前。  
  
 在客户端上，该示例演示如何使用自定义联合源格式化程序来读取网络流中的各个项，以便正在读取的源永远不会完全缓冲到内存中。  
  
 为了最充分地演示联合 API 的流处理功能，此示例使用了一个似乎不可能的方案，在这个方案中，服务器公开一个包含无数个项的源。在这种情况下，服务器继续在源中生成新的项，一直到它认为客户端已从源中读取指定数目（默认为 10）的项为止。为简单起见，客户端和服务器是在同一个进程中实现的，并且使用一个共享 `ItemCounter` 对象跟踪客户端生成的项数。`ItemCounter` 类型存在的唯一目的是为了使示例方案能够完全终止，它并不是所演示的模式的核心元素。  
  
 演示使用了 [!INCLUDE[csprcs](../../../../includes/csprcs-md.md)] 迭代器 （使用 `yield``return` 关键字构造）。[!INCLUDE[crabout](../../../../includes/crabout-md.md)] 迭代器，请参阅"使用迭代器"在 MSDN 上的主题。  
  
## 服务  
 服务实现包含一个操作的基本 <xref:System.ServiceModel.Web.WebGetAttribute> 协定，如下面的代码所示。  
  
```  
[ServiceContract]  
interface IStreamingFeedService  
{  
    [WebGet]  
    [OperationContract]  
    Atom10FeedFormatter StreamedFeed();  
}  
  
```  
  
 服务通过使用 `ItemGenerator` 类创建一个可能无限的 <xref:System.ServiceModel.Syndication.SyndicationItem> 实例流（使用迭代器）来实现此协定，如下面的代码所示。  
  
```  
class ItemGenerator  
{  
    public IEnumerable<SyndicationItem> GenerateItems()  
    {  
        while (counter.GetCount() < maxItemsRead)  
        {  
            itemsReturned++;  
            yield return CreateNextItem();  
        }  
  
    }  
    ...  
}  
  
```  
  
 当服务实现创建源时，使用 `ItemGenerator.GenerateItems()` 的输出，而不是使用缓冲的项集合。  
  
```  
public Atom10FeedFormatter StreamedFeed()  
{  
    SyndicationFeed feed = new SyndicationFeed("Streamed feed", "Feed to test streaming", null);  
    //Generate an infinite stream of items. Both the client and the service share  
    //a reference to the ItemCounter, which allows the sample to terminate  
    //execution after the client has read 10 items from the stream  
    ItemGenerator itemGenerator = new ItemGenerator(this.counter, 10);  
  
    feed.Items = itemGenerator.GenerateItems();  
    return feed.GetAtom10Formatter();  
}  
  
```  
  
 因此，项流永远不会完全缓冲到内存中。通过在 `ItemGenerator.GenerateItems()` 方法内的 `yield``return` 语句中设置一个断点，并注意此断点是服务在返回 `StreamedFeed()` 方法的结果后第一次遇到，可以观察到此行为。  
  
## 客户端  
 此示例中的客户端使用自定义 <xref:System.ServiceModel.Syndication.SyndicationFeedFormatter> 实现，该实现延迟各个项在源中的具体化，而不是将它们缓冲到内存中。自定义 `StreamedAtom10FeedFormatter` 实例的使用如下所示。  
  
```  
XmlReader reader = XmlReader.Create("http://localhost:8000/Service/Feeds/StreamedFeed");  
StreamedAtom10FeedFormatter formatter = new StreamedAtom10FeedFormatter(counter);  
  
SyndicationFeed feed = formatter.ReadFrom(reader);  
  
```  
  
 通常，在从网络中读取源的全部内容并将内容缓冲到内存中之前，并不会返回对 <xref:System.ServiceModel.Syndication.SyndicationFeedFormatter.ReadFrom%28System.Xml.XmlReader%29> 的调用。但是，`StreamedAtom10FeedFormatter` 对象重写了 <xref:System.ServiceModel.Syndication.Atom10FeedFormatter.ReadItems%28System.Xml.XmlReader%2CSystem.ServiceModel.Syndication.SyndicationFeed%2CSystem.Boolean%40%29> 以返回迭代器，而不是返回缓冲的集合，如下面的代码所示。  
  
```  
protected override IEnumerable<SyndicationItem> ReadItems(XmlReader reader, SyndicationFeed feed, out bool areAllItemsRead)  
{  
    areAllItemsRead = false;  
    return DelayReadItems(reader, feed);  
}  
  
private IEnumerable<SyndicationItem> DelayReadItems(XmlReader reader, SyndicationFeed feed)  
{  
    while (reader.IsStartElement("entry", "http://www.w3.org/2005/Atom"))  
    {  
        yield return this.ReadItem(reader, feed);  
    }  
  
    reader.ReadEndElement();  
}  
  
```  
  
 因此，在遍历 `ReadItems()` 结果的客户端应用程序准备好使用每个项之前，并不会从网络中读取每个项。通过在 `StreamedAtom10FeedFormatter.DelayReadItems()` 内的 `yield``return` 语句中设置一个断点，并注意此断点是对 `ReadFrom()` 的调用完成后第一次遇到，可以观察到此行为。  
  
 下面的说明演示如何生成并运行示例。请注意，尽管服务器在客户端读取 10 个项后停止生成项，但输出显示客户端读取的项数远远超过 10 个。这是因为示例使用的网络绑定以 4 KB 段传输数据。因此，客户端在有机会读取一个项之前，已收到 4KB 的项数据。这是正常的行为（以合理大小的段发送经过流处理的 HTTP 数据可以提高性能）。  
  
#### 设置、生成和运行示例  
  
1.  请确保已经执行了 [Windows Communication Foundation 示例的一次性安装过程](../../../../docs/framework/wcf/samples/one-time-setup-procedure-for-the-wcf-samples.md)。  
  
2.  若要生成 C\# 或 Visual Basic .NET 版本的解决方案，请按照[生成 Windows Communication Foundation 示例](../../../../docs/framework/wcf/samples/building-the-samples.md)中的说明进行操作。  
  
3.  若要用单机配置或跨计算机配置来运行示例，请按照[运行 Windows Communication Foundation 示例](../../../../docs/framework/wcf/samples/running-the-samples.md)中的说明进行操作。  
  
> [!IMPORTANT]
>  您的计算机上可能已安装这些示例。在继续操作之前，请先检查以下（默认）目录：  
>   
>  `<安装驱动器>:\WF_WCF_Samples`  
>   
>  如果此目录不存在，请访问[针对 .NET Framework 4 的 Windows Communication Foundation \(WCF\) 和 Windows Workflow Foundation \(WF\) 示例](http://go.microsoft.com/fwlink/?LinkId=150780)（可能为英文网页），下载所有 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 和 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 示例。此示例位于以下目录：  
>   
>  `<安装驱动器>:\WF_WCF_Samples\WCF\Extensibility\Syndication\StreamingFeeds`  
  
## 请参阅  
 [独立诊断源](../../../../docs/framework/wcf/samples/stand-alone-diagnostics-feed-sample.md)