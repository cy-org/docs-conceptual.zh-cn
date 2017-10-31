---
title: "EDM 生成器 (EdmGen.exe) | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
ms.assetid: fe8297a1-1fc3-48ce-8eeb-f70f63f857aa
caps.latest.revision: 6
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 6
---
# EDM 生成器 (EdmGen.exe)
EdmGen.exe 是用于处理[!INCLUDE[adonet_ef](../../../../../includes/adonet-ef-md.md)]模型和映射文件的命令行工具。  使用 EdmGen.exe 工具可以执行以下任务：  
  
-   使用特定于数据源的 .NET Framework 数据提供程序连接到数据源，生成[!INCLUDE[adonet_ef](../../../../../includes/adonet-ef-md.md)]使用的概念模型 \(.csdl\)、存储模型 \(.ssdl\) 以及映射 \(.msl\) 文件。  有关详细信息，请参阅[如何：使用 EdmGen.exe 生成模型和映射文件](../../../../../docs/framework/data/adonet/ef/how-to-use-edmgen-exe-to-generate-the-model-and-mapping-files.md)。  
  
-   验证现有模型。  有关详细信息，请参阅[如何：使用 EdmGen.exe 验证模型和映射文件](../../../../../docs/framework/data/adonet/ef/how-to-use-edmgen-exe-to-validate-model-and-mapping-files.md)。  
  
-   生成包含从概念模型 \(.csdl\) 文件生成的对象类的 C\# 或 Visual Basic 代码文件。  有关详细信息，请参阅[如何：使用 EdmGen.exe 生成对象层代码](../../../../../docs/framework/data/adonet/ef/how-to-use-edmgen-exe-to-generate-object-layer-code.md)。  
  
-   生成包含现有模型的预生成视图的 C\# 或 Visual Basic 代码文件。  有关更多信息，请参见[How to: Pre\-Generate Views to Improve Query Performance](http://msdn.microsoft.com/zh-cn/b18a9d16-e10b-4043-ba91-b632f85a2579)。  
  
 EdmGen.exe 工具安装在 [!INCLUDE[dnprdnshort](../../../../../includes/dnprdnshort-md.md)] 目录中。  多数情况下，它位于 C:\\windows\\Microsoft.NET\\Framework\\v4.0 中。  对于 64 位系统，它位于 C:\\windows\\Microsoft.NET\\Framework64\\v4.0 中。  此外，从 Visual Studio 命令提示也可以访问 EdmGen.exe 工具（单击**“开始”**，依次指向**“所有程序”**、**“Microsoft Visual Studio 2010”**、**“Visual Studio 工具”**，然后单击**“Visual Studio 2010 命令提示”**）。  
  
## 语法  
  
```  
EdmGen /mode:choice [options]  
```  
  
## 模式  
 使用 EdmGen.exe 工具时，必须指定以下模式之一。  
  
|模式|描述|  
|--------|--------|  
|`/mode:ValidateArtifacts`|验证 .csdl、.ssdl 和 .msl 文件并显示所有错误或警告。<br /><br /> 此选项需要至少一个 `/inssdl` 或 `/incsdl` 参数。  如果指定 `/inmsl`，则还需要 `/inssdl` 和 `/incsdl` 参数。|  
|`/mode:FullGeneration`|使用 `/connectionstring` 选项中指定的数据库连接信息，生成 .csdl、.ssdl、.msl、对象层和视图文件。<br /><br /> 此选项需要一个 `/connectionstring` 参数以及一个 `/project` 参数或 `/outssdl`、`/outcsdl`、`/outmsdl`、`/outobjectlayer`、`/outviews`、`/namespace` 和 `/entitycontainer` 参数。|  
|`/mode:FromSSDLGeneration`|根据指定的 .ssdl 文件生成 .csdl 和 .msl 文件、源代码和视图。<br /><br /> 此选项需要 `/inssdl` 参数，以及 `/project` 参数或 `/outcsdl`、`/outmsl`、`/outobjectlayer`、`/outviews`、`/namespace` 和 `/entitycontainer` 参数。|  
|`/mode:EntityClassGeneration`|创建包含根据 .csdl 文件生成的类的源代码文件。<br /><br /> 此选项需要 `/incsdl` 参数，以及 `/project` 参数或 `/outobjectlayer` 参数。  `/language` 参数是可选的。|  
|`/mode:ViewGeneration`|创建包含根据 .csdl、.ssdl 和 .msl 文件生成的视图的源代码文件。<br /><br /> 此选项需要 `/inssdl`、`/incsdl`、`/inmsl`，以及 `/project` 或 `/outviews` 参数。  `/language` 参数是可选的。|  
  
## 选项  
  
|选项|描述|  
|--------|--------|  
|`/p[roject]:`\<string\>|指定要使用的项目名称。  该项目名称用作命名空间设置、模型和映射文件的名称、对象源文件的名称以及视图生成源文件的名称的默认值。  实体容器名称设置为 \<项目\>Context。|  
|`/prov[ider]:`\<string\>|生成存储模型 \(.ssdl\) 文件要使用的 [!INCLUDE[dnprdnshort](../../../../../includes/dnprdnshort-md.md)] 数据提供程序的名称。  默认的提供程序是用于 SQL Server 的 [!INCLUDE[dnprdnshort](../../../../../includes/dnprdnshort-md.md)] 数据提供程序 \(<xref:System.Data.SqlClient?displayProperty=fullName>\)。|  
|`/c[onnectionstring]:`\<connection string\>|指定用于连接数据源的字符串。|  
|`/incsdl:`\<file\>|指定 .csdl 文件或 .csdl 文件所在的目录。  此参数可多次指定，这样可以指定多个目录或 .csdl 文件。  当概念模型跨多个文件拆分时，对于生成类 \(`/mode:EntityClassGeneration`\) 或视图 \(`/mode:ViewGeneration`\)，指定多个目录十分有用。  如果希望验证多个模型 \(`/mode:ValidateArtifacts`\)，这样做也很有用。|  
|`/refcsdl:`\<file\>|指定用于解析源 .csdl 文件中的任何引用的其他 .csdl 文件。  （源 .csdl 文件是 `/incsdl` 选项指定的文件）。  `/refcsdl` 文件包含源 .csdl 文件所依赖的类型。  此参数可多次指定。|  
|`/inmsl:`\<file\>|指定 .msl 文件或 .msl 文件所在的目录。  此参数可多次指定，这样可以指定多个目录或 .msl 文件。  当概念模型跨多个文件拆分时，对于生成视图 \(`/mode:ViewGeneration`\)，指定多个目录十分有用。  如果希望验证多个模型 \(`/mode:ValidateArtifacts`\)，这样做也很有用。|  
|`/inssdl:`\<file\>|指定 .ssdl 文件或 .ssdl 文件所在的目录。  此参数可多次指定，这样可以指定多个目录或 .ssdl 文件。  如果希望验证多个模型 \(`(/mode:ValidateArtifacts)`\)，这样做很有用。|  
|`/outcsdl:`\<file\>|指定将创建的 .csdl 文件的名称。|  
|`/outmsl:`\<file\>|指定将创建的 .msl 文件的名称。|  
|`/outssdl:`\<file\>|指定将创建的 .ssdl 文件的名称。|  
|`/outobjectlayer:`\<file\>|指定包含根据 .csdl 文件生成的对象的源代码文件的名称。|  
|`/outviews:`\<file\>|指定包含所生成的视图的源代码文件的名称。|  
|`/language:`\[VB&#124;CSharp\]|指定生成的源代码文件的语言。  默认语言为 C\#。|  
|`/namespace:`\<string\>|指定要使用的模型命名空间。  命名空间是在运行 `/mode:FullGeneration` 或 `/mode:FromSSDLGeneration` 时在 .csdl 文件中设置的。  在运行 `/mode:EntityClassGeneration` 时不使用该命名空间。|  
|`/entitycontainer:`\<string\>|指定要应用于生成的模型和映射文件中 `<EntityContainer>` 元素的名称。|  
|`/pl[uralize]`|对概念模型中 `Entity`、`EntitySet` 和 `NavigationProperty` 名称的单复数形式应用英语语言规则。  此选项将执行以下操作：<br /><br /> -   使所有 `EntityType` 名称采用单数形式。<br />-   使所有 `EntitySet` 名称采用复数形式。<br />-   对于每个最多返回一个实体的 `NavigationProperty`，使名称采用单数形式。<br />-   对于每个返回多个实体的 `NavigationProperty`，使名称采用复数形式。|  
|`/SupressForeignKeyProperties or /nofk`|防止外键列公开为概念模型中实体类型上的标量属性。|  
|`/help` 或`?`|显示该工具的命令语法和选项。|  
|`/nologo`|禁止显示版权信息。|  
|`/targetversion:` \<string\>|将用于编译生成的代码的 .NET Framework 版本。  支持的版本是 4 和 4.5。  默认值为 4。|  
  
## 本节内容  
 [如何：使用 EdmGen.exe 生成模型和映射文件](../../../../../docs/framework/data/adonet/ef/how-to-use-edmgen-exe-to-generate-the-model-and-mapping-files.md)  
  
 [如何：使用 EdmGen.exe 生成对象层代码](../../../../../docs/framework/data/adonet/ef/how-to-use-edmgen-exe-to-generate-object-layer-code.md)  
  
 [如何：使用 EdmGen.exe 验证模型和映射文件](../../../../../docs/framework/data/adonet/ef/how-to-use-edmgen-exe-to-validate-model-and-mapping-files.md)  
  
## 请参阅  
 [ADO.NET Entity Data Model  Tools](http://msdn.microsoft.com/zh-cn/91076853-0881-421b-837a-f582f36be527)   
 [实体数据模型](../../../../../docs/framework/data/adonet/entity-data-model.md)   
 [CSDL、SSDL 和 MSL 规范](../../../../../docs/framework/data/adonet/ef/language-reference/csdl-ssdl-and-msl-specifications.md)