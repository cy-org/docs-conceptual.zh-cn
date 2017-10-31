---
title: "演练：使用 Visual C# 创作复合控件 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-winforms"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "自定义控件 [C#]"
  - "自定义控件 [Windows 窗体], 创建"
  - "用户控件 [C#]"
  - "用户控件 [Windows 窗体], 使用 Visual C# 创建"
  - "UserControl 类, 演练"
ms.assetid: f88481a8-c746-4a36-9479-374ce5f2e91f
caps.latest.revision: 21
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 21
---
# 演练：使用 Visual C# 创作复合控件
复合控件提供了一种创建和重用自定义图形界面的方法。  复合控件本质上是具有可视化表示形式的组件。  因此，它可能包含一个或多个 Windows 窗体控件、组件或代码块，它们能够通过验证用户输入、修改显示属性或执行作者所需的其他任务来扩展功能。  可以按照与其他控件相同的方式将复合控件置于 Windows 窗体中。  在本演练的第一部分，将创建一个名为 `ctlClock` 的简单复合控件。  在本演练的第二部分，将通过继承扩展 `ctlClock` 的功能。  
  
> [!NOTE]
>  显示的对话框和菜单命令可能会与“帮助”中的描述不同，具体取决于您现用的设置或版本。  若要更改设置，请在**“工具”**菜单上选择**“导入和导出设置”**。  有关更多信息，请参见 [Customizing Development Settings in Visual Studio](http://msdn.microsoft.com/zh-cn/22c4debb-4e31-47a8-8f19-16f328d7dcd3)。  
  
## 创建项目  
 创建新的项目时应指定其名称，以设置根命名空间、程序集名称和项目名称，并确保默认组件将位于正确的命名空间中。  
  
#### 创建 ctlClockLib 控件库和 ctlClock 控件  
  
1.  在**“文件”**菜单上指向**“新建”**，再单击**“项目”**打开**“新建项目”**对话框。  
  
2.  从 [!INCLUDE[csprcs](../../../../includes/csprcs-md.md)] 项目列表中选择**“Windows 窗体控件库”**项目模板，在**“名称”**框中键入 `ctlClockLib`，然后单击**“确定”**。  
  
     默认情况下，项目名称 `ctlClockLib` 也被分配到根命名空间中。  根命名空间用于限定程序集中的组件名。  例如，如果两个程序集都提供名为 `ctlClock` 的组件，则可以使用 `ctlClockLib.ctlClock.`  指定 `ctlClock` 组件。  
  
3.  在解决方案资源管理器中，右击**“UserControl1.cs”**，然后选择**“重命名”**。  将文件名更改为 `ctlClock.cs`。  当系统询问是否重命名对代码元素“UserControl1”的所有引用时，单击**“是”**按钮。  
  
    > [!NOTE]
    >  默认情况下，复合控件从系统提供的 <xref:System.Windows.Forms.UserControl> 类继承。  <xref:System.Windows.Forms.UserControl> 类提供了所有复合控件要求的功能，并实现了标准方法和属性。  
  
4.  在**“文件”**菜单上，单击**“全部保存”**保存项目。  
  
## 向复合控件添加 Windows 控件和组件  
 可视化界面是复合控件的基本部分。  这种可视化界面是通过向设计器图面添加一个或多个 Windows 控件实现的。  在下面的演示中，将向复合控件中加入 Windows 控件并编写代码实现功能。  
  
#### 向复合控件添加标签和计时器  
  
1.  在解决方案资源管理器中，右击**“ctlClock.cs”**，然后单击**“视图设计器”**。  
  
2.  在**“工具箱”**中，展开**“公共控件”**节点，然后双击**“Label”**。  
  
     设计器图面上的控件中添加了一个名为 `label1` 的 <xref:System.Windows.Forms.Label> 控件。  
  
3.  在设计器中，单击**“label1”**。  在“属性”窗口中，设置下列属性。  
  
    |属性|更改为|  
    |--------|---------|  
    |**名称**|`lblDisplay`|  
    |**Text**|`（空白）`|  
    |**TextAlign**|`MiddleCenter`|  
    |**Font.Size**|`14`|  
  
4.  在**“工具箱”**中，展开**“组件”**节点，然后双击**“Timer”**。  
  
     因为 <xref:System.Windows.Forms.Timer> 是一个组件，所以它在运行时没有可视化的表示形式。  因而它不会和控件一起出现在设计器图面，而是出现在**“组件设计器”**（设计器图面底部的一栏）中。  
  
5.  在**“组件设计器”**中，单击**“Timer1”**，然后将 <xref:System.Windows.Forms.Timer.Interval%2A> 属性设置为 `1000`，将 <xref:System.Windows.Forms.Timer.Enabled%2A> 属性设置为 `true`。  
  
     <xref:System.Windows.Forms.Timer.Interval%2A> 属性控制 <xref:System.Windows.Forms.Timer> 组件的计时频率。  `timer1` 每走过一个刻度，它都会运行一次 `timer1_Tick` 事件中的代码。  interval 属性表示前后两次计时之间的毫秒数。  
  
6.  在**“组件设计器”**中，双击**“Timer1”**转到 `ctlClock` 的 `timer1_Tick` 事件。  
  
7.  将该代码修改为类似如下所示的代码示例。  确保将访问修饰符从 `private` 更改为 `protected`。  
  
     \[C\#\]  
  
    ```  
    protected void timer1_Tick(object sender, System.EventArgs e)  
    {  
        // Causes the label to display the current time.  
        lblDisplay.Text = DateTime.Now.ToLongTimeString();   
    }  
    ```  
  
     这些代码将使得当前时间显示在 `lblDisplay` 中。  因为 `timer1` 的间隔设置为 `1000`，所以该事件每 1000 毫秒发生一次，从而每一秒更新一次当前时间。  
  
8.  用 `virtual` 关键字修改该方法使其可重写。  有关更多信息，请参见下面的“从用户控件继承”一节。  
  
    ```  
    protected virtual void timer1_Tick(object sender, System.EventArgs e)  
    ```  
  
9. 在**“文件”**菜单上，单击**“全部保存”**保存项目。  
  
## 向复合控件添加属性  
 现在，clock 控件封装了 <xref:System.Windows.Forms.Label> 控件和 <xref:System.Windows.Forms.Timer> 组件，这两者各有一组继承属性。  尽管您的控件的后续用户无法访问这些控件的个别属性，但可以通过编写适当的代码块来创建和公开自定义属性。  在下面的过程中，将向控件添加属性，这些属性可使用户能够更改背景和文本的颜色。  
  
#### 向复合控件添加属性  
  
1.  在解决方案资源管理器中，右击**“ctlClock.cs”**，然后单击**“查看代码”**。  
  
     控件的**“代码编辑器”**打开。  
  
2.  找到 `public partial class ctlClock` 语句。  在左大括号 \(`{)` 下键入下列代码。  
  
     \[C\#\]  
  
    ```  
    private Color colFColor;  
    private Color colBColor;  
    ```  
  
     这些语句会创建私有变量，用来存储要创建的属性的值。  
  
3.  在步骤 2 中的变量声明下方键入以下代码。  
  
     \[C\#\]  
  
    ```  
    // Declares the name and type of the property.  
    public Color ClockBackColor  
    {  
        // Retrieves the value of the private variable colBColor.  
        get  
        {  
            return colBColor;  
        }  
        // Stores the selected value in the private variable colBColor, and   
        // updates the background color of the label control lblDisplay.  
        set  
        {  
            colBColor = value;  
            lblDisplay.BackColor = colBColor;     
        }  
    }  
    // Provides a similar set of instructions for the foreground color.  
    public Color ClockForeColor  
    {  
        get  
        {  
            return colFColor;  
        }  
        set  
        {  
            colFColor = value;  
            lblDisplay.ForeColor = colFColor;  
        }  
    }  
    ```  
  
     上述代码生成了两个自定义属性：`ClockForeColor` 和 `ClockBackColor`，该控件的后续用户可以使用这两个属性。  `get` 和 `set` 语句提供了该属性值的存储和检索，还提供了实现适合于该属性的功能的代码。  
  
4.  在**“文件”**菜单上，单击**“全部保存”**保存项目。  
  
## 测试控件  
 控件不是独立的应用程序，它们必须寄宿在容器中。  测试控件的运行时行为，并使用**“UserControl 测试容器”**运用其属性。  有关更多信息，请参见 [如何：测试 UserControl 的运行时行为](../../../../docs/framework/winforms/controls/how-to-test-the-run-time-behavior-of-a-usercontrol.md)。  
  
#### 测试控件  
  
1.  按 F5 生成该项目，然后在**“用户控件测试容器”**中运行控件。  
  
2.  在测试容器的属性网格中，找到 `ClockBackColor` 属性，然后选中该属性以显示调色板。  
  
3.  通过单击某个颜色来选择它。  
  
     控件的背景颜色更改为您选择的颜色。  
  
4.  使用类似的事件序列来验证 `ClockForeColor` 属性的功能是否与预期的相符。  
  
     本节和前面的几节演示了如何将组件和 Windows 控件与代码和打包相结合，以复合控件的形式提供自定义功能。  您已经学习了在复合控件中公开属性，以及如何在完成后对控件进行测试。  在下一节中，您将学习如何以 `ctlClock` 为基础构造继承的复合控件。  
  
## 从复合控件继承  
 在前面的章节中，您学习了如何将 Windows 控件、组件和代码组合成可重用的复合控件。  现在可将复合控件用作生成其他控件的基础了。  从基类派生类的过程称为继承。  在本节中，将创建一个称为 `ctlAlarmClock` 的复合控件。  此控件将从其父控件 `ctlClock` 派生。  您将学习如何通过重写父级方法并添加新的方法和属性来扩展 `ctlClock` 的功能。  
  
 创建继承控件的第一步是从它的父控件派生。  该操作创建一个新控件，它具有父控件的全部属性、方法和图形特征，但也可以用作添加新功能或修改过的功能的基础。  
  
#### 创建继承的控件  
  
1.  在解决方案资源管理器中，右击**“ctlClockLib”**，指向**“添加”**，然后单击**“用户控件”**。  
  
     **“添加新项”**对话框打开。  
  
2.  选择**“继承的用户控件”**模板。  
  
3.  在**“名称”**框中键入`“ctlAlarmClock.cs”`，然后单击**“添加”**。  
  
     **“继承选择器”**对话框出现。  
  
4.  在**“组件名称”**下，双击**“ctlClock”**。  
  
5.  在解决方案资源管理器中，浏览当前项目。  
  
    > [!NOTE]
    >  当前项目中添加了一个名为**“ctlAlarmClock.cs”**的文件。  
  
### 添加 Alarm 属性  
 将属性添加到继承的控件的方法与添加到复合控件的方法相同。  现在将使用属性声明语法向控件中添加两个属性：`AlarmTime` 和 `AlarmSet`，前者将存储发出警报的日期和时间值，后者指示是否设置了警报。  
  
##### 向复合控件添加属性  
  
1.  在解决方案资源管理器中，右击**“ctlAlarmClock”**，然后单击**“查看代码”**。  
  
2.  找到 `public class` 语句。  注意，控件继承自 `ctlClockLib.ctlClock`。  在左大括号 \(`{)` 语句下键入下列代码。  
  
     \[C\#\]  
  
    ```  
    private DateTime dteAlarmTime;  
    private bool blnAlarmSet;  
    // These properties will be declared as public to allow future   
    // developers to access them.  
    public DateTime AlarmTime  
    {  
        get  
        {  
            return dteAlarmTime;  
        }  
        set  
        {  
            dteAlarmTime = value;  
        }  
    }  
    public bool AlarmSet  
    {  
        get  
        {  
            return blnAlarmSet;  
        }  
        set  
        {  
            blnAlarmSet = value;  
        }  
    }  
    ```  
  
### 添加到控件的图形界面  
 继承的控件具有可视化的界面，该界面与它从中继承的控件的界面完全相同。  它与其父控件拥有相同的构成控件，但除非将构成控件的属性特别公开，否则它们将不可用。  可以向继承的复合控件的图形界面进行添加，方法与向任意复合控件进行添加相同。  若要继续向您的警报时钟的可视化界面进行添加，请您添加一个 label 控件，它将在警报响起时闪烁。  
  
##### 添加 label 控件  
  
1.  在解决方案资源管理器中，右击**“ctlAlarmClock”**，然后单击**“视图设计器”**。  
  
     `ctlAlarmClock` 的设计器在主窗口中打开。  
  
2.  单击该控件的显示部分，并查看“属性”窗口。  
  
    > [!NOTE]
    >  当显示所有属性时，属性是浅灰色的。  这表示这些属性是 `lblDisplay` 所固有的，不能在“属性”窗口中修改或访问。  默认情况下，复合控件中所包含的控件为 `private`，通过任何途径都无法访问其属性。  
  
    > [!NOTE]
    >  如果希望复合控件的后续用户可以访问其内部控件，则可将其声明为 `public` 或 `protected`。  这样就可以使用适当的代码来设置和修改复合控件内所包含控件的属性了。  
  
3.  向复合控件添加 <xref:System.Windows.Forms.Label> 控件。  
  
4.  使用鼠标将 <xref:System.Windows.Forms.Label> 控件拖到显示框的紧下方。  在“属性”窗口中，设置下列属性。  
  
    |属性|设置|  
    |--------|--------|  
    |**名称**|`lblAlarm`|  
    |**Text**|Alarm\!|  
    |**TextAlign**|`MiddleCenter`|  
    |**Visible**|`false`|  
  
### 添加警报功能  
 在前面的章节中，已经添加了一些属性和一个控件，它们将启用复合控件中的警报功能。  在本过程中，将添加代码以比较当前时间和警报时间，如果两者相同，则闪出警报。  通过重写 `ctlClock` 的 `timer1_Tick` 方法并向其中添加更多代码，`ctlAlarmClock` 的功能将得到扩展，同时会保持继承的所有 `ctlClock` 功能。  
  
##### 重写 ctlClock 的 timer1\_Tick 方法  
  
1.  在**“代码编辑器”**中，找到 `private bool blnAlarmSet;` 语句。  在其紧下方添加下列语句。  
  
     \[C\#\]  
  
    ```  
    private bool blnColorTicker;  
    ```  
  
2.  在**“代码编辑器”**中，在类的结尾找到右大括号 \(`})`。  在大括号的前面添加下列代码。  
  
     \[C\#\]  
  
    ```  
    protected override void timer1_Tick(object sender, System.EventArgs e)  
    {  
        // Calls the Timer1_Tick method of ctlClock.  
        base.timer1_Tick(sender, e);  
        // Checks to see if the alarm is set.  
        if (AlarmSet == false)  
            return;  
        else  
            // If the date, hour, and minute of the alarm time are the same as  
            // the current time, flash an alarm.   
        {  
            if (AlarmTime.Date == DateTime.Now.Date && AlarmTime.Hour ==   
                DateTime.Now.Hour && AlarmTime.Minute == DateTime.Now.Minute)  
            {  
                // Sets lblAlarmVisible to true, and changes the background color based on  
                // the value of blnColorTicker. The background color of the label   
                // will flash once per tick of the clock.  
                lblAlarm.Visible = true;  
                if (blnColorTicker == false)   
                {  
                    lblAlarm.BackColor = Color.Red;  
                    blnColorTicker = true;  
                }  
                else  
                {  
                    lblAlarm.BackColor = Color.Blue;  
                    blnColorTicker = false;  
                }  
            }  
            else  
            {  
                // Once the alarm has sounded for a minute, the label is made   
                // invisible again.  
                lblAlarm.Visible = false;  
            }  
        }  
    }  
    ```  
  
     添加此代码将完成几项任务。  `override` 语句指示控件使用此方法替换从基控件继承的方法。  此方法被调用时，它通过调用 `base.timer1_Tick` 语句来调用它重写的方法，从而确保在该控件中重现原始控件包含的所有功能。  然后，运行附加代码以合并警报功能。  当警报触发时，会出现闪烁的标签控件。  
  
     警报时钟控件已经基本完成。  剩下的唯一事情是实现关闭它的方法。  为此，将向 `lblAlarm_Click` 方法中添加代码。  
  
##### 实现关闭方法  
  
1.  在解决方案资源管理器中，右击**“ctlAlarmClock.cs”**，然后单击**“视图设计器”**。  
  
     设计器打开。  
  
2.  将一个按钮添加到控件中。  按下面的方式设置该按钮的属性。  
  
    |属性|值|  
    |--------|-------|  
    |**名称**|`btnAlarmOff`|  
    |**Text**|Disable Alarm|  
  
3.  在设计器中，双击 **btnAlarmOff**。  
  
     **“代码编辑器”**打开并显示 `private void btnAlarmOff_Click` 行。  
  
4.  像如下所示修改此方法。  
  
     \[C\#\]  
  
    ```  
    private void btnAlarmOff_Click(object sender, System.EventArgs e)  
    {  
        // Turns off the alarm.  
        AlarmSet = false;  
        // Hides the flashing label.  
        lblAlarm.Visible = false;  
    }  
    ```  
  
5.  在**“文件”**菜单上，单击**“全部保存”**保存项目。  
  
### 在窗体上使用继承的控件  
 可按测试基类控件 `ctlClock` 相同的方法测试继承的控件：按 F5 生成项目并在**“UserControl 测试容器”**中运行控件。  有关更多信息，请参见 [如何：测试 UserControl 的运行时行为](../../../../docs/framework/winforms/controls/how-to-test-the-run-time-behavior-of-a-usercontrol.md)。  
  
 要使用控件，还需要将其放入窗体中。  与标准复合控件一样，继承的复合控件不能独立存在，而必须寄宿在窗体或其他容器中。  由于 `ctlAlarmClock` 的功能更加深入，因此需要附加代码以对其进行测试。  在本过程中，将编写一个简单的程序来测试 `ctlAlarmClock` 的功能。  将编写代码以设置和显示 `ctlAlarmClock` 的 `AlarmTime` 属性，并测试其继承功能。  
  
##### 生成一个测试窗体并将您的控件添加到该窗体  
  
1.  在解决方案资源管理器中，右击**“ctlClockLib”**，然后单击**“生成”**。  
  
2.  向解决方案添加一个新的**“Windows 应用程序”**项目，并将其命名为`“Test”`。  
  
3.  在解决方案资源管理器中，右击测试项目的**“引用”**节点。  单击**“添加引用”**，显示**“添加引用”**对话框。  单击标记为**“项目”**的选项卡。  **“项目名称”**下将列出 `ctlClockLib` 项目。  双击该项目以将引用添加到测试项目。  
  
4.  在解决方案资源管理器中，右击**“测试”**，然后单击**“生成”**。  
  
5.  在**“工具箱”**中，展开**“ctlClockLib 组件”**节点。  
  
6.  双击**“ctlAlarmClock”**向窗体添加 `ctlAlarmClock` 的副本。  
  
7.  在**“工具箱”**中，找到并双击**“DateTimePicker”**以向窗体添加一个 <xref:System.Windows.Forms.DateTimePicker> 控件，然后通过双击**“Label”**添加一个 <xref:System.Windows.Forms.Label>。  
  
8.  使用鼠标将这些控件放置在窗体上合适的位置。  
  
9. 按下述方法设置这些控件的属性。  
  
    |控件|属性|值|  
    |--------|--------|-------|  
    |`label1`|**Text**|`（空白）`|  
    ||**名称**|`lblTest`|  
    |`dateTimePicker1`|**名称**|`dtpTest`|  
    ||**Format**|<xref:System.Windows.Forms.DateTimePickerFormat>|  
  
10. 在设计器中双击**“dtpTest”**。  
  
     **“代码编辑器”**将打开 `private void dtpTest_ValueChanged`。  
  
11. 像如下所示修改代码。  
  
     \[C\#\]  
  
    ```  
    private void dtpTest_ValueChanged(object sender, System.EventArgs e)  
    {  
        ctlAlarmClock1.AlarmTime = dtpTest.Value;  
        ctlAlarmClock1.AlarmSet = true;  
        lblTest.Text = "Alarm Time is " +  
            ctlAlarmClock1.AlarmTime.ToShortTimeString();  
    }  
    ```  
  
12. 在解决方案资源管理器中，右击**“测试”**，然后单击**“设为启动项目”**。  
  
13. 在**“调试”**菜单上，单击**“启动调试”**。  
  
     测试程序启动。  注意，`ctlAlarmClock` 控件中的当前时间更新了，并且 <xref:System.Windows.Forms.DateTimePicker> 控件中显示了启动时间。  
  
14. 单击 <xref:System.Windows.Forms.DateTimePicker>，其中显示小时的分钟值。  
  
15. 使用键盘设置一个分钟值，使它比 `ctlAlarmClock` 显示的当前时间快一分钟。  
  
     警报设置的时间显示在 `lblTest` 中。  等候显示的时间到达警报设置时间。  当显示的时间到达警报设置时间时，`lblAlarm` 将闪出。  
  
16. 单击 `btnAlarmOff` 关闭警报。  您现在可以重置警报。  
  
     本演练涉及了一些关键概念。  您学习了如何通过将控件和组件组合到复合控件容器中来创建复合控件。  您还已经学会将属性添加到控件，以及编写代码以实现自定义功能。  在最后一节中，您学习了如何通过继承来扩展给定复合控件的功能，以及如何通过重写宿主方法来改变这些方法的功能。  
  
## 请参阅  
 [各种自定义控件](../../../../docs/framework/winforms/controls/varieties-of-custom-controls.md)   
 [使用组件编程](../Topic/Programming%20with%20Components.md)   
 [Component Authoring Walkthroughs](../Topic/Component%20Authoring%20Walkthroughs.md)   
 [如何：在“选择工具箱项”对话框中显示控件](../../../../docs/framework/winforms/controls/how-to-display-a-control-in-the-choose-toolbox-items-dialog-box.md)   
 [演练：使用 Visual C\# 从 Windows 窗体控件继承](../../../../docs/framework/winforms/controls/walkthrough-inheriting-from-a-windows-forms-control-with-visual-csharp.md)