---
title: "如何：使用 XML 文档功能（C# 编程指南）"
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
helpviewer_keywords:
- XML documentation [C#]
- C# language, XML documentation features
ms.assetid: 8f33917b-9577-4c9a-818a-640dbbb0b399
caps.latest.revision: 19
author: BillWagner
ms.author: wiwagn
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
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: eeee77db523bc0ad97f425d4ba8076ae5740dfe8
ms.contentlocale: zh-cn
ms.lasthandoff: 07/28/2017

---
# <a name="how-to-use-the-xml-documentation-features-c-programming-guide"></a>如何：使用 XML 文档功能（C# 编程指南）
下面的示例提供对某个已存档类型的基本概述。  
  
## <a name="example"></a>示例  
 [!code-cs[csProgGuideDocComments#15](../../../csharp/programming-guide/xmldoc/codesnippet/CSharp/how-to-use-the-xml-documentation-features_1.cs)]  
  
 **// This .xml file was generated with the previous code sample.**  
**\<?xml version="1.0"?>**  
**\<doc>**  
 **\<assembly>**  
 **\<name>xmlsample\</name>**  
 **\</assembly>**  
 **\<members>**  
 **\<member name="T:SomeClass">**  
 **\<summary>**  
 **Class level summary documentation goes here.\</summary>**  
 **\<remarks>**  
 **Longer comments can be associated with a type or member**   
 **through the remarks tag\</remarks>**  
 **\</member>**  
 **\<member name="F:SomeClass.m_Name">**  
 **\<summary>**  
 **Store for the name property\</summary>**  
 **\</member>**  
 **\<member name="M:SomeClass.#ctor">**  
 **\<summary>The class constructor.\</summary>**   
 **\</member>**  
 **\<member name="M:SomeClass.SomeMethod(System.String)">**  
 **\<summary>**  
 **Description for SomeMethod.\</summary>**  
 **\<param name="s"> Parameter description for s goes here\</param>**  
 **\<seealso cref="T:System.String">**  
 **You can use the cref attribute on any tag to reference a type or member**   
 **and the compiler will check that the reference exists. \</seealso>**  
 **\</member>**  
 **\<member name="M:SomeClass.SomeOtherMethod">**  
 **\<summary>**  
 **Some other method. \</summary>**  
 **\<returns>**  
 **Return results are described through the returns tag.\</returns>**  
 **\<seealso cref="M:SomeClass.SomeMethod(System.String)">**  
 **Notice the use of the cref attribute to reference a specific method \</seealso>**  
 **\</member>**  
 **\<member name="M:SomeClass.Main(System.String[])">**  
 **\<summary>**  
 **The entry point for the application.**  
 **\</summary>**  
 **\<param name="args"> A list of command line arguments\</param>**  
 **\</member>**  
 **\<member name="P:SomeClass.Name">**  
 **\<summary>**  
 **Name property \</summary>**  
 **\<value>**  
 **A value tag is used to describe the property value\</value>**  
 **\</member>**  
 **\</members>**  
**\</doc>**   
## <a name="compiling-the-code"></a>编译代码  
 若要编译该示例，请键入以下命令行：  
  
 `csc XMLsample.cs /doc:XMLsample.xml`  
  
 这将创建 XML 文件 XMLsample.xml，可在浏览器中或使用 TYPE 命令查看该文件。  
  
## <a name="robust-programming"></a>可靠编程  
 XML 文档以 /// 开头。 创建新项目时，向导会放置一些以 /// 开头的行。 处理这些注释时存在一些限制：  
  
-   文档必须是格式正确的 XML。 如果 XML 格式不正确，则会生成警告，并且文档文件将包含一条注释，指出遇到错误。  
  
-   开发人员可以随意创建自己的标记集。 有建议的标记集（请参阅“更多参考资料”部分）。 部分建议标记具有特殊含义：  
  
    -   \<param> 标记用于描述参数。 如果使用，编译器将验证该参数是否存在，以及文档是否描述了所有参数。 如果验证失败，编译器会发出警告。  
  
    -   `cref` 属性可以附加到任何标记，以提供对代码元素的引用。 编译器将验证此代码元素是否存在。 如果验证失败，编译器会发出警告。 编译器在查找 `cref` 属性中描述的类型时会考虑所有 `using` 语句。  
  
    -   \<summary> 标记由 Visual Studio 中的 IntelliSense 用于显示有关某个类型或成员的附加信息。  
  
        > [!NOTE]
        >  XML 文件不提供有关该类型和成员的完整信息（例如，它不包含任何类型信息）。 若要获取有关类型或成员的完整信息，必须将文档文件与对实际类型或成员的反射一起使用。  
  
## <a name="see-also"></a>请参阅  
 [C# 编程指南](../../../csharp/programming-guide/index.md)   
 [/doc（C# 编译器选项）](../../../csharp/language-reference/compiler-options/doc-compiler-option.md)   
 [XML 文档注释](../../../csharp/programming-guide/xmldoc/xml-documentation-comments.md)

