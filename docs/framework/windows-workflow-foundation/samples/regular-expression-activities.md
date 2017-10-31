---
title: "正则表达式活动 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: b8f24694-49db-4339-92ec-014e3d4ae63b
caps.latest.revision: 9
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 9
---
# 正则表达式活动
此示例演示如何一组活动，这些活动公开 <xref:System.Text.RegularExpressions> 命名空间的正则表达式功能。可以在工作流应用程序内使用这些自定义活动。[!INCLUDE[crabout](../../../../includes/crabout-md.md)] 有关正则表达式，请参阅 [N:System.Text.RegularExpressions](http://go.microsoft.com/fwlink/?LinkId=150434) 命名空间。  
  
 下表详细介绍了此示例中的自定义活动。  
  
|活动|说明|  
|--------|--------|  
|IsMatch|指定正则表达式是否在输入字符串中找到了匹配项。|  
|Matches|在输入字符串中搜索所有正则表达式，然后返回所有成功的匹配项。|  
|Replace|在指定的输入字符串中，用指定的替换字符串来替换与正则表达式模式匹配的字符串。|  
  
## IsMatch  
 如果 `Input` 字符串属性在 `Pattern` 属性中指定的正则表达式中找到匹配项，则 `IsMatch` 自定义活动返回 `true`。该活动派生自 <xref:System.Activities.CodeActivity%601>，并在 <xref:System.Activities.CodeActivity%601.Execute%2A> 方法中调用 <xref:System.Text.RegularExpressions.Regex.IsMatch%2A> 方法。  
  
 下表描述了 `IsMatch` 自定义活动的属性和返回值。  
  
|属性或返回值|说明|  
|------------|--------|  
|Pattern（必需）|用于搜索的正则表达式。|  
|Input（必需）|要搜索的输入字符串。|  
|RegexOptions|[RegexOptions](http://go.microsoft.com/fwlink/?LinkId=150446) 枚举值的按位“或”组合。|  
|返回值|如果输入找到了符合所提供的模式的匹配项，则为 `true`；否则为 `false`。|  
  
 下面的代码示例演示如何使用 `IsMatch` 自定义活动。  
  
```  
new IsMatch  
{  
    Pattern = new InArgument<string>( @"^-?\d+(\.\d{2})?$"),  
    Input = "20.00",  
};  
  
```  
  
## Matches  
 `Matches` 自定义活动在输入字符串中搜索所有正则表达式，然后返回所有成功的匹配项。该活动派生自 <xref:System.Activities.CodeActivity%601>，并在 <xref:System.Activities.CodeActivity%601.Execute%2A> 方法中调用 <xref:System.Text.RegularExpressions.Regex.Matches%2A> 方法。  
  
 下表描述了 `IsMatch` 自定义活动的属性和返回值。  
  
|属性或返回值|说明|  
|------------|--------|  
|Pattern（必需）|用于搜索的正则表达式。|  
|Input（必需）|要搜索的输入字符串。|  
|RegexOptions|[RegexOptions](http://go.microsoft.com/fwlink/?LinkId=150446) 枚举值的按位“或”组合。|  
|返回值|一个包含成功匹配项的集合的 <xref:System.Text.RegularExpressions.MatchCollection>。|  
  
 下面的代码示例演示如何使用 `Matches` 自定义活动。  
  
```  
new Matches  
{  
    Pattern = @"\b(?<word>\w+)\s+(\k<word>)\b",  
    Input = "The quick brown fox  fox jumped over over the lazy dog dog.",  
};  
  
```  
  
## Replace  
 `Replace` 自定义活动搜索输入字符串，然后用一个字符串来替换与指定的正则表达式匹配的所有字符串。该活动派生自 <xref:System.Activities.CodeActivity%601>，并在 <xref:System.Activities.CodeActivity%601.Execute%2A> 方法中调用 <xref:System.Text.RegularExpressions.Regex.Replace%2A> 方法。  
  
 下表描述了 `Replace` 自定义活动的属性和返回值。  
  
|属性或返回值|说明|  
|------------|--------|  
|Pattern（必需）|用于搜索的正则表达式。|  
|Input（必需）|要搜索的输入字符串。|  
|Replacement|替换字符串。<br /><br /> 如果指定 `Replacement`，则将忽略 `MatchEvaluator` 属性。必须设置 `Replacement` 或 `MatchEvaluator` 属性中的一个。|  
|MatchEvaluator|一个自定义方法，该方法检查每个匹配项，然后返回原始的匹配字符串或替换字符串。<br /><br /> 如果指定 `Replacement`，则将忽略 `MatchEvaluator` 属性。必须设置 `Replacement` 或 `MatchEvaluator` 属性中的一个。|  
|RegexOptions|[RegexOptions](http://go.microsoft.com/fwlink/?LinkId=150446) 枚举值的按位“或”组合。|  
|返回值|一个包含成功匹配项的集合的 <xref:System.Text.RegularExpressions.MatchCollection>。|  
  
 下面的代码示例演示如何使用 `Replace` 自定义活动。  
  
```  
// Using the replacement string.  
new Replace  
{  
    Pattern = @"\bWorld\b",  
    Input = "Hello World! This is a wonderful World",  
    Replacement = "Universe"  
};  
  
// Using a match evaluator.  
new Replace  
{  
    Pattern = new InArgument<string>(pattern),  
    Input = new InArgument<string>(input),  
    MatchEvaluator = new MatchEvaluator(CapText)                  
};  
  
```  
  
#### 使用此示例  
  
1.  使用 [!INCLUDE[vs2010](../../../../includes/vs2010-md.md)] 打开 RegexActivities.sln 解决方案文件。  
  
2.  要生成解决方案，按 Ctrl\+Shift\+B。  
  
3.  若要运行解决方案，请按 Ctrl\+F5。  
  
> [!IMPORTANT]
>  您的计算机上可能已安装这些示例。在继续操作之前，请先检查以下（默认）目录：  
>   
>  `<安装驱动器>:\WF_WCF_Samples`  
>   
>  如果此目录不存在，请访问[针对 .NET Framework 4 的 Windows Communication Foundation \(WCF\) 和 Windows Workflow Foundation \(WF\) 示例](http://go.microsoft.com/fwlink/?LinkId=150780)（可能为英文网页），下载所有 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 和 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 示例。此示例位于以下目录：  
>   
>  `<安装驱动器>:\WF_WCF_Samples\WF\Scenario\ActivityLibrary\Regex`  
  
## 请参阅