---
title: "如何：定义 Windows Communication Foundation 服务协定 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
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
  - "服务协定 [WCF], 定义"
ms.assetid: 67bf05b7-1d08-4911-83b7-a45d0b036fc3
caps.latest.revision: 58
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 58
---
# 如何：定义 Windows Communication Foundation 服务协定
这是创建基本 [!INCLUDE[indigo1](../../../includes/indigo1-md.md)] 应用程序所需的六项任务中的第一项任务。有关全部六项任务的概述，请参见[入门教程](../../../docs/framework/wcf/getting-started-tutorial.md)主题。  
  
 创建 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] 服务时，第一项任务是定义服务协定。服务协定指定服务支持的操作。可以将操作视为一个 Web 服务方法。通过定义 C\+\+、C\# 或 Visual Basic \(VB\) 接口可创建协定。接口中的每个方法都对应于特定的服务操作。每个接口都必须将 <xref:System.ServiceModel.ServiceContractAttribute> 应用于自身，而每个操作都必须将 <xref:System.ServiceModel.OperationContractAttribute> 特性应用于自身。如果接口中的一个方法具有 <xref:System.ServiceModel.ServiceContractAttribute> 特性而没有 <xref:System.ServiceModel.OperationContractAttribute> 特性，则服务不公开该方法。  
  
 在操作过程后面的示例中提供了用于此任务的代码。  
  
### 定义服务协定的步骤  
  
1.  通过在**“开始”**菜单中右击 [!INCLUDE[vs_current_long](../../../includes/vs-current-long-md.md)] 并选择**“以管理员身份运行”**，以管理员身份打开该程序。  
  
2.  通过以下方式创建一个 WCF 服务库项目：单击**“文件”**菜单然后依次选择**“新建”**、**“项目”**。在**“新项目”** 对话框中，在对话框的左侧为 C\# 项目展开**“Visual C\#”**，或展开**“其他语言”** ，然后为 Visual Basic项目展开**“Visual Basic”** 。在所选的语言下，选择**“WCF”**，项目模板的列表将显示在对话框中的中心部分。选择**“WCF服务库”**，在**“名称”** 文本框中键入 `GettingStartedLib`，在对话框底部的**“解决方案名称”**文本框中键入 `GettingStarted`。  
  
3.  Visual Studio 将创建包含以下 3 个文件的项目：IService1.cs（或 IService1.vb）、Service1.cs（或 Service1.vb）和 App.config。IService1 文件包含默认服务协定。服务 1 文件包含服务协定的默认实现。App.config 文件包含 Visual Studio WCF 服务主机加载默认服务所需的配置。有关 WCF服务主机工具的更多信息，请参见 [WCF 服务主机 \(WcfSvcHost.exe\)](../../../docs/framework/wcf/wcf-service-host-wcfsvchost-exe.md)。  
  
4.  打开 IService1.cs 或 IService1.vb 文件，在离开命名空间声明时删除命名空间声明内的代码。在命名空间声明内定义名为 `ICalculator` 的新接口，如下面的代码所示。  
  
    ```  
    // IService.cs  
    using System;  
    using System.Collections.Generic;  
    using System.Linq;  
    using System.Runtime.Serialization;  
    using System.ServiceModel;  
    using System.Text;  
  
    namespace GettingStartedLib  
    {  
            [ServiceContract(Namespace = "http://Microsoft.ServiceModel.Samples")]  
            public interface ICalculator  
            {  
                [OperationContract]  
                double Add(double n1, double n2);  
                [OperationContract]  
                double Subtract(double n1, double n2);  
                [OperationContract]  
                double Multiply(double n1, double n2);  
                [OperationContract]  
                double Divide(double n1, double n2);  
            }  
    }  
  
    ```  
  
    ```  
    ‘IService.vb  
    Imports System  
    Imports System.ServiceModel  
  
    Namespace GettingStartedLib  
  
        <ServiceContract(Namespace:="http://Microsoft.ServiceModel.Samples")> _  
        Public Interface ICalculator  
  
            <OperationContract()> _  
            Function Add(ByVal n1 As Double, ByVal n2 As Double) As Double  
            <OperationContract()> _  
            Function Subtract(ByVal n1 As Double, ByVal n2 As Double) As Double  
            <OperationContract()> _  
            Function Multiply(ByVal n1 As Double, ByVal n2 As Double) As Double  
            <OperationContract()> _  
            Function Divide(ByVal n1 As Double, ByVal n2 As Double) As Double  
        End Interface  
    End Namespace  
  
    ```  
  
     本协定定义了一个在线计算器。注意，`ICalculator` 接口用 <xref:System.ServiceModel.ServiceContractAttribute> 特性标记。此特性定义用于消除协定名称的歧义的命名空间。每个计算器操作都用 <xref:System.ServiceModel.OperationContractAttribute> 特性标记。  
  
    > [!NOTE]
    >  使用特性给接口、成员或类添加批注时，可以从特性名称中去掉“Attribute”部分。因此 <xref:System.ServiceModel.ServiceContractAttribute> 在 C\# 中为 `[ServiceContract]`，在 Visual Basic 中为 `<ServiceContract>`。  
  
## 请参阅  
 <xref:System.ServiceModel.ServiceContractAttribute>   
 <xref:System.ServiceModel.OperationContractAttribute>   
 [如何：实现服务协定](../../../docs/framework/wcf/how-to-implement-a-wcf-contract.md)   
 [入门](../../../docs/framework/wcf/samples/getting-started-sample.md)   
 [自承载](../../../docs/framework/wcf/samples/self-host.md)