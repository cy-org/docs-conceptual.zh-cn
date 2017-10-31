---
title: "Walkthrough: Using BatchBlock and BatchedJoinBlock to Improve Efficiency | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-standard"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Task Parallel Library, dataflows"
  - "TPL dataflow library, improving efficiency"
ms.assetid: 5beb4983-80c2-4f60-8c51-a07f9fd94cb3
caps.latest.revision: 8
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 8
---
# Walkthrough: Using BatchBlock and BatchedJoinBlock to Improve Efficiency
TPL 数据流库提供 <xref:System.Threading.Tasks.Dataflow.BatchBlock%601?displayProperty=fullName> 和 <xref:System.Threading.Tasks.Dataflow.BatchedJoinBlock%602?displayProperty=fullName> 类，这样您就可以从一个或多个数据源接受或缓冲数据然后将该缓冲区的数据作为集合进行传播。  当从一个或多个源收集数据然后处理多个数据元素作为批时，此批处理机制很有用。  例如，考虑使用数据流向数据库插入记录的应用程序。  如果多个项目同时插入而不是按顺序一次一个，此操作会更高效。  本文档介绍如何使用 <xref:System.Threading.Tasks.Dataflow.BatchBlock%601> 类来提高这样的数据库插入操作的效率。  它还描述如何使用 <xref:System.Threading.Tasks.Dataflow.BatchedJoinBlock%602> 类来获取结果和当程序从数据库读取数据时产生的异常。  
  
> [!TIP]
>  TPL 数据流库 \(<xref:System.Threading.Tasks.Dataflow?displayProperty=fullName> 命名空间\) 不是由 [!INCLUDE[net_v45](../../../includes/net-v45-md.md)]分布的。  若要安装<xref:System.Threading.Tasks.Dataflow>命名空间，打开 [!INCLUDE[vs_dev11_long](../../../includes/vs-dev11-long-md.md)]中的项目，从`Microsoft.Tpl.Dataflow`包中选择**Manage NuGet Packages**并在线搜索。  
  
## 系统必备  
  
1.  在开始本演练之前，请阅读 [数据流](../../../docs/standard/parallel-programming/dataflow-task-parallel-library.md) 的连接块部分。  
  
2.  确保您具有 Northwind 数据库的副本Northwind.sdf ，并且在您的计算机上可用。  此文件通常位于文件夹 %Program Files%\\Microsoft SQL Server compact edition\\v3.5\\Samples\\。  
  
    > [!IMPORTANT]
    >  在 windows 的某些版本中，如果 [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] 在非管理员模式下运行，则无法连接到 Northwind.sdf。  若要连接到 Northwind.sdf，“以管理员身份运行”启动 [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] 或 [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] 命令提示。  
  
 本演练包含以下各节：  
  
-   [创建控制台应用程序](#creating)  
  
-   [定义员工类](#employeeClass)  
  
-   [定义员工数据库操作](#operations)  
  
-   [不使用缓冲添加员工数据到数据库](#nonBuffering)  
  
-   [使用缓冲添加员工数据到数据库。](#buffering)  
  
-   [使用缓冲连接读取数据库的中员工数据](#bufferedJoin)  
  
-   [完整示例](#complete)  
  
<a name="creating"></a>   
## 创建控制台应用程序  
  
<a name="consoleApp"></a>   
1.  在[!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)]中，创建一个 Visual Basic 或 Visual C\# “控制台应用程序” 项目。  在本文档，该项目命名为 `DataflowBatchDatabase`。  
  
2.  在项目中，向 System.Data.SqlServerCe.dll 及 System.Threading.Tasks.Dataflow.dll 添加引用。  
  
3.  确保 Form1.cs \( [!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)]的 Form1.vb\) 包含下面的 `using` \(在 [!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)]中的`Imports` \) 语句。  
  
     [!code-csharp[TPLDataflow_BatchDatabase#1](../../../samples/snippets/csharp/VS_Snippets_Misc/tpldataflow_batchdatabase/cs/dataflowbatchdatabase.cs#1)]
     [!code-vb[TPLDataflow_BatchDatabase#1](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpldataflow_batchdatabase/vb/dataflowbatchdatabase.vb#1)]  
  
4.  将以下数据成员添加到`Program`类中。  
  
     [!code-csharp[TPLDataflow_BatchDatabase#2](../../../samples/snippets/csharp/VS_Snippets_Misc/tpldataflow_batchdatabase/cs/dataflowbatchdatabase.cs#2)]
     [!code-vb[TPLDataflow_BatchDatabase#2](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpldataflow_batchdatabase/vb/dataflowbatchdatabase.vb#2)]  
  
<a name="employeeClass"></a>   
## 定义员工类  
 把`Employee` 类添加 `Program` 类。  
  
 [!code-csharp[TPLDataflow_BatchDatabase#3](../../../samples/snippets/csharp/VS_Snippets_Misc/tpldataflow_batchdatabase/cs/dataflowbatchdatabase.cs#3)]
 [!code-vb[TPLDataflow_BatchDatabase#3](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpldataflow_batchdatabase/vb/dataflowbatchdatabase.vb#3)]  
  
 `Employee` 类包含有三个属性， `EmployeeID`，`LastName` 和 `FirstName` 。  这些属性对应于Northwind 数据库的`Employees` 表中的 `Employee ID`、`Last Name`和 `First Name` 列。   此演示，`Employee` 类还定义了 `Random` 方法，该方法创建一个属性为任意值的 `Employee` 对象。  
  
<a name="operations"></a>   
## 定义员工数据库操作  
 在`Program` 类中添加 `InsertEmployees` ， `GetEmployeeCount` 和 `GetEmployeeID` 方法。  
  
 [!code-csharp[TPLDataflow_BatchDatabase#4](../../../samples/snippets/csharp/VS_Snippets_Misc/tpldataflow_batchdatabase/cs/dataflowbatchdatabase.cs#4)]
 [!code-vb[TPLDataflow_BatchDatabase#4](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpldataflow_batchdatabase/vb/dataflowbatchdatabase.vb#4)]  
  
 `InsertEmployees` 方法添加新员工记录到数据库。  `GetEmployeeCount` 方法在 `Employees` 表中检索项的数目。  `GetEmployeeID` 方法根据提供的名称检索第一个具有标识符的员工。  上述每种方法采用连接字符串连接到 Northwind 数据库并使用 `System.Data.SqlServerCe` 命名空间中的函数与数据库通信。  
  
<a name="nonBuffering"></a>   
## 不使用缓冲添加员工数据到数据库  
 在`Program`类中添加 `AddEmployees`和， `PostRandomEmployees` 方法。  
  
 [!code-csharp[TPLDataflow_BatchDatabase#5](../../../samples/snippets/csharp/VS_Snippets_Misc/tpldataflow_batchdatabase/cs/dataflowbatchdatabase.cs#5)]
 [!code-vb[TPLDataflow_BatchDatabase#5](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpldataflow_batchdatabase/vb/dataflowbatchdatabase.vb#5)]  
  
 `AddEmployees` 方法使用数据流添加任意雇员数据到数据库。   它创建一个调用 `InsertEmployees` 方法将雇员输入到数据库的 <xref:System.Threading.Tasks.Dataflow.ActionBlock%601>对象。   `AddEmployees` 然后调用 `PostRandomEmployees`方法将多个 `Employee` 对象传送到<xref:System.Threading.Tasks.Dataflow.ActionBlock%601>。  `AddEmployees` 方法等待所有插入操作完成。  
  
<a name="buffering"></a>   
## 使用缓冲添加员工数据到数据库。  
 添加到 `Program` 类的 `AddEmployeesBatched`方法。  
  
 [!code-csharp[TPLDataflow_BatchDatabase#6](../../../samples/snippets/csharp/VS_Snippets_Misc/tpldataflow_batchdatabase/cs/dataflowbatchdatabase.cs#6)]
 [!code-vb[TPLDataflow_BatchDatabase#6](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpldataflow_batchdatabase/vb/dataflowbatchdatabase.vb#6)]  
  
 此方法类似于 `AddEmployees`，除了它还使用 <xref:System.Threading.Tasks.Dataflow.BatchBlock%601> 类缓冲多个发送到 <xref:System.Threading.Tasks.Dataflow.ActionBlock%601> 对象之前的 `Employee` 对象。  由于 <xref:System.Threading.Tasks.Dataflow.BatchBlock%601> 类传播多个元素作为集合，修改 <xref:System.Threading.Tasks.Dataflow.ActionBlock%601> 对象使其可以操作 `Employee` 对象数组。  像 `AddEmployees` 方法，`AddEmployeesBatched` 调用 `PostRandomEmployees` 方法发送多个 `Employee` 对象一样；但是，`AddEmployeesBatched` 发送这些对象到 <xref:System.Threading.Tasks.Dataflow.BatchBlock%601> 对象。  `AddEmployeesBatched`  方法也等待所有插入操作完成。  
  
<a name="bufferedJoin"></a>   
## 使用缓冲连接读取数据库的中员工数据  
 添加到 `Program` 类的 `GetRandomEmployees`方法。  
  
 [!code-csharp[TPLDataflow_BatchDatabase#7](../../../samples/snippets/csharp/VS_Snippets_Misc/tpldataflow_batchdatabase/cs/dataflowbatchdatabase.cs#7)]
 [!code-vb[TPLDataflow_BatchDatabase#7](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpldataflow_batchdatabase/vb/dataflowbatchdatabase.vb#7)]  
  
 此方法打印有关任意雇员的信息传递给控制台。  它创建若干任意 `Employee` 对象并调用 `GetEmployeeID` 方法检索每个对象的唯一标识符。  因为如果不存在给定的名称匹配的雇员 `GetEmployeeID` 方法会抛出异常，`GetRandomEmployees` 方法使用 <xref:System.Threading.Tasks.Dataflow.BatchedJoinBlock%602> 类，如果成功调用 `GetEmployeeID`则存储 `Employee` 对象，失败则存储 <xref:System.Exception?displayProperty=fullName> 对象。  在此示例中的 <xref:System.Threading.Tasks.Dataflow.ActionBlock%601> 对象作用于 `Employee` 对象，保存 <xref:System.Exception> 对象列表和 <xref:System.Tuple%602> 对象对表。  在收到的 `Employee` 和 <xref:System.Exception> 对象的总和次数等于批量时，<xref:System.Threading.Tasks.Dataflow.BatchedJoinBlock%602> 对象传播此数据。  
  
<a name="complete"></a>   
## 完整示例  
 下面的示例演示完整的代码。  `Main` 方法比较执行批处理数据库插入需要的时间与执行非批处理数据库插入的时间。  它还演示如何使用缓冲连接读取数据库的 employees 数据并报告错误。  
  
 [!code-csharp[TPLDataflow_BatchDatabase#100](../../../samples/snippets/csharp/VS_Snippets_Misc/tpldataflow_batchdatabase/cs/dataflowbatchdatabase.cs#100)]
 [!code-vb[TPLDataflow_BatchDatabase#100](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpldataflow_batchdatabase/vb/dataflowbatchdatabase.vb#100)]  
  
## 请参阅  
 [数据流](../../../docs/standard/parallel-programming/dataflow-task-parallel-library.md)