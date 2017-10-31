---
title: "Oracle BFILE | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 341bbf84-4734-4d44-8723-ccedee954e21
caps.latest.revision: 3
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 3
---
# Oracle BFILE
Oracle .NET Framework 数据提供程序包括 <xref:System.Data.OracleClient.OracleBFile> 类，该类用于使用 Oracle <xref:System.Data.OracleClient.OracleType> 数据类型。  
  
 Oracle **BFILE** 数据类型是一种 Oracle **LOB** 数据类型，包含对最大为 4 GB 的二进制数据的引用。  Oracle **BFILE** 不同于其他 Oracle **LOB** 数据类型，原因在于它的数据存储在操作系统（而不是服务器）上的物理文件中。  请注意，**BFILE** 数据类型提供的是对数据的只读访问权。  
  
 **BFILE** 数据类型还具有其他一些与 **LOB** 数据类型不同的特性，这些特性是：  
  
-   包含非结构化数据。  
  
-   支持服务器端分块。  
  
-   使用引用复制语义。  例如，如果对 **BFILE** 执行复制操作，将只复制 **BFILE** 定位符（引用相应文件）。  而不会复制文件中的数据。  
  
 **BFILE** 数据类型应该用于引用尺寸较大的 LOB，因此，要将该数据类型存储在数据库中非常不切实际。  使用 **BFILE** 数据类型与使用 **LOB** 数据类型相比，需要更多的客户端、服务器和通信系统开销。  如果您只需要获取少许数据，则访问 **BFILE** 更为有效。  如果需要获取整个对象，访问数据库驻留的 LOB 会更加有效。  
  
 每个非空 **OracleBFile** 对象都与两个定义基础物理文件位置的实体关联：  
  
1.  一个 Oracle DIRECTORY 对象，它是文件系统中一个目录的数据库别名，以及  
  
2.  基础物理文件的文件名，它位于与 DIRECTORY 对象关联的目录中。  
  
## 示例  
 下面的 C\# 示例说明了如何在 Oracle 表中创建 **BFILE**，然后使用 **OracleBFile** 对象形式对它进行检索。  该示例演示如何使用 <xref:System.Data.OracleClient.OracleDataReader> 对象以及 **OracleBFile** **Seek** 和 **Read** 方法。  注意，为了使用此示例，必须先在 Oracle 服务器上创建一个名为“c:\\\\bfiles”的目录以及一个名为“MyFile.jpg”的文件。  
  
```csharp  
using System;  
using System.IO;  
using System.Data;  
using System.Data.OracleClient;  
  
public class Sample  
{  
   public static void Main(string[] args)  
   {  
      OracleConnection connection = new OracleConnection(  
        "Data Source=Oracle8i;Integrated Security=yes");  
      connection.Open();  
  
      OracleCommand command = connection.CreateCommand();  
      command.CommandText =   
        "CREATE or REPLACE DIRECTORY MyDir as 'c:\\bfiles'";  
      command.ExecuteNonQuery();  
      command.CommandText =   
        "DROP TABLE MyBFileTable";  
      try {  
        command.ExecuteNonQuery();  
      }  
      catch {  
      }  
      command.CommandText =   
        "CREATE TABLE MyBFileTable(col1 number, col2 BFILE)";  
      command.ExecuteNonQuery();  
      command.CommandText =   
        "INSERT INTO MyBFileTable values ('2', BFILENAME('MyDir', " +  
        "'MyFile.jpg'))";  
      command.ExecuteNonQuery();  
      command.CommandText = "SELECT * FROM MyBFileTable";  
  
        byte[] buffer = new byte[100];  
  
      OracleDataReader reader = command.ExecuteReader();  
      using (reader) {  
          if (reader.Read()) {  
                OracleBFile bFile = reader.GetOracleBFile(1);  
                using (bFile) {  
                  bFile.Seek(0, SeekOrigin.Begin);  
                  bFile.Read(buffer, 0, 100);  
              }  
          }  
      }  
  
      connection.Close();  
   }  
  
}  
```  
  
## 请参阅  
 [Oracle 和 ADO.NET](../../../../docs/framework/data/adonet/oracle-and-adonet.md)   
 [ADO.NET 托管提供程序和数据集开发人员中心](http://go.microsoft.com/fwlink/?LinkId=217917)