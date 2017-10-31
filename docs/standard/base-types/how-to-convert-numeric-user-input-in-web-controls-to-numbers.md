---
title: "如何：将用户在 Web 控件中输入的数值转换为数字 | Microsoft Docs"
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
  - "将数值用户输入转换为数字"
  - "格式设置 [.NET Framework], 数字"
  - "数字格式设置 [.NET Framework]"
  - "数字 [.NET Framework], 将数值用户输入转换为数字"
  - "数值格式字符串 [.NET Framework]"
  - "分析字符串 [.NET Framework], 数值字符串"
ms.assetid: f27ddfb8-7479-4b79-8879-02a3bd8402d4
caps.latest.revision: 8
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 8
---
# 如何：将用户在 Web 控件中输入的数值转换为数字
由于网页可以在世界上的任何地方显示，用户可能以近乎无限多的格式在 <xref:System.Web.UI.WebControls.TextBox> 控件中输入数值数据。  因此，确定网页用户的区域设置和区域性就变得十分重要。  在接下来的用户输入分析中，您可以应用由该用户的区域设置和区域性定义的格式化约定。  
  
### 将 Web TextBox 控件中的数值输入转换为数字  
  
1.  确定由 <xref:System.Web.HttpRequest.UserLanguages%2A?displayProperty=fullName> 属性返回的字符串数组是否已被填充。  如果没有，请继续步骤 6。  
  
2.  如果由 <xref:System.Web.HttpRequest.UserLanguages%2A> 属性返回的字符串数组已被填充，请检索它的第一个元素。  第一个元素指示用户默认或首选的语言和区域。  
  
3.  通过调用 <xref:System.Globalization.CultureInfo.%23ctor%28System.String%2CSystem.Boolean%29?displayProperty=fullName> 构造函数实例化表示用户首选区域性的 <xref:System.Globalization.CultureInfo> 对象。  
  
4.  对于要将用户输入转换为的数值类型，请调用其 `TryParse` 或 `Parse` 方法。  使用 `TryParse` 或 `Parse` 方法（带有 `provider` 参数）的重载，并向其传递下面两项当中的任意一项：  
  
    -   在步骤 3 中创建的 <xref:System.Globalization.CultureInfo> 对象。  
  
    -   由在步骤 3 中创建的 <xref:System.Globalization.CultureInfo> 对象的 <xref:System.Globalization.CultureInfo.NumberFormat%2A> 属性返回的 <xref:System.Globalization.NumberFormatInfo> 对象。  
  
5.  如果转换失败，请为由 <xref:System.Web.HttpRequest.UserLanguages%2A> 属性返回的字符串数组中剩余的每个元素重复步骤 2 到步骤 4。  
  
6.  如果转换仍然失败，或由 <xref:System.Web.HttpRequest.UserLanguages%2A> 属性返回的字符串数组为空，请使用由 <xref:System.Globalization.CultureInfo.InvariantCulture%2A?displayProperty=fullName> 属性返回的固定区域性分析字符串。  
  
## 示例  
 下面的示例是一个 Web 窗体的完整代码隐藏页，该窗体让用户在 <xref:System.Web.UI.WebControls.TextBox> 控件中输入一个数值，然后将其转换为数字。  该数字随后将被双写，并采用与原始输入相同的格式化规则显示。  
  
 [!code-csharp[Formatting.HowTo.ParseNumericInput#1](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.HowTo.ParseNumericInput/cs/NumericUserInput1.aspx.cs#1)]
 [!code-vb[Formatting.HowTo.ParseNumericInput#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.HowTo.ParseNumericInput/vb/NumericUserInput1.aspx.vb#1)]  
  
 <xref:System.Web.HttpRequest.UserLanguages%2A?displayProperty=fullName> 属性由 HTTP 请求中包含的 `Accept-Language` 标头中所含的区域性名称来填充。  但是，并非所有浏览器的请求中都包含 `Accept-Language` 标头，并且用户也可以完全禁止标头的显示。  因此，在分析用户输入时，就需要使用回退区域性。  通常情况下，回退区域性是由 <xref:System.Globalization.CultureInfo.InvariantCulture%2A?displayProperty=fullName> 返回的固定区域性。  用户也可以向 Internet Explorer 提供他们在文本框中输入的区域性名称，这样便可能出现区域性名称无效的情况。  因此，在实例化 <xref:System.Globalization.CultureInfo> 对象时，必须使用异常处理。  
  
 当从 Internet Explorer 提交的 HTTP 请求中检索到 <xref:System.Web.HttpRequest.UserLanguages%2A?displayProperty=fullName> 数组后，将按照用户的首选顺序对其进行填充。  数组中的第一个元素包含用户主区域性\/区域的名称。  如果该数组还包含任何其他项，Internet Explorer 将随意为它们分配一个质量说明符，并用分号将其与区域性名称分隔开。  例如，表示 fr\-FR 区域性的项可能采用 `fr-FR;q=0.7` 形式。  
  
 该示例调用 <xref:System.Globalization.CultureInfo.%23ctor%2A> 构造函数，调用时 `useUserOverride` 参数设置为 `false`，以创建新的 <xref:System.Globalization.CultureInfo> 对象。  这样可确保，如果区域性名称为服务器上的默认区域性名称，则由该类构造函数创建的新 <xref:System.Globalization.CultureInfo> 对象将包含区域性的默认设置，并且不反映使用服务器的**“区域和语言选项”**应用程序重写的任何设置。  服务器上任何已重写设置的值不可能存在于用户的系统上，也不会反映在用户输入中。  
  
 您可以在代码中调用要将用户输入转换为的数值类型的 `Parse` 或 `TryParse` 方法。  在一次分析操作中，可能需要重复调用某个分析方法。  因此，`TryParse` 方法更加适用，因为它可以在分析操作失败时返回 `false`。  与此相比，`Parse` 方法可能会不断引发异常，在 Web 应用程序中，处理这些异常将是一种非常占用资源的做法。  
  
## 编译代码  
 若要编译代码，请将其复制到 [!INCLUDE[vstecasp](../../../includes/vstecasp-md.md)] 代码隐藏页中，以便替换所有现有的代码。  该 [!INCLUDE[vstecasp](../../../includes/vstecasp-md.md)] 网页应包含下列控件：  
  
-   <xref:System.Web.UI.WebControls.Label> 控件，代码中并未引用。  请将其 <xref:System.Web.UI.WebControls.TextBox.Text%2A> 属性设置为“Enter a Number:”。  
  
-   名为 `NumericString` 的 <xref:System.Web.UI.WebControls.TextBox> 控件。  
  
-   名为 `OKButton` 的 <xref:System.Web.UI.WebControls.Button> 控件。  请将其 <xref:System.Web.UI.WebControls.Button.Text%2A> 属性设置为“OK”。  
  
 请将类名从 `NumericUserInput` 更改为由 [!INCLUDE[vstecasp](../../../includes/vstecasp-md.md)] 页的 `Page` 指令的 `Inherits` 特性所定义的类名。  同时将 `NumericInput` 对象引用的名称更改为由 [!INCLUDE[vstecasp](../../../includes/vstecasp-md.md)] 页的 `form` 标记的 `id` 特性所定义的名称。  
  
## .NET Framework 安全性  
 若要防止用户将脚本注入 HTML 流中，切勿在服务器响应中直接回送用户输入。  而是应改用 <xref:System.Web.HttpServerUtility.HtmlEncode%2A?displayProperty=fullName> 方法回送用户输入。  
  
## 请参阅  
 [执行格式设置操作](../../../docs/standard/base-types/performing-formatting-operations.md)   
 [分析数值字符串](../../../docs/standard/base-types/parsing-numeric.md)