---
title: "如何：在 Visual Studio 中创建 LINQ to DataSet 项目 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 49ba6cb0-cdd2-4571-aeaa-25bf0f40e9b3
caps.latest.revision: 2
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 2
---
# 如何：在 Visual Studio 中创建 LINQ to DataSet 项目
不同类型的 [!INCLUDE[vbteclinq](../../../../includes/vbteclinq-md.md)] 项目需要某些导入的命名空间 \(Visual Basic\) 或 `using` 指令 \(C\#\) 和引用。  最低要求是对 System.Core.dll 的引用和针对 <xref:System.Linq> 的 `using` 指令。  默认情况下，如果创建一个新的 [!INCLUDE[csharp_orcas_long](../../../../includes/csharp-orcas-long-md.md)] 项目，这些都可以自动提供。  [!INCLUDE[linq_dataset](../../../../includes/linq-dataset-md.md)] 还需要对 System.Data.dll 和 System.Data.DataSetExtensions.dll 的引用以及 `Imports` \(Visual Basic\) 或 `using` \(C\#\) 指令。  
  
 如果您要从早期版本的 Visual Studio 升级某个项目，则可能必须手动提供这些与 LINQ 相关的引用。  您可能还必须将项目手动设置为面向 .NET Framework 3.5 版。  
  
> [!NOTE]
>  如果要从命令提示符执行生成，则必须手动引用 `drive`**:**\\Program Files\\Reference Assemblies\\Microsoft\\Framework\\v3.5 中与 LINQ 相关的 DLL。  
  
### 面向 .NET Framework 3.5  
  
1.  在 [!INCLUDE[vs_orcas_long](../../../../includes/vs-orcas-long-md.md)] 中，创建一个新的 Visual Basic 或 C\# 项目。或者，您可以打开一个在 Visual Studio 2005 中创建的 Visual Basic 或 C\# 项目，并按照提示将其转换为 [!INCLUDE[vs_current_long](../../../../includes/vs-current-long-md.md)] 项目。  
  
2.  对于 C\# 项目，单击**“项目”**菜单，然后单击**“属性”**。  
  
    1.  在**“应用程序”**属性页的**“目标 Framework”**下拉列表中选择“.NET Framework 3.5”。  
  
3.  对于 Visual Basic 项目，单击**“项目”**菜单，然后单击**“属性”**。  
  
    1.  在**“编译”**属性页，单击**“高级编译选项”**，然后在**“目标 Framework\(所有配置\)”**下拉列表中选择“.NET Framework 3.5”。  
  
4.  在**“项目”**菜单上，单击**“添加引用”**，单击**“.NET”**选项卡，向下滚动到**“System.Core”**并单击，然后单击**“确定”**。  
  
5.  向源代码文件或项目中添加用于 <xref:System.Linq> 的 `using` 指令或导入的命名空间。  
  
     有关详细信息，请参阅[using 指令](../Topic/using%20Directive%20\(C%23%20Reference\).md)或[如何：添加或移除导入的命名空间 \(Visual Basic\)](../Topic/How%20to:%20Add%20or%20Remove%20Imported%20Namespaces%20\(Visual%20Basic\).md)。  
  
### 启用 LINQ to DataSet 功能  
  
1.  必要时，按照本主题前面的步骤添加对 System.Core.dll 的引用和用于 System.Linq 的 `using` 指令或导入的命名空间。  
  
2.  在 C\# 或 Visual Basic 中，单击**“项目”**菜单，然后单击**“添加引用”**。  
  
3.  在**“添加引用”**对话框中，单击**“.NET”**选项卡（如果它不在最前面）。  向下滚动到**“System.Data”**和**“System.Data.DataSetExtensions”**并单击它们。  单击**“确定”**按钮。  
  
4.  向源代码文件或项目中添加用于 <xref:System.Data> 的 `using` 指令或导入的命名空间。  有关详细信息，请参阅[using 指令](../Topic/using%20Directive%20\(C%23%20Reference\).md)或[如何：添加或移除导入的命名空间 \(Visual Basic\)](../Topic/How%20to:%20Add%20or%20Remove%20Imported%20Namespaces%20\(Visual%20Basic\).md)。  
  
5.  添加对 System.Data.DataSetExtensions.dll 的引用以便可以使用 LINQ to Dataset 的功能。  添加对 System.Data.dll 的引用（如果尚不存在）。  
  
6.  或者，添加用于 `System.Data.Common` 或 `System.Data.SqlClient` 的 `using` 指令或导入的命名空间，具体取决于如何连接到数据库。  
  
## 请参阅  
 [入门](../../../../docs/framework/data/adonet/getting-started-linq-to-dataset.md)   
 [Getting Started with LINQ](http://msdn.microsoft.com/zh-cn/6cc9af04-950a-4cc3-83d4-2aeb4abe4de9)