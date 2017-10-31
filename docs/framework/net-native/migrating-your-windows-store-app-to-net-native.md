---
title: "将 Windows 应用商店应用迁移到 .NET Native"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology:
- dotnet-clr
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 4153aa18-6f56-4a0a-865b-d3da743a1d05
caps.latest.revision: 29
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: 55414d4479ca3cca8a7b5fbb15e4982b5dd12aad
ms.contentlocale: zh-cn
ms.lasthandoff: 08/21/2017

---
# <a name="migrating-your-windows-store-app-to-net-native"></a>将 Windows 应用商店应用迁移到 .NET Native
[!INCLUDE[net_native](../../../includes/net-native-md.md)] 对 Windows 应用商店中或开发者的计算机上的应用进行静态编译。 这不同于及时生成 (JIT) 编译器或 [本地映像生成器 (Ngen.exe)](../../../docs/framework/tools/ngen-exe-native-image-generator.md) 在该设备上为 Windows 应用商店应用执行的动态编译。 尽管存在不同， [!INCLUDE[net_native](../../../includes/net-native-md.md)] 尝试保持与 [.NET for Windows 应用商店应用](http://msdn.microsoft.com/library/windows/apps/br230302.aspx)的兼容。 通常，在 Windows 应用商店应用的 .NET 上可以运行的程序在 [!INCLUDE[net_native](../../../includes/net-native-md.md)]上也可以运行。  然而，在某些情况下，你可能会遇到行为变更。 本文档从以下方面讨论了 Windows 应用商店应用的标准 .NET 和 [!INCLUDE[net_native](../../../includes/net-native-md.md)] 之间的差异：  
  
-   [常规运行时差异](#Runtime)  
  
-   [动态编程差异](#Dynamic)  
  
-   [其他与反射相关的差异](#Reflection)  
  
-   [不受支持的方案和 API](#Unsupported)  
  
-   [Visual Studio 差异](#VS)  
  
<a name="Runtime"></a>   
## <a name="general-runtime-differences"></a>常规运行时差异  
  
-   当一个应用在公共语言运行时 (CLR) 上运行时，由 JIT 编译器引起的 <xref:System.TypeLoadException>等异常在受到 [!INCLUDE[net_native](../../../includes/net-native-md.md)]处理时通常会产生编译时间错误。  
  
-   请勿从一个应用的 UI 线程调用 <xref:System.GC.WaitForPendingFinalizers%2A?displayProperty=fullName> 方法。 这可能会导致 [!INCLUDE[net_native](../../../includes/net-native-md.md)]发生死锁。  
  
-   请勿依赖静态类构造函数调用排序。 在 [!INCLUDE[net_native](../../../includes/net-native-md.md)]中，调用排序与标准运行时的排序不同。 （即使可以使用标准运行时，你也不应依赖静态类构造函数的执行顺序。）  
  
-   不在任何线程上执行调用（例如， `while(true);`）的无线循环可能会使应用异常终止。 同样，长期或无限等待也可能使应用异常终止。  
  
-   某些泛型初始化循环不会引起 [!INCLUDE[net_native](../../../includes/net-native-md.md)]的异常。 例如，以下代码导致标准 CLR 上 <xref:System.TypeLoadException> 发生了一个异常。 在 [!INCLUDE[net_native](../../../includes/net-native-md.md)]中，不会出现此问题。  
  
     [!code-csharp[ProjectN#8](../../../samples/snippets/csharp/VS_Snippets_CLR/projectn/cs/compat1.cs#8)]  
  
-   在某些情况下， [!INCLUDE[net_native](../../../includes/net-native-md.md)] 提供 .NET Framework 类库的不同实施。 从一个方法返回的对象总是实施返回类型的成员。 然而，由于它的后备实施是不同的，你可能无法像在其他 .NET Framework 平台上的操作一样将其转换到相同的类型集。 例如，在某些情况下，你可能无法将 <xref:System.Collections.Generic.IEnumerable%601> 或 <xref:System.Reflection.TypeInfo.DeclaredMembers%2A?displayProperty=fullName> 等方法返回的 <xref:System.Reflection.TypeInfo.DeclaredProperties%2A?displayProperty=fullName> 界面对象转换为 `T[]`。  
  
-   Windows 应用商店应用的 .NET 上的 WinInet 缓存不是默认启用的，但在 [!INCLUDE[net_native](../../../includes/net-native-md.md)]上是默认启用的。 这提高了性能但会影响工作集。 开发者无需执行任何操作。  
  
<a name="Dynamic"></a>   
## <a name="dynamic-programming-differences"></a>动态编程差异  
 [!INCLUDE[net_native](../../../includes/net-native-md.md)] 静态链接来自 .NET Framework 的代码，从而使应用本地代码实现最佳性能。 然而，由于二进制大小必须保持较小，这就使得整个 .NET Framework 无法进入。 [!INCLUDE[net_native](../../../includes/net-native-md.md)] 编译器通过使用一个将引用移动到未使用代码的依赖减压器来解决这个限制。 然而，如果该信息无法在编译时被静态推断出，则 [!INCLUDE[net_native](../../../includes/net-native-md.md)] 无法维持或生成某些类型信息和代码，但是在运行时可动态检索。  
  
 [!INCLUDE[net_native](../../../includes/net-native-md.md)] 可启用反射和动态编程。 然而，并非所有类型都可以标记为反射，因为这会导致生成的代码太大（尤其因为 .NET Framework 中支持反射到公共 API）。 [!INCLUDE[net_native](../../../includes/net-native-md.md)] 编译器会明智地选择哪些类型应该支持反射，并为只这些类型保存元数据和生成代码。  
  
 例如，绑定数据需要一个应用能够将属性名映射到函数。 在 Windows 应用商店应用的 .NET 中，公共语言运行时自动使用反射来向托管类型和公开可用的本机类型提供该能力。 在 [!INCLUDE[net_native](../../../includes/net-native-md.md)]中，编译器会自动添加你要向其绑定数据的类型的元数据。  
  
 [!INCLUDE[net_native](../../../includes/net-native-md.md)] 编译器还可以处理运行时无需任何提示或指令的常用泛型类型，比如 <xref:System.Collections.Generic.List%601> 和 <xref:System.Collections.Generic.Dictionary%602>。 [动态](~/docs/csharp/language-reference/keywords/dynamic.md) 关键字在某些限制内也受到支持。  
  
> [!NOTE]
>  在将你的应用转到 [!INCLUDE[net_native](../../../includes/net-native-md.md)]时，应彻底测试所有动态代码路径。  
  
 [!INCLUDE[net_native](../../../includes/net-native-md.md)] 的默认配置对大多数开发者已经足够使用，但是有些开发者可能会想通过使用运行时指令 (.rd.xml) 文件来微调配置。 此外，在某些情况下， [!INCLUDE[net_native](../../../includes/net-native-md.md)] 编译器无法确定反射必须使用哪些元数据并依赖提示，尤其是在以下情况下：  
  
-   <xref:System.Type.MakeGenericType%2A?displayProperty=fullName> 和 <xref:System.Reflection.MethodInfo.MakeGenericMethod%2A?displayProperty=fullName> 等一些构造无法静态确定。  
  
-   因为编译器无法确定实例化，因此你想要反射到的泛型类型必须通过运行时指令来指定。 这并不仅是因为所有的代码必须包含在内，还因为在泛型类型上的反射会形成一个无限循环（例如，当某泛型方法在某泛型类型上调用时）。  
  
> [!NOTE]
>  运行时指令是在运行时指令 (.rd.xml) 文件中定义的。 有关使用此文件的常规信息，请参阅[入门](../../../docs/framework/net-native/getting-started-with-net-native.md)。 有关运行时指令的信息，请参阅 [Runtime Directives (rd.xml) Configuration File Reference](../../../docs/framework/net-native/runtime-directives-rd-xml-configuration-file-reference.md)。  
  
 [!INCLUDE[net_native](../../../includes/net-native-md.md)] 也包括配置文件工具，可帮助开发者确定默认集合之外哪些类型应支持反射。  
  
<a name="Reflection"></a>   
## <a name="other-reflection-related-differences"></a>其他与反射相关的差异  
 Windows 应用商店应用的 .NET 和 [!INCLUDE[net_native](../../../includes/net-native-md.md)]的行为上存在许多其他单独的与反射有关的差异。  
  
 在 [!INCLUDE[net_native](../../../includes/net-native-md.md)]中：  
  
-   反射到 .NET Framework 类库中的类型和成员的私有反射不受支持。 然而，你可以反射到自己的私有类型和成员以及第三方库的类型和成员。  
  
-   <xref:System.Reflection.ParameterInfo.HasDefaultValue%2A?displayProperty=fullName> 属性为表示返回值的 `false` 对象正确返回 <xref:System.Reflection.ParameterInfo> 。 在 Windows 应用商店应用的 .NET 中，它返回 `true`。 中间语言 (IL) 不直接支持此操作，且解释需要由语言来进行。  
  
-   位于 <xref:System.RuntimeFieldHandle> 和 <xref:System.RuntimeMethodHandle> 结构上的公共成员不受支持。 这些受到支持的类型仅用于 LINQ、表达式树和静态阵列初始化。  
  
-   <xref:System.Reflection.RuntimeReflectionExtensions.GetRuntimeProperties%2A?displayProperty=fullName> 和 <xref:System.Reflection.RuntimeReflectionExtensions.GetRuntimeEvents%2A?displayProperty=fullName> 在基类中包含隐藏成员，因此可能会在没有显示重写的情况下遭到重写。 这也适用于其他 [RuntimeReflectionExtensions.GetRuntime*](http://msdn.microsoft.com/library/system.reflection.runtimereflectionextensions_methods.aspx) 方法。  
  
-   <xref:System.Type.MakeArrayType%2A?displayProperty=fullName> 和 <xref:System.Type.MakeByRefType%2A?displayProperty=fullName> 在你试图创建特定组合（例如，ByRef 阵列）时不会发生故障。  
  
-   你无法使用反射来调用具有指针参数的成员。  
  
-   你无法使用反射来获取或设置一个指针字段。  
  
-   当参数计数错误并且其中一个参数类型不正确， [!INCLUDE[net_native](../../../includes/net-native-md.md)] 会引起 <xref:System.ArgumentException> 而不是 <xref:System.Reflection.TargetParameterCountException>。  
  
-   异常的二进制序列化通常不受支持。 因此，不可序列化的对象可添加到 <xref:System.Exception.Data%2A?displayProperty=fullName> 字典。  
  
<a name="Unsupported"></a>   
## <a name="unsupported-scenarios-and-apis"></a>不受支持的方案和 API  
 以下部分列出了不受一般开发支持的方案和 API、互操作以及 HTTPClient 和 Windows Communication Foundation (WCF) 等技术：  
  
-   [常规开发](#General)  
  
-   [HttpClient](#HttpClient)  
  
-   [Interop](#Interop)  
  
-   [不受支持的 API](#APIs)  
  
<a name="General"></a>   
### <a name="general-development-differences"></a>常规开发差异  
 **值类型**  
  
-   如果你替代了一个值类型的 <xref:System.ValueType.Equals%2A?displayProperty=fullName> 和 <xref:System.ValueType.GetHashCode%2A?displayProperty=fullName> 方法，请勿调用基类实施。 在 Windows 应用商店应用的 .NET 中，这些方法依赖反射。 在编译时间， [!INCLUDE[net_native](../../../includes/net-native-md.md)] 会生成一个不依赖运行时反射的实施。 这表示如果你不替代这两种方法，它们会以预计的方式运行，因为 [!INCLUDE[net_native](../../../includes/net-native-md.md)] 会在编译时间生成该实施。 然而，替代这些方法并调用基类实施会产生一个异常。  
  
-   大于 1 MB 的值类型不受支持。  
  
-   在 [!INCLUDE[net_native](../../../includes/net-native-md.md)]中，值类型不能拥有默认构造函数。 （C# 和 Visual Basic 禁止值类型拥有默认构造函数。 然而，这些可以在 IL 中进行创建。）  
  
 **数组**  
  
-   界限低于零的阵列不受支持。 通常，这些阵列是通过调用 <xref:System.Array.CreateInstance%28System.Type%2CSystem.Int32%5B%5D%2CSystem.Int32%5B%5D%29?displayProperty=fullName> 重载来创建的。  
  
-   不支持动态创建多维阵列。 此类阵列一般是通过调用包括 <xref:System.Array.CreateInstance%2A?displayProperty=fullName> 参数的 `lengths` 方法重载来创建，或通过调用 <xref:System.Type.MakeArrayType%28System.Int32%29?displayProperty=fullName> 方法来创建。  
  
-   四维或更多维的多维阵列不受支持；因为它们的 <xref:System.Array.Rank%2A?displayProperty=fullName> 属性值是四或者更大。 可使用 [交错阵列](~/docs/csharp/programming-guide/arrays/jagged-arrays.md) （阵列的阵列）。 例如， `array[x,y,z]` 无效，但 `array[x][y][z]` 有效。  
  
-   多维阵列的差异不受支持且会在运行时导致 <xref:System.InvalidCastException> 异常。  
  
 **泛型**  
  
-   无限泛型类型扩展会导致编译器错误。 例如，该代码无法编译：  
  
     [!code-csharp[ProjectN # 9](../../../samples/snippets/csharp/VS_Snippets_CLR/projectn/cs/compat2.cs#9)]  
  
 **指针**  
  
-   指针阵列不受支持。  
  
-   你无法使用反射来获取或设置一个指针字段。  
  
 **序列化**  
  
 <xref:System.Runtime.Serialization.KnownTypeAttribute.%23ctor%28System.String%29> 特性不受支持。 使用 <xref:System.Runtime.Serialization.KnownTypeAttribute.%23ctor%28System.Type%29> 特性。  
  
 **资源**  
  
 不支持使用带 <xref:System.Diagnostics.Tracing.EventSource> 类的本地化资源。 <xref:System.Diagnostics.Tracing.EventSourceAttribute.LocalizationResources%2A?displayProperty=fullName> 属性无法定义本地化资源。  
  
 **委托**  
  
 `Delegate.BeginInvoke` 和 `Delegate.EndInvoke` 不受支持。  
  
 **Async**  
  
 Task IAsync 的重载中的线程逻辑不受支持。  
  
 **各种 API**  
  
-   如果 <xref:System.Reflection.TypeInfo.GUID%2A?displayProperty=fullName> 特性未应用于类型， <xref:System.PlatformNotSupportedException> 属性就会导致 <xref:System.Runtime.InteropServices.GuidAttribute> 异常。 GUID 主要用于 COM 支持。  
  
-   <xref:System.DateTime.Parse%2A?displayProperty=fullName> 方法会正确解析包含 [!INCLUDE[net_native](../../../includes/net-native-md.md)]中短日期的字符串。 然而，它不会继续兼容 Microsoft 知识库文章 [KB2803771](http://support.microsoft.com/kb/2803771) 和 [KB2803755](http://support.microsoft.com/kb/2803755)中描述的日期和时间解析的变更。  
  
-   <xref:System.Numerics.BigInteger.ToString%2A?displayProperty=fullName> `("E")` 中， [!INCLUDE[net_native](../../../includes/net-native-md.md)]的兼容。 在某些版本的 CLR 中，结果字符串会缩短，而不是舍入。  
  
<a name="HttpClient"></a>   
### <a name="httpclient-differences"></a>HttpClient 差异  
 在 [!INCLUDE[net_native](../../../includes/net-native-md.md)]中， <xref:System.Net.Http.HttpClientHandler> 类在内部使用 WinINet（通过 [HttpBaseProtocolFilter](http://msdn.microsoft.com/library/windows/apps/windows.web.http.filters.httpbaseprotocolfilter.aspx) 类），而不使用标准 .NET for Windows 应用商店应用中使用的 <xref:System.Net.WebRequest> 和 <xref:System.Net.WebResponse> 类。  WinINet 并不支持 <xref:System.Net.Http.HttpClientHandler> 类支持的所有配置选项。  因此：  
  
-   <xref:System.Net.Http.HttpClientHandler> 上的某些能力属性在 `false` 会返回 [!INCLUDE[net_native](../../../includes/net-native-md.md)]，而它们在 Windows 应用商店应用的标准 .NET 中返回 `true` 。  
  
-   某些配置属性 `get` 访问器始终在 [!INCLUDE[net_native](../../../includes/net-native-md.md)] 上返回固定值，而此固定值不同于 Windows 应用商店应用的 .NET 中的默认可配置值。  
  
 某些额外的行为差异涵盖在以下子节中。  
  
 **代理**  
  
 [HttpBaseProtocolFilter](http://msdn.microsoft.com/library/windows/apps/windows.web.http.filters.httpbaseprotocolfilter.aspx) 类不支持基于每个请求配置或重写代理。  这意味着 [!INCLUDE[net_native](../../../includes/net-native-md.md)] 上的所有请求都使用系统配置的代理服务器或没有代理服务器，具体取决于 <xref:System.Net.Http.HttpClientHandler.UseProxy%2A?displayProperty=fullName> 属性的值。  在 Windows 应用商店应用的 .NET 中，代理服务器由 <xref:System.Net.Http.HttpClientHandler.Proxy%2A?displayProperty=fullName> 属性定义。  在 [!INCLUDE[net_native](../../../includes/net-native-md.md)]上，如果将 <xref:System.Net.Http.HttpClientHandler.Proxy%2A?displayProperty=fullName> 值设置为 `null` 以外的值，将导致 <xref:System.PlatformNotSupportedException> 异常。  <xref:System.Net.Http.HttpClientHandler.SupportsProxy%2A?displayProperty=fullName> 属性在 `false` 上返回 [!INCLUDE[net_native](../../../includes/net-native-md.md)]，而在 Windows 应用商店应用的标准 .NET Framework 中返回 `true` 。  
  
 **自动重定向**  
  
 [HttpBaseProtocolFilter](http://msdn.microsoft.com/library/windows/apps/windows.web.http.filters.httpbaseprotocolfilter.aspx) 类不允许配置自动重新定向的最大数目。  Windows 应用商店应用的标准 .NET 中 <xref:System.Net.Http.HttpClientHandler.MaxAutomaticRedirections%2A?displayProperty=fullName> 属性的值默认为 50，且可修改。 在 [!INCLUDE[net_native](../../../includes/net-native-md.md)]，此属性的值为 10，修改该值会导致 <xref:System.PlatformNotSupportedException> 异常。  <xref:System.Net.Http.HttpClientHandler.SupportsRedirectConfiguration%2A?displayProperty=fullName> 属性在 `false` 上返回 [!INCLUDE[net_native](../../../includes/net-native-md.md)]，而在 Windows 应用商店应用的 .NET 中返回 `true` 。  
  
 **自动解压缩**  
  
 Windows 应用商店应用的 .NET 支持将 <xref:System.Net.Http.HttpClientHandler.AutomaticDecompression%2A?displayProperty=fullName> 属性设置为 <xref:System.Net.DecompressionMethods.Deflate>、 <xref:System.Net.DecompressionMethods.GZip>（ <xref:System.Net.DecompressionMethods.Deflate> 和 <xref:System.Net.DecompressionMethods.GZip>都可以）或 <xref:System.Net.DecompressionMethods.None>。  [!INCLUDE[net_native](../../../includes/net-native-md.md)] 仅支持 <xref:System.Net.DecompressionMethods.Deflate> 与 <xref:System.Net.DecompressionMethods.GZip>或 <xref:System.Net.DecompressionMethods.None>。  尝试仅将 <xref:System.Net.Http.HttpClientHandler.AutomaticDecompression%2A> 属性设置为 <xref:System.Net.DecompressionMethods.Deflate> 或 <xref:System.Net.DecompressionMethods.GZip> 会自动将其设置为 <xref:System.Net.DecompressionMethods.Deflate> 和 <xref:System.Net.DecompressionMethods.GZip>。  
  
 **Cookie**  
  
 Cookie 处理由 <xref:System.Net.Http.HttpClient> 和 WinINet 同时执行。  来自 <xref:System.Net.CookieContainer> 的 Cookies 与 WinINet cookie 缓存结合。  从 <xref:System.Net.CookieContainer> 删除 cookie 可防止 <xref:System.Net.Http.HttpClient> 发送 cookie，但如果 cookie 已被 WinINet 检测到且 cookies 未被用户删除，则 WinINet 将会发送 cookie。  无法通过编程的方式使用 <xref:System.Net.Http.HttpClient>、 <xref:System.Net.Http.HttpClientHandler>或 <xref:System.Net.CookieContainer> API 从 WinINet 中删除 cookie。  将 <xref:System.Net.Http.HttpClientHandler.UseCookies%2A?displayProperty=fullName> 属性设置为 `false` 只会导致 <xref:System.Net.Http.HttpClient> 停止发送 cookies；WinINet 仍可能会在请求中包括 cookies。  
  
 **凭据**  
  
 在 Windows 应用商店应用的 .NET 中， <xref:System.Net.Http.HttpClientHandler.UseDefaultCredentials%2A?displayProperty=fullName> 和 <xref:System.Net.Http.HttpClientHandler.Credentials%2A?displayProperty=fullName> 属性独立工作。  此外， <xref:System.Net.Http.HttpClientHandler.Credentials%2A> 属性接受实施 <xref:System.Net.ICredentials> 接口的任意对象。  在 [!INCLUDE[net_native](../../../includes/net-native-md.md)]，设置 <xref:System.Net.Http.HttpClientHandler.UseDefaultCredentials%2A> 属性为 `true` 会导致 <xref:System.Net.Http.HttpClientHandler.Credentials%2A> 属性变为 `null`。  此外， <xref:System.Net.Http.HttpClientHandler.Credentials%2A> 属性只能设置为 `null`、 <xref:System.Net.CredentialCache.DefaultCredentials%2A>或类型 <xref:System.Net.NetworkCredential>的对象。  将其他任意 <xref:System.Net.ICredentials> 对象（其中最常见的是 <xref:System.Net.CredentialCache>）分配至 <xref:System.Net.Http.HttpClientHandler.Credentials%2A> 属性都会导致 <xref:System.PlatformNotSupportedException>。  
  
 **其他不受支持或不可配置的功能**  
  
 在 [!INCLUDE[net_native](../../../includes/net-native-md.md)]中：  
  
-   <xref:System.Net.Http.HttpClientHandler.ClientCertificateOptions%2A?displayProperty=fullName> 属性的值始终为 <xref:System.Net.Http.ClientCertificateOption.Automatic>。  在 Windows 应用商店应用的 .NET 中，默认为 <xref:System.Net.Http.ClientCertificateOption.Manual>。  
  
-   <xref:System.Net.Http.HttpClientHandler.MaxRequestContentBufferSize%2A?displayProperty=fullName> 属性无法配置。  
  
-   <xref:System.Net.Http.HttpClientHandler.PreAuthenticate%2A?displayProperty=fullName> 属性始终为 `true`。  在 Windows 应用商店应用的 .NET 中，默认为 `false`。  
  
-   响应中的 `SetCookie2` 标题忽略为废弃。  
  
<a name="Interop"></a>   
### <a name="interop-differences"></a>互操作差异性  
 **弃用的 API**  
  
 多个带有托管代码的不常使用的互操作性 API 已弃用。 与 [!INCLUDE[net_native](../../../includes/net-native-md.md)]共同使用时，这些 API 会引起 <xref:System.NotImplementedException> 或 <xref:System.PlatformNotSupportedException> 异常，或导致编译器错误。 在 Windows 应用商店应用的 .NET 中，这些 API 标记为废弃，尽管调用这些 API 会生成编译器警告而非编译器错误。  
  
 `VARIANT` 封送的废弃 API：  
  
||  
|-|  
|<xref:System.Runtime.InteropServices.BStrWrapper?displayProperty=fullName>|  
|<xref:System.Runtime.InteropServices.CurrencyWrapper?displayProperty=fullName>|  
|<xref:System.Runtime.InteropServices.DispatchWrapper?displayProperty=fullName>|  
|<xref:System.Runtime.InteropServices.ErrorWrapper?displayProperty=fullName>|  
|<xref:System.Runtime.InteropServices.UnknownWrapper?displayProperty=fullName>|  
|<xref:System.Runtime.InteropServices.VariantWrapper?displayProperty=fullName>|  
|<xref:System.Runtime.InteropServices.UnmanagedType.IDispatch?displayProperty=fullName>|  
|<xref:System.Runtime.InteropServices.UnmanagedType.SafeArray?displayProperty=fullName>|  
|<xref:System.Runtime.InteropServices.VarEnum?displayProperty=fullName>|  
  
 <xref:System.Runtime.InteropServices.UnmanagedType.Struct?displayProperty=fullName> 受支持，但在某些情况下会引发异常，如与 [IDispatch](http://msdn.microsoft.com/library/windows/apps/ms221608.aspx) 或 byref 变量一起使用时。  
  
 不推荐将 API 用于 [IDispatch](http://msdn.microsoft.com/library/windows/apps/ms221608.aspx) 支持：  
  
|类型|成员|  
|----------|------------|  
|<xref:System.Runtime.InteropServices.ClassInterfaceType?displayProperty=fullName>|<xref:System.Runtime.InteropServices.ClassInterfaceType.AutoDispatch>|  
|<xref:System.Runtime.InteropServices.ClassInterfaceType?displayProperty=fullName>|<xref:System.Runtime.InteropServices.ClassInterfaceType.AutoDual>|  
|<xref:System.Runtime.InteropServices.ComDefaultInterfaceAttribute?displayProperty=fullName>|特性不受支持|  
  
 用于经典 COM 事件的弃用的 API：  
  
||  
|-|  
|<xref:System.Runtime.InteropServices.ComEventsHelper?displayProperty=fullName>|  
|<xref:System.Runtime.InteropServices.ComSourceInterfacesAttribute>|  
  
 <xref:System.Runtime.InteropServices.ICustomQueryInterface?displayProperty=fullName> 接口中弃用的 API（在 [!INCLUDE[net_native](../../../includes/net-native-md.md)]中不受支持）：  
  
|类型|成员|  
|----------|------------|  
|<xref:System.Runtime.InteropServices.ICustomQueryInterface?displayProperty=fullName>|所有成员。|  
|<xref:System.Runtime.InteropServices.CustomQueryInterfaceMode?displayProperty=fullName>|所有成员。|  
|<xref:System.Runtime.InteropServices.CustomQueryInterfaceResult?displayProperty=fullName>|所有成员。|  
|<xref:System.Runtime.InteropServices.Marshal?displayProperty=fullName>|<xref:System.Runtime.InteropServices.Marshal.GetComInterfaceForObject%28System.Object%2CSystem.Type%2CSystem.Runtime.InteropServices.CustomQueryInterfaceMode%29?displayProperty=fullName>|  
  
 其他不受支持的互操作性功能：  
  
|类型|成员|  
|----------|------------|  
|<xref:System.Runtime.InteropServices.ICustomAdapter?displayProperty=fullName>|所有成员。|  
|<xref:System.Runtime.InteropServices.SafeBuffer?displayProperty=fullName>|所有成员。|  
|<xref:System.Runtime.InteropServices.UnmanagedType?displayProperty=fullName>|<xref:System.Runtime.InteropServices.UnmanagedType.Currency>|  
|<xref:System.Runtime.InteropServices.UnmanagedType?displayProperty=fullName>|<xref:System.Runtime.InteropServices.UnmanagedType.VBByRefStr>|  
|<xref:System.Runtime.InteropServices.UnmanagedType?displayProperty=fullName>|<xref:System.Runtime.InteropServices.UnmanagedType.AnsiBStr>|  
|<xref:System.Runtime.InteropServices.UnmanagedType?displayProperty=fullName>|<xref:System.Runtime.InteropServices.UnmanagedType.AsAny>|  
|<xref:System.Runtime.InteropServices.UnmanagedType?displayProperty=fullName>|<xref:System.Runtime.InteropServices.UnmanagedType.CustomMarshaler>|  
  
 很少使用的封送 API：  
  
|类型|成员|  
|----------|------------|  
|<xref:System.Runtime.InteropServices.Marshal?displayProperty=fullName>|<xref:System.Runtime.InteropServices.Marshal.ReadByte%28System.Object%2CSystem.Int32%29>|  
|<xref:System.Runtime.InteropServices.Marshal?displayProperty=fullName>|<xref:System.Runtime.InteropServices.Marshal.ReadInt16%28System.Object%2CSystem.Int32%29>|  
|<xref:System.Runtime.InteropServices.Marshal?displayProperty=fullName>|<xref:System.Runtime.InteropServices.Marshal.ReadInt32%28System.Object%2CSystem.Int32%29>|  
|<xref:System.Runtime.InteropServices.Marshal?displayProperty=fullName>|<xref:System.Runtime.InteropServices.Marshal.ReadInt64%28System.Object%2CSystem.Int32%29>|  
|<xref:System.Runtime.InteropServices.Marshal?displayProperty=fullName>|<xref:System.Runtime.InteropServices.Marshal.ReadIntPtr%28System.Object%2CSystem.Int32%29>|  
|<xref:System.Runtime.InteropServices.Marshal?displayProperty=fullName>|<xref:System.Runtime.InteropServices.Marshal.WriteByte%28System.Object%2CSystem.Int32%2CSystem.Byte%29>|  
|<xref:System.Runtime.InteropServices.Marshal?displayProperty=fullName>|<xref:System.Runtime.InteropServices.Marshal.WriteInt16%28System.Object%2CSystem.Int32%2CSystem.Int16%29>|  
|<xref:System.Runtime.InteropServices.Marshal?displayProperty=fullName>|<xref:System.Runtime.InteropServices.Marshal.WriteInt32%28System.Object%2CSystem.Int32%2CSystem.Int32%29>|  
|<xref:System.Runtime.InteropServices.Marshal?displayProperty=fullName>|<xref:System.Runtime.InteropServices.Marshal.WriteInt64%28System.Object%2CSystem.Int32%2CSystem.Int64%29>|  
|<xref:System.Runtime.InteropServices.Marshal?displayProperty=fullName>|<xref:System.Runtime.InteropServices.Marshal.WriteIntPtr%28System.Object%2CSystem.Int32%2CSystem.IntPtr%29>|  
  
 **平台调用和 COM 互操作兼容性**  
  
 大多数平台调用和 COM 互操作情景在 [!INCLUDE[net_native](../../../includes/net-native-md.md)]中仍受支持。 特别地，Windows Runtime (WinRT) API 的所有互操作和 Windows Runtime 所需的所有封送都受支持。 这包括针对以下内容的封送支持：  
  
-   阵列（包括 <xref:System.Runtime.InteropServices.UnmanagedType.ByValArray?displayProperty=fullName>）  
  
-   `BStr`  
  
-   委托  
  
-   字符串（Unicode、Ansi 和 HSTRING）  
  
-   结构（`byref` 和 `byval`）  
  
-   Unions  
  
-   Win32 句柄  
  
-   所有 WinRT 构造  
  
-   部分支持封送变体类型。 以下内容受到支持：  
  
    -   <xref:System.Boolean>  
  
    -   <xref:System.Byte>  
  
    -   <xref:System.Decimal>  
  
    -   <xref:System.Double>  
  
    -   <xref:System.Int16>  
  
    -   <xref:System.Int32>  
  
    -   <xref:System.Int64>  
  
    -   <xref:System.SByte>  
  
    -   <xref:System.Single>  
  
    -   <xref:System.UInt16>  
  
    -   <xref:System.UInt32>  
  
    -   <xref:System.UInt64>  
  
    -   `BStr`  
  
    -   [IUnknown](http://msdn.microsoft.com/library/windows/desktop/ms680509.aspx)  
  
 然而， [!INCLUDE[net_native](../../../includes/net-native-md.md)] 不支持以下内容：  
  
-   使用经典 COM 事件  
  
-   在托管类型上实施 <xref:System.Runtime.InteropServices.ICustomQueryInterface?displayProperty=fullName> 接口  
  
-   通过 [属性，在托管类型上实现](http://msdn.microsoft.com/library/windows/apps/ms221608.aspx) IDispatch <xref:System.Runtime.InteropServices.ComDefaultInterfaceAttribute?displayProperty=fullName> 接口。 然而，请注意你无法通过 `IDispatch`调用 COM 对象，而且你的托管对象无法实施 `IDispatch`。  
  
 使用反射来调用平台调用方法不受支持。 你可以巧妙绕过这种限制，具体做法是将方法调用包装在另一种方法中，并使用反射调用包装方法。  
  
<a name="APIs"></a>   
### <a name="other-differences-from-net-apis-for-windows-store-apps"></a>与 Windows 应用商店应用 .NET API 的其他差异  
 这部分列出了 [!INCLUDE[net_native](../../../includes/net-native-md.md)]中不受支持的其余 API。 最大一部分不受支持的 API 是 Windows Communication Foundation (WCF) API。  
  
 **DataAnnotations (System.ComponentModel.DataAnnotations)**  
  
 <xref:System.ComponentModel.DataAnnotations> 和 <xref:System.ComponentModel.DataAnnotations.Schema> 命名空间中的类型在 [!INCLUDE[net_native](../../../includes/net-native-md.md)]中不受支持。 这些包括 Windows 8 的 Windows 应用商店应用的 .NET 中出现的以下类型：  
  
||  
|-|  
|<xref:System.ComponentModel.DataAnnotations.AssociationAttribute?displayProperty=fullName>|  
|<xref:System.ComponentModel.DataAnnotations.ConcurrencyCheckAttribute?displayProperty=fullName>|  
|<xref:System.ComponentModel.DataAnnotations.CustomValidationAttribute?displayProperty=fullName>|  
|<xref:System.ComponentModel.DataAnnotations.DataType?displayProperty=fullName>|  
|<xref:System.ComponentModel.DataAnnotations.DataTypeAttribute?displayProperty=fullName>|  
|<xref:System.ComponentModel.DataAnnotations.DisplayAttribute?displayProperty=fullName>|  
|<xref:System.ComponentModel.DataAnnotations.DisplayColumnAttribute?displayProperty=fullName>|  
|<xref:System.ComponentModel.DataAnnotations.DisplayFormatAttribute>|  
|<xref:System.ComponentModel.DataAnnotations.EditableAttribute>|  
|<xref:System.ComponentModel.DataAnnotations.EnumDataTypeAttribute>|  
|<xref:System.ComponentModel.DataAnnotations.FilterUIHintAttribute?displayProperty=fullName>|  
|<xref:System.ComponentModel.DataAnnotations.KeyAttribute?displayProperty=fullName>|  
|<xref:System.ComponentModel.DataAnnotations.RangeAttribute?displayProperty=fullName>|  
|<xref:System.ComponentModel.DataAnnotations.RegularExpressionAttribute?displayProperty=fullName>|  
|<xref:System.ComponentModel.DataAnnotations.RequiredAttribute?displayProperty=fullName>|  
|<xref:System.ComponentModel.DataAnnotations.StringLengthAttribute?displayProperty=fullName>|  
|<xref:System.ComponentModel.DataAnnotations.TimestampAttribute?displayProperty=fullName>|  
|<xref:System.ComponentModel.DataAnnotations.UIHintAttribute?displayProperty=fullName>|  
|<xref:System.ComponentModel.DataAnnotations.ValidationAttribute?displayProperty=fullName>|  
|<xref:System.ComponentModel.DataAnnotations.ValidationContext?displayProperty=fullName>|  
|<xref:System.ComponentModel.DataAnnotations.ValidationException?displayProperty=fullName>|  
|<xref:System.ComponentModel.DataAnnotations.ValidationResult?displayProperty=fullName>|  
|<xref:System.ComponentModel.DataAnnotations.Validator?displayProperty=fullName>|  
|<xref:System.ComponentModel.DataAnnotations.Schema.DatabaseGeneratedAttribute?displayProperty=fullName>|  
|<xref:System.ComponentModel.DataAnnotations.Schema.DatabaseGeneratedOption?displayProperty=fullName>|  
  
 **Visual Basic**  
  
 Visual Basic 当前在 [!INCLUDE[net_native](../../../includes/net-native-md.md)]中不受支持。 <xref:Microsoft.VisualBasic> 和 <xref:Microsoft.VisualBasic.CompilerServices> 命名空间中的以下类型在 [!INCLUDE[net_native](../../../includes/net-native-md.md)]中不受支持。  
  
||  
|-|  
|<xref:Microsoft.VisualBasic.CallType?displayProperty=fullName>|  
|<xref:Microsoft.VisualBasic.Constants?displayProperty=fullName>|  
|<xref:Microsoft.VisualBasic.HideModuleNameAttribute?displayProperty=fullName>|  
|<xref:Microsoft.VisualBasic.Strings?displayProperty=fullName>|  
|<xref:Microsoft.VisualBasic.CompilerServices.Conversions?displayProperty=fullName>|  
|<xref:Microsoft.VisualBasic.CompilerServices.DesignerGeneratedAttribute?displayProperty=fullName>|  
|<xref:Microsoft.VisualBasic.CompilerServices.IncompleteInitialization?displayProperty=fullName>|  
|<xref:Microsoft.VisualBasic.CompilerServices.NewLateBinding?displayProperty=fullName>|  
|<xref:Microsoft.VisualBasic.CompilerServices.ObjectFlowControl?displayProperty=fullName>|  
|<xref:Microsoft.VisualBasic.CompilerServices.ObjectFlowControl.ForLoopControl?displayProperty=fullName>|  
|<xref:Microsoft.VisualBasic.CompilerServices.Operators?displayProperty=fullName>|  
|<xref:Microsoft.VisualBasic.CompilerServices.OptionCompareAttribute?displayProperty=fullName>|  
|<xref:Microsoft.VisualBasic.CompilerServices.OptionTextAttribute?displayProperty=fullName>|  
|<xref:Microsoft.VisualBasic.CompilerServices.ProjectData?displayProperty=fullName>|  
|<xref:Microsoft.VisualBasic.CompilerServices.StandardModuleAttribute?displayProperty=fullName>|  
|<xref:Microsoft.VisualBasic.CompilerServices.StaticLocalInitFlag?displayProperty=fullName>|  
|<xref:Microsoft.VisualBasic.CompilerServices.Utils?displayProperty=fullName>|  
  
 **反射上下文（System.Reflection.Context 命名空间）**  
  
 <xref:System.Reflection.Context.CustomReflectionContext?displayProperty=fullName> 类在 [!INCLUDE[net_native](../../../includes/net-native-md.md)]中不受支持。  
  
 **RTC (System.Net.Http.Rtc)**  
  
 <xref:System.Net.Http.RtcRequestFactory?displayProperty=fullName> 类在 [!INCLUDE[net_native](../../../includes/net-native-md.md)]中不受支持。  
  
 **Windows Communication Foundation (WCF) (System.ServiceModel.\*)**  
  
 [System.ServiceModel.* 命名空间](http://msdn.microsoft.com/library/gg145010.aspx) 中的类型在 [!INCLUDE[net_native](../../../includes/net-native-md.md)]中不受支持。 这些包括以下类型：  
  
||  
|-|  
|<xref:System.ServiceModel.ActionNotSupportedException?displayProperty=fullName>|  
|<xref:System.ServiceModel.BasicHttpBinding?displayProperty=fullName>|  
|<xref:System.ServiceModel.BasicHttpMessageCredentialType?displayProperty=fullName>|  
|<xref:System.ServiceModel.BasicHttpSecurity?displayProperty=fullName>|  
|<xref:System.ServiceModel.BasicHttpSecurityMode?displayProperty=fullName>|  
|<xref:System.ServiceModel.CallbackBehaviorAttribute?displayProperty=fullName>|  
|<xref:System.ServiceModel.ChannelFactory?displayProperty=fullName>|  
|<xref:System.ServiceModel.ChannelFactory%601?displayProperty=fullName>|  
|<xref:System.ServiceModel.ClientBase%601?displayProperty=fullName>|  
|<xref:System.ServiceModel.ClientBase%601.BeginOperationDelegate?displayProperty=fullName>|  
|<xref:System.ServiceModel.ClientBase%601.ChannelBase%601?displayProperty=fullName>|  
|<xref:System.ServiceModel.ClientBase%601.EndOperationDelegate?displayProperty=fullName>|  
|<xref:System.ServiceModel.ClientBase%601.InvokeAsyncCompletedEventArgs?displayProperty=fullName>|  
|<xref:System.ServiceModel.CommunicationException?displayProperty=fullName>|  
|<xref:System.ServiceModel.CommunicationObjectAbortedException?displayProperty=fullName>|  
|<xref:System.ServiceModel.CommunicationObjectFaultedException?displayProperty=fullName>|  
|<xref:System.ServiceModel.CommunicationState?displayProperty=fullName>|  
|<xref:System.ServiceModel.DataContractFormatAttribute?displayProperty=fullName>|  
|<xref:System.ServiceModel.DnsEndpointIdentity?displayProperty=fullName>|  
|<xref:System.ServiceModel.DuplexChannelFactory%601?displayProperty=fullName>|  
|<xref:System.ServiceModel.DuplexClientBase%601?displayProperty=fullName>|  
|<xref:System.ServiceModel.EndpointAddress?displayProperty=fullName>|  
|<xref:System.ServiceModel.EndpointAddressBuilder?displayProperty=fullName>|  
|<xref:System.ServiceModel.EndpointIdentity?displayProperty=fullName>|  
|<xref:System.ServiceModel.EndpointNotFoundException?displayProperty=fullName>|  
|<xref:System.ServiceModel.EnvelopeVersion?displayProperty=fullName>|  
|<xref:System.ServiceModel.ExceptionDetail?displayProperty=fullName>|  
|<xref:System.ServiceModel.FaultCode?displayProperty=fullName>|  
|<xref:System.ServiceModel.FaultContractAttribute?displayProperty=fullName>|  
|<xref:System.ServiceModel.FaultException?displayProperty=fullName>|  
|<xref:System.ServiceModel.FaultException%601?displayProperty=fullName>|  
|<xref:System.ServiceModel.FaultReason?displayProperty=fullName>|  
|<xref:System.ServiceModel.FaultReasonText?displayProperty=fullName>|  
|<xref:System.ServiceModel.HttpBindingBase?displayProperty=fullName>|  
|<xref:System.ServiceModel.HttpClientCredentialType?displayProperty=fullName>|  
|<xref:System.ServiceModel.HttpTransportSecurity?displayProperty=fullName>|  
|<xref:System.ServiceModel.IClientChannel?displayProperty=fullName>|  
|<xref:System.ServiceModel.ICommunicationObject?displayProperty=fullName>|  
|<xref:System.ServiceModel.IContextChannel?displayProperty=fullName>|  
|<xref:System.ServiceModel.IDefaultCommunicationTimeouts?displayProperty=fullName>|  
|<xref:System.ServiceModel.IExtensibleObject%601?displayProperty=fullName>|  
|<xref:System.ServiceModel.IExtension%601?displayProperty=fullName>|  
|<xref:System.ServiceModel.IExtensionCollection%601?displayProperty=fullName>|  
|<xref:System.ServiceModel.InstanceContext?displayProperty=fullName>|  
|<xref:System.ServiceModel.InvalidMessageContractException?displayProperty=fullName>|  
|<xref:System.ServiceModel.MessageBodyMemberAttribute?displayProperty=fullName>|  
|<xref:System.ServiceModel.MessageContractAttribute?displayProperty=fullName>|  
|<xref:System.ServiceModel.MessageContractMemberAttribute?displayProperty=fullName>|  
|<xref:System.ServiceModel.MessageCredentialType?displayProperty=fullName>|  
|<xref:System.ServiceModel.MessageHeader%601?displayProperty=fullName>|  
|<xref:System.ServiceModel.MessageHeaderException?displayProperty=fullName>|  
|<xref:System.ServiceModel.MessageParameterAttribute?displayProperty=fullName>|  
|<xref:System.ServiceModel.MessageSecurityOverTcp?displayProperty=fullName>|  
|<xref:System.ServiceModel.MessageSecurityVersion?displayProperty=fullName>|  
|<xref:System.ServiceModel.NetHttpBinding?displayProperty=fullName>|  
|<xref:System.ServiceModel.NetHttpMessageEncoding?displayProperty=fullName>|  
|<xref:System.ServiceModel.NetTcpBinding?displayProperty=fullName>|  
|<xref:System.ServiceModel.NetTcpSecurity?displayProperty=fullName>|  
|<xref:System.ServiceModel.OperationContext?displayProperty=fullName>|  
|<xref:System.ServiceModel.OperationContextScope?displayProperty=fullName>|  
|<xref:System.ServiceModel.OperationContractAttribute?displayProperty=fullName>|  
|<xref:System.ServiceModel.OperationFormatStyle?displayProperty=fullName>|  
|<xref:System.ServiceModel.ProtocolException?displayProperty=fullName>|  
|<xref:System.ServiceModel.QuotaExceededException?displayProperty=fullName>|  
|<xref:System.ServiceModel.SecurityMode?displayProperty=fullName>|  
|<xref:System.ServiceModel.ServerTooBusyException?displayProperty=fullName>|  
|<xref:System.ServiceModel.ServiceActivationException?displayProperty=fullName>|  
|<xref:System.ServiceModel.ServiceContractAttribute?displayProperty=fullName>|  
|<xref:System.ServiceModel.ServiceKnownTypeAttribute?displayProperty=fullName>|  
|<xref:System.ServiceModel.SpnEndpointIdentity?displayProperty=fullName>|  
|<xref:System.ServiceModel.TcpClientCredentialType?displayProperty=fullName>|  
|<xref:System.ServiceModel.TcpTransportSecurity?displayProperty=fullName>|  
|<xref:System.ServiceModel.TransferMode?displayProperty=fullName>|  
|<xref:System.ServiceModel.UnknownMessageReceivedEventArgs?displayProperty=fullName>|  
|<xref:System.ServiceModel.UpnEndpointIdentity?displayProperty=fullName>|  
|<xref:System.ServiceModel.XmlSerializerFormatAttribute?displayProperty=fullName>|  
|<xref:System.ServiceModel.Channels.AddressHeader?displayProperty=fullName>|  
|<xref:System.ServiceModel.Channels.AddressHeaderCollection?displayProperty=fullName>|  
|<xref:System.ServiceModel.Channels.AddressingVersion?displayProperty=fullName>|  
|<xref:System.ServiceModel.Channels.BinaryMessageEncodingBindingElement?displayProperty=fullName>|  
|<xref:System.ServiceModel.Channels.ChannelManagerBase?displayProperty=fullName>|  
|<xref:System.ServiceModel.Channels.ChannelParameterCollection?displayProperty=fullName>|  
|<xref:System.ServiceModel.Channels.CommunicationObject?displayProperty=fullName>|  
|<xref:System.ServiceModel.Channels.CompressionFormat?displayProperty=fullName>|  
|<xref:System.ServiceModel.Channels.ConnectionOrientedTransportBindingElement?displayProperty=fullName>|  
|<xref:System.ServiceModel.Channels.CustomBinding?displayProperty=fullName>|  
|<xref:System.ServiceModel.Channels.FaultConverter?displayProperty=fullName>|  
|<xref:System.ServiceModel.Channels.HttpRequestMessageProperty?displayProperty=fullName>|  
|<xref:System.ServiceModel.Channels.HttpResponseMessageProperty?displayProperty=fullName>|  
|<xref:System.ServiceModel.Channels.HttpsTransportBindingElement?displayProperty=fullName>|  
|<xref:System.ServiceModel.Channels.HttpTransportBindingElement?displayProperty=fullName>|  
|<xref:System.ServiceModel.Channels.IChannel?displayProperty=fullName>|  
|<xref:System.ServiceModel.Channels.IChannelFactory?displayProperty=fullName>|  
|<xref:System.ServiceModel.Channels.IChannelFactory%601?displayProperty=fullName>|  
|<xref:System.ServiceModel.Channels.IDuplexChannel?displayProperty=fullName>|  
|<xref:System.ServiceModel.Channels.IDuplexSession?displayProperty=fullName>|  
|<xref:System.ServiceModel.Channels.IDuplexSessionChannel?displayProperty=fullName>|  
|<xref:System.ServiceModel.Channels.IHttpCookieContainerManager?displayProperty=fullName>|  
|<xref:System.ServiceModel.Channels.IInputChannel?displayProperty=fullName>|  
|<xref:System.ServiceModel.Channels.IInputSession?displayProperty=fullName>|  
|<xref:System.ServiceModel.Channels.IInputSessionChannel?displayProperty=fullName>|  
|<xref:System.ServiceModel.Channels.IMessageProperty?displayProperty=fullName>|  
|<xref:System.ServiceModel.Channels.IOutputChannel?displayProperty=fullName>|  
|<xref:System.ServiceModel.Channels.IOutputSession?displayProperty=fullName>|  
|<xref:System.ServiceModel.Channels.IOutputSessionChannel?displayProperty=fullName>|  
|<xref:System.ServiceModel.Channels.IRequestChannel?displayProperty=fullName>|  
|<xref:System.ServiceModel.Channels.IRequestSessionChannel?displayProperty=fullName>|  
|<xref:System.ServiceModel.Channels.ISession?displayProperty=fullName>|  
|<xref:System.ServiceModel.Channels.ISessionChannel%601?displayProperty=fullName>|  
|<xref:System.ServiceModel.Channels.LocalClientSecuritySettings?displayProperty=fullName>|  
|<xref:System.ServiceModel.Channels.Message?displayProperty=fullName>|  
|<xref:System.ServiceModel.Channels.MessageBuffer?displayProperty=fullName>|  
|<xref:System.ServiceModel.Channels.MessageEncoder?displayProperty=fullName>|  
|<xref:System.ServiceModel.Channels.MessageEncoderFactory?displayProperty=fullName>|  
|<xref:System.ServiceModel.Channels.MessageEncodingBindingElement?displayProperty=fullName>|  
|<xref:System.ServiceModel.Channels.MessageFault?displayProperty=fullName>|  
|<xref:System.ServiceModel.Channels.MessageHeader?displayProperty=fullName>|  
|<xref:System.ServiceModel.Channels.MessageHeaderInfo?displayProperty=fullName>|  
|<xref:System.ServiceModel.Channels.MessageHeaders?displayProperty=fullName>|  
|<xref:System.ServiceModel.Channels.MessageProperties?displayProperty=fullName>|  
|<xref:System.ServiceModel.Channels.MessageState?displayProperty=fullName>|  
|<xref:System.ServiceModel.Channels.MessageVersion?displayProperty=fullName>|  
|<xref:System.ServiceModel.Channels.RequestContext?displayProperty=fullName>|  
|<xref:System.ServiceModel.Channels.SecurityBindingElement?displayProperty=fullName>|  
|<xref:System.ServiceModel.Channels.SecurityHeaderLayout?displayProperty=fullName>|  
|<xref:System.ServiceModel.Channels.SslStreamSecurityBindingElement?displayProperty=fullName>|  
|<xref:System.ServiceModel.Channels.TcpConnectionPoolSettings?displayProperty=fullName>|  
|<xref:System.ServiceModel.Channels.TcpTransportBindingElement?displayProperty=fullName>|  
|<xref:System.ServiceModel.Channels.TextMessageEncodingBindingElement?displayProperty=fullName>|  
|<xref:System.ServiceModel.Channels.TransportBindingElement?displayProperty=fullName>|  
|<xref:System.ServiceModel.Channels.TransportSecurityBindingElement?displayProperty=fullName>|  
|<xref:System.ServiceModel.Channels.WebSocketTransportSettings?displayProperty=fullName>|  
|<xref:System.ServiceModel.Channels.WebSocketTransportUsage?displayProperty=fullName>|  
|<xref:System.ServiceModel.Channels.WindowsStreamSecurityBindingElement?displayProperty=fullName>|  
|<xref:System.ServiceModel.Description.ClientCredentials?displayProperty=fullName>|  
|<xref:System.ServiceModel.Description.ContractDescription?displayProperty=fullName>|  
|<xref:System.ServiceModel.Description.DataContractSerializerOperationBehavior?displayProperty=fullName>|  
|<xref:System.ServiceModel.Description.FaultDescription?displayProperty=fullName>|  
|<xref:System.ServiceModel.Description.FaultDescriptionCollection?displayProperty=fullName>|  
|<xref:System.ServiceModel.Description.IContractBehavior?displayProperty=fullName>|  
|<xref:System.ServiceModel.Description.IEndpointBehavior?displayProperty=fullName>|  
|<xref:System.ServiceModel.Description.IOperationBehavior?displayProperty=fullName>|  
|<xref:System.ServiceModel.Description.MessageBodyDescription?displayProperty=fullName>|  
|<xref:System.ServiceModel.Description.MessageDescription?displayProperty=fullName>|  
|<xref:System.ServiceModel.Description.MessageDescriptionCollection?displayProperty=fullName>|  
|<xref:System.ServiceModel.Description.MessageDirection?displayProperty=fullName>|  
|<xref:System.ServiceModel.Description.MessageHeaderDescription?displayProperty=fullName>|  
|<xref:System.ServiceModel.Description.MessageHeaderDescriptionCollection?displayProperty=fullName>|  
|<xref:System.ServiceModel.Description.MessagePartDescription?displayProperty=fullName>|  
|<xref:System.ServiceModel.Description.MessagePartDescriptionCollection?displayProperty=fullName>|  
|<xref:System.ServiceModel.Description.MessagePropertyDescription?displayProperty=fullName>|  
|<xref:System.ServiceModel.Description.MessagePropertyDescriptionCollection?displayProperty=fullName>|  
|<xref:System.ServiceModel.Description.OperationDescription?displayProperty=fullName>|  
|<xref:System.ServiceModel.Description.OperationDescriptionCollection?displayProperty=fullName>|  
|<xref:System.ServiceModel.Description.ServiceEndpoint?displayProperty=fullName>|  
|<xref:System.ServiceModel.Dispatcher.ClientOperation?displayProperty=fullName>|  
|<xref:System.ServiceModel.Dispatcher.ClientRuntime?displayProperty=fullName>|  
|<xref:System.ServiceModel.Dispatcher.DispatchOperation?displayProperty=fullName>|  
|<xref:System.ServiceModel.Dispatcher.DispatchRuntime?displayProperty=fullName>|  
|<xref:System.ServiceModel.Dispatcher.EndpointDispatcher?displayProperty=fullName>|  
|<xref:System.ServiceModel.Dispatcher.IClientMessageFormatter?displayProperty=fullName>|  
|<xref:System.ServiceModel.Dispatcher.IClientMessageInspector?displayProperty=fullName>|  
|<xref:System.ServiceModel.Dispatcher.IClientOperationSelector?displayProperty=fullName>|  
|<xref:System.ServiceModel.Dispatcher.IParameterInspector?displayProperty=fullName>|  
|<xref:System.ServiceModel.Security.BasicSecurityProfileVersion?displayProperty=fullName>|  
|<xref:System.ServiceModel.Security.HttpDigestClientCredential?displayProperty=fullName>|  
|<xref:System.ServiceModel.Security.MessageSecurityException?displayProperty=fullName>|  
|<xref:System.ServiceModel.Security.SecureConversationVersion?displayProperty=fullName>|  
|<xref:System.ServiceModel.Security.SecurityAccessDeniedException?displayProperty=fullName>|  
|<xref:System.ServiceModel.Security.SecurityPolicyVersion?displayProperty=fullName>|  
|<xref:System.ServiceModel.Security.SecurityVersion?displayProperty=fullName>|  
|<xref:System.ServiceModel.Security.TrustVersion?displayProperty=fullName>|  
|<xref:System.ServiceModel.Security.UserNamePasswordClientCredential?displayProperty=fullName>|  
|<xref:System.ServiceModel.Security.WindowsClientCredential?displayProperty=fullName>|  
|<xref:System.ServiceModel.Security.Tokens.SecureConversationSecurityTokenParameters?displayProperty=fullName>|  
|<xref:System.ServiceModel.Security.Tokens.SecurityTokenParameters?displayProperty=fullName>|  
|<xref:System.ServiceModel.Security.Tokens.SupportingTokenParameters?displayProperty=fullName>|  
|<xref:System.ServiceModel.Security.Tokens.UserNameSecurityTokenParameters?displayProperty=fullName>|  
  
### <a name="differences-in-serializers"></a>序列化程序中的差异  
 与 <xref:System.Runtime.Serialization.DataContractSerializer>、 <xref:System.Runtime.Serialization.Json.DataContractJsonSerializer>和 <xref:System.Xml.Serialization.XmlSerializer> 类的序列化和反序列化有关的以下差异：  
  
-   在 [!INCLUDE[net_native](../../../includes/net-native-md.md)]中， <xref:System.Runtime.Serialization.DataContractSerializer> 和 <xref:System.Runtime.Serialization.Json.DataContractJsonSerializer> 无法序列化或反序列化一个派生类，其中此派生类具有一个非根序列化类型的基类成员。 例如，在以下代码中，尝试序列化或反序列化 `Y` 会导致出现错误：  
  
     [!code-csharp[ProjectN#10](../../../samples/snippets/csharp/VS_Snippets_CLR/projectn/cs/compat3.cs#10)]  
  
     类型 `InnerType` 对序列程序而言是未知的，因为基类的成员在序列化期间无法遍历。  
  
-   <xref:System.Runtime.Serialization.DataContractSerializer> 和 <xref:System.Runtime.Serialization.Json.DataContractJsonSerializer> 无法序列化实施 <xref:System.Collections.Generic.IEnumerable%601> 接口的类或结构。 例如，以下类无法序列化或反序列化：  
  
  
  
-   <xref:System.Xml.Serialization.XmlSerializer> 无法序列化以下对象值，因为它不知道将序列化的对象的类型：  
  
  
  
-   如果将序列化的对象的类型是<xref:System.Xml.Serialization.XmlSerializer> ，则 <xref:System.Xml.XmlQualifiedName>无法序列化或反序列化。  
  
-   所有序列程序（<xref:System.Runtime.Serialization.DataContractSerializer>、 <xref:System.Runtime.Serialization.Json.DataContractJsonSerializer>和 <xref:System.Xml.Serialization.XmlSerializer>）都无法为 <xref:System.Xml.Linq.XElement?displayProperty=fullName> 类型或包含 <xref:System.Xml.Linq.XElement>的类型生成序列代码。 它们会显示生成时间错误。  
  
-   以下序列化类型的构造函数无法保证按照预期工作：  
  
    -   <xref:System.Runtime.Serialization.DataContractSerializer.%23ctor%28System.Type%2CSystem.Collections.Generic.IEnumerable%7BSystem.Type%7D%29?displayProperty=fullName>  
  
    -   <xref:System.Runtime.Serialization.DataContractSerializer.%23ctor%28System.Type%2CSystem.Runtime.Serialization.DataContractSerializerSettings%29?displayProperty=fullName>  
  
    -   <xref:System.Runtime.Serialization.DataContractSerializer.%23ctor%28System.Type%2CSystem.String%2CSystem.String%2CSystem.Collections.Generic.IEnumerable%7BSystem.Type%7D%29?displayProperty=fullName>  
  
    -   <xref:System.Runtime.Serialization.DataContractSerializer.%23ctor%28System.Type%2CSystem.Xml.XmlDictionaryString%2CSystem.Xml.XmlDictionaryString%2CSystem.Collections.Generic.IEnumerable%7BSystem.Type%7D%29?displayProperty=fullName>  
  
    -   <xref:System.Runtime.Serialization.Json.DataContractJsonSerializer.%23ctor%28System.Type%2CSystem.Runtime.Serialization.Json.DataContractJsonSerializerSettings%29?displayProperty=fullName>  
  
    -   <xref:System.Runtime.Serialization.Json.DataContractJsonSerializer.%23ctor%28System.Type%2CSystem.Collections.Generic.IEnumerable%7BSystem.Type%7D%29?displayProperty=fullName>  
  
    -   <xref:System.Xml.Serialization.XmlSerializer.%23ctor%28System.Type%2CSystem.String%29?displayProperty=fullName>  
  
    -   <xref:System.Xml.Serialization.XmlSerializer.%23ctor%28System.Type%2CSystem.Type%5B%5D%29?displayProperty=fullName>  
  
    -   <xref:System.Xml.Serialization.XmlSerializer.%23ctor%28System.Type%2CSystem.Xml.Serialization.XmlAttributeOverrides%29?displayProperty=fullName>  
  
    -   <xref:System.Xml.Serialization.XmlSerializer.%23ctor%28System.Type%2CSystem.Xml.Serialization.XmlRootAttribute%29?displayProperty=fullName>  
  
    -   <xref:System.Xml.Serialization.XmlSerializer.%23ctor%28System.Type%2CSystem.Xml.Serialization.XmlAttributeOverrides%2CSystem.Type%5B%5D%2CSystem.Xml.Serialization.XmlRootAttribute%2CSystem.String%29?displayProperty=fullName>  
  
-   <xref:System.Xml.Serialization.XmlSerializer> 无法为具有以下任意特性的方法的类型生成代码：  
  
    -   <xref:System.Runtime.Serialization.OnSerializingAttribute>  
  
    -   <xref:System.Runtime.Serialization.OnSerializedAttribute>  
  
    -   <xref:System.Runtime.Serialization.OnDeserializingAttribute>  
  
    -   <xref:System.Runtime.Serialization.OnDeserializedAttribute>  
  
-   <xref:System.Xml.Serialization.XmlSerializer> 不兼容 <xref:System.Xml.Serialization.IXmlSerializable> 自定义序列化接口。 如果你的类实施此接口， <xref:System.Xml.Serialization.XmlSerializer> 会考虑普通旧 CLR 对象 (POCO) 类型并仅对其公共属性进行序列化。  
  
-   对普通 <xref:System.Exception> 对象的序列化（如以下情况）对 <xref:System.Runtime.Serialization.DataContractSerializer> 和 <xref:System.Runtime.Serialization.Json.DataContractJsonSerializer>无效：  
  
  
  
<a name="VS"></a>   
## <a name="visual-studio-differences"></a>Visual Studio 差异  
 **异常和调试**  
  
 如果你在运行通过调试程序中的 [!INCLUDE[net_native](../../../includes/net-native-md.md)] 编译的应用，则以下异常类型启用最可能的异常：  
  
-   <xref:System.MemberAccessException>  
  
-   <xref:System.TypeAccessException>  
  
 **构建应用**  
  
 使用 Visual Studio 默认使用的 x86 构建工具。 我们不推荐使用 AMD64 MSBuild 工具（位置路径为 C:\Program Files (x86)\MSBuild\12.0\bin\amd64），因为这些工具会导致构建问题。  
  
 **探查器**  
  
-   Visual Studio CPU 探查器和 XAML 内存探查器不会正确显示 Just-My-Code。  
  
-   XAML 内存探查器不会精确显示托管的堆数据。  
  
-   CPU 探查器不会正确区分模块和显示前缀的功能名。  
  
 **单元测试库项目**  
  
 不支持启用 Windows 应用商店应用项目的单元测试库上的 [!INCLUDE[net_native](../../../includes/net-native-md.md)] ，因为这会导致项目无法构建。  
  
## <a name="see-also"></a>另请参阅  
 [入门](../../../docs/framework/net-native/getting-started-with-net-native.md)   
 [运行时指令 (rd.xml) 配置文件参考](../../../docs/framework/net-native/runtime-directives-rd-xml-configuration-file-reference.md)   
 [.NET for Windows Store 应用程序概述](http://msdn.microsoft.com/library/windows/apps/br230302.aspx)   
 [.NET Framework 对 Windows 应用商店应用和 Windows 运行时的支持情况](../../../docs/standard/cross-platform/support-for-windows-store-apps-and-windows-runtime.md)

