---
title: "WPF 安全策略 — 安全工程 | Microsoft Docs"
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
  - "关键代码管理"
  - "安全开发生命周期 (SDL), 关键代码管理"
  - "安全开发生命周期 (SDL), 安全分析"
  - "安全开发生命周期 (SDL), 源分析工具"
  - "安全开发生命周期 (SDL), 源编辑工具"
  - "安全开发生命周期 (SDL), 测试技术"
  - "安全开发生命周期 (SDL), 威胁建模"
  - "安全性, 测试技术"
  - "源分析工具"
  - "源编辑工具"
  - "测试, 安全性"
  - "威胁建模"
ms.assetid: 0fc04394-4e47-49ca-b0cf-8cd1161d95b9
caps.latest.revision: 11
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 9
---
# WPF 安全策略 — 安全工程
可信计算是 Microsoft 为确保生成安全代码而首创的一项技术。  可信计算技术的一个关键元素是 [!INCLUDE[TLA#tla_sdl](../../../includes/tlasharptla-sdl-md.md)]。  [!INCLUDE[TLA2#tla_sdl](../../../includes/tla2sharptla-sdl-md.md)] 是与标准工程过程一同用于简化提交安全代码的工程实践。  [!INCLUDE[TLA2#tla_sdl](../../../includes/tla2sharptla-sdl-md.md)] 包含十个阶段，将规范化、可度量性和附加结构的最佳实践结合在一起，包括：  
  
-   安全设计分析  
  
-   基于工具的质量检查  
  
-   渗透测试  
  
-   最终安全评审  
  
-   发布后产品安全管理  
  
## WPF 详细信息  
 [!INCLUDE[TLA2#tla_winclient](../../../includes/tla2sharptla-winclient-md.md)] 工程团队可以应用和扩展 [!INCLUDE[TLA2#tla_sdl](../../../includes/tla2sharptla-sdl-md.md)]，该产品组合包括以下主要方面：  
  
 [威胁建模](#thread_modeling)  
  
 [安全分析和编辑工具](#tools)  
  
 [测试技术](#techniques)  
  
 [关键代码管理](#critical_code)  
  
<a name="threat_modeling"></a>   
### 威胁建模  
 威胁建模是 [!INCLUDE[TLA2#tla_sdl](../../../includes/tla2sharptla-sdl-md.md)]的核心组件，用于分析系统，以确定潜在的安全漏洞。  一旦确定漏洞，威胁模型还可以确保采取适当的缓解措施。  
  
 我们以一个杂货店为例，说明威胁模型在高级别上所涉及的以下关键步骤：  
  
1.  **确定资产**。  杂货店的资产可能包括员工、保险箱、收银机和库存。  
  
2.  **枚举入口点**。  杂货店的入口点可能包括前门和后门、窗户、装货区和空调设备。  
  
3.  **使用入口点调查针对资产的攻击**。  可能进行的攻击包括通过*空调*入口点来对杂货店的*保险箱*资产进行攻击；有人可能会将空调设备拆掉，将保险箱通过空调处拉出杂货店。  
  
 威胁建模应用于整个 [!INCLUDE[TLA2#tla_winclient](../../../includes/tla2sharptla-winclient-md.md)]，包含以下各项：  
  
-   [!INCLUDE[TLA2#tla_xaml](../../../includes/tla2sharptla-xaml-md.md)] 分析器读取文件、将文本映射到相应的对象模型类并创建实际代码的方式。  
  
-   创建窗口句柄 \(hWnd\) 并通过其发送消息和呈现窗口内容的方式。  
  
-   数据绑定获取资源以及与系统交互的方式。  
  
 这些威胁模型对于在开发过程中确定安全设计需求以及缓解威胁非常重要。  
  
<a name="tools"></a>   
### 源分析和编辑工具  
 除 [!INCLUDE[TLA2#tla_sdl](../../../includes/tla2sharptla-sdl-md.md)] 的手动安全代码评审元素外，[!INCLUDE[TLA2#tla_winclient](../../../includes/tla2sharptla-winclient-md.md)] 团队使用多个工具进行源分析和关联编辑，目的是减少安全漏洞。  使用了多种源工具，包括以下各项：  
  
-   **FXCop**：查找托管代码中的常见安全问题，包括继承规则、代码访问安全的使用情况以及安全地与非托管代码交互操作的方式。  请参阅[FXCop](http://www.gotdotnet.com/team/fxcop/)。  
  
-   **Prefix\/Prefast**：查找非托管代码中的安全漏洞和常见安全问题，例如缓冲区溢出、格式字符串问题以及错误检查。  
  
-   **Banned API**：搜索源代码，以识别出众所周知的因意外使用而引发安全问题的函数，例如 `strcpy`。  一旦识别出这些函数，将用更安全的替代函数来取代它们。  
  
<a name="techniques"></a>   
### 测试技术  
 [!INCLUDE[TLA2#tla_winclient](../../../includes/tla2sharptla-winclient-md.md)] 使用多种安全测试技术，包括：  
  
-   **白盒测试**：测试人员查看源代码，然后生成利用测试  
  
-   **黑盒测试**：测试人员尝试通过检查 API 和功能来查找安全问题，然后尝试对产品进行攻击。  
  
-   **对来自其他产品的安全问题进行回归测试**：对来自相关产品的相关安全问题进行测试。  例如，对于 [!INCLUDE[TLA2#tla_ie](../../../includes/tla2sharptla-ie-md.md)]，已确定出大约六十个安全问题的相关变体，并已对它们在 [!INCLUDE[TLA2#tla_winclient](../../../includes/tla2sharptla-winclient-md.md)] 上的适用性进行了测试。  
  
-   **借助文件模糊化执行基于工具的渗透测试**：文件模糊化指利用文件读取器多种输入的输入范围。  在 [!INCLUDE[TLA2#tla_winclient](../../../includes/tla2sharptla-winclient-md.md)] 中的一个示例，使用此技术的一个示例就是检查图像解码代码的错误。  
  
<a name="critical_code"></a>   
### 关键代码管理  
 对于 [!INCLUDE[TLA#tla_xbap#plural](../../../includes/tlasharptla-xbapsharpplural-md.md)]，[!INCLUDE[TLA2#tla_winclient](../../../includes/tla2sharptla-winclient-md.md)] 通过使用 [!INCLUDE[TLA2#tla_winfx](../../../includes/tla2sharptla-winfx-md.md)] 对标记和跟踪可提升特权的安全关键代码的支持来生成安全沙盒（请参阅 [WPF 安全策略 — 平台安全性](../../../docs/framework/wpf/wpf-security-strategy-platform-security.md)中的**安全关键方法**）。  考虑到对安全关键代码有较高的安全质量要求，因此需要对此类代码进行其他级别的源管理控制和安全审核。  大约有 5% 到 10% 的 [!INCLUDE[TLA2#tla_winclient](../../../includes/tla2sharptla-winclient-md.md)] 由安全关键代码组成，这些代码由专门的审核团队进行审核。  通过跟踪安全关键代码和将每个关键实体（即，包含关键代码的方法）映射到其签署状态  来对源代码和签入过程进行管理。  签署状态包括一个或多个审阅者的姓名。  [!INCLUDE[TLA2#tla_winclient](../../../includes/tla2sharptla-winclient-md.md)] 的每个日常版本都将关键代码与前一版本中的该代码进行比较，以检查未经审批的更改。  如果工程师未经审核团队的批准而自行修改关键代码，则将识别并立即修复该代码。  通过这一过程，可以对 [!INCLUDE[TLA2#tla_winclient](../../../includes/tla2sharptla-winclient-md.md)] 沙盒代码应用级别特高的审核并加以维护。  
  
## 请参阅  
 [安全性](../../../docs/framework/wpf/security-wpf.md)   
 [WPF 部分信任安全](../../../docs/framework/wpf/wpf-partial-trust-security.md)   
 [WPF 安全策略 — 平台安全性](../../../docs/framework/wpf/wpf-security-strategy-platform-security.md)   
 [可信计算](http://www.microsoft.com/mscorp/twc/default.mspx)   
 [应用程序威胁建模](http://msdn.microsoft.com/security/securecode/threatmodeling/acetm/)   
 [安全指导原则：.NET Framework 2.0](http://msdn.microsoft.com/library/default.asp?url=/%20library/dnpag2/html/PAGGuidelines0003.asp)