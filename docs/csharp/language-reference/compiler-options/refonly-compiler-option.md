---
title: "-refonly（C# 编译器选项）"
ms.date: 2017-07-08
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
f1_keywords:
- /refonly
dev_langs:
- CSharp
helpviewer_keywords:
- /refonly compiler option [C#]
- -refonly compiler option [C#]
author: BillWagner
ms.author: wiwagn
ms.translationtype: HT
ms.sourcegitcommit: 81a2252314ef51b5dc01fddc081eb881aa4431a7
ms.openlocfilehash: af99f7565a43dd28b6271611bc8690e7a2e51482
ms.contentlocale: zh-cn
ms.lasthandoff: 08/16/2017

---

# <a name="refonly-c-compiler-options"></a>/refonly（C# 编译器选项）

/refonly 选项表示应输出引用程序集（而不是实现程序集）作为主输出。 `/refonly` 参数以无提示方式禁用输出 PDB，因为无法执行引用程序集。

## <a name="syntax"></a>语法

```console
/refonly
```

## <a name="remarks"></a>备注

仅包含元数据的程序集会将方法主体替换为一个 `throw null` 主体，但包括除匿名类型以外的所有成员。 使用 `throw null` 主体（而非不使用主体）的原因在于，这样做可以运行和传递 PEVerify（从而验证元数据的完整性）。

引用程序集包括程序集级 `ReferenceAssembly` 属性。 可以在源中指定此属性（之后编译器就不需要进行合成）。 由于有此属性，运行时会拒绝加载用于执行的引用程序集（但仍可在仅限反射的模式下加载）。 在程序集上反射的工具需要确保仅将引用程序集加载为反射模式，否则将生成运行时 typeload 错误。

引用程序集进一步从仅包含元数据的程序集中删除元数据（私有成员）：

- 引用程序集只包含在 API 外围应用中所需的引用。 实际程序集可能包含与特定实现相关的其他引用。 例如，`class C { private void M() { dynamic d = 1; ... } }` 的引用程序集不引用 `dynamic` 所需的任何类型。
- 删除私有函数成员（方法、属性和事件），前提是这不会对编译造成显著影响。 如果没有 `InternalsVisibleTo` 属性，也请删除内部函数成员。
- 但保留引用程序集中的所有类型（包括私有或嵌套类型）。 保留所有属性（甚至是内部属性）。
- 保留所有虚拟方法。 保留显式接口实现。 保留显式实现的属性和事件，因为它们的访问器是虚拟的（因此予以保留）。
- 保留结构的所有字段。 （这是 post-C#-7.1 优化候选项）

`/refonly` 和 [`/refout`](refout-compiler-option.md) 选项互斥。

## <a name="see-also"></a>另请参阅
 [（C# 编译器选项）](../../../csharp/language-reference/compiler-options/index.md)   
 [管理项目和解决方案属性](/visualstudio/ide/managing-project-and-solution-properties)

