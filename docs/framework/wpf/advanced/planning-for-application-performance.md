---
title: "规划应用程序性能 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-wpf"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "应用程序, 优化"
  - "WPF 应用程序, 优化"
ms.assetid: c91bd0c5-a193-46ff-9da1-eb7a3a76a3b3
caps.latest.revision: 6
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 6
---
# 规划应用程序性能
是否能够成功实现性能目标取决于您制定的性能策略的优劣。  规划是开发任何产品的第一个阶段。  本主题描述几个非常简单的规则，用于制定可实现绝佳性能的策略。  
  
## 从方案的角度考虑  
 方案可帮助您将重点放在应用程序的关键组件上。  方案通常派生自您的客户和竞争产品。  不断研究客户，并确定客户真正关注您的产品和竞争对手产品的哪些方面。  客户的反馈可帮助您确定应用程序的主要方案。  例如，如果您设计的组件将在启动时使用，则该组件很有可能将只在应用程序启动时调用一次。  启动时间将成为关键方案。  关键方案的其他示例可以是动画序列所需的帧速率或者应用程序所允许的最大工作集。  
  
## 制定目标  
 目标可帮助您确定应用程序的执行速度是慢还是快。  您应当为每个方案制定目标。  所有的性能目标都应当基于客户的预期来制定。  在应用程序开发周期的早期制定性能目标可能会有些困难，因为早期仍存在许多未解决的问题。  但是，最好制定初始目标并在以后进行修订，而不要根本就没有目标。  
  
## 了解平台  
 在应用程序开发过程中，总是按照度量、调查、简化\/更正这一周期来操作。  从开发周期的开始到结束，您需要在稳定而可靠的环境中度量应用程序的性能。  您应当避免由外部因素造成的变化。  例如，在测试性能时，应当禁用防病毒或任何自动更新功能（如 SMS），以防它们影响性能测试结果。  在对应用程序的性能进行度量之后，需要确定哪些更改将使性能获得最大的改进。  在对应用程序进行修改之后，请再次启动该周期。  
  
## 将性能调整设置为迭代过程  
 您应当知道将要使用的每个功能的相对成本。  例如，从计算资源的角度看，在 [!INCLUDE[TLA#tla_avalonwinfx](../../../../includes/tlasharptla-avalonwinfx-md.md)]中使用反射通常对性能的要求很高，因此您需要慎用反射。  这并不意味着避免使用反射，而只是表示您应当注意平衡应用程序的性能要求与所用功能的性能需求。  
  
## 以图形丰富性为目标生成内容  
 如需创建面向 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 应用程序性能的可伸缩方法，关键方法之一是以图形丰富性为目标生成内容。  总是首先使用对性能要求最低的资源来实现方案目标。  在实现这些目标之后，使用对性能要求较高的功能来生成包含大量图形的内容，同时始终牢记方案目标。  请记住，[!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 是一个非常丰富的平台，它提供了非常丰富的图形功能。  随意使用对性能要求很高的功能可能会对应用程序的整体性能产生负面影响。  
  
 [!INCLUDE[TLA2#tla_winclient](../../../../includes/tla2sharptla-winclient-md.md)] 控件在本质上具有可扩展性，它允许在不修改其控件行为的情况下对其外观进行广泛的自定义。  通过利用样式、数据模板和控件模板，可以根据您的性能要求来创建并逐步改造可自定义的[!INCLUDE[TLA#tla_ui](../../../../includes/tlasharptla-ui-md.md)]。  
  
## 请参阅  
 [优化 WPF 应用程序性能](../../../../docs/framework/wpf/advanced/optimizing-wpf-application-performance.md)   
 [利用硬件](../../../../docs/framework/wpf/advanced/optimizing-performance-taking-advantage-of-hardware.md)   
 [布局和设计](../../../../docs/framework/wpf/advanced/optimizing-performance-layout-and-design.md)   
 [二维图形和图像处理](../../../../docs/framework/wpf/advanced/optimizing-performance-2d-graphics-and-imaging.md)   
 [对象行为](../../../../docs/framework/wpf/advanced/optimizing-performance-object-behavior.md)   
 [应用程序资源](../../../../docs/framework/wpf/advanced/optimizing-performance-application-resources.md)   
 [Text](../../../../docs/framework/wpf/advanced/optimizing-performance-text.md)   
 [数据绑定](../../../../docs/framework/wpf/advanced/optimizing-performance-data-binding.md)   
 [其他性能建议](../../../../docs/framework/wpf/advanced/optimizing-performance-other-recommendations.md)