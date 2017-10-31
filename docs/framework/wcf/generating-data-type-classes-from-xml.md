---
title: "从 XML 生成数据类型类 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: e4e5e4e8-527f-44d1-92fa-8904a08784ea
caps.latest.revision: 5
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 5
---
# 从 XML 生成数据类型类
[!INCLUDE[net_v45](../../../includes/net-v45-md.md)] 包括用于从 XML 生成数据类型类的新功能。  本主题介绍如何为 MSDN 库 RSS 源自动生成数据类型。  
  
### 从 MSDN 库 RSS 源获取 XML  
  
1.  在 Internet Explorer 中，导航到 [MSDN RSS 源](http://go.microsoft.com/fwlink/?LinkId=225209)（可能为英文网页）。  
  
2.  右击该页，然后选择**“查看源”**。  
  
3.  通过按 **Ctrl\+A** 选择所有文本，然后按 **Ctrl\+C** 复制所选文本，复制源的文本。  
  
### 创建数据类型  
  
1.  打开要使用代理的代码文件。  此文件应为 [!INCLUDE[net_v45](../../../includes/net-v45-md.md)] 项目的一部分。  
  
2.  将游标放置于该文件中任何现有类之外的位置中。  
  
3.  选择**“编辑”**、**“选择性粘贴”**、**“将 XML 作为类粘贴”**。  
  
4.  使用所需成员创建调用 `rss`、`rssChannel`、`rssChannelImage` 和 `rssChannelItem` 的类，以便访问 RSS 源中的元素。  
  
### 使用生成的类  
  
1.  一旦生成了类，这些类就可以像任何其他类一样在代码中使用。  下面的代码示例返回 `rssChannelImage` 类的新实例。  
  
    ```  
    var channelImage = new rssChannelImage()   
    {   
        title = "MyImage",   
        link = "http://www.contoso.com/images/channelImage.jpg",   
        url = "http://www.contoso.com/entries/myEntry.html"   
    };  
  
    ```