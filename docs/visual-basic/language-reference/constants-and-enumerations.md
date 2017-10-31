---
title: "常量和枚举 (Visual Basic 中) |Microsoft 文档"
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-visual-basic
ms.topic: article
dev_langs:
- VB
helpviewer_keywords:
- enumerations [Visual Basic]
- constants
- constants, list of
ms.assetid: 309c0ad5-83e4-4f96-99ea-83cd95107417
caps.latest.revision: 18
author: dotnet-bot
ms.author: dotnetcontent
translation.priority.ht:
- cs-cz
- de-de
- es-es
- fr-fr
- it-it
- ja-jp
- ko-kr
- pl-pl
- pt-br
- ru-ru
- tr-tr
- zh-cn
- zh-tw
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: e37ef2e3c51e96e85cb214054195016e69d52382
ms.lasthandoff: 03/13/2017

---
# <a name="constants-and-enumerations-visual-basic"></a>常量和枚举 (Visual Basic)
[!INCLUDE[vbprvb](../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]提供许多预定义的常量和枚举，面向开发人员。 常数存储保持不变的应用程序的执行中的值。 枚举提供能够与组相关的常数，并且能够将常量值与名称相关联的简便方法。  
  
## <a name="constants"></a>常量  
  
### <a name="conditional-compilation-constants"></a>条件编译常量  
 下表列出可用于条件编译的预定义的常量。  
  
|**常量**|**描述**|  
|---|---|  
|`CONFIG`|一个字符串，对应的当前设置**活动解决方案配置**框中**Configuration Manager**。|  
|`DEBUG`|一个`Boolean`值，可以在设置**项目属性**对话框。 默认情况下，调试配置项目定义`DEBUG`。 当`DEBUG`定义，则<xref:System.Diagnostics.Debug>类方法将生成的输出传送到**输出**窗口。</xref:System.Diagnostics.Debug> 未定义时,<xref:System.Diagnostics.Debug>类方法不进行编译，不生成任何调试输出。</xref:System.Diagnostics.Debug>|  
|`TARGET`|一个表示项目或命令行中的设置的输出类型的字符串**target**选项。 可能值`TARGET`是︰<br /><br /> -"winexe"为 Windows 应用程序。<br />-"exe"控制台应用程序。<br />-类库"库"。<br />-模块"模块"。<br />- **Target**可能在中设置选项[!INCLUDE[vsprvs](../../csharp/includes/vsprvs_md.md)]集成的开发环境。 有关详细信息，请参阅[/target (Visual Basic 中)](../../visual-basic/reference/command-line-compiler/target.md)。|  
|`TRACE`|一个`Boolean`值，可以在设置**项目属性**对话框。 默认情况下，所有配置项目都定义`TRACE`。 当`TRACE`定义，则<xref:System.Diagnostics.Trace>类方法将生成的输出传送到**输出**窗口。</xref:System.Diagnostics.Trace> 未定义时,<xref:System.Diagnostics.Trace>类方法将不会被编译，但不`Trace`生成输出。</xref:System.Diagnostics.Trace>|  
|`VBC_VER`|一个数字，表示[!INCLUDE[vbprvb](../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]版本，请在*主要*。*次要*格式。 版本号[!INCLUDE[vbprvblong](../../visual-basic/developing-apps/customizing-extending-my/includes/vbprvblong_md.md)]为 8.0。|  
  
### <a name="print-and-display-constants"></a>打印和显示常量  
 当调用输出和显示功能时，您可以使用以下常量代替实际值在代码中。  
  
|**常量**|**描述**|  
|---|---|  
|`vbCrLf`|回车符/换行符的组合。|  
|`vbCr`|回车符。|  
|`vbLf`|换行字符。|  
|`vbNewLine`|换行字符。|  
|`vbNullChar`|Null 字符。|  
|`vbNullString`|不完全相同的长度为零的字符串 ("");用来调用外部过程。|  
|`vbObjectError`|错误号。 用户定义的错误号应大于此值。 例如: <br /><br /> `Err.Raise(Number) = vbObjectError + 1000`|  
|`vbTab`|制表符。|  
|`vbBack`|退格符。|  
|`vbFormFeed`|Microsoft Windows 中未使用。|  
|`vbVerticalTab`|Microsoft Windows 中不很有用。|  
  
## <a name="enumerations"></a>枚举  
 下表列出并描述由提供的枚举[!INCLUDE[vbprvb](../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]。  
  
|枚举|说明|  
|---|---|  
|<xref:Microsoft.VisualBasic.AppWinStyle></xref:Microsoft.VisualBasic.AppWinStyle>|指示要在调用时，可用于所调用的程序的窗口样式<xref:Microsoft.VisualBasic.Interaction.Shell%2A>函数。</xref:Microsoft.VisualBasic.Interaction.Shell%2A>|  
|<xref:Microsoft.VisualBasic.AudioPlayMode></xref:Microsoft.VisualBasic.AudioPlayMode>|指示如何在调用音频方法时播放声音。|  
|<xref:Microsoft.VisualBasic.ApplicationServices.BuiltInRole></xref:Microsoft.VisualBasic.ApplicationServices.BuiltInRole>|指示角色在调用时，检查类型<xref:Microsoft.VisualBasic.ApplicationServices.User.IsInRole%2A>方法。</xref:Microsoft.VisualBasic.ApplicationServices.User.IsInRole%2A>|  
|<xref:Microsoft.VisualBasic.CallType></xref:Microsoft.VisualBasic.CallType>|指示过程调用时，所调用的类型<xref:Microsoft.VisualBasic.Interaction.CallByName%2A>函数。</xref:Microsoft.VisualBasic.Interaction.CallByName%2A>|  
|<xref:Microsoft.VisualBasic.CompareMethod></xref:Microsoft.VisualBasic.CompareMethod>|指示如何比较字符串时调用比较函数。|  
|<xref:Microsoft.VisualBasic.DateFormat></xref:Microsoft.VisualBasic.DateFormat>|指示如何显示日期时调用<xref:Microsoft.VisualBasic.Strings.FormatDateTime%2A>函数。</xref:Microsoft.VisualBasic.Strings.FormatDateTime%2A>|  
|<xref:Microsoft.VisualBasic.DateInterval></xref:Microsoft.VisualBasic.DateInterval>|指示当调用与日期相关的函数时如何确定日期间隔并设置其格式。|  
|<xref:Microsoft.VisualBasic.FileIO.DeleteDirectoryOption></xref:Microsoft.VisualBasic.FileIO.DeleteDirectoryOption>|指定要从中删除一个目录包含文件或目录时应采取的操作。|  
|<xref:Microsoft.VisualBasic.DueDate></xref:Microsoft.VisualBasic.DueDate>|指示何时付款时调用财务方法。|  
|<xref:Microsoft.VisualBasic.FileIO.FieldType></xref:Microsoft.VisualBasic.FileIO.FieldType>|指示文本字段分隔的还是固定宽度。|  
|<xref:Microsoft.VisualBasic.FileAttribute></xref:Microsoft.VisualBasic.FileAttribute>|指示要在调用文件访问函数时使用的文件属性。|  
|<xref:Microsoft.VisualBasic.FirstDayOfWeek></xref:Microsoft.VisualBasic.FirstDayOfWeek>|指示在调用与日期相关的函数时使用的每周的第一天。|  
|<xref:Microsoft.VisualBasic.FirstWeekOfYear></xref:Microsoft.VisualBasic.FirstWeekOfYear>|指示要在调用与日期相关的函数时使用的年份的第一周。|  
|<xref:Microsoft.VisualBasic.MsgBoxResult></xref:Microsoft.VisualBasic.MsgBoxResult>|指示返回的消息框上按下了哪个按钮<xref:Microsoft.VisualBasic.Interaction.MsgBox%2A>函数。</xref:Microsoft.VisualBasic.Interaction.MsgBox%2A>|  
|<xref:Microsoft.VisualBasic.MsgBoxStyle></xref:Microsoft.VisualBasic.MsgBoxStyle>|指示要在调用时显示的按钮<xref:Microsoft.VisualBasic.Interaction.MsgBox%2A>函数。</xref:Microsoft.VisualBasic.Interaction.MsgBox%2A>|  
|<xref:Microsoft.VisualBasic.OpenAccess></xref:Microsoft.VisualBasic.OpenAccess>|指示如何在调用文件访问函数打开一个文件。|  
|<xref:Microsoft.VisualBasic.OpenMode></xref:Microsoft.VisualBasic.OpenMode>|指示如何在调用文件访问函数打开一个文件。|  
|<xref:Microsoft.VisualBasic.OpenShare></xref:Microsoft.VisualBasic.OpenShare>|指示如何在调用文件访问函数打开一个文件。|  
|<xref:Microsoft.VisualBasic.FileIO.RecycleOption></xref:Microsoft.VisualBasic.FileIO.RecycleOption>|指定是否应被永久删除或放在回收站中一个文件。|  
|<xref:Microsoft.VisualBasic.FileIO.SearchOption></xref:Microsoft.VisualBasic.FileIO.SearchOption>|指定是否以搜索所有或仅为顶级目录。|  
|<xref:Microsoft.VisualBasic.TriState></xref:Microsoft.VisualBasic.TriState>|指示`Boolean`值或数字格式的函数调用时是否应使用默认值。|  
|<xref:Microsoft.VisualBasic.FileIO.UICancelOption></xref:Microsoft.VisualBasic.FileIO.UICancelOption>|指定应使用哪些用户单击时执行此操作**取消**一次操作中。|  
|<xref:Microsoft.VisualBasic.FileIO.UIOption></xref:Microsoft.VisualBasic.FileIO.UIOption>|指定在复制、 删除或移动文件或目录时显示进度对话框。|  
|<xref:Microsoft.VisualBasic.VariantType></xref:Microsoft.VisualBasic.VariantType>|指示返回的变体对象的类型<xref:Microsoft.VisualBasic.Information.VarType%2A>函数。</xref:Microsoft.VisualBasic.Information.VarType%2A>|  
|<xref:Microsoft.VisualBasic.VbStrConv></xref:Microsoft.VisualBasic.VbStrConv>|指示哪种类型的转换调用时要执行<xref:Microsoft.VisualBasic.Strings.StrConv%2A>函数。</xref:Microsoft.VisualBasic.Strings.StrConv%2A>|  
  
## <a name="see-also"></a>另请参阅  
 [Visual Basic 语言参考](../../visual-basic/language-reference/index.md)   
 [Visual Basic](../../visual-basic/index.md)   
 [常量概述](../../visual-basic/programming-guide/language-features/constants-enums/constants-overview.md)   
 [枚举概述](../../visual-basic/programming-guide/language-features/constants-enums/enumerations-overview.md)
