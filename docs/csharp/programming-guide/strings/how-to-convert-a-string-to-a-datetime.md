---
title: "如何：将字符串转换为 DateTime（C# 编程指南）"
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
helpviewer_keywords:
- strings [C#], converting to DateTIme
ms.assetid: 88abef11-3a06-4b49-8dd2-61ed0e876fc3
caps.latest.revision: 21
author: BillWagner
ms.author: wiwagn
translation.priority.ht:
- de-de
- es-es
- fr-fr
- it-it
- ja-jp
- ko-kr
- ru-ru
- zh-cn
- zh-tw
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: 15ef1ec4debf242cdabc42f26add890bd4b61507
ms.contentlocale: zh-cn
ms.lasthandoff: 07/28/2017

---
# <a name="how-to-convert-a-string-to-a-datetime-c-programming-guide"></a>如何：将字符串转换为 DateTime（C# 编程指南）
通常，程序使用户能以字符串值的形式输入日期。 若要将基于字符串的日期转换为 <xref:System.DateTime?displayProperty=fullName> 对象，可以使用 <xref:System.Convert.ToDateTime%28System.String%29?displayProperty=fullName> 方法或 <xref:System.DateTime.Parse%28System.String%29?displayProperty=fullName> 静态方法，如下面的示例中所示。  
  
 **区域性**。  世界上不同区域以不同的方式编写日期字符串。  例如，在美国 01/20/2008 表示 2008 年 1 月 20 日。  在法国这将引发 InvalidFormatException。 因为法国以日/月/年的形式读取日期时间，而美国是月/日/年。  
  
 因此，像 20/01/2008 这样的字符串在法国将解析为 2008 年 1 月 20 日，而在美国则引发 InvalidFormatException。  
  
 若要确定当前的区域性设置，可使用 System.Globalization.CultureInfo.CurrentCulture。  
  
 请参阅下面的示例，了解有关将字符串转换为 dateTime 的简单示例。  
  
 有关日期字符串的更多示例，请参阅 <xref:System.Convert.ToDateTime%28System.String%29?displayProperty=fullName>。  
  
```csharp  
string dateTime = "01/08/2008 14:50:50.42";  
            DateTime dt = Convert.ToDateTime(dateTime);  
            Console.WriteLine("Year: {0}, Month: {1}, Day: {2}, Hour: {3}, Minute: {4}, Second: {5}, Millisecond: {6}",  
                              dt.Year, dt.Month, dt.Day, dt.Hour, dt.Minute, dt.Second, dt.Millisecond);  
            // Specify exactly how to interpret the string.  
            IFormatProvider culture = new System.Globalization.CultureInfo("fr-FR", true);  
  
            // Alternate choice: If the string has been input by an end user, you might    
            // want to format it according to the current culture:   
            // IFormatProvider culture = System.Threading.Thread.CurrentThread.CurrentCulture;  
            DateTime dt2 = DateTime.Parse(dateTime, culture, System.Globalization.DateTimeStyles.AssumeLocal);  
            Console.WriteLine("Year: {0}, Month: {1}, Day: {2}, Hour: {3}, Minute: {4}, Second: {5}, Millisecond: {6}",  
                              dt2.Year, dt2.Month, dt2.Day, dt2.Hour, dt2.Minute, dt2.Second, dt2.Millisecond  
/* Output (assuming first culture is en-US and second is fr-FR):  
    Year: 2008, Month: 1, Day: 8, Hour: 14, Minute: 50, Second: 50, Millisecond: 420  
Year: 2008, Month: 8, Day: 1, Hour: 14, Minute: 50, Second: 50, Millisecond: 420  
Press any key to continue . . .  
 */  
```  
  
## <a name="example"></a>示例  
 [!code-cs[csProgGuideStrings#13](../../../csharp/programming-guide/strings/codesnippet/CSharp/how-to-convert-a-string-to-a-datetime_1.cs)]  
  
## <a name="see-also"></a>请参阅  
 [字符串](../../../csharp/programming-guide/strings/index.md)

