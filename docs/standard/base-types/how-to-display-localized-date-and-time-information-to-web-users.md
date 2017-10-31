---
title: "如何：向 Web 用户显示本地化的日期和时间信息 | Microsoft Docs"
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
  - "显示日期和时间数据"
  - "格式设置 [.NET Framework], 日期"
  - "格式设置 [.NET Framework], 本地化数据"
  - "本地化 [.NET Framework], 日期和时间显示"
  - "本地化日期显示 [.NET Framework]"
  - "分析字符串 [.NET Framework], 日期和时间字符串"
ms.assetid: 377fe93c-32be-421a-a30a-be639a46ede8
caps.latest.revision: 8
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 8
---
# 如何：向 Web 用户显示本地化的日期和时间信息
由于网页可以在世界上的任何位置显示，因此在与用户交互时，不应依赖默认格式（通常为反映 Web 服务器本地区域性的格式）对日期和时间值执行分析和格式化操作。  正确的做法是，Web 窗体应使用用户首选的区域性来处理用户输入的日期和时间字符串。  同样，向用户显示的日期和时间数据的格式应符合用户的区域性。  本主题演示如何实现此目的。  
  
### 分析用户输入的日期和时间字符串  
  
1.  确定由 <xref:System.Web.HttpRequest.UserLanguages%2A?displayProperty=fullName> 属性返回的字符串数组是否已被填充。  如果没有，请继续步骤 6。  
  
2.  如果由 <xref:System.Web.HttpRequest.UserLanguages%2A> 属性返回的字符串数组已被填充，请检索它的第一个元素。  第一个元素指示用户默认或首选的语言和区域。  
  
3.  通过调用 <xref:System.Globalization.CultureInfo.%23ctor%28System.String%2CSystem.Boolean%29?displayProperty=fullName> 构造函数实例化表示用户首选区域性的 <xref:System.Globalization.CultureInfo> 对象。  
  
4.  调用 <xref:System.DateTime> 或 <xref:System.DateTimeOffset> 类型的 `TryParse` 或 `Parse` 方法，以尝试进行转换。  使用 `TryParse` 或 `Parse` 方法（带有 `provider` 参数）的重载，并向其传递下面两项当中的任意一项：  
  
    -   在步骤 3 中创建的 <xref:System.Globalization.CultureInfo> 对象。  
  
    -   由在步骤 3 中创建的 <xref:System.Globalization.CultureInfo> 对象的 <xref:System.Globalization.CultureInfo.DateTimeFormat%2A> 属性返回的 <xref:System.Globalization.DateTimeFormatInfo> 对象。  
  
5.  如果转换失败，请为由 <xref:System.Web.HttpRequest.UserLanguages%2A> 属性返回的字符串数组中剩余的每个元素重复步骤 2 到步骤 4。  
  
6.  如果转换仍然失败，或由 <xref:System.Web.HttpRequest.UserLanguages%2A> 属性返回的字符串数组为空，请使用由 <xref:System.Globalization.CultureInfo.InvariantCulture%2A?displayProperty=fullName> 属性返回的固定区域性分析字符串。  
  
### 分析用户请求的本地日期和时间  
  
1.  向 Web 窗体中添加一个 <xref:System.Web.UI.WebControls.HiddenField> 控件。  
  
2.  通过向 <xref:System.Web.UI.WebControls.HiddenField.Value%2A> 属性中写入当前日期和时间以及本地时区与协调世界时 \(UTC\) 之间的偏移量，创建一个用来处理 `Submit` 按钮的 `onClick` 事件的 JavaScript 函数。  请使用分隔符（例如分号）分隔字符串的两个组成部分。  
  
3.  通过向 <xref:System.Web.UI.ClientScriptManager.RegisterClientScriptBlock%28System.Type%2CSystem.String%2CSystem.String%2CSystem.Boolean%29?displayProperty=fullName> 方法传递脚本文本，使用 Web 窗体的 <xref:System.Web.UI.Control.PreRender> 事件向 HTML 输出流中注入该函数。  
  
4.  通过向 `Submit` 按钮的 `OnClientClick` 特性提供该 JavaScript 函数的名称，将事件处理程序连接到 `Submit` 按钮的 `onClick` 事件。  
  
5.  为 `Submit` 按钮的 <xref:System.Web.UI.WebControls.Button.Click> 事件创建一个处理程序。  
  
6.  在该事件处理程序中，确定由 <xref:System.Web.HttpRequest.UserLanguages%2A?displayProperty=fullName> 属性返回的字符串数组是否已被填充。  如果没有，请继续步骤 14。  
  
7.  如果由 <xref:System.Web.HttpRequest.UserLanguages%2A> 属性返回的字符串数组已被填充，请检索它的第一个元素。  第一个元素指示用户默认或首选的语言和区域。  
  
8.  通过调用 <xref:System.Globalization.CultureInfo.%23ctor%28System.String%2CSystem.Boolean%29?displayProperty=fullName> 构造函数实例化表示用户首选区域性的 <xref:System.Globalization.CultureInfo> 对象。  
  
9. 将分配给 <xref:System.Web.UI.WebControls.HiddenField.Value%2A> 属性的字符串传递给 <xref:System.String.Split%2A> 方法，以便将用户本地日期和时间的字符串表示形式以及用户本地时区偏移量的字符串表示形式存储在单独的数组元素中。  
  
10. 调用 <xref:System.DateTime.Parse%2A?displayProperty=fullName> 或 <xref:System.DateTime.TryParse%28System.String%2CSystem.IFormatProvider%2CSystem.Globalization.DateTimeStyles%2CSystem.DateTime%40%29?displayProperty=fullName> 方法，以便将用户请求的日期和时间转换为 <xref:System.DateTime> 值。  使用该方法（带有 `provider` 参数）的重载，并向其传递下面两项当中的任意一项：  
  
    -   在步骤 8 中创建的 <xref:System.Globalization.CultureInfo> 对象。  
  
    -   由在步骤 8 中创建的 <xref:System.Globalization.CultureInfo> 对象的 <xref:System.Globalization.CultureInfo.DateTimeFormat%2A> 属性返回的 <xref:System.Globalization.DateTimeFormatInfo> 对象。  
  
11. 如果分析操作在步骤 10 失败，则转到步骤 13。  否则，调用 <xref:System.UInt32.Parse%28System.String%29?displayProperty=fullName> 方法，以便将用户的时区偏移量字符串表示形式转换为一个整数。  
  
12. 调用 <xref:System.DateTimeOffset.%23ctor%28System.DateTime%2CSystem.TimeSpan%29?displayProperty=fullName> 构造函数，以此实例化表示用户本地时间的 <xref:System.DateTimeOffset>。  
  
13. 如果步骤 10 中的转换失败，请为由 <xref:System.Web.HttpRequest.UserLanguages%2A> 属性返回的字符串数组中剩余的每个元素重复步骤 7 到步骤 12。  
  
14. 如果转换仍然失败，或由 <xref:System.Web.HttpRequest.UserLanguages%2A> 属性返回的字符串数组为空，请使用由 <xref:System.Globalization.CultureInfo.InvariantCulture%2A?displayProperty=fullName> 属性返回的固定区域性分析字符串。  然后重复步骤 7 到步骤 12。  
  
 结果是一个表示网页用户本地时间的 <xref:System.DateTimeOffset> 对象。  接下来，可以通过调用 <xref:System.DateTimeOffset.ToUniversalTime%2A> 方法来确定等效的 UTC。  此外，还可以通过调用 <xref:System.TimeZoneInfo.ConvertTime%28System.DateTimeOffset%2CSystem.TimeZoneInfo%29?displayProperty=fullName> 方法并传递 <xref:System.TimeZoneInfo.Local%2A?displayProperty=fullName> 的值（作为要将时间转换到的时区）来确定 Web 服务器上等效的日期和时间。  
  
## 示例  
 下面的示例既包含 HTML 源代码，也包含让用户输入日期和时间值的 ASP.NET Web 窗体的代码。  另外，还有一个客户端脚本将用户请求的本地日期和时间以及用户所在时区与 UTC 的偏移量的相关信息写入一个隐藏字段中。  随后，服务器将分析此信息，并返回显示用户输入的网页。  它还会使用用户的本地时间、服务器时间以及 UTC 显示用户请求的日期和时间。  
  
 <!-- TODO: review snippet reference [!code-csharp[Formatting.HowTo.ParseDateInput#1](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.HowTo.ParseDateInput/cs/GetDateInfo.aspx#1)]  -->
 <!-- TODO: review snippet reference [!code-vb[Formatting.HowTo.ParseDateInput#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.HowTo.ParseDateInput/vb/GetDateInfo.aspx#1)]  -->  
  
 客户端脚本调用 JavaScript `toLocaleString` 方法。  这会生成一个符合用户区域设置格式化约定的字符串，从而更有利于服务器成功分析。  
  
 <xref:System.Web.HttpRequest.UserLanguages%2A?displayProperty=fullName> 属性由 HTTP 请求中包含的 `Accept-Language` 标头中所含的区域性名称来填充。  但是，并非所有浏览器的请求中都包含 `Accept-Language` 标头，并且用户也可以完全禁止标头的显示。  因此，在分析用户输入时，就需要使用回退区域性。  通常情况下，回退区域性是由 <xref:System.Globalization.CultureInfo.InvariantCulture%2A?displayProperty=fullName> 返回的固定区域性。  用户也可以向 Internet Explorer 提供他们在文本框中输入的区域性名称，这样便可能出现区域性名称无效的情况。  因此，在实例化 <xref:System.Globalization.CultureInfo> 对象时，必须使用异常处理。  
  
 当从 Internet Explorer 提交的 HTTP 请求中检索到 <xref:System.Web.HttpRequest.UserLanguages%2A?displayProperty=fullName> 数组后，将按照用户的首选顺序对其进行填充。  数组中的第一个元素包含用户主区域性\/区域的名称。  如果该数组还包含任何其他项，Internet Explorer 将随意为它们分配一个质量说明符，并用分号将其与区域性名称分隔开。  例如，表示 fr\-FR 区域性的项可能采用 `fr-FR;q=0.7` 形式。  
  
 该示例调用 <xref:System.Globalization.CultureInfo.%23ctor%2A> 构造函数，调用时 `useUserOverride` 参数设置为 `false`，以创建新的 <xref:System.Globalization.CultureInfo> 对象。  这样可确保，如果区域性名称为服务器上的默认区域性名称，则由该类构造函数创建的新 <xref:System.Globalization.CultureInfo> 对象将包含区域性的默认设置，并且不反映使用服务器的**“区域和语言选项”**应用程序重写的任何设置。  服务器上任何已重写设置的值不可能存在于用户的系统上，也不会反映在用户输入中。  
  
 由于此示例要分析日期和时间的两个字符串表示形式（一个由用户输入，另一个存储在隐藏字段中），因此它提前定义了可能需要使用的各个 <xref:System.Globalization.CultureInfo> 对象。  此示例先创建了一个 <xref:System.Globalization.CultureInfo> 对象的数组，并使其中的对象数目比 <xref:System.Web.HttpRequest.UserLanguages%2A?displayProperty=fullName> 属性返回的元素数大一。  接着，它为每个语言\/区域字符串实例化一个 <xref:System.Globalization.CultureInfo> 对象，同时实例化表示 <xref:System.Globalization.CultureInfo.InvariantCulture%2A?displayProperty=fullName> 的 <xref:System.Globalization.CultureInfo> 对象。  
  
 您可以在代码中调用 <xref:System.DateTime.Parse%2A> 或 <xref:System.DateTime.TryParse%2A> 方法，以便将用户的日期和时间字符串表示形式转换为 <xref:System.DateTime> 值。  在一次分析操作中，可能需要重复调用某个分析方法。  因此，<xref:System.DateTime.TryParse%2A> 方法更加适用，因为它可以在分析操作失败时返回 `false`。  与此相比，<xref:System.DateTime.Parse%2A> 方法可能会不断引发异常，在 Web 应用程序中，处理这些异常将是一种非常占用资源的做法。  
  
## 编译代码  
 若要编译该代码，请创建一个没有代码隐藏文件的 [!INCLUDE[vstecasp](../../../includes/vstecasp-md.md)] 网页。  然后将该示例复制到该网页中，以替换所有的现有代码。  该 [!INCLUDE[vstecasp](../../../includes/vstecasp-md.md)] 网页应包含下列控件：  
  
-   <xref:System.Web.UI.WebControls.Label> 控件，代码中并未引用。  请将其 <xref:System.Web.UI.WebControls.TextBox.Text%2A> 属性设置为“Enter a Number:”。  
  
-   名为 `DateString` 的 <xref:System.Web.UI.WebControls.TextBox> 控件。  
  
-   名为 `OKButton` 的 <xref:System.Web.UI.WebControls.Button> 控件。  请将其 <xref:System.Web.UI.WebControls.Button.Text%2A> 属性设置为“OK”。  
  
-   名为 `DateInfo` 的 <xref:System.Web.UI.WebControls.HiddenField> 控件。  
  
## .NET Framework 安全性  
 若要防止用户将脚本注入 HTML 流中，切勿在服务器响应中直接回送用户输入。  而是应改用 <xref:System.Web.HttpServerUtility.HtmlEncode%2A?displayProperty=fullName> 方法回送用户输入。  
  
## 请参阅  
 [执行格式设置操作](../../../docs/standard/base-types/performing-formatting-operations.md)   
 [标准日期和时间格式字符串](../../../docs/standard/base-types/standard-date-and-time-format-strings.md)   
 [自定义日期和时间格式字符串](../../../docs/standard/base-types/custom-date-and-time-format-strings.md)   
 [分析日期和时间字符串](../../../docs/standard/base-types/parsing-datetime.md)