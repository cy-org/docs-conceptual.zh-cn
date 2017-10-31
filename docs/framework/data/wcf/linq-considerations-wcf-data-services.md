---
title: "LINQ 注意事项（WCF 数据服务） | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-oob"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "WCF 数据服务 LINQ"
  - "查询数据服务 [WCF 数据服务]"
  - "WCF 数据服务查询"
ms.assetid: cc4ec9e9-348f-42a6-a78e-1cd40e370656
caps.latest.revision: 5
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 5
---
# LINQ 注意事项（WCF 数据服务）
本主题提供有关使用 [!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)] 客户端时 LINQ 查询的编写和执行方式的信息以及使用 LINQ 查询实现[!INCLUDE[ssODataFull](../../../../includes/ssodatafull-md.md)] 的数据服务的限制。 [!INCLUDE[crabout](../../../../includes/crabout-md.md)]编写和执行针对查询[!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)]-基于数据服务，请参阅[查询数据服务](../../../../docs/framework/data/wcf/querying-the-data-service-wcf-data-services.md)。  
  
## <a name="composing-linq-queries"></a>编写 LINQ 查询  
 LINQ 使您可以编写针对实现的对象集合查询<xref:System.Collections.Generic.IEnumerable%601>。 这两个**添加服务引用**中对话框[!INCLUDE[vs_current_short](../../../../includes/vs-current-short-md.md)]和 DataSvcUtil.exe 工具用于生成的表示形式[!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)]服务作为继承的实体容器类<xref:System.Data.Services.Client.DataServiceContext>，以及对象的表示源中返回的实体。 这些工具还可为由服务作为源公开的集合的实体容器类生成属性。 上述每个属性的类封装了数据服务返回的<xref:System.Data.Services.Client.DataServiceQuery%601>。 因为<xref:System.Data.Services.Client.DataServiceQuery%601>类实现<xref:System.Linq.IQueryable%601>接口定义的 LINQ 中，您可以编写 LINQ 查询针对数据服务公开的源会将其转换由客户端库为查询请求发送到执行数据服务的 URI。  
  
> [!IMPORTANT]
>  可以采用 LINQ 语法表示的查询集大于 [!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)] 数据服务使用的 URI 语法所支持的查询集。 一个<xref:System.NotSupportedException>时不能将查询映射到目标数据服务中的 URI，将引发。 [!INCLUDE[crdefault](../../../../includes/crdefault-md.md)][不受支持的 LINQ 方法](../../../../docs/framework/data/wcf/linq-considerations-wcf-data-services.md#unsupportedMethods)本主题中。  
  
 下面的示例是一个 LINQ 查询，它返回运费成本超过&30; 美元的 `Orders` 并按装运日期对结果进行排序，最近的装运日期排在最前面：  
  
  [Astoria NorthwindClient #AddQueryOptionsLinqSpecific](../../../../amples/snippets/xml/VS_Snippets_Misc/astoria northwind service/astoria.vsmdi NorthwindClient#AddQueryOptionsLinqSpecific)]  
  
 此 LINQ 查询转换为以下查询 URI 执行针对基于罗斯文的[快速入门](../../../../docs/framework/data/wcf/quickstart-wcf-data-services.md)数据服务︰  
  
```  
http://localhost:12345/Northwind.svc/Orders?Orderby=ShippedDate&?filter=Freight gt 30  
```  
  
 有关 LINQ 的更多常规信息，请参阅[LINQ （语言集成查询）](../Topic/LINQ%20\(Language-Integrated%20Query\).md)。  
  
 LINQ 允许使用语言特定声明查询语法（如上例所示）和一组称为标准查询运算符的查询方法编写查询。 通过仅使用基于方法的语法可以编写与上例等效的查询，如下面的示例所示：  
  
  [Astoria NorthwindClient #AddQueryOptionsLinqExpressionSpecific](../../../../amples/snippets/xml/VS_Snippets_Misc/astoria northwind service/astoria.vsmdi NorthwindClient#AddQueryOptionsLinqExpressionSpecific)]  
  
 [!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)]客户端能够将用这两种方式编写的查询转换为查询 URI，并且可以通过向查询表达式追加查询方法来扩展 LINQ 查询。 当向查询表达式追加方法语法编写 LINQ 查询或<xref:System.Data.Services.Client.DataServiceQuery%601>，操作添加到查询 URI 中调用方法的顺序。 这等效于调用<xref:System.Data.Services.Client.DataServiceQuery%601.AddQueryOption%2A>方法将每个查询选项添加到查询 URI。  
  
## <a name="executing-linq-queries"></a>执行 LINQ 查询  
 某些 LINQ 查询方法，如<xref:System.Linq.Enumerable.First%60%601%28System.Collections.Generic.IEnumerable%7B%60%600%7D%29>或<xref:System.Linq.Enumerable.Single%60%601%28System.Collections.Generic.IEnumerable%7B%60%600%7D%29>，当追加到查询中，导致要执行的查询。 在隐式枚举结果时也会执行查询，例如在 `foreach` 循环过程中或将查询分配给一个 `List` 集合时。 有关详细信息，请参阅[查询数据服务](../../../../docs/framework/data/wcf/querying-the-data-service-wcf-data-services.md)。  
  
 客户端分两个部分来执行 LINQ 查询。 只要有可能，将首先在客户端上计算查询中的 LINQ 表达式，然后生成基于 URI 的查询并将其发送至数据服务，以针对服务中的数据进行计算。 有关详细信息，请参阅部分[客户端与服务器执行](../../../../docs/framework/data/wcf/querying-the-data-service-wcf-data-services.md#executingQueries)中[查询数据服务](../../../../docs/framework/data/wcf/querying-the-data-service-wcf-data-services.md)。  
  
 如果 LINQ 查询无法在 [!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)] 兼容的查询 URI 中进行转换，则尝试执行时将引发异常。 有关详细信息，请参阅[查询数据服务](../../../../docs/framework/data/wcf/querying-the-data-service-wcf-data-services.md)。  
  
## <a name="linq-query-examples"></a>LINQ 查询示例  
 以下各小节中的示例揭示了可针对 [!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)] 服务执行的 LINQ 查询的种类。  
  
<a name="filtering"></a>   
### <a name="filtering"></a>筛选  
 本小节中的 LINQ 查询示例将筛选由服务返回的源中的数据。  
  
 下面这些示例是等效的查询，它们将筛选返回的 `Orders` 实体并仅返回运费成本高于&30; 美元的订单：  
  
-   使用 LINQ 查询语法：  
  
      [Astoria NorthwindClient #LinqWhereClauseSpecific](../../../../amples/snippets/xml/VS_Snippets_Misc/astoria northwind service/astoria.vsmdi NorthwindClient#LinqWhereClauseSpecific)]  
  
-   使用 LINQ 查询方法：  
  
      [Astoria NorthwindClient #LinqWhereMethodSpecific](../../../../amples/snippets/xml/VS_Snippets_Misc/astoria northwind service/astoria.vsmdi NorthwindClient#LinqWhereMethodSpecific)]  
  
-   URI 查询字符串 `$filter` 选项：  
  
      [Astoria NorthwindClient #ExplicitQueryWhereMethodSpecific](../../../../amples/snippets/xml/VS_Snippets_Misc/astoria northwind service/astoria.vsmdi NorthwindClient#ExplicitQueryWhereMethodSpecific)]  
  
 前面的所有示例都将转换为查询 URI：`http://localhost:12345/northwind.svc/Orders()?$filter=Freight gt 30M`。  
  
<a name="sorting"></a>   
### <a name="sorting"></a>排序  
 下面的示例显示了按公司名称和邮政编码降序排序返回的数据的等效查询：  
  
-   使用 LINQ 查询语法：  
  
      [Astoria NorthwindClient #LinqOrderByClauseSpecific](../../../../amples/snippets/xml/VS_Snippets_Misc/astoria northwind service/astoria.vsmdi NorthwindClient#LinqOrderByClauseSpecific)]  
  
-   使用 LINQ 查询方法：  
  
      [Astoria NorthwindClient #LinqOrderByMethodSpecific](../../../../amples/snippets/xml/VS_Snippets_Misc/astoria northwind service/astoria.vsmdi NorthwindClient#LinqOrderByMethodSpecific)]  
  
-   URI 查询字符串 `$orderby` 选项：  
  
      [Astoria NorthwindClient #ExplicitQueryOrderByMethodSpecific](../../../../amples/snippets/xml/VS_Snippets_Misc/astoria northwind service/astoria.vsmdi NorthwindClient#ExplicitQueryOrderByMethodSpecific)]  
  
 前面的所有示例都将转换为查询 URI：`http://localhost:12345/northwind.svc/Customers()?$orderby=CompanyName,PostalCode desc`。  
  
<a name="projection"></a>   
### <a name="projection"></a>投影  
 下面的示例显示了将返回的数据投影到较窄的 `CustomerAddress` 类型的等效查询：  
  
-   使用 LINQ 查询语法：  
  
      [Astoria NorthwindClient #LinqSelectClauseSpecific](../../../../amples/snippets/xml/VS_Snippets_Misc/astoria northwind service/astoria.vsmdi NorthwindClient#LinqSelectClauseSpecific)]  
  
-   使用 LINQ 查询方法：  
  
      [Astoria NorthwindClient #LinqSelectMethodSpecific](../../../../amples/snippets/xml/VS_Snippets_Misc/astoria northwind service/astoria.vsmdi NorthwindClient#LinqSelectMethodSpecific)]  
  
> [!NOTE]
>  `$select`使用，无法将查询选项添加到查询 URI <xref:System.Data.Services.Client.DataServiceQuery%601.AddQueryOption%2A>方法。 我们建议使用 LINQ<xref:System.Linq.Enumerable.Select%2A>方法，以使客户端生成`$select`查询请求 URI 中的选项。\</TSource, TResult>  
  
 前面的两个示例都将转换为查询 URI：`"http://localhost:12345/northwind.svc/Customers()?$filter=Country eq 'GerGerm'&$select=CustomerID,Address,City,Region,PostalCode,Country"`。  
  
<a name="paging"></a>   
### <a name="client-paging"></a>客户端分页  
 下面所示的等效查询示例将请求返回一页包含 25 个订单的排序订单实体，并跳过前 50 个订单：  
  
-   为 LINQ 查询应用查询方法：  
  
      [Astoria NorthwindClient #LinqSkipTakeMethodSpecific](../../../../amples/snippets/xml/VS_Snippets_Misc/astoria northwind service/astoria.vsmdi NorthwindClient#LinqSkipTakeMethodSpecific)]  
  
-   URI 查询字符串 `$skip` 和 `$top` 选项：  
  
      [Astoria NorthwindClient #ExplicitQuerySkipTakeMethodSpecific](../../../../amples/snippets/xml/VS_Snippets_Misc/astoria northwind service/astoria.vsmdi NorthwindClient#ExplicitQuerySkipTakeMethodSpecific)]  
  
 前面的两个示例都将转换为查询 URI：`http://localhost:12345/northwind.svc/Orders()?$orderby=OrderDate desc&$skip=50&$top=25`。  
  
<a name="expand"></a>   
### <a name="expand"></a>展开  
 查询 [!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)] 数据服务时，可以请求在返回的源中包含与查询的目标实体相关的实体。 <xref:System.Data.Services.Client.DataServiceQuery%601.Expand%2A>上调用方法<xref:System.Data.Services.Client.DataServiceQuery%601> LINQ 查询的目标的实体集，相关实体集名称作为提供`path`参数。 有关详细信息，请参阅[加载延迟的内容](../../../../docs/framework/data/wcf/loading-deferred-content-wcf-data-services.md)。  
  
 下面的示例演示使用的等效方法<xref:System.Data.Services.Client.DataServiceQuery%601.Expand%2A>在查询中的方法︰  
  
-   在 LINQ 查询语法中：  
  
      [Astoria NorthwindClient #LinqQueryExpandSpecific](../../../../amples/snippets/xml/VS_Snippets_Misc/astoria northwind service/astoria.vsmdi NorthwindClient#LinqQueryExpandSpecific)]  
  
-   使用 LINQ 查询方法：  
  
      [Astoria NorthwindClient #LinqQueryExpandMethodSpecific](../../../../amples/snippets/xml/VS_Snippets_Misc/astoria northwind service/astoria.vsmdi NorthwindClient#LinqQueryExpandMethodSpecific)]  
  
 前面的两个示例都将转换为查询 URI：`http://localhost:12345/northwind.svc/Orders()?$filter=CustomerID eq 'ALFKI'&$expand=Order_Details`。  
  
<a name="unsupportedMethods"></a>   
## <a name="unsupported-linq-methods"></a>不支持的 LINQ 方法  
 下表所列的 LINQ 方法的类不受支持，不能包含在针对 [!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)] 服务执行的查询中：  
  
|运算类型|不支持的方法|  
|--------------------|------------------------|  
|集合运算符|所有集合运算符都都不能用于<xref:System.Data.Services.Client.DataServiceQuery%601>，其中包括︰<br /><br /> -   <xref:System.Linq.Enumerable.All%2A><br />-   <xref:System.Linq.Enumerable.Any%2A><br />-   <xref:System.Linq.Enumerable.Concat%2A><br />-   <xref:System.Linq.Enumerable.DefaultIfEmpty%2A><br />-   <xref:System.Linq.Enumerable.Distinct%2A><br />-   <xref:System.Linq.Enumerable.Except%2A><br />-   <xref:System.Linq.Enumerable.Intersect%2A><br />-   <xref:System.Linq.Enumerable.Union%2A><br />-   <xref:System.Linq.Enumerable.Zip%2A>\</TFirst, TSecond, TResult>|  
|排序运算符|需要的以下排序运算符<xref:System.Collections.Generic.IComparer%601>都不能用于<xref:System.Data.Services.Client.DataServiceQuery%601>:<br /><br /> -   <xref:System.Linq.Enumerable.OrderBy%60%602%28System.Collections.Generic.IEnumerable%7B%60%600%7D%2CSystem.Func%7B%60%600%2C%60%601%7D%2CSystem.Collections.Generic.IComparer%7B%60%601%7D%29> </TSource, TKey> </TSource, TKey><br />-   <xref:System.Linq.Enumerable.OrderByDescending%60%602%28System.Collections.Generic.IEnumerable%7B%60%600%7D%2CSystem.Func%7B%60%600%2C%60%601%7D%2CSystem.Collections.Generic.IComparer%7B%60%601%7D%29> \</TSource, TKey> \</TSource, TKey><br />-   <xref:System.Linq.Enumerable.ThenBy%60%602%28System.Linq.IOrderedEnumerable%7B%60%600%7D%2CSystem.Func%7B%60%600%2C%60%601%7D%2CSystem.Collections.Generic.IComparer%7B%60%601%7D%29> </TSource, TKey> </TSource, TKey><br />-   <xref:System.Linq.Enumerable.ThenByDescending%60%602%28System.Linq.IOrderedEnumerable%7B%60%600%7D%2CSystem.Func%7B%60%600%2C%60%601%7D%2CSystem.Collections.Generic.IComparer%7B%60%601%7D%29> \</TSource, TKey> \</TSource, TKey>|  
|投影和筛选运算符|下面的投影和接受位置参数的筛选运算符不能用于<xref:System.Data.Services.Client.DataServiceQuery%601>:<br /><br /> -   <xref:System.Linq.Enumerable.Join%60%604%28System.Collections.Generic.IEnumerable%7B%60%600%7D%2CSystem.Collections.Generic.IEnumerable%7B%60%601%7D%2CSystem.Func%7B%60%600%2C%60%602%7D%2CSystem.Func%7B%60%601%2C%60%602%7D%2CSystem.Func%7B%60%600%2C%60%601%2C%60%603%7D%2CSystem.Collections.Generic.IEqualityComparer%7B%60%602%7D%29> </TOuter, TInner, TResult> </TInner, TKey> </TOuter, TKey> </TOuter, TInner, TKey, TResult><br />-   <xref:System.Linq.Enumerable.Select%60%602%28System.Collections.Generic.IEnumerable%7B%60%600%7D%2CSystem.Func%7B%60%600%2CSystem.Int32%2C%60%601%7D%29> </TSource, Int32, TResult> </TSource, TResult><br />-   <xref:System.Linq.Enumerable.SelectMany%60%602%28System.Collections.Generic.IEnumerable%7B%60%600%7D%2CSystem.Func%7B%60%600%2CSystem.Collections.Generic.IEnumerable%7B%60%601%7D%7D%29> </TSource, TResult><br />-   <xref:System.Linq.Enumerable.SelectMany%60%602%28System.Collections.Generic.IEnumerable%7B%60%600%7D%2CSystem.Func%7B%60%600%2CSystem.Int32%2CSystem.Collections.Generic.IEnumerable%7B%60%601%7D%7D%29> </TSource, TResult><br />-   <xref:System.Linq.Enumerable.SelectMany%60%603%28System.Collections.Generic.IEnumerable%7B%60%600%7D%2CSystem.Func%7B%60%600%2CSystem.Collections.Generic.IEnumerable%7B%60%601%7D%7D%2CSystem.Func%7B%60%600%2C%60%601%2C%60%602%7D%29> \</TSource, TCollection, TResult> \</TSource, TCollection, TResult><br />-   <xref:System.Linq.Enumerable.SelectMany%60%603%28System.Collections.Generic.IEnumerable%7B%60%600%7D%2CSystem.Func%7B%60%600%2CSystem.Int32%2CSystem.Collections.Generic.IEnumerable%7B%60%601%7D%7D%2CSystem.Func%7B%60%600%2C%60%601%2C%60%602%7D%29> </TSource, TCollection, TResult> </TSource, TCollection, TResult><br />-   <xref:System.Linq.Enumerable.Where%60%601%28System.Collections.Generic.IEnumerable%7B%60%600%7D%2CSystem.Func%7B%60%600%2CSystem.Int32%2CSystem.Boolean%7D%29> \</TSource, Int32, Boolean>|  
|分组运算符|所有分组运算符都不能用于<xref:System.Data.Services.Client.DataServiceQuery%601>，其中包括︰<br /><br /> -   <xref:System.Linq.Enumerable.GroupBy%2A>\</TSource, TKey><br />-   <xref:System.Linq.Enumerable.GroupJoin%2A>\</TOuter, TInner, TKey, TResult><br /><br /> 分组运算符必须在客户端上执行。|  
|聚合运算符|所有聚合运算符都不能用于<xref:System.Data.Services.Client.DataServiceQuery%601>，其中包括︰<br /><br /> -   <xref:System.Linq.Enumerable.Aggregate%2A><br />-   <xref:System.Linq.Enumerable.Average%2A><br />-   <xref:System.Linq.Enumerable.Count%2A><br />-   <xref:System.Linq.Enumerable.LongCount%2A><br />-   <xref:System.Linq.Enumerable.Max%2A><br />-   <xref:System.Linq.Enumerable.Min%2A><br />-   <xref:System.Linq.Enumerable.Sum%2A><br /><br /> 聚合运算符必须在客户端上执行或由服务操作封装。|  
|分页运算符|以下分页运算符不能用于<xref:System.Data.Services.Client.DataServiceQuery%601>:<br /><br /> -   <xref:System.Linq.Enumerable.ElementAt%2A><br />-   <xref:System.Linq.Enumerable.Last%2A><br />-   <xref:System.Linq.Enumerable.LastOrDefault%2A><br />-   <xref:System.Linq.Enumerable.SkipWhile%2A><br />-   <xref:System.Linq.Enumerable.TakeWhile%2A> **注意︰**对空序列执行的分页运算符将返回 null。|  
|其他运算符|以下其他运算符不能用于<xref:System.Data.Services.Client.DataServiceQuery%601>:<br /><br /> 1.<xref:System.Linq.Enumerable.Empty%2A><br />2.<xref:System.Linq.Enumerable.Range%2A><br />3.<xref:System.Linq.Enumerable.Repeat%2A><br />4.<xref:System.Linq.Enumerable.ToDictionary%2A></TSource, TKey><br />5.<xref:System.Linq.Enumerable.ToLookup%2A>\</TSource, TKey>|  
  
<a name="supportedExpressions"></a>   
## <a name="supported-expression-functions"></a>支持的表达式函数  
 支持以下公共语言运行时 (CLR) 方法和属性，因为它们可以在查询表达式中进行转换以包含在 [!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)] 服务的请求 URI 中：  
  
|<xref:System.String>成员|支持的 [!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)] 函数|  
|-----------------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------|  
|<xref:System.String.Concat%28System.String%2CSystem.String%29>|`string concat(string p0, string p1)`|  
|<xref:System.String.Contains%28System.String%29>|`bool substringof(string p0, string p1)`|  
|<xref:System.String.EndsWith%28System.String%29>|`bool endswith(string p0, string p1)`|  
|<xref:System.String.IndexOf%28System.String%2CSystem.Int32%29>|`int indexof(string p0, string p1)`|  
|<xref:System.String.Length>|`int length(string p0)`|  
|<xref:System.String.Replace%28System.String%2CSystem.String%29>|`string replace(string p0, string find, string replace)`|  
|<xref:System.String.Substring%28System.Int32%29>|`string substring(string p0, int pos)`|  
|<xref:System.String.Substring%28System.Int32%2CSystem.Int32%29>|`string substring(string p0, int pos, int length)`|  
|<xref:System.String.ToLower>|`string tolower(string p0)`|  
|<xref:System.String.ToUpper>|`string toupper(string p0)`|  
|<xref:System.String.Trim>|`string trim(string p0)`|  
  
|<xref:System.DateTime>成员<sup>1</sup>|支持的 [!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)] 函数|  
|-------------------------------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------|  
|<xref:System.DateTime.Day>|`int day(DateTime p0)`|  
|<xref:System.DateTime.Hour>|`int hour(DateTime p0)`|  
|<xref:System.DateTime.Minute>|`int minute(DateTime p0)`|  
|<xref:System.DateTime.Month>|`int month(DateTime p0)`|  
|<xref:System.DateTime.Second>|`int second(DateTime p0)`|  
|<xref:System.DateTime.Year>|`int year(DateTime p0)`|  
  
 <sup>1</sup>等效的日期和时间属性<xref:Microsoft.VisualBasic.DateAndTime?displayProperty=fullName>，以及<xref:Microsoft.VisualBasic.DateAndTime.DatePart%2A>还支持在 Visual Basic 中的方法。  
  
|<xref:System.Math>成员|支持的 [!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)] 函数|  
|---------------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------|  
|<xref:System.Math.Ceiling%28System.Decimal%29>|`decimal ceiling(decimal p0)`|  
|<xref:System.Math.Ceiling%28System.Double%29>|`double ceiling(double p0)`|  
|<xref:System.Math.Floor%28System.Decimal%29>|`decimal floor(decimal p0)`|  
|<xref:System.Math.Floor%28System.Double%29>|`double floor(double p0)`|  
|<xref:System.Math.Round%28System.Decimal%29>|`decimal round(decimal p0)`|  
|<xref:System.Math.Round%28System.Double%29>|`double round(double p0)`|  
  
|<xref:> System.Linq.Expressions.Expression?qualifyHint=False&autoUpgrade=True成员|支持的 [!INCLUDE[ssODataShort](../../../../includes/ssodatashort-md.md)] 函数|  
|---------------------------------------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------|  
|<xref:System.Linq.Expressions.Expression.TypeIs%28System.Linq.Expressions.Expression%2CSystem.Type%29>|`bool isof(type p0)`|  
  
 客户端或许还可以在客户端上计算其他 CLR 函数。 一个<xref:System.NotSupportedException>引发的任何表达式不能在客户端上进行评估，不能转换为有效请求 URI 以便在服务器上的评估。  
  
## <a name="see-also"></a>另请参阅  
 [查询数据服务](../../../../docs/framework/data/wcf/querying-the-data-service-wcf-data-services.md)   
 [查询投影](../../../../docs/framework/data/wcf/query-projections-wcf-data-services.md)   
 [对象具体化](../../../../docs/framework/data/wcf/object-materialization-wcf-data-services.md)   
 [OData: URI 约定](http://go.microsoft.com/fwlink/?LinkID=185564)