---
title: "查询支持 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 093c22f5-3294-4642-857a-5252233d6796
caps.latest.revision: 11
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 11
---
# 查询支持
SQL 工作流实例存储中记录了存储区中的一组已知属性。用户可以根据这些属性查询实例。下面的列表包含这些已知属性的一部分：  
  
-   **站点名称。**包含服务的网站的名称。  
  
-   **相对应用程序路径。**应用程序相对于网站的路径。  
  
-   **相对服务路径。**服务相对于应用程序的路径。  
  
-   **服务名称。**服务的名称。  
  
-   **服务命名空间。**服务使用的命名空间的名称。  
  
-   **当前计算机。**  
  
-   **上一计算机**。上次运行工作流服务实例的计算机。  
  
> [!NOTE]
>  对于使用工作流服务主机的自承载方案，仅填充最后四个属性。对于工作流应用程序方案，仅填充最后一个属性。  
  
 工作流运行时为前三个属性提供值。工作流服务主机为**挂起原因**属性提供值。SQL 工作流实例存储自身为**上次更新的计算机**属性提供值。  
  
 使用 SQL 工作流实例存储的功能还可以指定自定义属性，您可以在持久性数据库中存储这些属性的值并且在查询中使用这些属性。有关自定义促销的更多信息，请参见[存储扩展性](../../../docs/framework/windows-workflow-foundation//store-extensibility.md)。  
  
## 视图  
 实例存储区包含下列视图。有关更多详细信息，请参见[持久性数据库架构](../../../docs/framework/windows-workflow-foundation//persistence-database-schema.md)。  
  
### Instances 视图  
 Instances 视图包含下列字段：  
  
1.  **Id**  
  
2.  **PendingTimer**  
  
3.  **CreationTime**  
  
4.  **LastUpdatedTime**  
  
5.  **ServiceDeploymentId**  
  
6.  **SuspensionExceptionName**  
  
7.  **SuspensionReason**  
  
8.  **ActiveBookmarks**  
  
9. **CurrentMachine**  
  
10. **LastMachine**  
  
11. **ExecutionStatus**  
  
12. **IsInitialized**  
  
13. **IsSuspended**  
  
14. **IsCompleted**  
  
15. **EncodingOption**  
  
16. **ReadWritePrimitiveDataProperties**  
  
17. **WriteOnlyPrimitiveDataProperties**  
  
18. **ReadWriteComplexDataProperties**  
  
19. **WriteOnlyComplexDataProperties**  
  
### ServiceDeployments 视图  
 ServiceDeployments 视图包含下列字段：  
  
1.  **SiteName**  
  
2.  **RelativeServicePath**  
  
3.  **RelativeApplicationPath**  
  
4.  **ServiceName**  
  
5.  **ServiceNamespace**  
  
### InstancePromotedProperties 视图  
 InstancePromotedProperties 视图包含下列字段。有关促销属性的详细信息，请参见[存储扩展性](../../../docs/framework/windows-workflow-foundation//store-extensibility.md)。  
  
1.  **InstanceId**  
  
2.  **EncodingOption**  
  
3.  **PromotionName**  
  
4.  **Value\#**（从 **Value1** 到 **Value64** 的一系列字段）。