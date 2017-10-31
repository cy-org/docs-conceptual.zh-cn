---
title: "使用 .NET Core 创建 REST 客户端"
description: "此教程将介绍 .NET Core 和 C# 语言的许多功能。"
keywords: .NET, .NET Core
author: BillWagner
ms.author: wiwagn
ms.date: 03/06/2017
ms.topic: article
ms.prod: .net-core
ms.technology: devlang-csharp
ms.devlang: csharp
ms.assetid: 51033ce2-7a53-4cdd-966d-9da15c8204d2
ms.translationtype: HT
ms.sourcegitcommit: b647c5dc4e565f9813212d75fab4a2e46c1a47b9
ms.openlocfilehash: 8c747f65dca44fcca25fe67dccaa897561eefcc7
ms.contentlocale: zh-cn
ms.lasthandoff: 09/12/2017

---

# <a name="rest-client"></a>REST 客户端

## <a name="introduction"></a>介绍
此教程将介绍 .NET Core 和 C# 语言的许多功能。 你将了解：
*   .NET Core 命令行接口 (CLI) 的基础知识。
*   C# 语言功能概述。
*   如何使用 NuGet 管理依赖项
*   HTTP 通信
*   如何处理 JSON 信息
*   如何管理含特性的配置。 

将生成一个应用程序，向 GitHub 上的 REST 服务发出 HTTP 请求。 需要读取 JSON 格式的信息，并将相应的 JSON 数据包转换成 C# 对象。 最后将了解如何使用 C# 对象。

此教程将介绍许多功能。 我们将逐个生成这些功能。

如果想要按照针对本主题的[最终示例](https://github.com/dotnet/docs/tree/master/samples/csharp/getting-started/console-webapiclient)操作，可以下载它。 有关下载说明，请参阅[示例和教程](../../samples-and-tutorials/index.md#viewing-and-downloading-samples)。

## <a name="prerequisites"></a>先决条件
必须将计算机设置为运行 .Net Core。 有关安装说明，请访问 [.NET Core](https://www.microsoft.com/net/core) 页。 可以在 Windows、Linux、macOS 或 Docker 容器中运行此应用程序。 必须安装常用的代码编辑器。 在以下说明中，我们使用的是开放源代码跨平台编辑器 [Visual Studio Code](https://code.visualstudio.com/)。 不过，你可以使用习惯使用的任意工具。
## <a name="create-the-application"></a>创建应用程序
第一步是新建应用程序。 打开命令提示符，然后新建应用程序的目录。 将新建的目录设为当前目录。 在命令提示符处，键入命令 `dotnet new console`。 这将为基本的“Hello World”应用程序创建起始文件。

在开始进行修改之前，我们先来逐步了解一下如何运行简单的 Hello World 应用程序。 创建应用程序之后，在命令提示符处键入 `dotnet restore`。 此命令将运行 NuGet 包还原进程。 NuGet 是 .NET 程序包管理器。 此命令会下载项目缺少的所有依赖项。 由于这是一个新项目，尚无任何依赖项，因此首次运行只会下载 .NET Core 框架。 执行这一初始步骤后，只需运行 `dotnet restore`，即可添加新的依赖项包，或更新任意依赖项的版本。  

还原包后，运行 `dotnet build`。 这将运行生成引擎，并创建应用程序。 最后，执行 `dotnet run` 来运行应用程序。

## <a name="adding-new-dependencies"></a>添加新的依赖项
.NET Core 的主要设计目标之一是，最大限度地减少 .NET 框架安装大小。 .NET Core 应用程序框架只包含 .NET 完整框架的最常用元素。 如果应用程序需要使用其他库来生成某些功能，请将这些依赖项添加到 C# 项目 (*.csproj) 文件中。 对于我们的示例，将需要添加 `System.Runtime.Serialization.Json` 包，以便应用程序可以处理 JSON 响应。

打开 `csproj` 项目文件。 此文件的第一行应如下所示：

```xml
<Project Sdk="Microsoft.NET.Sdk">
```

在这行后面紧接着添加以下代码： 

```xml
   <ItemGroup>
      <PackageReference Include="System.Runtime.Serialization.Json" Version="4.3.0" />
   </ItemGroup> 
```
大多数代码编辑器都会完成这些库的不同版本。 通常需要使用所添加的任意包的最新版本。 不过，请务必确保所有包的版本均一致，且与 .NET Core 应用程序框架的版本一致。

进行这些更改之后，应该再次运行 `dotnet restore`，以便在系统上安装包。

## <a name="making-web-requests"></a>发出 Web 请求
现在，可以开始检索 Web 数据了。 在此应用程序中，需要读取 [GitHub API](https://developer.github.com/v3/) 返回的信息。 让我们在 [.NET Foundation](http://www.dotnetfoundation.org/) 的保护下读取项目信息。 先向 GitHub API 发出请求，以检索项目信息。 将用到终结点 [https://api.github.com/orgs/dotnet/repos](https://api.github.com/orgs/dotnet/repos)。 由于要检索这些项目的所有信息，因此将发出 HTTP GET 请求。
此外，浏览器也使用 HTTP GET 请求，以便你可以将相应的 URL 粘贴到浏览器，查看将要收到并处理的信息。

使用 @System.Net.Http.HttpClient 类发出 Web 请求。 与所有新式 .NET API 一样，@System.Net.Http.HttpClient 只支持长时间运行 API 的异步方法。
从异步方法入手。 将一边填充实现代码，一边生成应用程序功能。 首先，打开项目目录中的 `program.cs` 文件，然后向 `Program` 类添加以下方法：

```csharp
private static async Task ProcessRepositories()
{
    
}
```

需要在 `Main` 方法的最上面添加 `using` 语句，以便 C# 编译器能够识别 @System.Threading.Tasks.Task 类型：

```csharp
using System.Threading.Tasks;
```

如果此时生成项目，将会看到系统针对此方法生成的警告，因为其中不含任何 `await` 运算符，将以同步方式运行。 暂且忽略此警告；将在填充方法时添加 `await` 运算符。

接下来，将 `namespace` 语句中定义的命名空间从默认名称 `ConsoleApp` 重命名为 `WebAPIClient`。 我们稍后将在此命名空间中定义 `repo` 类。

接下来，将 `Main` 方法更新为调用此方法。 `ProcessRepositories` 方法会返回一个任务，不得在此任务完成前退出程序。 因此，必须使用 `Wait` 方法来阻止退出并等待任务完成：

```csharp
public static void Main(string[] args)
{
    ProcessRepositories().Wait();
}
```

现在，生成了一个不执行任何操作但具备异步功能的程序。 让我们回到 `ProcessRepositories` 方法，并填充它的第一个版本：

```csharp
private static async Task ProcessRepositories()
{
    var client = new HttpClient();
    client.DefaultRequestHeaders.Accept.Clear();
    client.DefaultRequestHeaders.Accept.Add(
        new MediaTypeWithQualityHeaderValue("application/vnd.github.v3+json"));
    client.DefaultRequestHeaders.Add("User-Agent", ".NET Foundation Repository Reporter");

    var stringTask = client.GetStringAsync("https://api.github.com/orgs/dotnet/repos");

    var msg = await stringTask;
    Console.Write(msg);
}
```

此外，为了让编译能够顺利进行，还需要在文件的最上面添加两个新的 using 语句：

```csharp
using System.Net.Http;
using System.Net.Http.Headers;
```

第一个版本发出 Web 请求来读取 .NET Foundation 组织下的所有存储库列表。 （.NET Foundation 的 gitHub ID 为“dotnet”）。 首先，新建一个 @System.Net.Http.HttpClient 。 此对象负责处理请求和响应。 接下来的几行代码将 @System.Net.Http.HttpClient 设置为处理此请求。 在第一行中，它被配置为接受 GitHub JSON 响应。
此格式仅为 JSON。 下一代码行将用户代理标头添加到此对象发出的所有请求中。 这两个标头均由 GitHub 服务器代码进行检查，必须使用它们，才能检索 GitHub 中的信息。

配置 @System.Net.Http.HttpClient 后，发出 Web 请求并检索响应。 在此第一个版本中，将使用 <xref:System.Net.Http.HttpClient.GetStringAsync(System.String)?displayProperty=fullname> 便捷方法。 此便捷方法先执行发出 Web 请求的任务，然后当返回请求时读取响应流，并从流中提取内容。 响应正文以 @System.String 的形式返回。 此字符串在任务完成时可用。 

此方法的最后两行代码用于等待任务完成，然后在控制台中打印输出响应。
生成并运行应用程序。 此时，生成警告不再显示，因为 `ProcessRepositories` 现在的确包含 `await` 运算符。 将看到很长的 JSON 格式文本。   

## <a name="processing-the-json-result"></a>处理 JSON 结果

此时，你已编写用于检索来自 Web 服务器的响应，并显示响应文本的代码。 接下来，让我们将相应的 JSON 响应转换成 C# 对象。

JSON 序列化程序将 JSON 数据转换成 C# 对象。 首要任务是定义 C# 类类型来包含要使用的此响应信息。 我们将慢慢生成，所以从包含存储库名称的简单 C# 类型入手：

```csharp
using System;

namespace WebAPIClient
{
    public class repo
    {
        public string name;
    }
}
``` 

将以上代码添加到“repo.cs”新文件中。 此版本的类表示处理 JSON 数据的最简单路径。 类名和成员名称与 JSON 数据包中使用的名称一致，而不是遵循以下 C# 约定。 稍后将通过提供某些配置特性进行修复。 此类展示了 JSON 序列化和反序列化的另一大功能，即并非 JSON 数据包中的所有字段都属于此类。
JSON 序列化程序将忽略所使用的类类型未包含的信息。
借助此功能，可更轻松地创建仅处理一部分 JSON 数据包字段的类型。

至此，你已创建类型，让我们来进行反序列化吧。 需要创建 @System.Runtime.Serialization.Json.DataContractJsonSerializer 对象。 此对象必须知道它检索的 JSON 数据包的预期 CLR 类型。 GitHub 发送的数据包中有一系列存储库，所以正确的类型是 `List<repo>`。 将下面这行代码添加到 `ProcessRepositories` 方法中：

```csharp
var serializer = new DataContractJsonSerializer(typeof(List<repo>));
```

由于要使用两个新的命名空间，因此还需要添加以下代码：

```csharp
using System.Collections.Generic;
using System.Runtime.Serialization.Json;
```

接下来，使用序列化程序将 JSON 转换成 C# 对象。 使用以下两行代码替换 `ProcessRepositories` 方法中对 @System.Net.Http.HttpClient.GetStringAsync(System.String) 的调用：

```csharp
var streamTask = client.GetStreamAsync("https://api.github.com/orgs/dotnet/repos");
var repositories = serializer.ReadObject(await streamTask) as List<repo>;
```

请注意，现在使用的是 @System.Net.Http.HttpClient.GetStreamAsync(System.String) ，而不是 @System.Net.Http.HttpClient.GetStringAsync(System.String) 。 序列化程序使用流（而不是字符串）作为其源。 让我们来看看上面第二行代码所使用的两项 C# 语言功能。 @System.Runtime.Serialization.Json.DataContractJsonSerializer.ReadObject(System.IO.Stream) 的自变量是 `await` 表达式。 Await 表达式可以出现在代码中的几乎任何位置，尽管到目前为止，你只在赋值语句中看到过它们。

其次，`as` 运算符将编译时类型 `object` 转换成 `List<repo>`。 声明 @System.Runtime.Serialization.Json.DataContractJsonSerializer.ReadObject(System.IO.Stream) 即声明其返回 <xref:System.Object?displayProperty=fullName> 类型的对象。 @System.Runtime.Serialization.Json.DataContractJsonSerializer.ReadObject(System.IO.Stream) 将返回你在构造它时指定的类型（在此教程中，为 `List<repo>`）。 如果转换失败，那么 `as` 运算符的计算结果为 `null`，而不是抛出异常。

即将完成此部分的操作。 至此，你已将 JSON 数据转换成 C# 对象，让我们来显示每个存储库的名称。 将以下代码行：

```csharp
var msg = await stringTask;   //**Deleted this
Console.Write(msg);
```

替换为：

```csharp
foreach (var repo in repositories)
    Console.WriteLine(repo.name);
```

编译并运行该应用程序。 将打印输出属于 .NET Foundation 的存储库的名称。

## <a name="controlling-serialization"></a>控制序列化

在添加更多功能之前，让我们来处理一下 `repo` 类型，使其更加遵循标准的 C# 约定。 为此，使用可控制 JSON 序列化程序的工作方式的*特性*对 `repo` 类型添加批注。 在此示例中，将使用这些特性来定义 JSON 键名和 C# 类名及成员名称之间的映射。 使用 `DataContract` 和 `DataMember` 这两个特性。 按照约定，所有特性类均以后缀 `Attribute` 结尾。 不过，在应用特性时无需使用此后缀。 

由于 `DataContract` 和 `DataMember` 特性位于不同的库中，因此需要将相应的库作为依赖项添加到 C# 项目文件中。 将下面这行代码添加到项目文件的 `<ItemGroup>` 部分中：

```xml
<PackageReference Include="System.Runtime.Serialization.Primitives" Version="4.3.0" />
```

保存项目文件后，运行 `dotnet restore` 来检索此包。

接下来，打开 `repo.cs` 文件。 让我们改用 Pascal 命名法，完整拼写出全称 `Repository`。 我们仍要将 JSON“repo”节点映射到此类型，所以需要将 `DataContract` 特性添加到类声明。 将特性的 `Name` 属性设置为映射到此类型的 JSON 节点的名称：

```csharp
[DataContract(Name="repo")]
public class Repository
```

由于 @System.Runtime.Serialization.DataContractAttribute 属于 @System.Runtime.Serialization 命名空间，因此需要在文件的最上面添加适当的 `using` 语句：

```csharp
using System.Runtime.Serialization;
```

由于已将 `repo` 类名更改为 `Repository`，因此需要在 Program.cs 中执行相同的名称更改（某些编辑器可能支持重命名重构，这样就可以自动执行此更改了）：

```csharp
var serializer = new DataContractJsonSerializer(typeof(List<Repository>));

// ...

var repositories = serializer.ReadObject(await streamTask) as List<Repository>;
```

接下来，让我们使用 @System.Runtime.Serialization.DataMemberAttribute 类对 `name` 字段执行相同的更改。 对 repo.cs 中的 `name` 字段声明执行以下更改：

```csharp
[DataMember(Name="name")]
public string Name;
```

此更改意味着需要更改用于在 program.cs 中写入每个存储库名称的代码：

```csharp
Console.WriteLine(repo.Name);
```

依次执行 `dotnet build` 和 `dotnet run`，以确保生成正确映射。 应能看到与之前一样的输出。 让我们先对 `Repository` 类执行另一项更改，然后再处理更多 Web 服务器属性。 `Name` 成员是可公开访问的字段。 这不是一种很好的面向对象的做法，因此，让我们将其更改为属性。 鉴于我们的目的，获取或设置属性时，我们不需要运行任何特定代码，但更改为属性，稍后就可以更加轻松地添加这些更改，同时还不会破坏任何使用 `Repository` 类的代码。

删除字段定义，然后将其替换为[自动实现的属性](../programming-guide/classes-and-structs/auto-implemented-properties.md)：

```csharp
public string Name { get; set; }
```

编译器生成 `get` 和 `set` 访问器的主体，以及用于存储名称的专用字段。 代码如下（可以手动键入）：

```csharp
public string Name 
{ 
    get { return this._name; }
    set { this._name = value; }
}
private string _name;
```

让我们在添加新功能前执行另一项更改。 `ProcessRepositories` 方法可以执行异步工作，并返回一组存储库。 我们将使用此方法返回 `List<Repository>`，并将用于写入信息的代码移到 `Main` 方法中。

更改 `ProcessRepositories` 的签名，以返回可生成 `Repository` 对象列表的任务：

```csharp
private static async Task<List<Repository>> ProcessRepositories()
```

然后，在处理 JSON 响应后仅返回存储库：

```csharp
var repositories = serializer.ReadObject(await streamTask) as List<Repository>;
return repositories;
```

编译器将生成返回内容的 `Task<T>` 对象，因为你已将此方法标记为 `async`。
然后，我们将把 `Main` 方法修改为，捕获这些结果并将每个存储库名称写入控制台。 现在，`Main` 方法如下所示：

```csharp
public static void Main(string[] args)
{
    var repositories = ProcessRepositories().Result;

    foreach (var repo in repositories)
        Console.WriteLine(repo.Name);
}
```

只有在任务完成后，才能访问任务的 `Result` 属性。 通常情况下，在 `ProcessRepositories` 方法中，你倾向于 `await`（等待）任务完成，但在 `Main` 方法中这是不允许的。

## <a name="reading-more-information"></a>读取详细信息

最后，让我们来处理 GitHub API 发送的 JSON 数据包中的其他一些属性。 虽然你不想面面俱到，但添加其他一些属性将展示更多的 C# 语言功能。

首先，将其他一些简单类型添加到 `Repository` 类定义中。 将这些属性添加到此类：

```csharp
[DataMember(Name="description")]
public string Description { get; set; }

[DataMember(Name="html_url")]
public Uri GitHubHomeUrl { get; set; }

[DataMember(Name="homepage")]
public Uri Homepage { get; set; }

[DataMember(Name="watchers")]
public int Watchers { get; set; }
```

这些属性内置转换功能，可从字符串类型（即 JSON 数据包所含）转换成目标类型。 你可能是刚开始接触 @System.Uri 类型。 它代表 URI（或在此示例中，代表 URL）。 在有 `Uri` 和 `int` 类型的情况下，如果 JSON 数据包内的数据未转换成目标类型，那么序列化操作将会抛出异常。

添加这些元素后，将 `Main` 方法更新为显示它们：

```csharp
foreach (var repo in repositories)
{
    Console.WriteLine(repo.Name);
    Console.WriteLine(repo.Description);
    Console.WriteLine(repo.GitHubHomeUrl);
    Console.WriteLine(repo.Homepage);
    Console.WriteLine(repo.Watchers);
    Console.WriteLine();
}
```
最后一步，让我们添加最后一次推送操作的信息。 此信息按如下方式在 JSON 响应中进行格式化：

```json
2016-02-08T21:27:00Z
```

此格式不符合任何标准 .NET @System.DateTime 格式。 因此，需要编写一个自定义转换方法。 你可能也不希望向 `Repository` 类的用户公开原始字符串。 特性还有助于控制此情况。 首先，定义 `private` 属性，用于在 `Repository` 类中保存日期时间的字符串表示形式：

```csharp
[DataMember(Name="pushed_at")]
private string JsonDate { get; set; }
```

`DataMember` 特性指示序列化程序应对此进行处理，即使不是公共成员，也不例外。 接下来，需要编写一个公共只读属性，将字符串转换成有效的 @System.DateTime 对象，并返回 @System.DateTime:

```csharp
[IgnoreDataMember]
public DateTime LastPush
{
    get
    {
        return DateTime.ParseExact(JsonDate, "yyyy-MM-ddTHH:mm:ssZ", CultureInfo.InvariantCulture);
    }
}
```

让我们来看一下上面的新构造。 `IgnoreDataMember` 特性指示序列化程序，不得将此类型读入任何 JSON 对象，也不得从中写入此类型。 此属性只包含 `get` 访问器。 不存在 `set` 访问器。 这就是在 C# 中定义*只读*属性的方式。 （是的，可以在 C# 中创建*只写*属性，但属性值受限。）@System.DateTime.ParseExact(System.String,System.String,System.IFormatProvider) 方法分析字符串，并使用提供的日期格式创建 @System.DateTime 对象，然后使用 `CultureInfo` 对象将其他元数据添加到 `DateTime` 中。 如果分析操作失败，那么属性访问器会抛出异常。

若要使用 @System.Globalization.CultureInfo.InvariantCulture ，需要将 @System.Globalization 命名空间添加到 `repo.cs` 中的 `using` 语句：

```csharp
using System.Globalization;
```

最后，在控制台中再添加一个输出语句，然后就可以再次生成并运行此应用程序：

```csharp
Console.WriteLine(repo.LastPush);
```

你的版本现在应与[已完成的示例](https://github.com/dotnet/docs/tree/master/samples/csharp/getting-started/console-webapiclient)匹配。
 
## <a name="conclusion"></a>结束语

此教程介绍了如何发出 Web 请求、分析结果，以及如何显示这些结果的属性。 你也已经在项目中将新的包添加为依赖项， 并已了解一些支持面向对象的技术的 C# 语言功能。


