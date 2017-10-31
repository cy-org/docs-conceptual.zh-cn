---
title: "如何：定义和使用自定义数值格式提供程序 | Microsoft Docs"
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
  - "自定义格式字符串"
  - "自定义数字格式字符串"
  - "显示日期和时间数据"
  - "格式提供程序 [.NET Framework]"
  - "格式设置 [.NET Framework], 数字"
  - "数字格式设置 [.NET Framework]"
  - "数字 [.NET Framework], 自定义数字格式字符串"
  - "数值格式字符串 [.NET Framework]"
ms.assetid: a281bfbf-6596-45ed-a2d6-3782d535ada2
caps.latest.revision: 11
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 11
---
# 如何：定义和使用自定义数值格式提供程序
在 [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] 中，您可以对数值的字符串表示形式施加广泛的控制。  它支持用于自定义数值格式的下列功能：  
  
-   标准数值格式字符串，提供用于将数字转换为其字符串表示形式的预定义格式集。  可以将这些字符串与带有 `format` 参数的任何数值格式化方法（例如 <xref:System.Decimal.ToString%28System.String%29?displayProperty=fullName>）一起使用。  有关详细信息，请参见[标准数字格式字符串](../../../docs/standard/base-types/standard-numeric-format-strings.md)。  
  
-   自定义数值格式字符串，提供可通过组合来定义自定义数值格式说明符的符号集。  它们也可以与带 `format` 参数的任何数值格式化方法（例如 <xref:System.Decimal.ToString%28System.String%29?displayProperty=fullName>）一起使用。  有关详细信息，请参见[自定义数字格式字符串](../../../docs/standard/base-types/custom-numeric-format-strings.md)。  
  
-   自定义 <xref:System.Globalization.CultureInfo> 或 <xref:System.Globalization.NumberFormatInfo> 对象，用于定义显示数值的字符串表示形式时使用的符号和格式模式。  可以将这些字符串与带有 `provider` 参数的任何数值格式化方法（例如 <xref:System.Int32.ToString%2A>）一起使用。  通常情况下，`provider` 参数用于指定区域性特定的格式。  
  
 在某些情况下（例如当应用程序必须显示已格式化的帐号、标识号或邮政编码时），这三种方法都不适用。  在 [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] 中，还可以定义既非 <xref:System.Globalization.CultureInfo> 又非 <xref:System.Globalization.NumberFormatInfo> 对象的格式化对象，以确定数值如何格式化。  本主题将分步说明如何实现此类对象，并提供格式化电话号码的示例。  
  
### 定义自定义格式提供程序  
  
1.  定义一个实现 <xref:System.IFormatProvider> 和 <xref:System.ICustomFormatter> 接口的类。  
  
2.  实现 <xref:System.IFormatProvider.GetFormat%2A?displayProperty=fullName> 方法。  <xref:System.IFormatProvider.GetFormat%2A> 是一个回调方法，格式化方法（例如 [String.Format\(IFormatProvider, String, Object\<xref:System.String.Format%28System.IFormatProvider%2CSystem.String%2CSystem.Object%5B%5D%29?displayProperty=fullName> 方法）会调用该方法来检索真正负责执行自定义格式化的对象。  典型的 <xref:System.IFormatProvider.GetFormat%2A> 实现可执行下列任务：  
  
    1.  确定以方法参数的形式传递的 <xref:System.Type> 对象是否表示 <xref:System.ICustomFormatter> 接口。  
  
    2.  如果该参数的确表示 <xref:System.ICustomFormatter> 接口，<xref:System.IFormatProvider.GetFormat%2A> 将返回一个实现负责提供自定义格式化的 <xref:System.ICustomFormatter> 接口的对象。  通常情况下，自定义格式化对象会返回自身。  
  
    3.  如果该参数不表示 <xref:System.ICustomFormatter> 接口，<xref:System.IFormatProvider.GetFormat%2A> 将返回 `null`。  
  
3.  实现 <xref:System.ICustomFormatter.Format%2A> 方法。  此方法由 [String.Format\(IFormatProvider, String, Object\<xref:System.String.Format%28System.IFormatProvider%2CSystem.String%2CSystem.Object%5B%5D%29?displayProperty=fullName> 方法调用，它负责返回数字的字符串表示形式。  实现该方法通常涉及以下过程：  
  
    1.  （可选）通过检查 `provider` 参数确保该方法要以合法的方式提供格式化服务。  对于同时实现 <xref:System.IFormatProvider> 和 <xref:System.ICustomFormatter> 的格式化对象，这涉及到测试 `provider` 参数与当前的格式化对象是否相等。  
  
    2.  确定格式化对象是否应支持自定义格式说明符。\(例如，格式说明符“N”可能指示应以 NANP 格式输出美国电话号码，而“I”可能指示以 ITU\-T 建议 E.123 格式。\)如果使用了格式说明符，该方法就应处理特定的格式说明符。  格式说明符将以 `format` 参数的形式传递给该方法。  如果不存在说明符，`format` 参数的值将为 <xref:System.String.Empty?displayProperty=fullName>。  
  
    3.  检索以 `arg` 参数的形式传递给该方法的数值。  执行将该参数转换为字符串表示形式所需的任何操作。  
  
    4.  返回 `arg` 参数的字符串表示形式。  
  
### 使用自定义数值格式化对象  
  
1.  创建自定义格式化类的一个新实例。  
  
2.  调用 [String.Format\(IFormatProvider, String, Object\<xref:System.String.Format%28System.IFormatProvider%2CSystem.String%2CSystem.Object%5B%5D%29?displayProperty=fullName> 格式化方法，并向其传递自定义格式化对象、格式化说明符（如果未使用说明符，则为 <xref:System.String.Empty?displayProperty=fullName>）以及要格式化的数值。  
  
## 示例  
 下面的示例定义一个名为 `TelephoneFormatter` 的自定义数值格式提供程序，该提供程序把代表一个U.S电话号码的数字转化为它的NANP或E.123格式。  该方法要处理两个格式说明符：“N”（输出 NANP 格式）和“I”（输出国际 E.123 格式）。  
  
 [!code-csharp[Formatting.HowTo.NumericValue#1](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.HowTo.NumericValue/cs/Telephone1.cs#1)]
 [!code-vb[Formatting.HowTo.NumericValue#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.HowTo.NumericValue/vb/Telephone1.vb#1)]  
  
 自定义数值格式提供程序只能结合 [String.Format\(IFormatProvider, String, Object\<xref:System.String.Format%28System.IFormatProvider%2CSystem.String%2CSystem.Object%5B%5D%29?displayProperty=fullName> 方法使用。  带有 <xref:System.IFormatProvider> 类型参数的数值格式化方法（例如 `ToString`）的其他重载都会向 <xref:System.IFormatProvider.GetFormat%2A?displayProperty=fullName> 实现传递一个表示 <xref:System.Globalization.NumberFormatInfo> 类型的 <xref:System.Type> 对象。  反过来，它们期望该方法返回 <xref:System.Globalization.NumberFormatInfo> 对象。  如果未返回该对象，将忽略自定义数值格式提供程序，并改用当前区域性的 <xref:System.Globalization.NumberFormatInfo> 对象。  在该示例中，`TelephoneFormatter.GetFormat` 方法会处理被不当传递给数值格式化方法的可能性，其方式是检查方法参数，如果方法参数表示的是 <xref:System.ICustomFormatter> 以外的类型，它将返回 `null`。  
  
 如果自定义数值格式提供程序支持一组格式说明符，则应确保提供当 [String.Format\(IFormatProvider, String, Object\<xref:System.String.Format%28System.IFormatProvider%2CSystem.String%2CSystem.Object%5B%5D%29?displayProperty=fullName> 方法调用中使用的格式项中未提供格式说明符时的默认行为。  在该示例中，“N”是默认的格式说明符。  这样，通过提供显式的格式说明符，即可将数字转换为格式化的电话号码。  下面的示例阐释了这样一个方法调用。  
  
 [!code-csharp[Formatting.HowTo.NumericValue#2](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.HowTo.NumericValue/cs/Telephone1.cs#2)]
 [!code-vb[Formatting.HowTo.NumericValue#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.HowTo.NumericValue/vb/Telephone1.vb#2)]  
  
 但是，即使未提供格式说明符，它也允许进行转换。  下面的示例阐释了这样一个方法调用。  
  
 [!code-csharp[Formatting.HowTo.NumericValue#3](../../../samples/snippets/csharp/VS_Snippets_CLR/Formatting.HowTo.NumericValue/cs/Telephone1.cs#3)]
 [!code-vb[Formatting.HowTo.NumericValue#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Formatting.HowTo.NumericValue/vb/Telephone1.vb#3)]  
  
 如果未定义默认的格式说明符，<xref:System.ICustomFormatter.Format%2A?displayProperty=fullName> 方法的实现就应包括诸如以下内容的代码，以便 .NET Framework 可以提供您的代码所不支持的格式化。  
  
 [!code-csharp[System.ICustomFormatter.Format#1](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.ICustomFormatter.Format/cs/format.cs#1)]
 [!code-vb[System.ICustomFormatter.Format#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.ICustomFormatter.Format/vb/Format.vb#1)]  
  
 在此示例中，实现 <xref:System.ICustomFormatter.Format%2A?displayProperty=fullName> 的方法将用作 [String.Format\(IFormatProvider, String, Object\<xref:System.String.Format%28System.IFormatProvider%2CSystem.String%2CSystem.Object%5B%5D%29?displayProperty=fullName> 方法的回调方法。  因此，它将检查 `formatProvider` 参数，以确定其是否包含对当前 `TelephoneFormatter` 对象的引用。  但是，您也可以在代码中直接调用该方法。  在这种情况下，可以使用 `formatProvider` 参数来提供 <xref:System.Globalization.CultureInfo> 或 <xref:System.Globalization.NumberFormatInfo> 对象，以提供区域性特定的格式化信息。  
  
## 编译代码  
 在命令行处使用 csc.exe 或 vb.exe 编译代码。  若要在 [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] 中编译代码，请将代码置于控制台应用程序项目模板中。  
  
## 请参阅  
 [执行格式设置操作](../../../docs/standard/base-types/performing-formatting-operations.md)