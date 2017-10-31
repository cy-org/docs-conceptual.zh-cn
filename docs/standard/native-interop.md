---
title: "本机互操作性"
description: "了解如何与 .NET 中的本机组件交互。"
keywords: ".NET、.NET Core"
author: blackdwarf
ms.author: ronpet
ms.date: 06/20/2016
ms.topic: article
ms.prod: .net
ms.technology: dotnet-standard
ms.devlang: dotnet
ms.assetid: 3c357112-35fb-44ba-a07b-6a1c140370ac
ms.translationtype: HT
ms.sourcegitcommit: 3155295489e1188640dae5aa5bf9fdceb7480ed6
ms.openlocfilehash: 9652986491f087b8fa175e2b4041063c71211178
ms.contentlocale: zh-cn
ms.lasthandoff: 08/21/2017

---

# <a name="native-interoperability"></a>本机互操作性

在本文档中，我们将略为深入地探讨使用 .NET 可实现“本机互操作性”的所有三种方式。

调用本机代码的原因有以下几种：

*   在操作系统附带的 API 有很多并不在托管类库中。 最好的例子就是对硬件或操作系统管理功能的访问。
*   与包含或者可以生成 C 式 ABI（本机 ABI）的其他组件通信。 例如，这包括通过 [Java 本机接口 (JNI)](http://docs.oracle.com/javase/8/docs/technotes/guides/jni/) 或其他任何可以生成本机组件的托管语言公开的 Java 代码。
*   在 Windows 上，安装的大部分软件（例如 Microsoft Office 套件）会注册 COM 组件，用于代表软件的程序，并使开发人员能够自动化或者使用它们。 在这种情况下，也需要本机互操作性。

当然，上述列表并未包括开发人员想要/偏向于/需要与本机组件交互的所有可能场合与情境。 例如，.NET 类库使用本机互操作性支持来实现其相当多的 API，如控制台支持和操作、文件系统访问，等等。 但务必知道，本机互操作性总能提供相应的选项来满足用户的需要。

> [!NOTE]
> 本文档中的大部分示例是针对 .NET Core 支持的所有三个平台（Windows、Linux 和 macOS）提供的。 但是，在某些简短的演示性示例中，只显示了一个使用 Windows 文件名和扩展名（即，库的扩展名“dll”）的例子。 这并不意味着这些功能不能在 Linux 或 macOS 上使用，只是出于方便而未提到这些平台。

## <a name="platform-invoke-pinvoke"></a>平台调用 (P/Invoke)

P/Invoke 是可用于从托管代码访问非托管库中的结构、回调和函数的一种技术。 大多数 P/Invoke API 包含在以下两个命名空间中：`System` 和 `System.Runtime.InteropServices`。 使用这两个命名空间可以访问用于描述如何与本机组件通信的特性。

我们从最常见的示例着手。该示例在托管代码中调用非托管函数。 让我们从命令行应用程序显示一个消息框：

```csharp
using System.Runtime.InteropServices;

public class Program {

    // Import user32.dll (containing the function we need) and define
    // the method corresponding to the native function.
    [DllImport("user32.dll")]
    public static extern int MessageBox(IntPtr hWnd, String text, String caption, int options);

    public static void Main(string[] args) {
        // Invoke the function as a regular managed method.
        MessageBox(IntPtr.Zero, "Command-line message box", "Attention!", 0);
    }
}
```

上述示例非常简单，但确实演示了从托管代码调用非托管函数需要做些什么。 让我们逐步分析该示例：

*   第 1 行显示 `System.Runtime.InteropServices`（用于保存全部所需项的命名空间）的 using 语句。
*   第 5 行引入 `DllImport` 特性。 此特性至关重要，因为它告诉运行时要加载非托管 DLL。 这也是我们要调用的 DLL。
*   第 6 行显示了 P/Invoke 的关键作用。 它定义了一个托管方法，该方法的签名与非托管方法**完全相同**。 可以看到，声明中包含一个新关键字 `extern`，告诉运行时这是一个外部方法。调用该方法时，运行时应在 `DllImport` 特性中指定的 DLL 内查找该方法。

该示例的剩余部分无非就是调用该方法，就像调用其他任何托管方法一样。

在 macOS 上也可以使用类似的示例。 当然，需要更改的一项设置就是 `DllImport` 特性中的库名称，因为 macOS 使用不同的方案来命名动态库。 下面的示例使用 `getpid(2)` 函数获取应用程序的进程 ID，然后控制台上列显该 ID。

```csharp
using System;
using System.Runtime.InteropServices;

namespace PInvokeSamples {
    public static class Program {

        // Import the libc and define the method corresponding to the native function.
        [DllImport("libSystem.dylib")]
        private static extern int getpid();

        public static void Main(string[] args){
            // Invoke the function and get the process ID.
            int pid = getpid();
            Console.WriteLine(pid);
        }
    }
}
```

当然，在 Linux 上也可以使用类似的示例。 函数名称是相同的，因为 `getpid(2)` 是 [POSIX](https://en.wikipedia.org/wiki/POSIX) 系统调用。

```csharp
using System;
using System.Runtime.InteropServices;

namespace PInvokeSamples {
    public static class Program {

        // Import the libc and define the method corresponding to the native function.
        [DllImport("libc.so.6")]
        private static extern int getpid();

        public static void Main(string[] args){
            // Invoke the function and get the process ID.
            int pid = getpid();
            Console.WriteLine(pid);
        }
    }
}
```

### <a name="invoking-managed-code-from-unmanaged-code"></a>从非托管代码调用托管代码

运行时允许通信流量双向流通，这样，你便可以使用函数指针从本机函数调用托管项目。 在托管代码中，与函数指针最接近的功能就是**委托**，正是凭借这个功能，才能从本机代码回调托管代码。

此功能的使用方式类似于上面所述的从托管代码调用本机进程。 对于给定的回调，需要定义一个与签名匹配的委托，并将其传入外部方法。 运行时将负责处理所有剩余工作。

```csharp
using System;
using System.Runtime.InteropServices;

namespace ConsoleApplication1 {

    class Program {

        // Define a delegate that corresponds to the unmanaged function.
        delegate bool EnumWC(IntPtr hwnd, IntPtr lParam);

        // Import user32.dll (containing the function we need) and define
        // the method corresponding to the native function.
        [DllImport("user32.dll")]
        static extern int EnumWindows(EnumWC lpEnumFunc, IntPtr lParam);

        // Define the implementation of the delegate; here, we simply output the window handle.
        static bool OutputWindow(IntPtr hwnd, IntPtr lParam) {
            Console.WriteLine(hwnd.ToInt64());
            return true;
        }

        static void Main(string[] args) {
            // Invoke the method; note the delegate as a first parameter.
            EnumWindows(OutputWindow, IntPtr.Zero);
        }
    }
}
```

在演练示例之前，最好是回顾一下所要使用的非托管函数的签名。 要调用以枚举所有窗口的函数具有以下签名：`BOOL EnumWindows (WNDENUMPROC lpEnumFunc, LPARAM lParam);`

第一个参数是回调。 该回调具有以下签名：`BOOL CALLBACK EnumWindowsProc (HWND hwnd, LPARAM lParam);`

了解签名后，让我们继续演练示例：

*   示例中的第 8 行定义与非托管代码中回调签名匹配的委托。 请注意如何在托管代码中使用 `IntPtr` 表示 LPARAM 和 HWND 类型。
*   第 10 和 11 行从 user32.dll 库中引入 `EnumWindows` 函数。
*   第 13 - 16 行实现该委托。 在这个简单的示例中，我们只要将句柄输出到控制台。
*   最后，第 19 行调用外部方法并传入委托。

下面显示了 Linux 和 macOS 示例。 在这些平台上，我们可以使用 C 库 `libc` 中的 `ftw` 函数。 此函数用于遍历目录层次结构，它使用指向某个函数的指针作为其参数之一。 该函数具有以下签名：`int (*fn) (const char *fpath, const struct stat *sb, int typeflag)`。

```csharp
using System;
using System.Runtime.InteropServices;

namespace PInvokeSamples {
    public static class Program {

            // Define a delegate that has the same signature as the native function.
            delegate int DirClbk(string fName, StatClass stat, int typeFlag);

            // Import the libc and define the method to represent the native function.
            [DllImport("libc.so.6")]
            static extern int ftw(string dirpath, DirClbk cl, int descriptors);

            // Implement the above DirClbk delegate;
            // this one just prints out the filename that is passed to it.
            static int DisplayEntry(string fName, StatClass stat, int typeFlag) {
                    Console.WriteLine(fName);
                    return 0;
            }

            public static void Main(string[] args){
                    // Call the native function.
                    // Note the second parameter which represents the delegate (callback).
                    ftw(".", DisplayEntry, 10);
            }
    }

    // The native callback takes a pointer to a struct. The below class
    // represents that struct in managed code. You can find more information
    // about this in the section on marshalling below.
    [StructLayout(LayoutKind.Sequential)]
    public class StatClass {
            public uint DeviceID;
            public uint InodeNumber;
            public uint Mode;
            public uint HardLinks;
            public uint UserID;
            public uint GroupID;
            public uint SpecialDeviceID;
            public ulong Size;
            public ulong BlockSize;
            public uint Blocks;
            public long TimeLastAccess;
            public long TimeLastModification;
            public long TimeLastStatusChange;
    }
}
```

macOS 示例使用相同的函数，唯一的差别在于 `DllImport` 特性的自变量，因为 macOS 将 `libc` 保留在不同的位置。

```csharp
using System;
using System.Runtime.InteropServices;

namespace PInvokeSamples {
        public static class Program {

                // Define a delegate that has the same signature as the native function.
                delegate int DirClbk(string fName, StatClass stat, int typeFlag);

                // Import the libc and define the method to represent the native function.
                [DllImport("libSystem.dylib")]
                static extern int ftw(string dirpath, DirClbk cl, int descriptors);

                // Implement the above DirClbk delegate;
                // this one just prints out the filename that is passed to it.
                static int DisplayEntry(string fName, StatClass stat, int typeFlag) {
                        Console.WriteLine(fName);
                        return 0;
                }

                public static void Main(string[] args){
                        // Call the native function.
                        // Note the second parameter which represents the delegate (callback).
                        ftw(".", DisplayEntry, 10);
                }
        }

        // The native callback takes a pointer to a struct. The below class
        // represents that struct in managed code. You can find more information
        // about this in the section on marshalling below.
        [StructLayout(LayoutKind.Sequential)]
        public class StatClass {
                public uint DeviceID;
                public uint InodeNumber;
                public uint Mode;
                public uint HardLinks;
                public uint UserID;
                public uint GroupID;
                public uint SpecialDeviceID;
                public ulong Size;
                public ulong BlockSize;
                public uint Blocks;
                public long TimeLastAccess;
                public long TimeLastModification;
                public long TimeLastStatusChange;
        }
}
```

上面两个示例都依赖于参数，在这两种情况下，参数是作为托管类型提供的。 运行时将采取“适当的措施”，在另一个平台上将这些代码处理成等效的代码。 由于此过程对于编写优质本机互操作代码非常重要，接下来让我们看看运行时在_封送_类型时会发生什么情况。

## <a name="type-marshalling"></a>类型封送

**封送**是当类型需要跨越托管边界进入本机代码（或反之）时转换类型的过程。

需要封送的原因是托管代码与非托管代码中的类型并不相同。 例如，在托管代码中，可指定 `String`。但在非托管环境中，字符串类型可以是 Unicode（“宽型”）、非 Unicode、null 结尾、ASCII 等。默认情况下，P/Invoke 子系统会根据默认行为尽量采取适当的措施。相关信息请参阅 [MSDN](https://msdn.microsoft.com/library/zah6xy75.aspx)。 但是，如果需要额外的控制，可以使用 `MarshalAs` 特性指定要在非托管端上使用哪种预期类型。 例如，如果要将字符串作为以 null 结尾的 ANSI 字符串发送，可以执行类似于下面的操作：

```csharp
[DllImport("somenativelibrary.dll")]
static extern int MethodA([MarshalAs(UnmanagedType.LPStr)] string parameter);
```

### <a name="marshalling-classes-and-structs"></a>封送类和结构

有关类型封送的另一个问题是如何将结构传入非托管方法。 例如，某些非托管方法需要使用结构作为参数。 在这种情况下，需要在环境的托管部分中创建相应的结构或类，以便将它用作参数。 不过，仅仅是定义类并不足够，还需要告知封送拆收器如何将类中的字段映射到非托管结构。 这就是 `StructLayout` 特性的作用所在。

```csharp
[DllImport("kernel32.dll")]
static extern void GetSystemTime(SystemTime systemTime);

[StructLayout(LayoutKind.Sequential)]
class SystemTime {
    public ushort Year;
    public ushort Month;
    public ushort DayOfWeek;
    public ushort Day;
    public ushort Hour;
    public ushort Minute;
    public ushort Second;
    public ushort Milsecond;
}

public static void Main(string[] args) {
    SystemTime st = new SystemTime();
    GetSystemTime(st);
    Console.WriteLine(st.Year);
}
```

上面这个简单的示例演示了如何调用 `GetSystemTime()` 函数。 值得注意的部分是第 4 行。 该属性指定应按顺序将类的字段映射到另一端（非托管端）上的结构。 这意味着，字段的命名并不重要，唯一重要的是字段顺序，因为这种顺序需对应于非托管结构，如下所示：

```c
typedef struct _SYSTEMTIME {
  WORD wYear;
  WORD wMonth;
  WORD wDayOfWeek;
  WORD wDay;
  WORD wHour;
  WORD wMinute;
  WORD wSecond;
  WORD wMilliseconds;
} SYSTEMTIME, *PSYSTEMTIME*;
```

前一示例中已经演示了如何在 Linux 和 macOS 上执行此过程。 下面再演示一次。

```csharp
[StructLayout(LayoutKind.Sequential)]
public class StatClass {
        public uint DeviceID;
        public uint InodeNumber;
        public uint Mode;
        public uint HardLinks;
        public uint UserID;
        public uint GroupID;
        public uint SpecialDeviceID;
        public ulong Size;
        public ulong BlockSize;
        public uint Blocks;
        public long TimeLastAccess;
        public long TimeLastModification;
        public long TimeLastStatusChange;
}
```

`StatClass` 类表示 UNIX 系统上的 `stat` 系统调用返回的结构。 它显示有关给定文件的信息。 上面的类是托管代码中的 stat 结构表示形式。 同样，该类中的字段顺序必须与本机结构相同（可以在偏好的 UNIX 实现上的手册页中找到相关信息），并且这些字段的基础类型必须相同。

## <a name="more-resources"></a>更多资源

*   [PInvoke.net wiki](http://www.pinvoke.net) 是一个极佳的 Wiki 站点，其中提供了有关常用 Win32 API 以及如何调用这些 API 的信息。
*   [MSDN 上的 P/Invoke](https://msdn.microsoft.com/library/zbz07712.aspx)
*   [有关 P/Invoke 的 Mono 文档](http://www.mono-project.com/docs/advanced/pinvoke/)

