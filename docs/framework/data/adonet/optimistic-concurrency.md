---
title: "开放式并发 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: e380edac-da67-4276-80a5-b64decae4947
caps.latest.revision: 6
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 6
---
# 开放式并发
在多用户环境中，有两种用于更新数据库中数据的模型：开放式并发和保守式并发。  设计 <xref:System.Data.DataSet> 对象的目的是为了促进将开放式并发用于长时间运行的活动，例如对数据进行远程处理以及与数据进行交互时。  
  
 保守式并发涉及到锁定数据源中的行，以防止其他用户因修改数据而影响当前用户。  在保守式模型中，当用户执行会应用锁的操作时，其他用户将无法执行可能与锁发生冲突的操作，直到锁所有者释放锁为止。  此模型主要用于以下环境：对数据存在激烈争用，使得用锁保护数据的成本少于在发生并发冲突时回滚事务的成本。  
  
 因此，在保守式并发模型中，更新行的用户将会建立锁。  在该用户完成更新并释放锁之前，其他任何用户都无法更改锁定行。  因此，如果锁定时间将会比较短（例如在以编程方式处理记录时），最好实现保守式并发。  如果用户与数据进行交互，会使记录锁定相对长的时间，保守式并发并不是可伸缩的选项。  
  
> [!NOTE]
>  如果您需要在同一个操作中更新多个行，则创建事务要比使用保守式锁定更具伸缩性。  
  
 对比之下，使用开放式并发的用户在读取行时不会锁定该行。  当用户要更新某行时，应用程序必须确定自读取该行以来，其他用户是否更改了该行。  开放式并发通常用于对数据争用较少的环境。  由于不需要锁定任何记录，开放式并发将会提高性能，因为锁定记录需要更多的服务器资源。  另外，为了维护记录锁，需要与数据库服务器保持持久连接。  由于在开放式并发模型中并不会这样，所以与服务器的连接可以在较少的时间内为更多的客户端提供服务。  
  
 在开放式并发模型中，如果当某用户接收到来自数据库的值后，另一用户在该用户试图修改该值之前即将其修改，则认为发生了冲突。  首先通过以下示例说明服务器如何解决并发冲突。  
  
 以下各表是根据一个开放式并发示例生成的。  
  
 下午 1:00，用户 1 从具有以下值的数据库中读取一行：  
  
 **CustID     LastName     FirstName**  
  
 101          Smith             Bob  
  
|列名称|原始值|当前值|数据库中的值|  
|---------|---------|---------|------------|  
|CustID|101|101|101|  
|LastName|Smith|Smith|Smith|  
|FirstName|Bob|Bob|Bob|  
  
 下午 1:01，用户 2 读取同一行。  
  
 下午 1:03，用户 2 将 **FirstName** 从“Bob”更改为“Robert”并更新数据库。  
  
|列名称|原始值|当前值|数据库中的值|  
|---------|---------|---------|------------|  
|CustID|101|101|101|  
|LastName|Smith|Smith|Smith|  
|FirstName|Bob|Robert|Bob|  
  
 由于更新时数据库中的值匹配用户 2 具有的原始值，因此更新成功。  
  
 下午 1:05，用户 1 将“Bob”的名更改为“James”并试图更新该行。  
  
|列名称|原始值|当前值|数据库中的值|  
|---------|---------|---------|------------|  
|CustID|101|101|101|  
|LastName|Smith|Smith|Smith|  
|FirstName|Bob|James|Robert|  
  
 此时，由于数据库中的值（“Robert”）不再匹配 User1 所预期的原始值（“Bob”），因此 User1 遇到开放式并发冲突。  并发冲突仅向您表明更新失败。  现在，需要决定是用用户 1 提供的更改来重写用户 2 提供的更改还是取消用户 1 的更改。  
  
## 测试是否存在开放式并发冲突  
 测试是否存在开放式并发冲突的方法有若干种。  其中一种涉及到在表中包含时间戳列。  数据库通常会提供时间戳功能，该功能可用于标识上次更新记录的日期和时间。  当使用这种方法时，将在表定义中包含时间戳列。  每当更新记录时，时间戳都将得到更新，以反映当前的日期和时间。  在测试是否存在开放式并发冲突时，对表内容的任何查询都会返回时间戳列。  当试图执行更新时，数据库中的时间戳值将与所修改行中包含的原始时间戳值进行比较。  如果两者匹配，则会执行更新，并用当前时间更新时间戳列以反映更新。  如果两者不匹配，则发生了开放式并发冲突。  
  
 测试是否存在开放式并发冲突的另一种方法是验证某行中的所有原始列值是否仍匹配数据库中的相应值。  例如，考虑以下查询：  
  
```  
SELECT Col1, Col2, Col3 FROM Table1  
```  
  
 若要在更新 **Table1** 中的某行时测试是否存在开放式并发冲突，请发出以下 UPDATE 语句：  
  
```  
UPDATE Table1 Set Col1 = @NewCol1Value,  
              Set Col2 = @NewCol2Value,  
              Set Col3 = @NewCol3Value  
WHERE Col1 = @OldCol1Value AND  
      Col2 = @OldCol2Value AND  
      Col3 = @OldCol3Value  
```  
  
 只要原始值匹配数据库中的值，就会执行更新。  如果已修改某个值，由于 WHERE 子句找不到匹配项，更新将不会修改该行。  
  
 请注意，建议始终在查询中返回唯一的主键值。  否则，以上 UPDATE 语句会更新多个行，这可能会有悖于您的意图。  
  
 如果数据源中的列允许空值，则可能需要扩展 WHERE 子句，以查找本地表和数据源中的匹配空引用。  例如，以下 UPDATE 语句验证本地行中的空引用是否仍匹配数据源中的空引用，或者本地行中的值是否匹配数据源中的值。  
  
```  
UPDATE Table1 Set Col1 = @NewVal1  
  WHERE (@OldVal1 IS NULL AND Col1 IS NULL) OR Col1 = @OldVal1  
```  
  
 当使用开放式并发模型时，也可以选择应用限制较少的条件。  例如，如果只在 WHERE 子句中使用主键列，那么无论自上次查询以来是否已更新其他列，数据都将被重写。  也可以只将 WHERE 子句应用于特定列，除非自上次查询特定字段以来已将其更新，否则数据也会被重写。  
  
### DataAdapter.RowUpdated 事件  
 <xref:System.Data.Common.DataAdapter> 对象的 **RowUpdated** 事件可以与上述方法一起用来向应用程序提供有关开放式并发冲突的通知。  在每次尝试从 **DataSet** 更新 **Modified** 行之后，将发生 **RowUpdated**。  它使您能够添加特殊的处理代码，包括在发生异常时进行处理，添加自定义错误信息，添加重试逻辑等。  <xref:System.Data.Common.RowUpdatedEventArgs> 对象为表中已修改的行返回 **RecordsAffected** 属性，其中包含特定更新命令所影响的行数。  通过设置更新命令来测试是否存在开放式并发，当开放式并发冲突已发生时，因为没有更新任何记录，所以 **RecordsAffected** 属性最终将返回值 0。  如果是这种情况，则将引发异常。  **RowUpdated** 事件使您能够通过设置合适的 **RowUpdatedEventArgs.Status** 值（例如 **UpdateStatus.SkipCurrentRow**）来处理这种情况并避免异常。  有关 **RowUpdated** 事件的更多信息，请参见[处理 DataAdapter 事件](../../../../docs/framework/data/adonet/handling-dataadapter-events.md)。  
  
 或者，可以在调用 **Update** 之前将 **DataAdapter.ContinueUpdateOnError** 设置为 **true**，并在完成 **Update** 后响应存储在特定行的 **RowError** 属性中的错误信息。  有关详细信息，请参阅[行错误信息](../../../../docs/framework/data/adonet/dataset-datatable-dataview/row-error-information.md)。  
  
## 开放式并发示例  
 下面是一个简单的示例，通过设置 **DataAdapter** 的 **UpdateCommand** 来测试是否存在开放式并发，然后使用 **RowUpdated** 事件来测试是否存在开放式并发冲突。  当遇到开放式并发冲突时，应用程序将设置发出更新命令的目标行的 **RowError**，以反映开放式并发冲突。  
  
 请注意，传递给 UPDATE 命令的 WHERE 子句的参数值映射到其相应列的 **Original** 值。  
  
```vb  
' Assumes connection is a valid SqlConnection.  
Dim adapter As SqlDataAdapter = New SqlDataAdapter( _  
  "SELECT CustomerID, CompanyName FROM Customers ORDER BY CustomerID", _  
  connection)  
  
' The Update command checks for optimistic concurrency violations  
' in the WHERE clause.  
adapter.UpdateCommand = New SqlCommand("UPDATE Customers " &  
  "(CustomerID, CompanyName) VALUES(@CustomerID, @CompanyName) " & _  
  "WHERE CustomerID = @oldCustomerID AND CompanyName = " &  
  "@oldCompanyName", connection)  
adapter.UpdateCommand.Parameters.Add( _  
  "@CustomerID", SqlDbType.NChar, 5, "CustomerID")  
adapter.UpdateCommand.Parameters.Add( _  
  "@CompanyName", SqlDbType.NVarChar, 30, "CompanyName")  
  
' Pass the original values to the WHERE clause parameters.  
Dim parameter As SqlParameter = dataSet.UpdateCommand.Parameters.Add( _  
  "@oldCustomerID", SqlDbType.NChar, 5, "CustomerID")  
parameter.SourceVersion = DataRowVersion.Original  
parameter = adapter.UpdateCommand.Parameters.Add( _  
  "@oldCompanyName", SqlDbType.NVarChar, 30, "CompanyName")  
parameter.SourceVersion = DataRowVersion.Original  
  
' Add the RowUpdated event handler.  
AddHandler adapter.RowUpdated, New SqlRowUpdatedEventHandler( _  
  AddressOf OnRowUpdated)  
  
Dim dataSet As DataSet = New DataSet()  
adapter.Fill(dataSet, "Customers")  
  
' Modify the DataSet contents.  
adapter.Update(dataSet, "Customers")  
  
Dim dataRow As DataRow  
  
For Each dataRow In dataSet.Tables("Customers").Rows  
    If dataRow.HasErrors Then   
       Console.WriteLine(dataRow (0) & vbCrLf & dataRow.RowError)  
    End If  
Next  
  
Private Shared Sub OnRowUpdated( _  
  sender As object, args As SqlRowUpdatedEventArgs)  
   If args.RecordsAffected = 0  
      args.Row.RowError = "Optimistic Concurrency Violation!"  
      args.Status = UpdateStatus.SkipCurrentRow  
   End If  
End Sub  
```  
  
```csharp  
// Assumes connection is a valid SqlConnection.  
SqlDataAdapter adapter = new SqlDataAdapter(  
  "SELECT CustomerID, CompanyName FROM Customers ORDER BY CustomerID",  
  connection);  
  
// The Update command checks for optimistic concurrency violations  
// in the WHERE clause.  
adapter.UpdateCommand = new SqlCommand("UPDATE Customers Set CustomerID = @CustomerID, CompanyName = @CompanyName " +  
   "WHERE CustomerID = @oldCustomerID AND CompanyName = @oldCompanyName, connection);  
adapter.UpdateCommand.Parameters.Add(  
  "@CustomerID", SqlDbType.NChar, 5, "CustomerID");  
adapter.UpdateCommand.Parameters.Add(  
  "@CompanyName", SqlDbType.NVarChar, 30, "CompanyName");  
  
// Pass the original values to the WHERE clause parameters.  
SqlParameter parameter = adapter.UpdateCommand.Parameters.Add(  
  "@oldCustomerID", SqlDbType.NChar, 5, "CustomerID");  
parameter.SourceVersion = DataRowVersion.Original;  
parameter = adapter.UpdateCommand.Parameters.Add(  
  "@oldCompanyName", SqlDbType.NVarChar, 30, "CompanyName");  
parameter.SourceVersion = DataRowVersion.Original;  
  
// Add the RowUpdated event handler.  
adapter.RowUpdated += new SqlRowUpdatedEventHandler(OnRowUpdated);  
  
DataSet dataSet = new DataSet();  
adapter.Fill(dataSet, "Customers");  
  
// Modify the DataSet contents.  
  
adapter.Update(dataSet, "Customers");  
  
foreach (DataRow dataRow in dataSet.Tables["Customers"].Rows)  
{  
    if (dataRow.HasErrors)  
       Console.WriteLine(dataRow [0] + "\n" + dataRow.RowError);  
}  
  
protected static void OnRowUpdated(object sender, SqlRowUpdatedEventArgs args)  
{  
  if (args.RecordsAffected == 0)   
  {  
    args.Row.RowError = "Optimistic Concurrency Violation Encountered";  
    args.Status = UpdateStatus.SkipCurrentRow;  
  }  
}  
```  
  
## 请参阅  
 [在 ADO.NET 中检索和修改数据](../../../../docs/framework/data/adonet/retrieving-and-modifying-data.md)   
 [使用 DataAdapter 更新数据源](../../../../docs/framework/data/adonet/updating-data-sources-with-dataadapters.md)   
 [行错误信息](../../../../docs/framework/data/adonet/dataset-datatable-dataview/row-error-information.md)   
 [事务和并发](../../../../docs/framework/data/adonet/transactions-and-concurrency.md)   
 [ADO.NET 托管提供程序和数据集开发人员中心](http://go.microsoft.com/fwlink/?LinkId=217917)