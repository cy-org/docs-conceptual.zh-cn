---
title: "实体活动 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: c04f7413-7fb8-40c6-819e-dc92b145b62e
caps.latest.revision: 9
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 9
---
# 实体活动
此示例演示如何结合使用 ADO.NET 实体框架和 [!INCLUDE[wf2](../../../../includes/wf2-md.md)] 来简化数据访问。  
  
 ADO.NET 实体框架使开发人员可以处理以下形式的数据：特定于域的对象、属性和关系（例如客户、订单、订单详细信息以及这些实体之间的关系）。ADO.NET Entity Framework 通过提供一个抽象级别以便能够针对一个概念应用程序模型编程（而不是针对一个关系存储架构直接编程）来做到这一点。[!INCLUDE[crabout](../../../../includes/crabout-md.md)] ADO.NET Entity Framework 的更多信息，请参见 [ADO.NET 实体框架](http://go.microsoft.com/fwlink/?LinkId=165549)（可能为英文网页）。  
  
## 示例详细信息  
 此示例使用 `Northwind` 数据库，并包含用于创建和移除 `Northwind` 数据库的脚本（Setup.cmd 和 Cleanup.cmd）。此示例中的项目包含一个基于 `Northwind` 数据库的实体数据模型。您可以通过打开包含在项目中的 `Northwind.edmx` 文件找到此模型。此模型用于定义可使用 ADO.NET 实体框架访问的对象的形状。  
  
 此示例中包括以下活动：  
  
-   `EntitySQLQuery`：`EntitySQLQuery` 活动允许您基于 Entity SQL 查询字符串从数据库中检索对象。Entity SQL 是一种与 SQL 相似的、独立于存储的语言，它允许您基于概念模型以及属于该模型或域的一部分的实体来指定查询。[!INCLUDE[crabout](../../../../includes/crabout-md.md)] Entity SQL 语言的更多信息，请参见 [Entity SQL 语言](http://go.microsoft.com/fwlink/?LinkId=165646)（可能为英文网页）。  
  
-   `EntityLinqQuery`：此活动允许您基于 LINQ 查询或谓词从数据库中检索对象。  
  
-   `EntityAdd`：`EntityAdd` 活动允许您在数据库中添加一个实体或一个实体集合。  
  
-   `EntityDelete`：`EntityDelete` 活动允许您从数据库中删除一个实体或一个实体集合。  
  
-   `ObjectContextScope`：前面提及的活动只能在一个包含 `ObjectContextScope` 活动实例中使用。`ObjectContextScope` 活动设置与数据库的连接。该活动要求一个连接字符串（既可以传入此字符串，也可以使用配置文件设置检索此字符串）。`ObjectContextScope` 活动可以简化对实体执行一组相关操作的任务。因为此范围维护一个活动连接, 所以它是一个非持久范围。此外，当 `ObjectContextScope` 活动退出时，对在该范围内使用实体活动检索到的对象所做的任何更改将会自动保存回数据库，而无需执行显式的或后续的操作来将对象保存到数据库。  
  
## 使用实体活动  
 以下代码段演示如何使用此实例中提供的实体活动。  
  
### EntitySql  
 以下代码段演示如何查询所有位于伦敦的客户并按名称排序，并演示如何循环访问客户列表。  
  
```  
Variable<IEnumerable<Customer>> londonCustomers = new Variable<IEnumerable<Customer>>();  
DelegateInArgument<Customer> iterationVariable = new DelegateInArgument<Customer>();  
  
// create and return the workflow  
return new ObjectContextScope  
{  
    ConnectionString = new InArgument<string>(connStr),  
    ContainerName = "NorthwindEntities",  
    Variables = { londonCustomers },  
    Body = new Sequence  
        {  
            Activities =   
                {               
                    new WriteLine { Text = "Executing query" },                            
                    // query for all customers that are in london   
                    new EntitySqlQuery<Customer>  
                    {  
                        EntitySql =  @"SELECT VALUE Customer   
                                        FROM NorthwindEntities.Customers AS Customer   
                                        WHERE Customer.City = 'London'   
                                        ORDER BY Customer.ContactName",  
                        Result = londonCustomers  
                    },  
  
                    // iterate through the list of customers and display them   
                    new ForEach<Customer>  
                    {                                      
                        Values = londonCustomers,  
                        Body = new ActivityAction<Customer>  
                        {  
                            Argument = iterationVariable,  
                            Handler = new WriteLine   
                            {   
                                  Text = new InArgument<String>(e =>    
                                              iterationVariable.Get(e).ContactName)   
                            }  
                        }  
                    }  
                }  
        }                 
};  
  
```  
  
### EntityLinqQuery  
 以下代码段演示如何查询所有位于伦敦的客户，并演示如何循环生成的访问客户列表。  
  
```  
Variable<IEnumerable<Customer>> londonCustomers = new Variable<IEnumerable<Customer>>() { Name = "LondonCustomers" };  
DelegateInArgument<Customer> iterationVariable = new DelegateInArgument<Customer>() { Name = "iterationVariable" };  
  
return new ObjectContextScope  
{  
    ConnectionString = new InArgument<string>(connStr),  
    ContainerName = "NorthwindEntities",  
    Variables = { londonCustomers },  
    Body = new Sequence  
    {  
        Activities =   
        {               
            // return all the customers that match with the provided Linq predicate  
            new EntityLinqQuery<Customer>  
            {   
                Predicate = new LambdaValue<Func<Customer, bool>>(  
                          ctx => new Func<Customer, bool>(c => c.City.Equals("London"))),                              
                Result = londonCustomers  
            },  
  
            // iterate through the list of customers and display in the console  
            new ForEach<Customer>  
            {                                      
                Values = londonCustomers,  
                Body = new ActivityAction<Customer>  
                {  
                    Argument = iterationVariable,  
                    Handler = new WriteLine   
                    {   
                        Text = new InArgument<String>(e =>   
                                      iterationVariable.Get(e).ContactName)   
                    }  
                }  
            }  
        }  
    }  
};  
  
```  
  
### EntityAdd  
 以下代码段演示如何将一个 OrderDetail 记录添加到一个现有的 Order 中。  
  
```  
Variable<IEnumerable<Order>> orders = new Variable<IEnumerable<Order>>();  
Variable<IEnumerable<OrderDetail>> orderDetails = new Variable<IEnumerable<OrderDetail>>();  
Variable<Order> order = new Variable<Order>();  
Variable<OrderDetail> orderDetail = new Variable<OrderDetail>();              
  
return new ObjectContextScope  
{  
    Variables = { order, orders, orderDetail, orderDetails },  
    ContainerName = "NorthwindEntities",  
    ConnectionString = new InArgument<string>(connStr),                  
    Body = new Sequence  
    {                      
        Activities =   
        {                            
           // get the order where we want to add the detail  
           new EntitySqlQuery<Order>  
           {  
               EntitySql =    
                    @"SELECT VALUE [Order]  
                      FROM NorthwindEntities.Orders as [Order]  
                      WHERE Order.OrderID == 10249",  
               Result = orders  
           },  
  
           // store the order in a variable  
           new Assign<Order>   
           {  
               To = new OutArgument<Order>(order),  
               Value = new InArgument<Order>(c => orders.Get(c).First<Order>())  
           },  
  
           // add the detail to the order  
           new EntityAdd<OrderDetail>  
           {  
               Entity = new InArgument<OrderDetail>(c =>   
                                         new OrderDetail {   
                                                  OrderID=10249, ProductID=11,   
                                                  Quantity=1, UnitPrice = 15,   
                                                  Discount = 0, Order = order.Get(c) })  
           }  
        }  
    }  
};  
  
```  
  
### EntityDelete  
 以下代码段演示如何在一个 Order 中删除一个现有的 OrderDetail 记录（如果它存在）。  
  
```  
Variable<IEnumerable<OrderDetail>> orderDetails = new Variable<IEnumerable<OrderDetail>>();              
  
return new ObjectContextScope  
{  
    Variables = { orderDetails },  
    ConnectionString = new InArgument<string>(connStr),  
    ContainerName = "NorthwindEntities",  
    Body = new Sequence  
    {  
        Activities =   
        {               
            // find the entitiy to be deleted (order detail for product 11 in order 10249)  
            new EntitySqlQuery<OrderDetail>  
            {  
                EntitySql = @"SELECT VALUE OrderDetail  
                                FROM NorthwindEntities.OrderDetails as OrderDetail  
                               WHERE OrderDetail.OrderID == 10249   
                                 AND OrderDetail.ProductID == 11",  
                Result = orderDetails  
            },  
  
            // if the order detail is found, delete it, otherwise, display a message  
            new If  
            {  
                Condition = new InArgument<bool>(c=>orderDetails.Get(c).Count() > 0),  
                Then = new Sequence  
                {   
                    Activities =   
                    {                                      
                        new EntityDelete<OrderDetail>  
                        {  
                            Entity = new InArgument<OrderDetail>(c =>   
                                              orderDetails.Get(c).First<OrderDetail>())  
                        },  
                    }  
                },                              
                Else = new WriteLine { Text = "Order Detail for Deleting not found" }                              
            }                                                  
        }  
    }  
};  
  
```  
  
## 使用此示例  
 运行此示例之前，必须在本地 SQL Server Express 实例中创建 `Northwind` 数据库。  
  
#### 设置 Northwind 数据库  
  
1.  打开命令提示。  
  
2.  在新的命令提示窗口中，定位到 EntityActivities\\CS 文件夹。  
  
3.  键入 `setup.cmd`，然后按 Enter。  
  
#### 运行示例  
  
1.  使用 [!INCLUDE[vs_current_long](../../../../includes/vs-current-long-md.md)] 打开 EntityActivities.sln 解决方案文件。  
  
2.  要生成解决方案，按 Ctrl\+Shift\+B。  
  
3.  若要运行解决方案，请按 Ctrl\+F5。  
  
 运行此示例之后，您可能需要移除 `Northwind` 数据库。  
  
#### 卸载 Northwind 数据库  
  
1.  打开命令提示。  
  
2.  在新的命令提示窗口中，定位到 EntityActivities\\CS 文件夹。  
  
3.  键入 `cleanup.cmd`，然后按 Enter。  
  
> [!IMPORTANT]
>  您的计算机上可能已安装这些示例。在继续操作之前，请先检查以下（默认）目录：  
>   
>  `<安装驱动器>:\WF_WCF_Samples`  
>   
>  如果此目录不存在，请访问[针对 .NET Framework 4 的 Windows Communication Foundation \(WCF\) 和 Windows Workflow Foundation \(WF\) 示例](http://go.microsoft.com/fwlink/?LinkId=150780)（可能为英文网页），下载所有 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] 和 [!INCLUDE[wf1](../../../../includes/wf1-md.md)] 示例。此示例位于以下目录：  
>   
>  `<安装驱动器>:\WF_WCF_Samples\WF\Scenario\ActivityLibrary\EntityActivities`  
  
## 请参阅