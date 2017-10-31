---
title: "在集合中执行不区分区域性的字符串操作 | Microsoft Docs"
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
  - "ArrayList.Sort 方法"
  - "CaseInsensitiveComparer 类, using"
  - "CaseInsensitiveHashCodeProvider 类, using"
  - "集合 [.NET Framework], 不区分区域性的字符串操作"
  - "CollectionsUtil.CreateCaseInsensitiveHashtable 方法"
  - "区域性参数"
  - "不区分区域性的字符串操作, 集合"
  - "SortedList 类, 不区分区域性的字符串操作"
ms.assetid: 5cdc9396-a64b-4615-a1cd-b605db4c5983
caps.latest.revision: 12
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 11
---
# 在集合中执行不区分区域性的字符串操作
在 <xref:System.Collections> 命名空间中有一些类和成员在默认情况下提供区分区域性的行为。  <xref:System.Collections.CaseInsensitiveComparer> 和 <xref:System.Collections.CaseInsensitiveHashCodeProvider> 类的默认构造函数使用 <xref:System.Threading.Thread.CurrentCulture%2A?displayProperty=fullName> 属性来初始化新实例。  默认情况下，[CollectionsUtil.CreateCaseInsensitiveHashTable](frlrfSystemCollectionsSpecializedCollectionsUtilClassCreateCaseInsensitiveHashtableTopic) 方法的所有重载都使用 `Thread.CurrentCulture` 属性来创建 <xref:System.Collections.Hashtable> 类的新实例。  默认情况下，<xref:System.Collections.ArrayList.Sort%2A?displayProperty=fullName> 方法的重载使用 `Thread.CurrentCulture` 来执行区分区域性的排序。  将字符串用作键时，在 <xref:System.Collections.SortedList> 中进行排序和查找会受 `Thread.CurrentCulture` 的影响。  请按本节提供的用法建议，使用 `Collections` 命名空间中的这些类和方法获取不区分区域性的结果。  
  
 **注意** 将 <xref:System.Globalization.CultureInfo.InvariantCulture%2A?displayProperty=fullName> 传递给比较方法时，将执行不区分区域性的比较。  但是，这样做不会导致对文件路径、注册表项、环境变量等进行非语义比较，  也不支持基于比较结果的安全决策。  若要进行非语义比较或支持基于结果的安全决策，应用程序应使用接受 <xref:System.StringComparison> 值的比较方法。  因而，应用程序应传递 <xref:System.StringComparison>。  
  
## 使用 CaseInsensitiveComparer 和 CaseInsensitiveHashCodeProvider 类  
 `CaseInsensitiveHashCodeProvider` 和 `CaseInsensitiveComparer` 的默认构造函数使用 `Thread.CurrentCulture` 来初始化类的新实例，因而产生区分区域性的行为。  下面的代码示例演示一个 `Hashtable` 的构造函数，该构造函数使用 `CaseInsensitiveHashCodeProvider` 和 `CaseInsensitiveComparer` 的默认构造函数，因而区分区域性。  
  
```vb  
internalHashtable = New Hashtable(CaseInsensitiveHashCodeProvider.Default, CaseInsensitiveComparer.Default)  
  
```  
  
```csharp  
internalHashtable = new Hashtable(CaseInsensitiveHashCodeProvider.Default, CaseInsensitiveComparer.Default);  
```  
  
 如果要使用 `CaseInsensitiveComparer` 和 `CaseInsensitiveHashCodeProvider` 类创建不区分区域性的 `Hashtable`，请使用接受 `culture` 参数的构造函数来初始化这些类的新实例。  对于 `culture` 参数，请指定 <xref:System.Globalization.CultureInfo.InvariantCulture%2A?displayProperty=fullName>。  下面的代码示例演示不区分区域性的 `Hashtable` 的构造函数。  
  
```vb  
internalHashtable = New Hashtable(New  
    CaseInsensitiveHashCodeProvider(CultureInfo.InvariantCulture),  
    New CaseInsensitiveComparer(CultureInfo.InvariantCulture))  
  
```  
  
```csharp  
internalHashtable = new Hashtable(new CaseInsensitiveHashCodeProvider  
    (CultureInfo.InvariantCulture),   
    new CaseInsensitiveComparer(CultureInfo.InvariantCulture));  
```  
  
## 使用 CollectionsUtil.CreateCaseInsensitiveHashTable 方法  
 若要为 `Hashtable` 类创建一个忽略字符串大小写的新实例，`CollectionsUtil.CreateCaseInsensitiveHashTable` 方法是一种十分有用的便捷方式。  但是，`CollectionsUtil.CreateCaseInsensitiveHashTable` 方法的所有重载都区分区域性，因为这些重载使用 `Thread.CurrentCulture` 属性。  您无法使用此方法创建不区分区域性的 `Hashtable`。  若要创建不区分区域性的 `Hashtable`，请使用接受 `culture` 参数的 `Hashtable` 构造函数。  对于 `culture` 参数，请指定 `CultureInfo.InvariantCulture`。  下面的代码示例演示不区分区域性的 `Hashtable` 的构造函数。  
  
```vb  
internalHashtable = New Hashtable(New  
    CaseInsensitiveHashCodeProvider(CultureInfo.InvariantCulture),  
    New CaseInsensitiveComparer(CultureInfo.InvariantCulture))  
  
```  
  
```csharp  
internalHashtable = new Hashtable(new CaseInsensitiveHashCodeProvider  
    (CultureInfo.InvariantCulture),   
    new CaseInsensitiveComparer(CultureInfo.InvariantCulture));  
```  
  
<a name="cpconperformingculture-insensitivestringoperationsincollectionsanchor1"></a>   
## 使用 SortedList 类  
 `SortedList` 表示键\/值对的集合，这些键\/值对按键排序，可按键和索引进行访问。  在使用以字符串作为键的 `SortedList` 时，排序和查找会受 `Thread.CurrentCulture` 属性的影响。  若要从 `SortedList` 获取不区分区域性的行为，请使用某个接受 `comparer` 参数的构造函数来创建 `SortedList`。  `comparer` 参数指定比较键时要使用的 <xref:System.Collections.IComparer> 实现。  对于该参数，请指定使用 `CultureInfo.InvariantCulture` 来比较键的自定义比较器类。  下面的示例说明一个不区分区域性的自定义比较器类，您可将其指定为 `SortedList` 构造函数的 `comparer` 参数。  
  
```vb  
Imports System  
Imports System.Collections  
Imports System.Globalization  
  
Friend Class InvariantComparer  
    Implements IComparer   
    Private m_compareInfo As CompareInfo  
    Friend Shared [Default] As New InvariantComparer()  
  
    Friend Sub New()  
        m_compareInfo = CultureInfo.InvariantCulture.CompareInfo  
    End Sub     
  
    Public Function Compare(a As Object, b As Object) As Integer _  
            Implements IComparer.Compare  
        Dim sa As String = CType(a, String)  
        Dim sb As String = CType(b, String)  
        If Not (sa Is Nothing) And Not (sb Is Nothing) Then  
            Return m_compareInfo.Compare(sa, sb)  
        Else  
            Return Comparer.Default.Compare(a, b)  
        End If  
    End Function  
End Class  
  
```  
  
```csharp  
using System;  
using System.Collections;  
using System.Globalization;  
  
internal class InvariantComparer : IComparer   
{  
    private CompareInfo m_compareInfo;  
    internal static readonly InvariantComparer Default = new  
        InvariantComparer();  
  
    internal InvariantComparer()   
    {  
        m_compareInfo = CultureInfo.InvariantCulture.CompareInfo;  
    }  
  
    public int Compare(Object a, Object b)  
    {  
        String sa = a as String;  
        String sb = b as String;  
        if (sa != null && sb != null)  
            return m_compareInfo.Compare(sa, sb);  
        else  
            return Comparer.Default.Compare(a,b);  
    }  
}  
```  
  
 一般而言，如果对字符串使用 `SortedList` 而不指定自定义固定比较器，则在填充列表后，更改 `Thread.CurrentCulture` 会使列表失效。  
  
## 使用 ArrayList.Sort 方法  
 默认情况下，`ArrayList.Sort` 方法的重载使用 `Thread.CurrentCulture` 属性来执行区分区域性的排序。  由于排序顺序不同，结果可能会因区域性而异。  若要消除区分区域性的行为，请使用此方法的接受 `IComparer` 实现的重载。  对于 `comparer` 参数，请指定使用 `CultureInfo.InvariantCulture` 的自定义固定比较器类。  [使用 SortedList 类](#cpconperformingculture-insensitivestringoperationsincollectionsanchor1)主题中提供了自定义固定比较器类的示例。  
  
## 请参阅  
 <xref:System.Collections.CaseInsensitiveComparer>   
 <xref:System.Collections.CaseInsensitiveHashCodeProvider>   
 <xref:System.Collections.ArrayList.Sort%2A?displayProperty=fullName>   
 <xref:System.Collections.SortedList>   
 <xref:System.Collections.Hashtable>   
 <xref:System.Collections.IComparer>   
 [执行不区分区域性的字符串操作](../../../docs/standard/globalization-localization/performing-culture-insensitive-string-operations.md)   
 [CollectionsUtil.CreateCaseInsensitiveHashTable 方法](frlrfSystemCollectionsSpecializedCollectionsUtilClassCreateCaseInsensitiveHashtableTopic)