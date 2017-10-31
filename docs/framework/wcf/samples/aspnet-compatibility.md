---
title: "ASP.NET 兼容性 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: c8b51f1e-c096-4c42-ad99-0519887bbbc5
caps.latest.revision: 25
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 25
---
# ASP.NET 兼容性
本示例演示如何在 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 中启用 [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)] 兼容性模式。  在 [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)] 兼容性模式中运行的服务可完全参与 [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)] 应用程序管道并可利用 [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)] 功能，如文件\/URL 授权、会话状态和 <xref:System.Web.HttpContext> 类。  使用 <xref:System.Web.HttpContext> 类可以访问 Cookie、会话和其他 [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)] 功能。  此模式要求绑定使用 HTTP 传输，且服务本身必须承载于 IIS 中。  
  
 在此示例中，客户端是一个控制台应用程序（一个可执行文件），服务由 Internet 信息服务 \(IIS\) 承载。  
  
> [!NOTE]
>  本主题的最后介绍了此示例的设置过程和生成说明。  
  
> [!NOTE]
>  此示例需要 [!INCLUDE[netfx40_long](../../../../includes/netfx40-long-md.md)] 应用程序池才能运行。  若要创建新的应用程序池或修改默认应用程序池，请按照以下步骤操作。  
>   
>  1.  打开**“控制面板”**。  打开**“系统和安全”**标题下的**“管理工具”**小程序。  打开**“Internet 信息服务\(IIS\)管理器”**小程序。  
> 2.  展开**“连接”**窗格中的树视图。  选择**“应用程序池”**节点。  
> 3.  若要将默认应用程序池设置为使用 [!INCLUDE[netfx40_long](../../../../includes/netfx40-long-md.md)]（可能会导致与现有站点的不兼容问题），请右击**“DefaultAppPool”**列表项并选择**“基本设置…”**。  将**“.Net Framework 版本”**下拉列表设置为**“.Net Framework v4.0.30128”**（或更高版本）。  
> 4.  若要创建使用 [!INCLUDE[netfx40_long](../../../../includes/netfx40-long-md.md)] 的新应用程序池（保持与其他应用程序的兼容性），请右击**“应用程序池”**节点并选择**“添加应用程序池…”**。  为新应用程序池命名，然后将**“.Net Framework 版本”**下拉列表设置为**“.Net Framework v4.0.30128”**（或更高版本）。  运行下面的设置步骤后，右击**“ServiceModelSamples”**应用程序，然后依次选择**“管理应用程序”**、**“高级设置…”**。  将**“应用程序池”**设置为新的应用程序池。  
  
> [!IMPORTANT]
>  您的计算机上可能已安装这些示例。  在继续操作之前，请先检查以下（默认）目录：  
>   
>  `<安装驱动器>:\WF_WCF_Samples`  
>   
>  如果此目录不存在，请访问[针对 .NET Framework 4 的 Windows Communication Foundation \(WCF\) 和 Windows Workflow Foundation \(WF\) 示例](http://go.microsoft.com/fwlink/?LinkId=150780)（可能为英文网页），下载所有 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 和 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 示例。  此示例位于以下目录：  
>   
>  `<安装驱动器>:\WF_WCF_Samples\WCF\Basic\Services\Hosting\WebHost\ASPNetCompatibility`  
  
 此示例基于实现计算器服务的[入门](../../../../docs/framework/wcf/samples/getting-started-sample.md)。  `ICalculator` 协定已根据 `ICalculatorSession` 协定进行修改，允许在保持运行结果的同时执行一组运算。  
  
```  
[ServiceContract(Namespace="http://Microsoft.ServiceModel.Samples")]  
public interface ICalculatorSession  
{  
    [OperationContract]  
    void Clear();  
    [OperationContract]  
    void AddTo(double n);  
    [OperationContract]  
    void SubtractFrom(double n);  
    [OperationContract]  
    void MultiplyBy(double n);  
    [OperationContract]  
    void DivideBy(double n);  
    [OperationContract]  
    double Result();  
}  
  
```  
  
 在调用多个服务操作来执行计算时，服务将使用该功能保持每个客户端的状态。  客户端可以通过调用 `Result` 来检索当前结果，通过调用 `Clear` 将结果清零。  
  
 服务使用 [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)] 会话来存储每个客户端会话的结果。  这使服务可以为跨多个服务调用的每个客户端保持运行结果。  
  
> [!NOTE]
>  [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)] 会话状态和 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 会话截然不同。  有关 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 会话的详细信息，请参见[会话](../../../../docs/framework/wcf/samples/session.md)。  
  
 服务直接依赖于 [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)] 会话状态，并需要 [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)] 兼容性模式才能正常工作。  这些要求是通过应用 `AspNetCompatibilityRequirements` 属性以声明性方式表示的。  
  
```  
[AspNetCompatibilityRequirements(RequirementsMode =  
                       AspNetCompatibilityRequirementsMode.Required)]  
public class CalculatorService : ICalculatorSession  
{  
    double Result  
    {  // store result in AspNet Session  
       get {  
          if (HttpContext.Current.Session["Result"] != null)  
             return (double)HttpContext.Current.Session["Result"];  
          return 0.0D;  
       }  
       set  
       {  
          HttpContext.Current.Session["Result"] = value;  
       }  
    }  
    public void Clear()  
    {  
        Result = 0.0D;  
    }  
    public void AddTo(double n)  
    {  
        Result += n;  
    }  
    public void SubtractFrom(double n)  
    {  
        Result -= n;  
    }  
    public void MultiplyBy(double n)  
    {  
        Result *= n;  
    }  
    public void DivideBy(double n)  
    {  
        Result /= n;  
    }  
    public double Result()  
    {  
        return Result;  
    }  
}  
```  
  
 运行示例时，操作请求和响应将显示在客户端控制台窗口中。  在客户端窗口中按 Enter 可以关闭客户端。  
  
```  
  
0, + 100, - 50, * 17.65, / 2 = 441.25  
Press <ENTER> to terminate client.  
  
```  
  
### 设置、生成和运行示例  
  
1.  请确保已执行 [Windows Communication Foundation 示例的一次性安装过程](../../../../docs/framework/wcf/samples/one-time-setup-procedure-for-the-wcf-samples.md)。  
  
2.  若要生成 C\# 或 Visual Basic .NET 版本的解决方案，请按照[生成 Windows Communication Foundation 示例](../../../../docs/framework/wcf/samples/building-the-samples.md)中的说明进行操作。  
  
3.  生成解决方案后，运行 Setup.bat 在 [!INCLUDE[iisver](../../../../includes/iisver-md.md)] 中设置 ServiceModelSamples 应用程序。  现在，ServiceModelSamples 目录应显示为 [!INCLUDE[iisver](../../../../includes/iisver-md.md)] 应用程序。  
  
4.  若要用单机配置或跨计算机配置来运行示例，请按照[运行 Windows Communication Foundation 示例](../../../../docs/framework/wcf/samples/running-the-samples.md)中的说明进行操作。  
  
## 请参阅  
 [AppFabric 承载和持久性示例 （可能为英文网页）](http://go.microsoft.com/fwlink/?LinkId=193961)