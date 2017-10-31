---
title: "如何：手动生成客户端数据服务类（WCF 数据服务） | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-oob"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "WCF 数据服务, 客户端库"
  - "WCF 数据服务, 配置"
ms.assetid: b98cb1d6-956a-4e50-add6-67e4f2587346
caps.latest.revision: 3
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 3
---
# 如何：手动生成客户端数据服务类（WCF 数据服务）
[!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)] 与 Visual Studio 集成，使您能够在使用**“添加服务引用”**对话框在 Visual Studio 项目中添加对数据服务的引用时自动生成客户端数据服务类。  有关详细信息，请参阅[如何：添加数据服务引用](../../../../docs/framework/data/wcf/how-to-add-a-data-service-reference-wcf-data-services.md)。  通过使用代码生成工具 `DataSvcUtil.exe`，可以手动生成相同的客户端数据服务类。[!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)] 附带此工具，它可根据数据服务定义生成 .NET Framework 类。  还可以使用此工具根据概念模型 \(.csdl\) 文件和表示 Visual Studio 项目中的实体框架模型的 .edmx 文件生成数据服务类。  
  
 本主题中的示例基于 Northwind 示例数据服务创建客户端数据服务类。  此服务是在完成 [WCF 数据服务快速入门](../../../../docs/framework/data/wcf/quickstart-wcf-data-services.md)时创建的。  本主题中的某些示例需要 Northwind 模型的概念模型文件。  有关详细信息，请参阅[如何：使用 EdmGen.exe 生成模型和映射文件](../../../../docs/framework/data/adonet/ef/how-to-use-edmgen-exe-to-generate-the-model-and-mapping-files.md)。  本主题中的某些示例需要 Northwind 模型的 .edmx 文件。  有关详细信息，请参阅[.edmx File Overview](http://msdn.microsoft.com/zh-cn/f4c8e7ce-1db6-417e-9759-15f8b55155d4)。  
  
### 生成支持数据绑定的 C\# 类  
  
-   在命令提示符下执行以下命令（无换行符）：  
  
    ```  
    "%windir%\Microsoft.NET\Framework\v3.5\DataSvcUtil.exe" /dataservicecollection /version:2.0 /language:CSharp /out:Northwind.cs /uri:http://localhost:12345/Northwind.svc  
    ```  
  
    > [!NOTE]
    >  必须用 Northwind 示例数据服务实例的 URI 替换向 `/uri:` 参数提供的值。  
  
### 生成支持数据绑定的 Visual Basic 类  
  
-   在命令提示符下执行以下命令（无换行符）：  
  
    ```  
    "%windir%\Microsoft.NET\Framework\v3.5\DataSvcUtil.exe" /dataservicecollection /version:2.0 /language:VB /out:Northwind.vb /uri:http://localhost:12345/Northwind.svc  
    ```  
  
    > [!NOTE]
    >  必须用 Northwind 示例数据服务实例的 URI 替换向 `/uri:` 参数提供的值。  
  
### 基于服务 URI 生成 C\# 类  
  
-   在命令提示符下执行以下命令（无换行符）：  
  
    ```  
    "%windir%\Microsoft.NET\Framework\v3.5\DataSvcUtil.exe" /language:CSharp /out:northwind.cs /uri:http://localhost:12345/Northwind.svc  
    ```  
  
    > [!NOTE]
    >  必须用 Northwind 示例数据服务实例的 URI 替换向 `/uri:` 参数提供的值。  
  
### 基于服务 URI 生成 Visual Basic 类  
  
-   在命令提示符下执行以下命令（无换行符）：  
  
    ```  
    "%windir%\Microsoft.NET\Framework\v3.5\datasvcutil.exe" /language:VB /out:Northwind.vb /uri:http://localhost:12345/Northwind.svc  
    ```  
  
    > [!NOTE]
    >  必须用 Northwind 示例数据服务实例的 URI 替换向 `/uri:` 参数提供的值。  
  
### 基于概念模型文件 \(CSDL\) 生成 C\# 类  
  
-   在命令提示符下执行以下命令（无换行符）：  
  
    ```  
    "%windir%\Microsoft.NET\Framework\v3.5\datasvcutil.exe" /language:CSharp /in:Northwind.csdl /out:Northwind.cs  
    ```  
  
### 基于概念模型文件 \(CSDL\) 生成 Visual Basic 类  
  
-   在命令提示符下执行以下命令（无换行符）：  
  
    ```  
    "%windir%\Microsoft.NET\Framework\v3.5\datasvcutil.exe" /language:VB /in:Northwind.csdl /out:Northwind.vb  
    ```  
  
### 基于 .edmx 文件生成 C\# 类  
  
-   在命令提示符下执行以下命令（无换行符）：  
  
    ```  
    "%windir%\Microsoft.NET\Framework\v3.5\datasvcutil.exe" /language:CSharp /in:Northwind.edmx /out:c:\northwind.cs   
    ```  
  
### 基于 .edmx 文件生成 Visual Basic 类  
  
-   在命令提示符下执行以下命令（无换行符）：  
  
    ```  
    "%windir%\Microsoft.NET\Framework\v3.5\datasvcutil.exe" /language:VB /in:Northwind.edmx /out:c:\northwind.vb   
    ```  
  
## 请参阅  
 [生成数据服务客户端库](../../../../docs/framework/data/wcf/generating-the-data-service-client-library-wcf-data-services.md)   
 [如何：添加数据服务引用](../../../../docs/framework/data/wcf/how-to-add-a-data-service-reference-wcf-data-services.md)   
 [WCF 数据服务客户端实用工具 \(DataSvcUtil.exe\)](../../../../docs/framework/data/wcf/wcf-data-service-client-utility-datasvcutil-exe.md)