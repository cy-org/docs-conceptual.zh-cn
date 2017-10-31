---
title: "如何：注册和配置服务标记 | Microsoft Docs"
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
  - "COM [WCF], 配置服务标记"
  - "COM [WCF], 注册服务标记"
ms.assetid: e5e16c80-8a8e-4eef-af53-564933b651ef
caps.latest.revision: 20
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 20
---
# 如何：注册和配置服务标记
在 COM 应用程序中使用具有类型化协定的 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 服务标记之前，必须先向 COM 注册所需的属性化类型，然后为 COM 应用程序和标记配置所需的绑定配置。  
  
### 向 COM 注册所需的属性化类型  
  
1.  使用 [ServiceModel 元数据实用工具 \(Svcutil.exe\)](../../../../docs/framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md) 工具从 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 服务检索元数据协定。  这会为 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 客户端程序集和客户端应用程序配置文件生成源代码。  
  
2.  确保将程序集中的类型标记为 `ComVisible`。  为此，请将下面的属性添加到 Visual Studio 项目的 AssemblyInfo.cs 文件中。  
  
    ```  
    [assembly: ComVisible(true)]  
    ```  
  
3.  将托管的 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 客户端编译为强名称程序集。  这要求使用加密密钥对进行签名。  [!INCLUDE[crdefault](../../../../includes/crdefault-md.md)] 《.NET 开发员指南》中的[使用强名称为程序集签名](http://go.microsoft.com/fwlink/?LinkId=94874)（可能为英文网页）。  
  
4.  使用带有 `/tlb` 选项的程序集注册 \(Regasm.exe\) 工具向 COM 注册程序集中的类型。  
  
5.  使用全局程序集缓存 \(Gacutil.exe\) 工具将该程序集添加到全局程序集缓存中。  
  
    > [!NOTE]
    >  对程序集进行签名并将其添加到全局程序集缓存中是可选步骤，不过，这两个步骤可以简化在运行时从正确位置加载程序集的过程。  
  
### 为 COM 应用程序和标记配置所需的绑定配置  
  
-   将绑定定义（由 [ServiceModel 元数据实用工具 \(Svcutil.exe\)](../../../../docs/framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md) 在生成的客户端应用程序配置文件中生成）放置到客户端应用程序的配置文件中。  例如，对于名为 CallCenterClient.exe 的 Visual Basic 6.0 可执行文件，配置应放置到该可执行文件所在目录中名为 CallCenterConfig.exe.config 的文件中。  此时，客户端应用程序就可以使用标记了。  请注意，如果使用 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 提供的标准绑定类型之一，则绑定配置不是必需的。  
  
     注册下面的类型。  
  
    ```  
    using System.ServiceModel;  
  
    ...  
  
    [ServiceContract]   
    public interface IMathService   
    {  
    [OperationContract]  
    public int Add(int x, int y);  
    [OperationContract]  
    public int Subtract(int x, int y);  
    }  
    ```  
  
     使用 `wsHttpBinding` 绑定来公开应用程序。  对于给定的类型和应用程序配置，将使用以下的示例标记字符串。  
  
    ```  
    service4:address=http://localhost/MathService, binding=wsHttpBinding, bindingConfiguration=Binding1  
  
    ```  
  
     `or`  
  
    ```  
    service4:address=http://localhost/MathService, binding=wsHttpBinding, bindingConfiguration=Binding1, contract={36ADAD5A-A944-4d5c-9B7C-967E4F00A090}  
  
    ```  
  
     在将引用添加到包含 `IMathService` 类型的程序集后，您可以使用 Visual Basic 6.0 应用程序中的这些标记字符串中的任何一个，如下面的示例代码中所示。  
  
    ```  
    Dim MathProxy As IMathService  
    Dim result As Integer  
  
    Set MathProxy = GetObject( _  
            "service4:address=http://localhost/MathService, _  
            binding=wsHttpBinding, _  
            bindingConfiguration=Binding1")  
  
    result = MathProxy.Add(3, 5)  
  
    ```  
  
     在本示例中，绑定配置 `Binding1` 的定义存储在该客户端应用程序的适当命名的配置文件中，如 vb6appname.exe.config。  
  
    > [!NOTE]
    >  您可以在 C\#、C\+\+ 或其他任何 .NET 语言的应用程序中使用类似的代码。  
  
    > [!NOTE]
    >  ：如果标记格式不正确，或者服务不可用，则对 `GetObject` 的调用会返回一个“语法无效”错误。  如果您收到此错误，请确保所使用的标记正确无误且服务可用。  
  
     尽管此主题重点介绍通过 VB 6.0 代码使用服务标记，您还是可以通过其他语言使用服务标记。  当通过 C\+\+ 代码使用标记时，应使用“no\_namespace named\_guids raw\_interfaces\_only”导入 Svcutil.exe 生成的程序集，如下面的代码中所示。  
  
    ```  
    #import "ComTestProxy.tlb" no_namespace named_guids  
    ```  
  
     这会修改导入的接口定义，以便所有方法均会返回一个 `HResult`。  其他任何返回值都将转换为 out 参数。  方法的总体执行情况保持不变。  这将允许您确定在代理上调用方法时出现异常的原因。  仅可通过 C\+\+ 代码来使用此功能。  
  
## 请参阅  
 [ServiceModel 元数据实用工具 \(Svcutil.exe\)](../../../../docs/framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md)