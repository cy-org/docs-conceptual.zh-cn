---
title: "检索二进制数据 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 56c5a9e3-31f1-482f-bce0-ff1c41a658d0
caps.latest.revision: 5
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 5
---
# 检索二进制数据
默认情况下，**DataReader** 在整个数据行可用时立即以行的形式加载传入数据。  但是，对于二进制大对象 \(BLOB\) 则需要进行不同的处理，因为它们可能包含数十亿字节的数据，而单个行中无法包含如此多的数据。  **Command.ExecuteReader** 方法具有一个重载，它将采用 <xref:System.Data.CommandBehavior> 参数来修改 **DataReader** 的默认行为。  您可以将 <xref:System.Data.CommandBehavior> 传递到 **ExecuteReader** 方法来修改 **DataReader** 的默认行为，使其按照顺序在接收到数据时立即将其加载，而不是加载数据行。  这是加载 BLOB 或其他大数据结构的理想方案。  请注意，该行为可能会因数据源的不同而不同。  例如，从 Microsoft Access 中返回 BLOB 会将整个 BLOB 加载到内存中，而不是按照顺序在接收到数据时立即将其加载。  
  
 在将 **DataReader** 设置为使用 **SequentialAccess** 时，务必要注意访问所返回字段的顺序。  **DataReader** 的默认行为是在整个行可用时立即加载该行，这样可以在读取下一行之前按任何顺序访问所返回的字段。  但是，当使用 **SequentialAccess** 时，必须按顺序访问由 **DataReader** 返回的字段。  例如，如果查询返回三个列，其中第三列是 BLOB，则必须在访问第三个字段中的 BLOB 数据之前返回第一个和第二个字段的值。  如果在访问第一个或第二个字段之前访问第三个字段，则第一个和第二个字段值将不再可用。  这是因为 **SequentialAccess** 已修改 **DataReader**，使其按顺序返回数据，当 **DataReader** 已经读取超过特定数据时，该数据将不可用。  
  
 在访问 BLOB 字段中的数据时，请使用 **DataReader** 的 **GetBytes** 或 **GetChars** 类型化访问器，它们将用数据来填充数组。  还可以对字符数据使用 **GetString**；但是  为了节省系统资源，您可能不希望将整个 BLOB 值加载到单个字符串变量中。  您可以指定要返回的特定数据缓冲区大小，以及从返回的数据中读取的第一个字节或字符的起始位置。  **GetBytes** 和 **GetChars** 将返回一个 `long` 值，它表示返回的字节或字符数。  如果将一个空数组传递给 **GetBytes** 或 **GetChars**，则返回的长值将是 BLOB 中字节或字符的总数。  您可以选择将数组中的某个索引指定为所读取数据的起始位置。  
  
## 示例  
 下面的示例从 Microsoft SQL Server 中的 **pubs** 示例数据库返回发行者 ID 和徽标。  发行者 ID \(`pub_id`\) 是字符字段，而徽标则是图像，属于 BLOB。  由于 **logo** 字段是位图，因此该示例使用 **GetBytes** 返回二进制数据。  请注意，由于必须按顺序访问字段，所以将在访问徽标之前访问当前数据行的发行者 ID。  
  
```vb  
' Assumes that connection is a valid SqlConnection object.  
Dim command As SqlCommand = New SqlCommand( _  
  "SELECT pub_id, logo FROM pub_info", connection)  
  
' Writes the BLOB to a file (*.bmp).  
Dim stream As FileStream                   
' Streams the binary data to the FileStream object.  
Dim writer As BinaryWriter                 
' The size of the BLOB buffer.  
Dim bufferSize As Integer = 100        
' The BLOB byte() buffer to be filled by GetBytes.  
Dim outByte(bufferSize - 1) As Byte    
' The bytes returned from GetBytes.  
Dim retval As Long                     
' The starting position in the BLOB output.  
Dim startIndex As Long = 0             
  
' The publisher id to use in the file name.  
Dim pubID As String = ""              
  
' Open the connection and read data into the DataReader.  
connection.Open()  
Dim reader As SqlDataReader = command.ExecuteReader(CommandBehavior.SequentialAccess)  
  
Do While reader.Read()  
  ' Get the publisher id, which must occur before getting the logo.  
  pubID = reader.GetString(0)  
  
  ' Create a file to hold the output.  
  stream = New FileStream( _  
    "logo" & pubID & ".bmp", FileMode.OpenOrCreate, FileAccess.Write)  
  writer = New BinaryWriter(stream)  
  
  ' Reset the starting byte for a new BLOB.  
  startIndex = 0  
  
  ' Read bytes into outByte() and retain the number of bytes returned.  
  retval = reader.GetBytes(1, startIndex, outByte, 0, bufferSize)  
  
  ' Continue while there are bytes beyond the size of the buffer.  
  Do While retval = bufferSize  
    writer.Write(outByte)  
    writer.Flush()  
  
    ' Reposition start index to end of the last buffer and fill buffer.  
    startIndex += bufferSize  
    retval = reader.GetBytes(1, startIndex, outByte, 0, bufferSize)  
  Loop  
  
  ' Write the remaining buffer.  
  writer.Write(outByte, 0 , retval - 1)  
  writer.Flush()  
  
  ' Close the output file.  
  writer.Close()  
  stream.Close()  
Loop  
  
' Close the reader and the connection.  
reader.Close()  
connection.Close()  
  
```  
  
```csharp  
// Assumes that connection is a valid SqlConnection object.  
SqlCommand command = new SqlCommand(  
  "SELECT pub_id, logo FROM pub_info", connection);  
  
// Writes the BLOB to a file (*.bmp).  
FileStream stream;                            
// Streams the BLOB to the FileStream object.  
BinaryWriter writer;                          
  
// Size of the BLOB buffer.  
int bufferSize = 100;                     
// The BLOB byte[] buffer to be filled by GetBytes.  
byte[] outByte = new byte[bufferSize];    
// The bytes returned from GetBytes.  
long retval;                              
// The starting position in the BLOB output.  
long startIndex = 0;                      
  
// The publisher id to use in the file name.  
string pubID = "";                       
  
// Open the connection and read data into the DataReader.  
connection.Open();  
SqlDataReader reader = command.ExecuteReader(CommandBehavior.SequentialAccess);  
  
while (reader.Read())  
{  
  // Get the publisher id, which must occur before getting the logo.  
  pubID = reader.GetString(0);    
  
  // Create a file to hold the output.  
  stream = new FileStream(  
    "logo" + pubID + ".bmp", FileMode.OpenOrCreate, FileAccess.Write);  
  writer = new BinaryWriter(stream);  
  
  // Reset the starting byte for the new BLOB.  
  startIndex = 0;  
  
  // Read bytes into outByte[] and retain the number of bytes returned.  
  retval = reader.GetBytes(1, startIndex, outByte, 0, bufferSize);  
  
  // Continue while there are bytes beyond the size of the buffer.  
  while (retval == bufferSize)  
  {  
    writer.Write(outByte);  
    writer.Flush();  
  
    // Reposition start index to end of last buffer and fill buffer.  
    startIndex += bufferSize;  
    retval = reader.GetBytes(1, startIndex, outByte, 0, bufferSize);  
  }  
  
  // Write the remaining buffer.  
  writer.Write(outByte, 0, (int)retval - 1);  
  writer.Flush();  
  
  // Close the output file.  
  writer.Close();  
  stream.Close();  
}  
  
// Close the reader and the connection.  
reader.Close();  
connection.Close();  
```  
  
## 请参阅  
 [Working with DataReaders](http://msdn.microsoft.com/zh-cn/126a966a-d08d-4d22-a19f-f432908b2b54)   
 [SQL Server 二进制和大值数据](../../../../docs/framework/data/adonet/sql/sql-server-binary-and-large-value-data.md)   
 [ADO.NET 托管提供程序和数据集开发人员中心](http://go.microsoft.com/fwlink/?LinkId=217917)