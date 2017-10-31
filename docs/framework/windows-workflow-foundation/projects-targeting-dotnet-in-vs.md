---
title: "在 Visual Studio 2010 中编写面向 .NET Framework 3.0 和 3.5 的项目 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 81858ab7-763c-4eac-83fe-d7205e5c4c98
caps.latest.revision: 7
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 7
---
# 在 Visual Studio 2010 中编写面向 .NET Framework 3.0 和 3.5 的项目
可使用 [!INCLUDE[vs2010](../../../includes/vs2010-md.md)] 创建面向 [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] 版本 3.0 或 3.5 的项目。本主题介绍如何执行此操作。  
  
> [!NOTE]
>  在添加活动时，请确保设置所需版本的 [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)]。在添加活动后更改工作流的目标版本将导致工作流验证失败。  
  
> [!WARNING]
>  在 [!INCLUDE[vs2010](../../../includes/vs2010-md.md)] 中打开具有 .Net Framework 3.5 活动的现有工作流将导致 `this.SetValue()` 出错。若要打开用早期版本的 .Net Framework 创建的项目，请先在设计器中打开一个空白工作流并添加一个 .Net Framework 3.5 活动。  
  
## 使用 Visual Studio 2010 创建 .NET Framework 3.0 或 3.5 项目  
  
1.  打开 [!INCLUDE[vs2010](../../../includes/vs2010-md.md)]。  
  
2.  依次选择**“文件”**、**“新建”**和**“项目”**。  
  
3.  在对话框顶部的下拉列表中，选择所需版本的 [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)]。  
  
## 升级 .NET Framework 的目标版本  
  
1.  在“解决方案资源管理器”中右击该项目并选择**“属性”**。  
  
2.  在**“目标 Framework”**下拉列表中，选择所需的版本。