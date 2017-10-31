---
title: "SqlMetal.exe（代码生成工具）"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology:
- dotnet-clr
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- VB
- CSharp
- C++
- jsharp
helpviewer_keywords:
- SQLMetal [LINQ to SQL]
- code generation tool
- SQLMetal.exe
- LINQ to SQL, serialization
- LINQ to SQL, DBML files
- LINQ to SQL, SQLMetal
ms.assetid: 819e5a96-7646-4fdb-b14b-fe31221b0614
caps.latest.revision: 43
author: Erikre
ms.author: erikre
manager: erikre
ms.translationtype: HT
ms.sourcegitcommit: 306c608dc7f97594ef6f72ae0f5aaba596c936e1
ms.openlocfilehash: 6d0ac9c682c60db8eb9e5188a71916dc5d97de60
ms.contentlocale: zh-cn
ms.lasthandoff: 07/28/2017

---
# <a name="sqlmetalexe-code-generation-tool"></a>SqlMetal.exe（代码生成工具）
SqlMetal 命令行工具可为 [!INCLUDE[vbtecdlinq](../../../includes/vbtecdlinq-md.md)] 的 [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)]组件生成代码和映射。 通过应用本主题后面出现的选项，可以指示 SqlMetal 执行若干种不同的操作，其中包括：  
  
-   从数据库生成源代码和映射特性或映射文件。  
  
-   从数据库生成供自定义使用的中间数据库标记语言 (.dbml) 文件。  
  
-   从 .dbml 文件生成代码和映射特性或映射文件。  
  
 此工具会自动随 Visual Studio 一起安装。 默认情况下，此文件位于 `drive`:\Program Files\Microsoft SDKs\Windows\v`n.nn`\bin 下。 如果没有安装 Visual Studio，也可以通过下载 [Windows SDK](http://go.microsoft.com/fwlink/?LinkId=142225)获取 SQLMetal 文件。  
  
> [!NOTE]
>  使用 Visual Studio 的开发人员还可以使用 [!INCLUDE[vs_ordesigner_long](../../../includes/vs-ordesigner-long-md.md)] 生成实体类。 对于大型数据库，这种命令行方法具有很好的扩展性。 由于 SqlMetal 是一个命令行工具，因此可以在生成过程中使用它。  
  
 若要运行此工具，请使用开发人员命令提示（或 Windows 7 中的 Visual Studio 命令提示）。 有关详细信息，请参阅[命令提示符](../../../docs/framework/tools/developer-command-prompt-for-vs.md)。在命令提示符处，键入以下内容：  
  
## <a name="syntax"></a>语法  
  
```  
sqlmetal [options] [<input file>]  
```  
  
## <a name="options"></a>选项  
 要查看最新的选项列表，请在安装位置的命令提示符处键入 `sqlmetal /?` 。  
  
 **连接选项**  
  
|选项|描述|  
|------------|-----------------|  
|/server: \<name>|指定数据库服务器名称。|  
|/database: \<name>|指定服务器上的数据库目录。|  
|/user: \<name>|指定登录用户 ID。 默认值：使用 Windows 身份验证。|  
|/password: \<password>|指定登录密码。 默认值：使用 Windows 身份验证。|  
|/conn: \<connection string>|指定数据库连接字符串。 不能与 **/server**、 **/database**、 **/user**或 **/password** 选项一起使用。<br /><br /> 不要在连接字符串中包含文件名， 而应将文件名作为输入文件添加到命令行中。 例如，下一行命令将“c:\northwnd.mdf”指定为输入文件： **sqlmetal /code:"c:\northwind.cs" /language:csharp "c:\northwnd.mdf"**。|  
|/timeout: \<seconds>|指定 SqlMetal 访问数据库时的超时值。 默认值：0（即没有时间限制）。|  
  
 **提取选项**  
  
|选项|描述|  
|------------|-----------------|  
|**/views**|提取数据库视图。|  
|**/functions**|提取数据库函数。|  
|**/sprocs**|提取存储过程。|  
  
 **输出选项**  
  
|选项|描述|  
|------------|-----------------|  
|**/dbml** *[:file]*|采用 .dbml 格式发送输出。 不能与 **/map** 选项一起使用。|  
|**/code** *[:file]*|以源代码形式发送输出。 不能与 **/dbml** 选项一起使用。|  
|**/map** *[:file]*|生成 XML 映射文件而不是特性。 不能与 **/dbml** 选项一起使用。|  
  
 **杂项**  
  
|选项|描述|  
|------------|-----------------|  
|/language: \<language>|指定源代码语言。<br /><br /> 有效 \<language>：vb、csharp。<br /><br /> 默认值：从代码文件的扩展名派生。|  
|/namespace: \<name>|为生成的代码指定命名空间。 默认值：无命名空间。|  
|/context: \<type>|指定数据上下文类的名称。 默认值：从数据库名称派生。|  
|/entitybase: \<type>|指定生成的代码中的实体类的基类。 默认值：实体没有基类。|  
|**/pluralize**|自动为类和成员名称应用复数或单数形式。<br /><br /> 此选项仅在美国可用。英文版。|  
|/serialization: \<option>|生成可序列化类。<br /><br /> 有效 \<option>：None、Unidirectional。 默认值：None。<br /><br /> 有关详细信息，请参阅[序列化](../../../docs/framework/data/adonet/sql/linq/serialization.md)。|  
  
 **输入文件**  
  
|选项|描述|  
|------------|-----------------|  
|\<input file>|指定 SQL Server Express .mdf 文件、 [!INCLUDE[ssEW](../../../includes/ssew-md.md)] .sdf 文件或 .dbml 中间文件。|  
  
## <a name="remarks"></a>备注  
 SqlMetal 功能实际涉及两个步骤：  
  
-   将数据库的元数据提取到一个 .dbml 文件中。  
  
-   生成一个代码输出文件。  
  
     通过使用适当的命令行选项，可以生成 [!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)] 或 C# 源代码，也可以生成 XML 映射文件。  
  
 若要从 .mdf 文件中提取元数据，必须在所有其他选项后指定 .mdf 文件的名称。  
  
 如果没有指定 **/server** ，则假定为 **localhost/sqlexpress** 。  
  
 如果存在下列一种或多种情况，[!INCLUDE[sqprsqext](../../../includes/sqprsqext-md.md)] 将引发异常：  
  
-   SqlMetal 尝试提取进行自我调用的存储过程。  
  
-   存储过程、函数或视图的嵌套级别超过 32。  
  
     SqlMetal 将捕获此异常并将其报告为警告。  
  
 若要指定一个输入文件名，请将该名称作为输入文件添加到命令行。 不支持在连接字符串中包含文件名（使用 **/conn** 选项）。  
  
## <a name="examples"></a>示例  
 生成一个包含提取的 SQL 元数据的 .dbml 文件：  
  
 **sqlmetal /server:myserver /database:northwind /dbml:mymeta.dbml**  
  
 使用 SQL Server Express 生成一个包含从 .mdf 文件中提取的 SQL 元数据的 .dbml 文件：  
  
 **sqlmetal /dbml:mymeta.dbml mydbfile.mdf**  
  
 生成一个包含从 SQL Server Express 中提取的 SQL 元数据的 .dbml 文件：  
  
 **sqlmetal /server:.\sqlexpress /dbml:mymeta.dbml /database:northwind**  
  
 从 .dbml 元数据文件生成源代码：  
  
 **sqlmetal /namespace:nwind /code:nwind.cs /language:csharp mymetal.dbml**  
  
 直接从 SQL 元数据生成源代码：  
  
 **sqlmetal /server:myserver /database:northwind /namespace:nwind /code:nwind.cs /language:csharp**  
  
> [!NOTE]
>  如果对 Northwind 示例数据库应用 **/pluralize** 选项，请注意以下行为。 如果 SqlMetal 为表创建了行类型的名称，表名将采用单数形式。 如果它为表创建了 <xref:System.Data.Linq.DataContext> 属性，则表名将采用复数形式。 巧合的是，Northwind 示例数据库中的表名已采用复数形式。 因此，你将看不到这种效果。 尽管数据库表普遍命名为单数形式，但在 .NET 中，将集合命名为复数形式也是一种常见的做法。  
  
## <a name="see-also"></a>另请参阅  
 [如何：在 Visual Basic 或 C# 中生成对象模型](../../../docs/framework/data/adonet/sql/linq/how-to-generate-the-object-model-in-visual-basic-or-csharp.md)   
 [LINQ to SQL 中的代码生成](../../../docs/framework/data/adonet/sql/linq/code-generation-in-linq-to-sql.md)   
 [外部映射](../../../docs/framework/data/adonet/sql/linq/external-mapping.md)

