---
title: "演练：在 WPF 应用程序中缓存应用程序数据 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-wpf"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "缓存 [.NET Framework]"
  - "缓存 [WPF]"
  - "演练 [WPF], 缓存"
ms.assetid: dac2c9ce-042b-4d23-91eb-28f584415cef
caps.latest.revision: 25
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 25
---
# 演练：在 WPF 应用程序中缓存应用程序数据
缓存使您能够在内存中存储数据以实现快速访问。  当再次访问数据时，应用程序可以从缓存获取数据，而不是从原始源检索数据。  这可以改进性能和伸缩性。  此外，缓存还使数据在数据源临时不可用时可用。  
  
 [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] 提供在 [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] 应用程序可以使用缓存的类。  这些类在 <xref:System.Runtime.Caching> 命名空间。  
  
> [!NOTE]
>  <xref:System.Runtime.Caching> 命名空间是 [!INCLUDE[net_v40_short](../../../../includes/net-v40-short-md.md)] 中新增的命名空间。  此命名空间使缓存对所有的 [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] 应用程序可用。  在 [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] 的早期版本中，缓存仅可用于 <xref:System.Web> 命名空间，因此在 ASP.NET 类上需要有依赖项。  
  
 本演练演示如何在 [!INCLUDE[TLA#tla_winclient](../../../../includes/tlasharptla-winclient-md.md)] 应用程序中使用 [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] 中提供的缓存功能。  在本演练中，您将缓存文本文件的内容。  
  
 本演练涉及以下任务：  
  
-   创建 WPF 应用程序项目。  
  
-   添加对 [!INCLUDE[net_v40_short](../../../../includes/net-v40-short-md.md)] 的引用。  
  
-   初始化缓存。  
  
-   添加包含文本文件内容的缓存项。  
  
-   为缓存项提供逐出策略。  
  
-   监视缓存文件的路径，并向缓存实例通知被监视项的更改情况。  
  
## 系统必备  
 若要完成本演练，您需要：  
  
-   Microsoft [!INCLUDE[vs_dev10_long](../../../../includes/vs-dev10-long-md.md)]。  
  
-   包含少量文本的文本文件。  （将在消息框中显示文本文件的内容。） 本演练中演示的代码假定您使用以下文件：  
  
     `c:\cache\cacheText.txt`  
  
     但是，您可以使用任何文本文件，并对本演练中的代码进行少量更改。  
  
## 创建 WPF 应用程序项目  
 您将首先创建一个 WPF 应用程序项目。  
  
#### 创建 WPF 应用程序  
  
1.  启动 [!INCLUDE[vsprvs](../../../../includes/vsprvs-md.md)]。  
  
2.  在**“文件”**菜单中单击**“新建”**，再单击**“新建项目”**。  
  
     将显示**“新建项目”**对话框。  
  
3.  在**“已安装的模板”**下，选择要使用的编程语言（**“Visual Basic”**或**“Visual C\#”**）。  
  
4.  在**“新建项目”**对话框中，选择**“WPF 应用程序”**。  
  
    > [!NOTE]
    >  如果没有看到**“WPF 应用程序”**模板，请确保您以支持 WPF 的 [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] 版本为目标。  在**“新建项目”**对话框中，从列表选择 [!INCLUDE[net_v40_short](../../../../includes/net-v40-short-md.md)]。  
  
5.  在**“名称”**文本框中，输入项目的名称。  例如，您可以输入 WPFCaching。  
  
6.  选中**“创建解决方案的目录”**复选框。  
  
7.  单击**“确定”**。  
  
     WPF 设计器会在**“设计”**视图中打开，并显示 MainWindow.xaml 文件。  [!INCLUDE[vsprvs](../../../../includes/vsprvs-md.md)] 会创建**“我的项目”**文件夹、Application.xaml 文件和 MainWindow.xaml 文件。  
  
## 以 .NET Framework 为目标并添加对缓存程序集的引用  
 默认情况下，WPF 应用程序以 [!INCLUDE[net_client_v40_long](../../../../includes/net-client-v40-long-md.md)] 为目标。  若要在 WPF 应用程序中使用 <xref:System.Runtime.Caching> 命名空间，应用程序必须以 [!INCLUDE[net_v40_short](../../../../includes/net-v40-short-md.md)]（而不是 [!INCLUDE[net_client_v40_long](../../../../includes/net-client-v40-long-md.md)]）为目标，并且必须包含对该命名空间的引用。  
  
 因此，下一步是更改 .NET Framework 目标并添加对 <xref:System.Runtime.Caching> 命名空间的引用。  
  
> [!NOTE]
>  更改 .NET Framework 目标的过程在 Visual Basic 项目和 Visual C\# 项目中是不同的。  
  
#### 在 Visual Basic 中更改目标 .NET Framework  
  
1.  在**“解决方案资源管理器”**中右击项目名称，然后单击**“属性”**。  
  
     此时会显示应用程序的属性窗口。  
  
2.  单击**“编译”**选项卡。  
  
3.  在该窗口底部，单击**“高级编译选项…”**。  
  
     此时会显示**“高级编译器设置”**对话框。  
  
4.  在 **目标框架 \(所有配置\)** 列表中，选择 [!INCLUDE[net_v40_short](../../../../includes/net-v40-short-md.md)]。  \(不要选择 [!INCLUDE[net_client_v40_long](../../../../includes/net-client-v40-long-md.md)]。\)  
  
5.  单击**“确定”**。  
  
     将显示**“目标 Framework 更改”**对话框。  
  
6.  在**“目标 Framework 更改”**对话框中，单击**“是”**。  
  
     项目将关闭，然后重新打开。  
  
7.  通过以下这些步骤添加对缓存程序集的引用：  
  
    1.  在**“解决方案资源管理器”**中，右击项目名称，然后单击**“添加引用”**。  
  
    2.  选择**“.NET”**选项卡，选择 `System.Runtime.Caching`，然后单击**“确定”**。  
  
#### 在 Visual C\# 项目中更改目标 .NET Framework  
  
1.  在**“解决方案资源管理器”**中右击项目名称，然后单击**“属性”**。  
  
     此时会显示应用程序的属性窗口。  
  
2.  单击**“应用程序”**选项卡。  
  
3.  在**“目标 Framework”**列表中，选择 [!INCLUDE[net_v40_short](../../../../includes/net-v40-short-md.md)]。  （不要选择**“.NET Framework 4 Client Profile”**。）  
  
4.  通过以下这些步骤添加对缓存程序集的引用：  
  
    1.  右击**“引用”**文件夹，然后单击**“添加引用”**。  
  
    2.  选择**“.NET”**选项卡，选择 `System.Runtime.Caching`，然后单击**“确定”**。  
  
## 向 WPF 窗口添加按钮  
 接下来，您将添加一个按钮控件，并为该按钮的 `Click` 事件创建事件处理程序。  稍后将添加代码，以便在单击该按钮时，会缓存并显示文本文件的内容。  
  
#### 添加按钮控件  
  
1.  在**“解决方案资源管理器”**中，双击 MainWindow.xaml 文件以将其打开。  
  
2.  在**“工具箱”**中的**“通用 WPF 控件”**下，将一个 `Button` 控件拖到 `MainWindow` 窗口中。  
  
3.  在**“属性”**窗口中，将 `Button` 控件的 `Content` 属性设置为“Get Cache”。  
  
## 初始化缓存并缓存某项  
 接下来，您将添加代码来执行以下任务：  
  
-   创建一个缓存类实例，也就是说，您将实例化新的 <xref:System.Runtime.Caching.MemoryCache> 对象。  
  
-   指定缓存将使用 <xref:System.Runtime.Caching.HostFileChangeMonitor> 对象来监视文本文件中的更改。  
  
-   读取文本文件并将其内容缓存为缓存项。  
  
-   显示缓存文本文件的内容。  
  
#### 创建缓存对象  
  
1.  双击刚添加的按钮以在 MainWindow.xaml.cs 或 MainWindow.Xaml.vb 文件中创建一个事件处理程序。  
  
2.  在文件的顶部（在类声明前面），添加以下 `Imports` \(Visual Basic\) 或 `using` \(C\#\) 语句：  
  
    ```csharp  
    using System.Runtime.Caching;  
    using System.IO;  
    ```  
  
    ```vb  
    Imports System.Runtime.Caching  
    Imports System.IO  
    ```  
  
3.  在事件处理程序中，添加以下代码以实例化缓存对象：  
  
    ```csharp  
    ObjectCache cache = MemoryCache.Default;  
    ```  
  
    ```vb  
    Dim cache As ObjectCache = MemoryCache.Default  
    ```  
  
     <xref:System.Runtime.Caching.ObjectCache> 类是一个提供内存中对象缓存的内置类。  
  
4.  添加以下代码以读取名为 `filecontents` 的缓存项的内容：  
  
    ```vb  
    Dim fileContents As String = TryCast(cache("filecontents"), String)  
    ```  
  
    ```csharp  
    string fileContents = cache["filecontents"] as string;  
    ```  
  
5.  添加以下代码以检查是否存在名为 `filecontents` 的缓存项：  
  
    ```vb  
    If fileContents Is Nothing Then  
  
    End If  
    ```  
  
    ```csharp  
    if (fileContents == null)  
    {  
  
    }  
    ```  
  
     如果指定的缓存项不存在，则您必须读取该文本文件并将其作为一个缓存项添加到缓存。  
  
6.  在 `if/then` 块中，添加以下代码以创建一个新的 <xref:System.Runtime.Caching.CacheItemPolicy> 对象，该对象指定缓存项将在 10 秒后过期。  
  
    ```vb  
    Dim policy As New CacheItemPolicy()  
    policy.AbsoluteExpiration = DateTimeOffset.Now.AddSeconds(10.0)  
    ```  
  
    ```csharp  
    CacheItemPolicy policy = new CacheItemPolicy();  
    policy.AbsoluteExpiration = DateTimeOffset.Now.AddSeconds(10.0);  
    ```  
  
     如果未提供任何逐出或过期信息，则默认值为 <xref:System.Runtime.Caching.ObjectCache.InfiniteAbsoluteExpiration>，这意味着缓存项永远不会仅基于绝对时间而过期。  相反，缓存项仅当存在内存压力时才过期。  最佳做法是，您应始终明确提供一个绝对过期或可调过期。  
  
7.  在 `if/then` 块内部，在上一步中所添加的代码后面添加以下代码，以便为要监视的文件路径创建一个集合，并向该集合中添加文本文件的路径：  
  
    ```vb  
    Dim filePaths As New List(Of String)()  
    filePaths.Add("c:\cache\cacheText.txt")  
    ```  
  
    ```csharp  
    List<string> filePaths = new List<string>();  
    filePaths.Add("c:\\cache\\cacheText.txt");  
    ```  
  
    > [!NOTE]
    >  如果要使用的文本文件不是 `c:\cache\cacheText.txt`，请指定要使用的文本文件所处位置的路径。  
  
8.  在上一步中所添加的代码后面添加以下代码，以便将新的 <xref:System.Runtime.Caching.HostFileChangeMonitor> 对象添加到缓存项的更改监视器集合：  
  
    ```vb  
    policy.ChangeMonitors.Add(New HostFileChangeMonitor(filePaths))  
    ```  
  
    ```csharp  
    policy.ChangeMonitors.Add(new HostFileChangeMonitor(filePaths));  
    ```  
  
     <xref:System.Runtime.Caching.HostFileChangeMonitor> 对象将监视文本文件的路径并向缓存通知是否发生更改。  在此示例中，如果文件的内容发生更改，则缓存项将过期。  
  
9. 在上一步中所添加的代码后面添加以下代码，以读取文本文件的内容：  
  
    ```vb  
    fileContents = File.ReadAllText("c:\cache\cacheText.txt") & vbCrLf & DateTime.Now.ToString()  
    ```  
  
    ```csharp  
    fileContents = File.ReadAllText("c:\\cache\\cacheText.txt") + + "\n" + DateTime.Now;   
    ```  
  
     会添加日期和时间戳，以便您能够看到缓存项何时过期。  
  
10. 在上一步中所添加的代码后面添加以下代码，以将文件内容作为 <xref:System.Runtime.Caching.CacheItem> 实例插入到缓存对象中：  
  
    ```vb  
    cache.Set("filecontents", fileContents, policy)  
    ```  
  
    ```csharp  
    cache.Set("filecontents", fileContents, policy);  
    ```  
  
     通过作为参数传递前面创建的 <xref:System.Runtime.Caching.CacheItemPolicy> 对象，来指定有关应如何逐出缓存项的信息。  
  
11. 在 `if/then` 块的后面添加以下代码，以便在消息框中显示缓存的文件内容：  
  
    ```vb  
    MessageBox.Show(fileContents)  
    ```  
  
    ```csharp  
    MessageBox.Show(fileContents);  
    ```  
  
12. 在**“生成”**菜单中，单击**“生成 WPFCaching”**以生成项目。  
  
## 在 WPF 应用程序中测试缓存  
 您现在可以测试应用程序。  
  
#### 在 WPF 应用程序中测试缓存  
  
1.  按 Ctrl\+F5 以运行应用程序。  
  
     将显示 `MainWindow` 窗口。  
  
2.  单击**“Get Cache”**。  
  
     文本文件的缓存内容会显示在消息框中。  请注意文件上的时间戳。  
  
3.  关闭该消息框，然后再次单击**“Get Cache”** **。**  
  
     时间戳未更改。  这将指示显示缓存的内容。  
  
4.  等待 10 秒或更长时间，然后单击**“Get Cache”**。  
  
     这次将显示一个新的时间戳。  这指示策略让缓存项过期并显示新的缓存内容。  
  
5.  在文本编辑器中，打开创建的文本文件。  不要进行任何更改。  
  
6.  关闭该消息框，然后再次单击**“Get Cache”** **。**  
  
     再次注意时间戳。  
  
7.  对文本文件进行更改，然后保存文件。  
  
8.  关闭该消息框，然后再次单击**“Get Cache”**。  
  
     此消息框包含文本文件的更新内容和新的时间戳。  这指示主机文件更改监视器在您更改文件时立即逐出了缓存项，即使绝对超时时间尚未过期也是如此。  
  
    > [!NOTE]
    >  您可将逐出时间提高到 20 秒或更长，以允许您在文件中进行更长时间的更改。  
  
## 代码示例  
 完成本演练后，您创建的项目的代码与下面的示例类似。  
  
 [!code-csharp[CachingWPFApplications#1](../../../../samples/snippets/csharp/VS_Snippets_Wpf/CachingWPFApplications/CSharp/MainWindow.xaml.cs#1)]
 [!code-vb[CachingWPFApplications#1](../../../../samples/snippets/visualbasic/VS_Snippets_Wpf/CachingWPFApplications/VisualBasic/MainWindow.xaml.vb#1)]  
  
## 请参阅  
 <xref:System.Runtime.Caching.MemoryCache>   
 <xref:System.Runtime.Caching.ObjectCache>   
 <xref:System.Runtime.Caching>   
 [.NET Framework 应用程序中的缓存](../../../../docs/framework/performance/caching-in-net-framework-applications.md)