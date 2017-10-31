---
title: "如何：在配置中指定客户端绑定 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 4a7c79aa-50ee-4991-891e-adc0599323a7
caps.latest.revision: 11
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 11
---
# 如何：在配置中指定客户端绑定
在此示例中，创建了一个使用计算器服务的客户端控制台应用程序，并在配置中以声明方式为该客户端指定了绑定。 客户端访问`CalculatorService`，该类实现`ICalculator`接口，并且服务和客户端都使用<xref:System.ServiceModel.BasicHttpBinding>类。  
  
 上述过程假设计算器服务正在运行。 有关如何生成该服务的信息，请参阅[如何︰ 在配置中指定服务绑定](../../../docs/framework/wcf/how-to-specify-a-service-binding-in-configuration.md)。 它还使用[ServiceModel 元数据实用工具 (Svcutil.exe)](../../../docs/framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md) ，[!INCLUDE[indigo1](../../../includes/indigo1-md.md)]提供来自动生成的客户端组件。 该工具生成用于访问服务的客户端代码和配置。  
  
 客户端分两部分生成。 Svcutil.exe 生成实现 `ClientCalculator` 接口的 `ICalculator`。 然后，通过构造 `ClientCalculator` 的实例来构造客户端应用程序。  
  
 通常，最佳做法是以声明方式在配置中指定绑定和地址信息，而不是在代码中强制指定。 在代码中定义终结点通常是不可行的，因为已部署服务的绑定和地址通常与在部署服务时所用的绑定和地址不同。 一般说来，通过将绑定和寻址信息放置在代码之外，无需重新编译或重新部署应用程序即可更改这些信息。  
  
 您可以通过执行所有以下配置步骤[配置编辑器工具 (SvcConfigEditor.exe)](../../../docs/framework/wcf/configuration-editor-tool-svcconfigeditor-exe.md)。  
  
 此示例的源副本，请参阅[BasicBinding](../../../docs/framework/wcf/samples/basicbinding.md)示例。  
  
### <a name="specifying-a-client-binding-in-configuration"></a>在配置中指定客户端绑定  
  
1.  在命令行中，使用 Svcutil.exe 根据服务元数据生成代码。  
  
    ```  
    Svcutil.exe <service's Metadata Exchange (MEX) address or HTTP GET address>   
    ```  
  
2.  生成的客户端包含 `ICalculator` 接口，该接口定义了客户端实现必须满足的服务协定。  
  
     [!code-csharp[C_HowTo_ConfigureClientBinding#1](../../../samples/snippets/csharp/VS_Snippets_CFX/c_howto_configureclientbinding/cs/generatedclient.cs#1)]
     [!code-csharp[C_HowTo_ConfigureClientBinding#1](../../../samples/snippets/csharp/VS_Snippets_CFX/c_howto_configureclientbinding/cs/source.cs#1)]  
  
3.  生成的客户端还包含 `ClientCalculator` 的实现。  
  
     [!code-csharp[C_HowTo_ConfigureClientBinding#2](../../../samples/snippets/csharp/VS_Snippets_CFX/c_howto_configureclientbinding/cs/generatedclient.cs#2)]
     [!code-csharp[C_HowTo_ConfigureClientBinding#2](../../../samples/snippets/csharp/VS_Snippets_CFX/c_howto_configureclientbinding/cs/source.cs#2)]  
  
4.  Svcutil.exe 还生成使用的客户端的配置<xref:System.ServiceModel.BasicHttpBinding>类。 使用 [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] 时，请将此文件命名为 App.config。 请注意，在服务的实现内部，未指定地址和绑定信息。 而且，不必编写代码也可从配置文件中检索该信息。  
  
     <!-- TODO: review snippet reference [!code[C_HowTo_ConfigureClientBinding#100](../../../samples/snippets/common/VS_Snippets_CFX/c_howto_configureclientbinding/common/client.exe.config#100)]  -->  
  
5.  在应用程序中创建 `ClientCalculator` 的实例，然后调用服务操作。  
  
     [!code-csharp[C_HowTo_ConfigureClientBinding#3](../../../samples/snippets/csharp/VS_Snippets_CFX/c_howto_configureclientbinding/cs/client.cs#3)]  
  
6.  编译并运行客户端。  
  
## <a name="see-also"></a>另请参阅  
 [使用绑定配置服务和客户端](../../../docs/framework/wcf/using-bindings-to-configure-services-and-clients.md)