---
title: "模拟客户端 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "模拟客户端示例 [Windows Communication Foundation]"
  - "模拟, Windows Communication Foundation 示例"
  - "服务行为, 模拟示例"
ms.assetid: 8bd974e1-90db-4152-95a3-1d4b1a7734f8
caps.latest.revision: 25
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 25
---
# 模拟客户端
此模拟示例演示如何在服务中模拟调用方应用程序，以便服务可以代表调用方访问系统资源。  
  
 此示例基于[自承载](../../../../docs/framework/wcf/samples/self-host.md)示例。服务和客户端配置文件与[自承载](../../../../docs/framework/wcf/samples/self-host.md)示例中的配置文件相同。  
  
> [!NOTE]
>  本主题的末尾介绍了此示例的设置过程和生成说明。  
  
 对于服务代码已经进行了修改，以便服务上的 `Add` 方法使用 <xref:System.ServiceModel.OperationBehaviorAttribute> 来模拟调用方，如下面的示例代码中所示。  
  
```  
[OperationBehavior(Impersonation = ImpersonationOption.Required)]  
public double Add(double n1, double n2)  
{  
    double result = n1 + n2;  
    Console.WriteLine("Received Add({0},{1})", n1, n2);  
    Console.WriteLine("Return: {0}", result);  
    DisplayIdentityInformation();  
    return result;  
}  
  
```  
  
 因此，执行线程的安全上下文将在进入 `Add` 方法之前进行切换以模拟调用方，并在退出该方法时恢复。  
  
 以下示例代码中所示的 `DisplayIdentityInformation` 方法是一个用来显示调用方标识的实用工具函数。  
  
```  
static void DisplayIdentityInformation()  
{  
    Console.WriteLine("\t\tThread Identity            :{0}",  
         WindowsIdentity.GetCurrent().Name);  
    Console.WriteLine("\t\tThread Identity level  :{0}",   
         WindowsIdentity.GetCurrent().ImpersonationLevel);  
    Console.WriteLine("\t\thToken                     :{0}",  
         WindowsIdentity.GetCurrent().Token.ToString());  
    return;  
}  
  
```  
  
 服务上的 `Subtract` 方法使用命令性调用来模拟调用方，如下面的示例代码中所示。  
  
```  
public double Subtract(double n1, double n2)  
{  
    double result = n1 - n2;  
    Console.WriteLine("Received Subtract({0},{1})", n1, n2);  
    Console.WriteLine("Return: {0}", result);  
Console.WriteLine("Before impersonating");  
DisplayIdentityInformation();  
  
    if (ServiceSecurityContext.Current.WindowsIdentity.ImpersonationLevel == TokenImpersonationLevel.Impersonation ||  
        ServiceSecurityContext.Current.WindowsIdentity.ImpersonationLevel == TokenImpersonationLevel.Delegation)  
    {  
        // Impersonate.  
        using (ServiceSecurityContext.Current.WindowsIdentity.Impersonate())  
        {  
            // Make a system call in the caller's context and ACLs   
            // on the system resource are enforced in the caller's context.   
            Console.WriteLine("Impersonating the caller imperatively");  
            DisplayIdentityInformation();  
        }  
    }  
    else  
    {  
        Console.WriteLine("ImpersonationLevel is not high enough to perform this operation.");  
    }  
  
Console.WriteLine("After reverting");  
DisplayIdentityInformation();  
    return result;  
}  
```  
  
 请注意，在本例中，并未针对整个调用模拟调用方，而只是针对调用的一部分来模拟调用方。通常，针对最小范围进行模拟比针对整个操作进行模拟更可取。  
  
 其他方法不能模拟调用方。  
  
 已经对客户端代码进行了修改，以便将模拟级别设置为 <xref:System.Security.Principal.TokenImpersonationLevel>。客户端通过使用 <xref:System.Security.Principal.TokenImpersonationLevel> 枚举来指定要由服务使用的模拟级别。枚举支持下列值：<xref:System.Security.Principal.TokenImpersonationLevel>、<xref:System.Security.Principal.TokenImpersonationLevel>、<xref:System.Security.Principal.TokenImpersonationLevel>、<xref:System.Security.Principal.TokenImpersonationLevel> 和 <xref:System.Security.Principal.TokenImpersonationLevel>。如果要在访问使用 Windows ACL 保护的本地计算机上的系统资源时执行访问检查，则必须将模拟级别设置为 <xref:System.Security.Principal.TokenImpersonationLevel>，如下面的示例代码中所示。  
  
```  
// Create a client with given client endpoint configuration  
CalculatorClient client = new CalculatorClient();  
  
client.ClientCredentials.Windows.AllowedImpersonationLevel = TokenImpersonationLevel.Impersonation;  
```  
  
 运行示例时，操作请求和响应将显示在服务和客户端控制台窗口中。在每个控制台窗口中按 Enter 可以关闭服务和客户端。  
  
> [!NOTE]
>  服务必须在管理帐户下运行，或者运行服务时所使用的帐户必须被授予向 HTTP 层注册 http:\/\/localhost:8000\/ServiceModelSamples URI 的权限。可以通过使用 [Httpcfg.exe 工具](http://go.microsoft.com/fwlink/?LinkId=95010)（可能为英文网页）设置[命名空间保留](http://go.microsoft.com/fwlink/?LinkId=95012)（可能为英文网页），来授予这样的权限。  
  
> [!NOTE]
>  在运行 [!INCLUDE[ws2003](../../../../includes/ws2003-md.md)] 的计算机上，只有当 Host.exe 应用程序具有“模拟”特权时，才支持进行模拟。（默认情况下，只有管理员才具有此权限。）若要将该特权添加到运行服务时所使用的帐户中，请转至**“管理工具”**，打开**“本地安全策略”**，打开**“本地策略”**，单击**“用户权限分配”**，选择**“身份验证后模拟客户端”**，再双击**“属性”**以添加用户或组。  
  
### 设置、生成和运行示例  
  
1.  请确保已经执行了 [Windows Communication Foundation 示例的一次性安装过程](../../../../docs/framework/wcf/samples/one-time-setup-procedure-for-the-wcf-samples.md)。  
  
2.  若要生成 C\# 或 Visual Basic .NET 版本的解决方案，请按照[生成 Windows Communication Foundation 示例](../../../../docs/framework/wcf/samples/building-the-samples.md)中的说明进行操作。  
  
3.  若要用单机配置或跨计算机配置来运行示例，请按照[运行 Windows Communication Foundation 示例](../../../../docs/framework/wcf/samples/running-the-samples.md)中的说明进行操作。  
  
4.  若要演示服务对调用方的模拟，请在与运行服务时所用帐户不同的其他帐户下运行客户端。为此，请在命令提示符下键入：  
  
    ```  
    runas /user:<machine-name>\<user-name> client.exe  
    ```  
  
     系统随后将提示您输入一个密码。请输入您以前为帐户指定的密码。  
  
5.  运行客户端时，请注意它在用不同的凭据运行前后的标识。  
  
## 请参阅