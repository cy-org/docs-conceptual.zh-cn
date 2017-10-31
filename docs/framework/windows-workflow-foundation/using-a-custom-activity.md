---
title: "使用自定义活动 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 8f356419-681a-4175-ae93-878eee970249
caps.latest.revision: 2
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 2
---
# 使用自定义活动
派生自 <xref:System.Activities.Activity> 或其子类的活动可以组合到更大的工作流中，或以代码直接创建。此主题说明如何使用工作流中以代码或通过设计器创建的自定义活动。  
  
> [!NOTE]
>  自定义活动可在定义这些活动的同一项目中使用，只要自定义活动与使用它的活动经过编译即可（即：由正在实例化的、生成过程所生成的类型所加载）。如果引用活动动态加载（例如使用 ActivityXAMLServices），则被引用的程序集应放到其他项目中，否则设计器生成的 XAML 需要经过手动编辑才能实现这一功能。  
  
#### 将自定义活动用于工作流项目  
  
1.  添加从宿主项目指向包含自定义活动的活动库项目的引用。  
  
2.  生成解决方案。  
  
3.  如要在设计器中使用自定义活动，须先在工具箱中找到自定义活动，并将该活动拖放到设计器图面上。  
  
4.  如要在代码中使用自定义活动，须添加 Using 语句，使该语句引用自定义活动项目，并将该活动的一个新实例传递给 <xref:System.Activities.WorkflowInvoker.Invoke%2A>。