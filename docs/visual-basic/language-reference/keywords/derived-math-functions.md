---
title: "派生的数学函数 (Visual Basic) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "角度"
  - "反余割函数"
  - "反余弦函数"
  - "反余切函数"
  - "反正割函数"
  - "反正弦函数"
  - "算术运算, 导出数学函数"
  - "余割函数"
  - "余切函数"
  - "度"
  - "导出数学函数"
  - "函数 [Visual Basic], 导出数学函数"
  - "双曲函数"
  - "反函数"
  - "对数"
  - "数学函数, 派生"
  - "正割函数"
  - "三角函数"
ms.assetid: 63e449d8-9444-44fb-8db1-6d9cf346e2aa
caps.latest.revision: 11
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 11
---
# 派生的数学函数 (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/includes/vs2017banner.md)]

下表显示了非内部数学函数，这些函数可由 <xref:System.Math?displayProperty=fullName> 对象的内部数学函数导出。  通过向文件或项目添加 `Imports System.Math`，可以访问内部数学函数。  
  
|功能|导出的等效公式|  
|--------|-------------|  
|正切 \(Sec\(x\)\)|1 \/ Cos\(x\)|  
|余切 \(Csc\(x\)\)|1 \/ Sin\(x\)|  
|余切 \(Ctan\(x\)\)|1 \/ Tan\(x\)|  
|反正弦 \(Asin\(x\)\)|Atan\(x \/ Sqrt\(\-x \* x \+ 1\)\)|  
|反余弦 \(Acos\(x\)\)|Atan\(\-x \/ Sqrt\(\-x \* x \+ 1\)\) \+ 2 \* Atan\(1\)|  
|反正割 \(Asec\(x\)\)|2 \* Atan\(1\) – Atan\(Sign\(x\) \/ Sqrt\(x \* x – 1\)\)|  
|反余割 \(Acsc\(x\)\)|Atan\(Sign\(x\) \/ Sqrt\(x \* x – 1\)\)|  
|反余切 \(Acot\(x\)\)|2 \* Atan\(1\) \- Atan\(x\)|  
|双曲正弦 \(Sinh\(x\)\)|\(Exp\(x\) – Exp\(\-x\)\) \/ 2|  
|双曲余弦 \(Cosh\(x\)\)|\(Exp\(x\) \+ Exp\(\-x\)\) \/ 2|  
|双曲正切 \(Tanh\(x\)\)|\(Exp\(x\) – Exp\(\-x\)\) \/ \(Exp\(x\) \+ Exp\(\-x\)\)|  
|双曲正割 \(Sech\(x\)\)|2 \/ \(Exp\(x\) \+ Exp\(\-x\)\)|  
|双曲余割 \(Csch\(x\)\)|2 \/ \(Exp\(x\) – Exp\(\-x\)\)|  
|双曲余切 \(Coth\(x\)\)|\(Exp\(x\) \+ Exp\(\-x\)\) \/ \(Exp\(x\) – Exp\(\-x\)\)|  
|反双曲正弦 \(Asinh\(x\)\)|Log\(x \+ Sqrt\(x \* x \+ 1\)\)|  
|反双曲余弦 \(Acosh\(x\)\)|Log\(x \+ Sqrt\(x \* x – 1\)\)|  
|反双曲正切 \(Atanh\(x\)\)|Log\(\(1 \+ x\) \/ \(1 – x\)\) \/ 2|  
|反双曲正割 \(AsecH\(x\)\)|Log\(\(Sqrt\(\-x \* x \+ 1\) \+ 1\) \/ x\)|  
|反双曲余割 \(Acsch\(x\)\)|Log\(\(Sign\(x\) \* Sqrt\(x \* x \+ 1\) \+ 1\) \/ x\)|  
|反双曲余切 \(Acoth\(x\)\)|Log\(\(x \+ 1\) \/ \(x – 1\)\) \/ 2|  
  
## 请参阅  
 [数学函数](../../../visual-basic/language-reference/functions/math-functions.md)