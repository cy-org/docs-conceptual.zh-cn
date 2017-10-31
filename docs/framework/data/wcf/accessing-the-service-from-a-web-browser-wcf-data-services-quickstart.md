---
title: "从 Web 浏览器访问服务（WCF 数据服务快速入门） | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-oob"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 5a6fa180-3094-4e6e-ba2b-8c80975d18d1
caps.latest.revision: 4
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 4
---
# 从 Web 浏览器访问服务（WCF 数据服务快速入门）
在此任务中，您将从 [!INCLUDE[vs_current_short](../../../../includes/vs-current-short-md.md)] 启动 [!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)]，然后可以选择在 Web 浏览器中禁用源读取。  然后，通过 Web 浏览器将 HTTP GET 请求提交给公开的资源，进而检索服务定义文档以及访问数据服务资源。  
  
> [!NOTE]
>  默认情况下，[!INCLUDE[vs_current_short](../../../../includes/vs-current-short-md.md)] 自动为计算机上的 `localhost` URI 分配一个端口号。  本任务在 URI 示例中使用端口号 `12345`。  [!INCLUDE[crabout](../../../../includes/crabout-md.md)]如何在 [!INCLUDE[vs_current_short](../../../../includes/vs-current-short-md.md)] 项目中设置特定端口号的更多信息，请参见[创建数据服务](../../../../docs/framework/data/wcf/creating-the-data-service.md)。  
  
### 使用 Internet Explorer 请求默认服务文档  
  
1.  在 Internet Explorer 的**“工具”**菜单中，选择**“Internet 选项”**，依次单击**“内容”**选项卡、**“设置”**，然后清除**“打开源阅读视图”**。  
  
     这可确保禁用源阅读。  如果未禁用此功能，则 Web 浏览器会将返回的 AtomPub 编码文档视为 XML 源，而不是显示原始 XML 数据。  
  
    > [!NOTE]
    >  当浏览器无法将该源作为原始 XML 数据显示时，您应该仍能够以页面源代码的形式查看该源。  
  
2.  在 [!INCLUDE[vs_current_short](../../../../includes/vs-current-short-md.md)] 中，按 F5 键以开始调试应用程序。  
  
3.  在本地计算机上打开 Web 浏览器。  在地址栏中，输入以下 URI：  
  
    ```  
    http://localhost:12345/northwind.svc  
    ```  
  
     这会返回默认服务文档，其中包含由此数据服务公开的实体集的列表。  
  
### 从 Web 浏览器访问实体集资源  
  
1.  在 Web 浏览器的地址栏中，输入以下 URI：  
  
    ```  
    http://localhost:12345/northwind.svc/Customers  
    ```  
  
     这会返回 Northwind 示例数据库中所有客户的集。  
  
2.  在 Web 浏览器的地址栏中，输入以下 URI：  
  
    ```  
    http://localhost:12345/northwind.svc/Customers('ALFKI')  
    ```  
  
     这会返回特定客户 `ALFKI` 的实体实例。  
  
3.  在 Web 浏览器的地址栏中，输入以下 URI：  
  
    ```  
    http://localhost:12345/northwind.svc/Customers('ALFKI')/Orders  
    ```  
  
     这会遍历客户与订单之间的关系，以返回特定客户 `ALFKI` 的所有订单的集。  
  
4.  在 Web 浏览器的地址栏中，输入以下 URI：  
  
    ```  
    http://localhost:12345/northwind.svc/Customers('ALFKI')/Orders?$filter=OrderID eq 10643  
    ```  
  
     这会筛选属于特定客户 `ALFKI` 的订单，以便只根据提供的 `OrderID` 值返回特定订单。  
  
## 后续步骤  
 您已成功从 Web 浏览器访问 [!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)]，浏览器会向指定资源发出 HTTP GET 请求。  使用 Web 浏览器，可以轻松试验请求的寻址语法并查看结果。  不过，通常情况下并不会通过此方式访问生产数据服务。  通常，应用程序通过应用程序代码或脚本语言与数据服务交互。下一步，您将创建一个客户端应用程序，该应用程序使用客户端库来访问数据服务资源，就如同它们是公共语言运行时 \(CLR\) 对象一样：  
  
 [创建 .NET Framework 客户端应用程序](../../../../docs/framework/data/wcf/creating-the-dotnet-client-application-wcf-data-services-quickstart.md)  
  
## 请参阅  
 [访问数据服务资源](../../../../docs/framework/data/wcf/accessing-data-service-resources-wcf-data-services.md)