---
title: "异步活动中的错误处理 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: e8f8ce2b-50c9-4e44-b187-030e0cf30a5d
caps.latest.revision: 3
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 3
---
# 异步活动中的错误处理
通过活动的回调系统提供错误处理在 <xref:System.Activities.AsyncCodeActivity> 涉及路由错误。本主题描述如何获取 SendMail 活动示例回到主机引发的异步操作错误。  
  
## 返回异步活动回主机引发的错误  
 在异步操作回到 SendMail 活动示例中的主机路由错误涉及以下步骤：  
  
-   将 Exception 属性添加到 `SendMailAsyncResult` 类。  
  
-   该属性在 `SendCompleted` 事件处理程序中复制引发的错误。  
  
-   事件处理程序中 `EndExecute` 引发的异常。  
  
 生成代码如下所示。  
  
```csharp  
class SendMailAsyncResult : IAsyncResult  
        {  
            …  
            public Exception Error { get; set; }   
            …  
            void SendCompleted(object sender, AsyncCompletedEventArgs e)  
            {  
                Error = e.Error;  
                this.asyncWaitHandle.Set();  
                callback(this);  
            }  
         }  
  
    public sealed class SendMail: AsyncCodeActivity  
    {  
         …  
        protected override void EndExecute(AsyncCodeActivityContext context, IAsyncResult result)  
        {  
            SendMailAsyncResult sendMailResult = result as SendMailAsyncResult;  
            if (sendMailResult != null && sendMailResult.Error != null)  
                throw sendMailResult.Error;   
        }  
    }  
  
```