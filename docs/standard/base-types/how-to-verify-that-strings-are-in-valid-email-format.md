---
title: "如何：确认字符串是有效的电子邮件格式 | Microsoft Docs"
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
  - "正则表达式，示例"
  - "用户输入，示例"
  - "Regex.IsMatch 方法"
  - "正则表达式 [.NET Framework]，示例"
  - "示例 [Visual Basic]，字符串"
  - "IsValidEmail"
  - "验证，电子邮件字符串"
  - "输入，检查"
  - "字符串 [.NET Framework]，示例 [Visual Basic]"
  - "电子邮件 [.NET Framework]，验证"
  - "IsMatch 方法"
ms.assetid: 7536af08-4e86-4953-98a1-a8298623df92
caps.latest.revision: 30
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 30
---
# 如何：确认字符串是有效的电子邮件格式
下面的示例使用正则表达式来验证一个字符串是否为有效的电子邮件格式。  
  
## 示例  
 该示例定义 `IsValidEmail` 方法，如果字符串包含有效的电子邮件地址，则该方法返回 `true`，否则返回 `false`，但不采取其他任何操作。  
  
 若要验证电子邮件地址是否有效，方法 `IsValidEmail` 将使用<xref:System.Text.RegularExpressions.Regex.Replace%28System.String%2CSystem.String%2CSystem.Text.RegularExpressions.MatchEvaluator%29?displayProperty=fullName>正则表达式模式调用 `(@)(.+)$` 方法将域名从电子邮件地址分离。 第三个参数是表示了处理和替换匹配文本的方法的 <xref:System.Text.RegularExpressions.MatchEvaluator> 委托。 正则表达式模式的解释如下。  
  
|模式|描述|  
|--------|--------|  
|`(@)`|匹配 @ 字符。 这是第一个捕获组。|  
|`(.+)`|匹配任意字符的一个或多个匹配项。 这是第二个捕获组。|  
|`$`|在字符串的结尾结束匹配。|  
  
 使用 @ 字符的域名已传递给 `DomainMapper` 方法，该方法使用 <xref:System.Globalization.IdnMapping> 类将 US\-ASCII 字符范围外的 Unicode 字符转换为 Punycode。 如果 `invalid` 方法在域名中检测到任何无效字符，该方法还会将 `True` 标志设置为 <xref:System.Globalization.IdnMapping.GetAscii%2A?displayProperty=fullName>。 该方法将冠以 @ 符号的 Punycode 域名返回给 `IsValidEmail` 方法。  
  
 然后 `IsValidEmail` 方法调用 <xref:System.Text.RegularExpressions.Regex.IsMatch%28System.String%2CSystem.String%29?displayProperty=fullName> 方法验证该地址是否符合正则表达式模式。  
  
 请注意，`IsValidEmail` 方法不执行身份验证来验证电子邮件地址。 它只确定其格式对于电子邮件地址是否有效。 此外，`IsValidEmail` 方法不对顶级域名是否是 [IANA 根区域数据库](https://www.iana.org/domains/root/db)中列出的有效域名进行验证，这需执行查找操作。 相反，正则表达式仅验证由二到二十四个 ASCII 字符组成的顶级域名，该域名以字母数字开头并以字符结尾，且其余的字符是字母数字或连字符 \(\-\)。  
  
 [!code-csharp[RegularExpressions.Examples.Email#7](../../../samples/snippets/csharp/VS_Snippets_CLR/RegularExpressions.Examples.Email/cs/example4.cs#7)]
 [!code-vb[RegularExpressions.Examples.Email#7](../../../samples/snippets/visualbasic/VS_Snippets_CLR/RegularExpressions.Examples.Email/vb/example4.vb#7)]  
  
 在本例中，正则表达式模式 `^(?(")(".+?(?<!\\)"@)|(([0-9a-z]((\.(?!\.))|[-!#\$%&'\*\+/=\?\^`\{\}\|~\w])*)(?<=[0-9a-z])@))(?(\[)(\[(\d{1,3}\.){3}\d{1,3}\])|(([0-9a-z][-\w]*[0-9a-z]*\.)+[a-z0-9][\-a-z0-9]{0,22}[a-z0-9]))$` 按下表中的方式解释。 注意，使用 <xref:System.Text.RegularExpressions.RegexOptions?displayProperty=fullName> 标志编译正则表达式。  
  
|模式|描述|  
|--------|--------|  
|`^`|从字符串的开头部分开始匹配。|  
|`(?(")`|确定第一个字符是否为引号。`(?(")` 为替换构造的开头。|  
|`(?("")("".+?(?<!\\)""@)`|如果第一个字符是引号，则匹配一个开始引号，后跟至少一个任意字符，再后跟一个结束引号。 不得在结束引号前面加反斜杠字符 \(\\\)。`(?<!` 是零宽度负预测先行断言的开头。 字符串应以 at 符号 \(@\) 结束。|  
|`&#124;(([0-9a-z]`|如果第一个字符不是引号，则匹配从 a 到 z 或 A 到 Z（比较不区分大小写）的任意字母字符或从 0 到 9 的任意数字字符。|  
|`(\.(?!\.))`|如果下一个字符为句点，则匹配它。 如果下一个字符不为句点，则看下一个字符并继续进行匹配。`(?!\.)` 是宽度为零的负预测先行断言，可防止两个连续句号出现在电子邮件地址的本地部分中。|  
|`&#124;[-!#\$%&'\*\+/=\?\^`\{\}\&#124;~\w]`|如果下一个字符不为句点，则匹配任意单词字符或下列字符之一：\-\!\#$%'\*\+\=?^\`{}&#124;~。|  
|`((\.(?!\.))&#124;[-!#\$%'\*\+/=\?\^`\{\}\&#124;~\w])*`|匹配替换模式（一个句点，后跟一个非句点或许多字符中的某个字符）零次或多次。|  
|`@`|匹配 @ 字符。|  
|`(?<=[0-9a-z])`|如果 @ 字符之前的字符为从 A 到 Z、从 a 到 z 或从 0 到 9 的字符，则继续进行匹配。`(?<=[0-9a-z])` 构造定义零宽度正回顾断言。|  
|`(?(\[)`|检查 @ 后面的字符是否为左括号。|  
|`(\[(\d{1,3}\.){3}\d{1,3}\])`|如果该字符为左括号，则匹配该左括号，后跟 IP 地址（四个数字组，每个数字组包含一到三位数字，并且每个数字组用句点隔开）和右括号。|  
|`&#124;(([0-9a-z][-\w]*[0-9a-z]*\.)+`|如果 @ 后面的字符不是左括号，则匹配一个字母数字字符（A\-Z、a\-z 或 0\-9 中的某个值），后跟一个单词字符或连字符的零个或多个匹配项，接着跟 0 或一个字母数字字符（A\-Z、a\-z 或 0\-9 中的某个值），再跟一个句点。 此模式可以重复一次或多次，并且必须后跟顶级域名。|  
|`[a-z0-9][\-a-z0-9]{0,22}[a-z0-9]))`|顶级域名必须以字母数字字符（a\-z、A\-Z 和 0\-9）开始和结束。 它还可以包括从零到 22 个字母数字或连字符的 ASCII 字符。|  
|`$`|在字符串的结尾结束匹配。|  
  
> [!NOTE]
>  你可以使用 <xref:System.Net.Mail.MailAddress?displayProperty=fullName> 类，而不使用正则表达式来验证电子邮件地址。 若要确定电子邮件地址是否有效，将该电子邮件地址传递到 <xref:System.Net.Mail.MailAddress.%23ctor%28System.String%29?displayProperty=fullName> 类构造函数。  
  
## 编译代码  
 `IsValidEmail` 方法和 `DomainMapper` 方法可以包括在正则表达式实用工具方法库中，或者作为私有静态或实例方法包括在应用程序类中。  
  
 如需将它们包含在正则表达式库中，可将代码复制并粘贴到 Visual Studio 类库项目中，或复制并粘贴到一个文本文件中并从命令行使用如下命令来对其进行编译（假定源代码文件的名称是 RegexUtilities.cs 或 RegexUtilities.vb：  
  
```csharp  
csc /t:library RegexUtilities.cs  
```  
  
```vb  
vbc /t:library RegexUtilities.vb  
```  
  
 还可以使用 <xref:System.Text.RegularExpressions.Regex.CompileToAssembly%2A?displayProperty=fullName> 方法将此正则表达式包含到正则表达式库中。  
  
 如果在正则表达式库中对其进行使用，则可使用例如以下代码对其进行调用：  
  
 [!code-csharp[RegularExpressions.Examples.Email#8](../../../samples/snippets/csharp/VS_Snippets_CLR/RegularExpressions.Examples.Email/cs/example4.cs#8)]
 [!code-vb[RegularExpressions.Examples.Email#8](../../../samples/snippets/visualbasic/VS_Snippets_CLR/RegularExpressions.Examples.Email/vb/example4.vb#8)]  
  
 假设你已创建了一个名为 RegexUtilities.dll 的类库，其中包括你的电子邮件验证正则表达式，你可通过以下方法之一来编译此示例：  
  
-   在 Visual Studio 中，创建一个控制台应用程序并为项目添加一个对 RegexUtilities.dll 的引用。  
  
-   从命令行，将源代码复制和粘贴到文本文件中并使用如下命令来对其进行编译（假定源代码文件的名称是 Example.cs 或 Example.vb：  
  
    ```csharp  
    csc Example.cs /r:RegexUtilities.dll  
    ```  
  
    ```vb  
    vbc Example.vb /r:RegexUtilities.dll  
    ```  
  
## 请参阅  
 [.NET Framework 正则表达式](../../../docs/standard/base-types/regular-expressions.md)