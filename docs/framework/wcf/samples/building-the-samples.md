---
title: "生成 Windows Communication Foundation 示例 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 2899e7a5-9cb2-4e8d-b8d2-f31391549198
caps.latest.revision: 33
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 33
---
# 生成 Windows Communication Foundation 示例
可以使用 Visual Studio 2010 或使用 **msbuild** 命令从命令行中生成 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 示例。本主题介绍这两个过程。  
  
> [!NOTE]
>  在生成或运行任何 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] 示例之前，请确保已经执行了 [Windows Communication Foundation 示例的一次性安装过程](../../../../docs/framework/wcf/samples/one-time-setup-procedure-for-the-wcf-samples.md)。  
  
### 使用命令提示生成示例  
  
1.  使用管理员特权打开 [!INCLUDE[vs_current_long](../../../../includes/vs-current-long-md.md)] 命令提示，然后定位到安装示例的目录位置下的语言特定的子目录。  
  
2.  在命令行中键入 `msbuild`。客户端程序文件在 client\\bin 中生成，服务程序文件在 service\\bin 中生成。如果服务由 Internet Information Services \(IIS\) 承载，服务程序文件还将被复制到 servicemodelsamples 目录及其 \\bin 子目录中。  
  
> [!NOTE]
>  您必须在 %systemdrive%\\inetpub\\wwwroot 上设置 ACL，以便为您运行的帐户授予修改权限。否则，某些后期生成事件将失败。或者，您可以将 ACL 保留原样，而以管理员身份运行 SDK 命令提示。  
  
### 使用 Visual Studio 生成示例  
  
1.  如果使用的是 [!INCLUDE[wv](../../../../includes/wv-md.md)]、[!INCLUDE[lserver](../../../../includes/lserver-md.md)]、Windows 7 或 Windows Server 2008 R2，同时运行了 [!INCLUDE[vs_current_long](../../../../includes/vs-current-long-md.md)]，则必须用提升的权限运行 [!INCLUDE[vsprvs](../../../../includes/vsprvs-md.md)]。为此，请在“开始”菜单上右击其图标，然后单击**“以管理员身份运行”**。  
  
2.  在 [!INCLUDE[vs_current_short](../../../../includes/vs-current-short-md.md)] 的**“文件”**菜单上单击**“打开”**，再单击**“项目\/解决方案”**。定位至示例安装目录下的语言特定的子目录，然后双击 .sln 文件图标，以便在 [!INCLUDE[vsprvs](../../../../includes/vsprvs-md.md)] 中打开该解决方案。  
  
3.  在**“生成”**菜单中选择**“重新生成解决方案”**。客户端程序文件在 client\\bin 中生成，服务程序文件在 service\\bin 中生成。如果服务在 IIS 中承载，服务程序文件还将被复制到 servicemodelsamples 目录及其 \\bin 子目录中。  
  
> [!NOTE]
>  您必须在 %systemdrive%\\inetpub\\wwwroot 上设置 ACL，以便为您运行的帐户授予修改权限。否则，某些后期生成事件将失败。或者，您可以将 ACL 保留原样，而以管理员身份运行 SDK 命令提示或 Visual Studio。某些 Visual Studio 操作（例如，为 ASP.Net 工作进程附加调试器）也需要管理特权。  
  
## 设置批处理文件和脚本  
 Setup.exe 和 Cleanup.exe 批处理文件和脚本应在 Visual Studio 命令提示中运行。有几个设置和清理文件将执行需要具有管理特权的任务，应使用管理特权来启动它们。  
  
## 有关元数据终结点的重要安全信息  
 为了防止无意中泄露潜在的敏感服务元数据，[!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 服务的默认配置将禁用元数据发布。默认情况下此行为是安全的，但也意味着您无法使用元数据导入工具（例如 Svcutil.exe）生成调用服务所需的客户端代码，除非在配置中显式启用服务的元数据发布行为。为了使示例体验更简单，几乎所有示例都公开一个不安全的元数据发布终结点。此类终结点或许可以供未通过身份验证的匿名使用者使用，因此在部署此类终结点之前，必须谨慎以确保适合公开透露服务元数据。[!INCLUDE[crabout](../../../../includes/crabout-md.md)]发布服务元数据的更多消息，请参见[元数据发布行为](../../../../docs/framework/wcf/samples/metadata-publishing-behavior.md)示例。有关确保元数据终结点安全的示例，请参见[自定义安全元数据终结点](../../../../docs/framework/wcf/samples/custom-secure-metadata-endpoint.md)示例。  
  
## 异常处理  
 一般情况下，这些示例不包括异常处理，以使代码集中说明示例的主题。[!INCLUDE[crabout](../../../../includes/crabout-md.md)]异常处理的更多消息，请参见[预期异常](../../../../docs/framework/wcf/samples/expected-exceptions.md)示例。  
  
## 使用 Svcutil 重新生成客户端和配置  
 您可以使用 [ServiceModel 元数据实用工具 \(Svcutil.exe\)](../../../../docs/framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md) 为大多数示例生成客户端代码和配置。某些示例需要手动编辑的配置。例如，如果您使用 Svcutil.exe 为某个使用客户端证书凭据的示例重新生成配置，必须手动指定之前配置的凭据。某些示例使用特定的 Svcutil.exe 选项来影响生成的代码，这些选项在具体的示例主题中进行指定。  
  
#### 重新生成客户端和配置文件  
  
1.  打开 SDK 命令提示，然后定位到安装示例的目录位置下的语言特定的子目录。  
  
2.  如果服务是 Web 承载的类型，请使用以下命令。  
  
    ```  
    svcutil.exe /n:"http://Microsoft.ServiceModel.Samples,Microsoft.ServiceModel.Samples" http://localhost/servicemodelsamples/service.svc/mex /out:generatedClient.cs  
    ```  
  
     如果服务是自承载类型，请键入以下命令。  
  
    ```  
    svcutil.exe /n:"http://Microsoft.ServiceModel.Samples,Microsoft.ServiceModel.Samples" http://localhost:8000/servicemodelsamples/service.svc/mex /out:generatedClient.cs  
    ```  
  
     用自承载服务的 mex 终结点的地址替换 http:\/\/localhost:8000\/ServiceModelSamples\/service.svc\/mex。  
  
     若要在 Visual Basic 类型中生成客户端，请使用以下命令。  
  
    ```  
    svcutil.exe /n:"http://Microsoft.ServiceModel.Samples,Microsoft.ServiceModel.Samples" http://localhost/servicemodelsamples/service.svc/mex /l:vb /out:generatedClient.vb  
  
    ```  
  
     如果服务是自承载类型，请使用以下命令。  
  
    ```  
    svcutil.exe /n:"http://Microsoft.ServiceModel.Samples,Microsoft.ServiceModel.Samples" http://localhost:8000/servicemodelsamples/service.svc/mex /l:vb /out:generatedClient.vb  
    ```  
  
    > [!NOTE]
    >  若要跳过客户端配置的生成，请添加 **\/noConfig** 选项。  
  
## 请参阅  
 [运行 Windows Communication Foundation 示例](../../../../docs/framework/wcf/samples/running-the-samples.md)   
 [ServiceModel 元数据实用工具 \(Svcutil.exe\)](../../../../docs/framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md)