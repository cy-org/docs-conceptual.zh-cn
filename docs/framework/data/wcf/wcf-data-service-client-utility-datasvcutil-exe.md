---
title: "WCF 数据服务客户端实用工具 (DataSvcUtil.exe) | Microsoft Docs"
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
  - "WCF 数据服务, 使用"
  - "WCF 数据服务, 生成客户端数据类"
ms.assetid: 9d0af606-929b-4c03-b307-3ef5f705afce
caps.latest.revision: 2
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 2
---
# WCF 数据服务客户端实用工具 (DataSvcUtil.exe)
DataSvcUtil.exe 是由 [!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)]提供的命令行工具，它使用[!INCLUDE[ssODataFull](../../../../includes/ssodatafull-md.md)] 源，并生成从 .NET Framework 客户端应用程序访问数据服务所需的客户端数据服务类。  通过使用以下元数据源，该实用工具可以生成数据类：  
  
-   数据服务的根 URI。  该实用工具会请求描述数据服务所公开的数据模型的服务元数据文档。  有关更多信息，请参见 [OData：服务元数据文档](http://go.microsoft.com/fwlink/?LinkId=186070)（可能为英文网页）。  
  
-   使用概念架构定义语言 \(CSDL\) 定义的数据模型文件 \(.csdl\)，如 [\[MC\-CSDL\]：概念架构定义文件格式](http://go.microsoft.com/fwlink/?LinkID=159072)（可能为英文网页）规范中所定义。  
  
-   使用随实体框架提供的实体数据模型工具创建的 .edmx 文件。  有关更多信息，请参见 [\[MC\-EDMX\]：用于数据服务打包格式的实体数据模型](http://go.microsoft.com/fwlink/?LinkID=178833)（可能为英文网页）规范。  
  
 有关详细信息，请参阅[如何：手动生成客户端数据服务类](../../../../docs/framework/data/wcf/how-to-manually-generate-client-data-service-classes-wcf-data-services.md)。  
  
 DataSvcUtil.exe 工具安装在 [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] 目录中。  多数情况下，它位于 C:\\Windows\\Microsoft.NET\\Framework\\v4.0 中。  对于 64 位系统，它位于 C:\\Windows\\Microsoft.NET\\Framework64\\v4.0 中。  此外，从 Visual Studio 命令提示也可以访问 DataSvcUtil.exe 工具（单击**“开始”**，依次指向**“所有程序”**、**“Microsoft Visual Studio 2010”**、**“Visual Studio 工具”**，然后单击**“Visual Studio 2010 命令提示”**）。  
  
## 语法  
  
```  
datasvcutil /out:file [/in:file | /uri:serviceuri] [/dataservicecollection] [/language:devlang] [/nologo] [/version:ver] [/help]  
```  
  
#### 参数  
  
|选项|描述|  
|--------|--------|  
|`/dataservicecollection`|指定还生成了将对象绑定到控件所需的代码。|  
|`/help`<br /><br /> \- 或 \-<br /><br /> `/?`|显示该工具的命令语法和选项。|  
|`/in:` *\<file\>*|指定 .csdl 或 .edmx 文件或该文件所在的目录。|  
|`/language:`\[VB&#124;CSharp\]|指定生成的源代码文件的语言。  默认语言为 C\#。|  
|`/nologo`|禁止显示版权信息。|  
|`/out:` *\<file\>*|指定包含生成的客户端数据服务类的源代码文件的名称。|  
|`/uri:` *\<string\>*|[!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)] 源的 URI。|  
|`/version:`\[1.0&#124;2.0\]|指定接受的最高 [!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)] 版本。  版本是根据返回的数据服务元数据中的 DataService 元素的 `DataServiceVersion` 特性确定的。  有关详细信息，请参阅[数据服务版本管理](../../../../docs/framework/data/wcf/data-service-versioning-wcf-data-services.md)。  指定 `/dataservicecollection` 参数时，还必须指定 `/version:2.0` 才能启用数据绑定。|  
  
## 请参阅  
 [生成数据服务客户端库](../../../../docs/framework/data/wcf/generating-the-data-service-client-library-wcf-data-services.md)   
 [如何：添加数据服务引用](../../../../docs/framework/data/wcf/how-to-add-a-data-service-reference-wcf-data-services.md)