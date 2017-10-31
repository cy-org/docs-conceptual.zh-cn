---
title: "如何：使用双工协定访问服务 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
helpviewer_keywords: 
  - "双工协定 [WCF]"
ms.assetid: 746a9d64-f21c-426c-b85d-972e916ec6c5
caps.latest.revision: 18
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 18
---
# 如何：使用双工协定访问服务
[!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 的一个功能是可以创建使用双工消息传递模式的服务。此模式允许服务通过回调与客户端进行通信。本主题演示在实现回调接口的客户端类中创建 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 客户端的步骤。  
  
 双向绑定向服务公开客户端的 IP 地址。客户端应使用安全来确保仅连接到自己信任的服务。  
  
 有关创建基本 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 服务和客户端的教程，请参见 [入门教程](../../../../docs/framework/wcf/getting-started-tutorial.md)。  
  
### 访问双工服务  
  
1.  创建包含两个接口的服务。第一个接口用于服务，第二个接口用于回调。[!INCLUDE[crabout](../../../../includes/crabout-md.md)]创建双工服务的更多信息，请参见[如何：创建双工协定](../../../../docs/framework/wcf/feature-details/how-to-create-a-duplex-contract.md)。  
  
2.  运行该服务。  
  
3.  使用 [ServiceModel 元数据实用工具 \(Svcutil.exe\)](../../../../docs/framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md) 为客户端生成协定（接口）。有关如何执行该操作的信息，请参见[如何：创建客户端](../../../../docs/framework/wcf/how-to-create-a-wcf-client.md)。  
  
4.  在客户端类中实现回调接口，如下面的示例所示。  
  
    ```csharp  
    public class CallbackHandler : ICalculatorDuplexCallback  
    {  
        public void Result(double result)  
        {  
            Console.WriteLine("Result ({0})", result);  
        }  
        public void Equation(string equation)  
        {  
            Console.WriteLine("Equation({0})", equation);  
        }  
    }  
    ```  
  
    ```vb  
    Public Class CallbackHandler   
    Implements ICalculatorDuplexCallback  
       Public Sub Result (ByVal result As Double)  
          Console.WriteLine("Result ({0})", result)  
       End Sub  
        Public Sub Equation(ByVal equation As String)  
            Console.Writeline("Equation({0})", equation)  
        End Sub  
    End Class  
  
    ```  
  
5.  创建 <xref:System.ServiceModel.InstanceContext> 类的一个实例。构造函数需要客户端类的一个实例。  
  
    ```csharp  
    InstanceContext site = new InstanceContext(new CallbackHandler());  
    ```  
  
    ```vb  
    Dim site As InstanceContext = New InstanceContext(new CallbackHandler())  
    ```  
  
6.  使用需要 <xref:System.ServiceModel.InstanceContext> 对象的构造函数创建 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 客户端的一个实例。该构造函数的第二个参数是配置文件中找到的终结点的名称。  
  
    ```csharp  
    CalculatorDuplexClient wcfClient =   
    new CalculatorDuplexClient(site, "default")  
    ```  
  
    ```vb  
    Dim wcfClient As New CalculatorDuplexClient(site, "default")  
    ```  
  
7.  根据需要调用 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 客户端的方法。  
  
## 示例  
 下面的代码示例演示如何创建一个访问双工协定的客户端类。  
  
 [!code-csharp[S_DuplexClients#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/s_duplexclients/cs/client.cs#1)]
 [!code-vb[S_DuplexClients#1](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/s_duplexclients/vb/client.vb#1)]  
  
## .NET Framework 安全性  
  
## 请参阅  
 [入门教程](../../../../docs/framework/wcf/getting-started-tutorial.md)   
 [如何：创建双工协定](../../../../docs/framework/wcf/feature-details/how-to-create-a-duplex-contract.md)   
 [ServiceModel 元数据实用工具 \(Svcutil.exe\)](../../../../docs/framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md)   
 [如何：创建客户端](../../../../docs/framework/wcf/how-to-create-a-wcf-client.md)   
 [如何：使用 ChannelFactory](../../../../docs/framework/wcf/feature-details/how-to-use-the-channelfactory.md)