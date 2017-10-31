---
title: "使用复杂类型的 AJAX 服务示例 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 88242b99-4811-4cbe-8201-52ddf48fb174
caps.latest.revision: 16
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 16
---
# 使用复杂类型的 AJAX 服务示例
此示例演示如何使用 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 来创建 ASP.NET 异步 JavaScript 和 XML \(AJAX\) 服务，此服务创建复杂类型的实例并将这些实例作为 JavaScript 对象表示法 \(JSON\) 在服务和客户端之间发送。可以从 Web 浏览器客户端使用 JavaScript 代码来访问 AJAX 服务。此示例是基于[基本 AJAX 服务](../../../../docs/framework/wcf/samples/basic-ajax-service.md)示例生成的。  
  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 中对 AJAX 的支持经过了优化，以便可以通过 <xref:System.Web.UI.ScriptManager> 控件与 ASP.NET AJAX 一起使用。有关将 ASP.NET AJAX 与 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 一起使用的示例，请参见 [AJAX Samples](http://msdn.microsoft.com/zh-cn/f3fa45b3-44d5-4926-8cc4-a13c30a3bf3e)。  
  
> [!NOTE]
>  本主题的末尾介绍了此示例的设置过程和生成说明。  
  
 以下示例中的服务是不包含 AJAX 特定代码的 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 服务。由于未应用 <xref:System.ServiceModel.Web.WebGetAttribute> 属性，因此将使用默认的 HTTP 谓词（“POST”）。该服务有一个操作 `DoMath`，该操作返回一个名为 `MathResult` 的复杂类型。该复杂类型是标准的数据协定类型，也不包含特定于 AJAX 的代码。  
  
```  
[DataContract]  
    public class MathResult  
    {  
        [DataMember]  
        public double sum;  
        [DataMember]  
        public double difference;  
        [DataMember]  
        public double product;  
        [DataMember]  
        public double quotient;  
    }  
```  
  
 通过使用 <xref:System.ServiceModel.Activation.WebScriptServiceHostFactory> 在服务上创建 AJAX 终结点，就像在基本 AJAX 服务示例中一样。  
  
 客户端网页 ComplexTypeClientPage.aspx 包含 ASP.NET 和 JavaScript 代码，当用户在页面上单击**“Perform calculation”（执行计算）**按钮时，该代码会调用相应的服务。这个用来调用服务的代码会构造 JSON 正文并使用 HTTP POST 发送它，这与[使用 HTTP POST 的 AJAX 服务](../../../../docs/framework/wcf/samples/ajax-service-using-http-post.md)示例相似。  
  
 在服务调用成功之后，您可以在所得到的 JavaScript 对象上访问各个数据成员（`sum`、`difference`、`product` 和 `quotient`）。  
  
```  
function onSuccess(mathResult){  
     document.getElementById("sum").value = mathResult.sum;  
     document.getElementById("difference").value = mathResult.difference;  
     document.getElementById("product").value = mathResult.product;  
     document.getElementById("quotient").value = mathResult.quotient;  
}  
  
```  
  
### 设置、生成和运行示例  
  
1.  请确保已经执行了 [Windows Communication Foundation 示例的一次性安装过程](../../../../docs/framework/wcf/samples/one-time-setup-procedure-for-the-wcf-samples.md)。  
  
2.  按照[生成 Windows Communication Foundation 示例](../../../../docs/framework/wcf/samples/building-the-samples.md)中的说明生成解决方案 ComplexTypeAjaxService.sln。  
  
3.  定位到 http:\/\/localhost\/ServiceModelSamples\/ComplexTypeClientPage.aspx（不要在浏览器中从项目目录中打开 ComplexTypeClientPage.aspx）。  
  
> [!IMPORTANT]
>  您的计算机上可能已安装这些示例。在继续操作之前，请先检查以下（默认）目录。  
>   
>  `<安装驱动器>:\WF_WCF_Samples`  
>   
>  如果此目录不存在，请访问[针对 .NET Framework 4 的 Windows Communication Foundation \(WCF\) 和 Windows Workflow Foundation \(WF\) 示例](http://go.microsoft.com/fwlink/?LinkId=150780)（可能为英文网页），下载所有 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 和 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 示例。此示例位于以下目录：  
>   
>  `<安装驱动器>:\WF_WCF_Samples\WCF\Basic\Ajax\ComplexTypeAjaxService`  
  
## 请参阅  
 [基本 AJAX 服务](../../../../docs/framework/wcf/samples/basic-ajax-service.md)