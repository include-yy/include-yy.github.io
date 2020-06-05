在正式开始介绍控制台应用之前，先看看什么是控制台和终端。

以下是科普时间。

# 什么是 console，terminal

## console（控制台）

控制台是用于输入和显示系统用户消息的设备，尤指来自于 [BIOS](https://en.wikipedia.org/wiki/BIOS) 和 [boot loader](https://en.wikipedia.org/wiki/Booting) 的信息。它是由键盘和屏幕组成的物理设备，屏幕一般是文本终端（[text terminal](https://en.wikipedia.org/wiki/Text_terminal "Text terminal")），但也可以是图形终端（[graphical terminal](https://en.wikipedia.org/wiki/Graphical_terminal "Graphical terminal")）。控制台被概括为计算机终端（[computer terminals](https://en.wikipedia.org/wiki/Computer_terminal "Computer terminal")），计算机终端相应地被抽象为了虚拟终端（[virtual consoles](https://en.wikipedia.org/wiki/Virtual_console)）和终端模拟器（[terminal emulators](https://en.wikipedia.org/wiki/Terminal_emulator)）。现今，与控制台的沟通被抽象化了，通过标准流（[stdin](https://en.wikipedia.org/wiki/Stdin "Stdin"), [stdout](https://en.wikipedia.org/wiki/Stdout "Stdout"),，和 [stderr](https://en.wikipedia.org/wiki/Stderr "Stderr")）进行，但也许存在系统特定的接口，比如由系统内核使用的那些。

## terminal （终端）

终端可以是指物理设备，也可以指软件。先从物理设备说起。

计算机终端是用于输入或显示来自电脑或系统数据的电子设备，tty （[teletype](https://en.wikipedia.org/wiki/Teleprinter)）是早期终端的一种，它的出现比电脑屏幕的使用早了数十年。

早期的终端价格并不昂贵，但是相比打孔卡（[punched cards](https://en.wikipedia.org/wiki/Punched_card "Punched card")）和打孔带（[paper tape](https://en.wikipedia.org/wiki/Paper_tape)）而言速度很慢。但随着技术的进步和显示设备（[video displays](https://en.wikipedia.org/wiki/Video_display "Video display")）的引入，终端将这些交互形式挤出了工业界。与终端相关的是分时系统（[timesharing](https://en.wikipedia.org/wiki/Timesharing "Timesharing")）的发展，它与终端共同发展，能够支持多个用户通过多个终端使用一台机器，从而弥补了用户低效的输入能力。

终端的功能被限制在输入和显示数据；具有显著本地可编程或数据处理能力的设备可称为“智能终端”或胖客户端（[fat client](https://en.wikipedia.org/wiki/Fat_client "Fat client")）。依赖于主机（host computer）处理能力的终端被称为“哑终端”或瘦终端（[thin client](https://en.wikipedia.org/wiki/Thin_client "Thin client")）。个人电脑可以通过运行终端模拟器来复现终端的功能，这些终端模拟器可能允许并发运行本地程序和访问非本地终端主机系统。

## 两者的关联和区别是什么

控制台和终端的关系是非常紧密的，它们都是指一种设备，通过它你可以与计算机进行交互。“终端”这个名字来自于电子视角，“控制台”这个名字来自于器物的视角。

但它们又是不同的。一台主机可以有多个终端，但在主机的系统完成启动之前，终端无法连接到主机上。为了能够记录主机开机日志，需要有控制台。一个主机只能有一个控制台【4】。

## 作为软件的 console 和 terminal

以下内容引自参考资料【3】

> 在 \*nix 术语中，**终端** 是一种设备文件（[device file](http://en.wikipedia.org/wiki/Device_file)），它在读写之上实现了一些额外的命令（[ioctls](http://en.wikipedia.org/wiki/Ioctl#Terminals)）。某些终端由内核代表硬件设备提供，例如来自键盘的输入和到达文本屏幕的输出，或是通过串口传输的输入和输出。其他的终端，有时叫做伪终端，由叫做终端模拟器（[terminal emulators](http://en.wikipedia.org/wiki/Terminal_emulator)）的程序提供（通过内核的薄层封装）。
> 
> 控制台在操作系统中以终端（由内核负责实现）的形式显示，在一些系统上，比如 Linux 和 FreeBSD，控制台显示为多个终端。它们的名字可以是 ”控制台“，”虚拟控制台”，“虚拟终端”，（“console”, ”virtual console”, ”virtual terminal”）等等其他版本，这些名字只起到了混淆的作用（just to confuse matters）

### 什么是终端模拟器

> 终端模拟器是一种计算机程序，它模拟其他显示架构中的物理视频终端 —— 摘自维基百科

在带图形用户界面的环境中，终端模拟器一般叫做终端窗口。终端窗口允许用户访问文本终端和命令行应用。这些工作可以在本地机器上完成，也可以通过 [telnet](https://en.wikipedia.org/wiki/Telnet "Telnet")， [ssh](https://en.wikipedia.org/wiki/Secure_Shell "Secure Shell") 在其他电脑上进行。在类 Unix （[Unix-like](https://en.wikipedia.org/wiki/Unix-like "Unix-like")）系统上，有一个或多个与本地机器连接的终端是很常见的。

终端模拟器通常支持一个转义字符集，来进行比如控制颜色，控制光标位置的一系列操作。

终端模拟器一般都提供了本地编辑功能，也叫做 "line-at-a-time" 模式。在这个模式下，终端模拟器只会向主机系统发送完整的一行输入。用户输入并编辑一行，在编辑时它保留在终端编辑器中。它在用户发出完成信号前不会被传输，传输信号一般是键盘上的 `↵ Enter` 键或是某些用户界面的 “send” 按钮，信号发出后，一整行会被传输。line-at-a-time 模式一般会包含回显（echo），因为不这样的话用户就不能看到之前编辑的行了。不过， line-at-a-time 模式与回显模式是独立的，它对是否回显不进行要求。（例如输入密码时回显一般是关闭的）

一些不同类型的终端模拟器：

- 在 [X Window System](http://en.wikipedia.org/wiki/X_Window_System) 中运行的 GUI 程序：[Xterm](http://en.wikipedia.org/wiki/Xterm)，Gnome Terminal，Konsole，Terminator，等等

- [Screen](http://en.wikipedia.org/wiki/Gnu_screen) 和 [tmux](http://en.wikipedia.org/wiki/Tmux)，它们提供了在程序和终端之间的分隔层

- [Ssh](http://en.wikipedia.org/wiki/Secure_shell) ，它将一个机器上的终端与另一个机器上的程序连接起来

### 什么是 Shell ，以及它与终端模拟器的关系

[shell](http://en.wikipedia.org/wiki/Shell_%28computing%29) 是用户登入系统时的初始界面。在 Unix 圈子中，shell 特指命令行 shell（[command-line shell](http://en.wikipedia.org/wiki/Shell_%28computing%29#Text_.28CLI.29_shells)），输入想要启动的应用名称，后面跟着应用程序执行的文件或其他对象的名称，然后按下 Enter 键。其他类型的环境通常不使用 shell 这个词，例如， windows 系统使用 "window manager" 和 "desktop environment"，而不是 "shell“。

存在着各种各样的 Unix shell。Ubuntu 的默认 shell 是 [Bash](http://en.wikipedia.org/wiki/Bash_(Unix_shell)（和大多数 Linux 发行版一样）。其他比较流行的比如 [zsh](http://en.wikipedia.org/wiki/Zsh) （强调功能和个性化）和 [fish](http://en.wikipedia.org/wiki/Friendly_interactive_shell) （强调简便性）。

命令行 sehll 包括了组合命令的控制流结构。除了在命令提示符处输入命令外，用户也可以编写脚本。大多数的 shell 都有基于 [Bourne_shell](http://en.wikipedia.org/wiki/Bourne_shell) 的基本语法。当谈到 ”shell 编程“ 时，shell 几乎总是指 Bourne-风格的 shell。几乎说有的类 Unix 系统都有一个 Bourne-风格 的 shell，安装在 `/bin/sh` 目录下。

终端模拟器（下文简称终端）和 shell 的分工并不是非常明显，下面列出了它们的主要工作：

- 输入：终端将击键转化为控制序列（比如，Left → `\e[D`）。shell 将控制序列转化为命令（比如，`\e[D` → `backward-char`）

- 行编辑，输入历史和补全功能由 shell 提供。（终端可能提供它自己的行编辑，历史和补全，并只是将一行发送给准备好执行的 shell，唯一以这种方式运行的终端是 Emacs 中的 `M-x shell`）

- 输出：shell 忽略像是 “display `foo`”， “switch the foreground color to green”，“move the cursor to the next line” 之类的命令。这些工作由终端完成

- 提示符完全是 shell 中的概念

- shell 永远不会看到它运行的命令的输出（除非进行了重定向）。输出历史是终端中的概念

- 应用间的 复制-粘贴 是由终端提供的（通常使用 `Ctrl`+`Shift`+`V` 或 `Shift`+`Insert` ）。 shell 可能也有它自己的内部 复制-粘贴 机制（比如`Meta`+`W` 和 `Ctrl`+`Y`）

- 工作控制（[Job control](http://en.wikipedia.org/wiki/Job_control)）（在后台运行并管理程序）大多数是由 shell 进行的。然而，像是使用组合键 `Ctrl`+`C` 杀掉前台作业或 `Ctrl`+`Z` 来进行折叠之类的工作是由终端完成的

对于 shell 和终端的区别的描述来自【3】。

shell 指的是一个界面，而不局限于命令行。从上述内容来看，用户与命令行 shell 的沟通是需要终端模拟器的参与的。输入经过终端模拟器到达 shell，shell 输出的显示、排版和字体颜色由终端模拟器负责。

根据：（来源：【3】 中的某个回答）

> **Terminal** is a program that `run` a **shell** 

我们至少可以这样说：shell 运行在终端模拟器中。

# Windows 中的控制台

控制台（或终端）是为字符模式应用（控制台应用）提供 I/O 的应用程序。这个处理器无关的机制使得移植现有控制台应用或创建新的控制台应用很容易。

控制台由一个输入缓冲区和一个或多个屏幕缓冲区组成。*输入缓冲区* 包含一个输入记录队列，队列中的成员包含着输入事件的信息。输入队列总是包括键-按下和键-松起的事件。它也包括鼠标事件（指针移动和鼠标的按下和释放）和用户影响了屏幕缓冲区大小的事件。*屏幕缓冲区* 在控制台窗口中是一个字符和颜色数据的二维数组。一个控制台可以被任意数量的进程共享。

## 控制台的创建

当启动一个控制台进程，即一个入口点函数是 main 函数的字符模式进程时，系统会创建一个新的控制台。例如，系统会在启动命令行处理器时（cmd）创建一个新的控制台。当 cmd 中开始一个新的控制台进程时，用户可以指定是由系统为这个新进程创建一个新的控制台，还是继承 cmd 的控制台。

一个进程可以通过以下方法来创建一个新的控制台：

- 一个 GUI 或控制台进程可以使用 [**CreateProcess**](https://msdn.microsoft.com/library/windows/desktop/ms682425) （使用 CREATE\_NEW\_CONSOLE）来创建一个使用新的控制台的控制台进程。（默认情况下，控制台进程会继承它的父进程的控制台，而且不能保证输入是由所认为的进程接收的）

- 没有附加到控制台的 GUI 或控制台进程可以使用 [**AllocConsole**](https://docs.microsoft.com/en-us/windows/console/allocconsole) 来创建一个新的控制台。（GUI 进程在创建时没有附加到一个控制台。如果使用[**CreateProcess**](https://msdn.microsoft.com/library/windows/desktop/ms682425) （使用 DETACHED\_PROCESS） 创建，控制台进程就不会附加到一个控制台。

一般而言，当错误出现，且需要与用户进行交互时，进程会使用 [**AllocConsole**](https://docs.microsoft.com/en-us/windows/console/allocconsole) 来创建一个控制台。例如，一个 GUI 进程可以在错误出现时创建一个控制台，来避免使用图形界面。或者，一个一般不与用户交互的控制台进程可以创建一个控制台来显示错误。

通过在 [**CreateProcess**](https://msdn.microsoft.com/library/windows/desktop/ms682425) 中使用 CREATE\_NEW\_CONSOLE 标志可以创建一个控制台。这种方法创建了一个可由子进程访问，但不能由父进程访问的控制台。分离的控制台允许子进程和父进程在没有矛盾的情况下与用户交互。如果在创建控制台进程时没有指定标志，进程都会附加到同样的控制台，这样就不能保证你所倾向的那个进程会接收到输入。应用可以通过创建不继承输出缓冲区句柄的子进程来避免混乱，或者在一定时间内只允许子进程继承输入缓冲区句柄，而不允许父进程从控制台输入中进行读入，直到子进程完成工作。

创建一个控制台会得到一个新的控制台窗口，和分离的 I/O 屏幕缓冲区。与新控制台关联的进程可使用 [**GetStdHandle**](https://docs.microsoft.com/en-us/windows/console/getstdhandle) 函数来取得新控制台的输入和屏幕缓冲区句柄。这些句柄允许进程对控制台进行访问。

当一个进程使用了 [**CreateProcess**](https://msdn.microsoft.com/library/windows/desktop/ms682425) ，它可以指定一个[**STARTUPINFO**](https://msdn.microsoft.com/library/windows/desktop/ms686331) 结构，该结构的成员对第一个为子进程创建的控制台起控制作用。 在对 CreateProcess 的调用中指定的 STARTUPINFO 结构会通过是否指定了 CREATE\_NEW\_CONSOLE 这个标志影响控制台的创建。如果子进程随后使用了 [**AllocConsole**](https://docs.microsoft.com/en-us/windows/console/allocconsole) ，它也会对控制台的创建造成影响。以下控制台特性可以被指定：

- 新控制台的窗口大小，以字符为单位

- 新控制台窗口的位置，以屏幕像素坐标为单位

- 控制台屏幕缓冲区的大小，以字符为单位

- 控制台屏幕缓冲区的文本和背景颜色属性

- 窗口标题栏名字的显示

如果没有指定 [**STARTUPINFO**](https://msdn.microsoft.com/library/windows/desktop/ms686331) 结构的值，系统会使用默认值。子进程可以使用 [**GetStartupInfo**](https://msdn.microsoft.com/library/windows/desktop/ms683230) 函数来得到 STARTUPINFO 结构中的值。

进程不能改变它的控制台窗口在屏幕上的位置，但是下面的一些控制台函数可以设置或检索由 STARTUPINFO 中的其他性质。

- [**GetConsoleScreenBufferInfo**](https://docs.microsoft.com/en-us/windows/console/getconsolescreenbufferinfo) ：检索窗口的大小，屏幕缓冲区大小，和颜色属性

- [**SetConsoleWindowInfo**](https://docs.microsoft.com/en-us/windows/console/setconsolewindowinfo) ：改变窗口的大小

- [**SetConsoleScreenBufferSize**](https://docs.microsoft.com/en-us/windows/console/setconsolescreenbuffersize) ：改变控制台的屏幕缓冲区大小

- [**SetConsoleTextAttribute**](https://docs.microsoft.com/en-us/windows/console/setconsoletextattribute) ：设置颜色属性

- [**SetConsoleTitle**](https://docs.microsoft.com/en-us/windows/console/setconsoletitle) ：设置控制台窗口标题

- [**GetConsoleTitle**](https://docs.microsoft.com/en-us/windows/console/getconsoletitle) ：设置控制台窗口标题

进程可以使用 [**FreeConsole**](https://docs.microsoft.com/en-us/windows/console/freeconsole) 来将自己与继承的控制台或使用 [**AllocConsole**](https://docs.microsoft.com/en-us/windows/console/allocconsole) 创建的控制台分离。

## 附加到控制台

进程可以使用 [**AttachConsole**](https://docs.microsoft.com/en-us/windows/console/attachconsole) 函数来附加到一个控制台。进程可以附加到一个控制台。

一个控制台可以有很多个进程附加于它。若要检索附加进程表，可调用 [**GetConsoleProcessList**](https://docs.microsoft.com/en-us/windows/console/getconsoleprocesslist) 函数。

## 控制台的关闭

进程可以使用 [**FreeConsole**](https://docs.microsoft.com/en-us/windows/console/freeconsole) 来于它的控制台分离。如果有其他控制台在共享这个控制台，控制台不会被销毁，但已调用 FreeConsole 的进程不能再使用它。在调用 FreeConsole 后，进程可以使用 [**AllocConsole**](https://docs.microsoft.com/en-us/windows/console/allocconsole) 创建新的控制台或使用 [**AttachConsole**](https://docs.microsoft.com/en-us/windows/console/attachconsole) 来附加到另一个控制台。

当最后一个附加于它的进程终止或调用 FreeConsole 后，控制台会被关闭。

## 控制台句柄

控制台进程使用句柄来访问它的控制台的输入和屏幕缓冲区。进程可以使用 [**GetStdHandle**](https://docs.microsoft.com/en-us/windows/console/getstdhandle)，[**CreateFile**](https://msdn.microsoft.com/library/windows/desktop/aa363858) 或 [**CreateConsoleScreenBuffer**](https://docs.microsoft.com/en-us/windows/console/createconsolescreenbuffer) 函数来打开这些句柄。

函数 [**GetStdHandle**](https://docs.microsoft.com/en-us/windows/console/getstdhandle) 提供了一种检索与线程关联的标准输入（STDIN），标准输出（STDOUT）和标准错误（STDERR）句柄的机制。在控制台创建时，系统会创建这些句柄。初始条件下，STDIN 是与控制台输入缓冲区的句柄，STDOUT 和 STDERR 是控制台活跃屏幕缓冲区的句柄。然而，[**SetStdHandle**](https://docs.microsoft.com/en-us/windows/console/setstdhandle) 可以可以通过改变句柄与 STDIN，STDOUT 或 STDERR 的关联来重定向标准句柄。因为父进程的标准句柄由子进程继承，故在 SetStdHandle 调用后，GetStdHandle 会返回被重定向的句柄。由 GetStdHandle 返回的句柄因此可能指向不是控制台 I/O 的其他东西。例如，在创建子进程之前，父进程可以使用 SetStdHandle 将管道句柄（pipe handle）设置为 STDIN 句柄，并交给子进程继承。当子进程调用 GetStdHandle 时，它会得到管道句柄。这就意味着父进程可以控制子进程的标准句柄。由 GetStdHandle 返回的句柄拥有 GENERIC\_READ | GENERIC\_WRITE 许可，除非使用 SetStdHandle 将标准句柄的许可减少。

由 [**GetStdHandle**](https://docs.microsoft.com/en-us/windows/console/getstdhandle) 返回的句柄值并不是 0，1 和 2，因此在 Stdio.h 中预定义的流常数（STDIN，STDOUT，STDERR）不能在需要控制台句柄的函数中使用。

函数 [**CreateFile**](https://msdn.microsoft.com/library/windows/desktop/aa363858) 语序进程获得指向控制台输入缓冲区和活跃屏幕缓冲区的句柄，即便 STDIN 和 STDOUT 已经被重定向了。要打开控制台输入缓冲区的句柄，需要在 CreateFile 调用中指定 `CONIN$` 值。在 CreateFile 中指定 `CONOUT$` 值来打开控制台的活跃屏幕句柄。CreateFile 允许指定对它返回句柄进行 读/写 访问。

[**CreateConsoleScreenBuffer**](https://docs.microsoft.com/en-us/windows/console/createconsolescreenbuffer) 函数创建一个新的屏幕缓冲区并返回一个句柄。这个句柄可用于任何接收控制台输出句柄的函数。新的屏幕缓冲区不是活跃的，除非它在 [**SetConsoleActiveScreenBuffer**](https://docs.microsoft.com/en-us/windows/console/setconsoleactivescreenbuffer) 的调用中被指定。注意到改变屏幕活跃缓冲区不会影响由 GetStdHandle 返回的句柄。相似地，使用 [**SetStdHandle**](https://docs.microsoft.com/en-us/windows/console/setstdhandle) 对 STDOUT 句柄的改变不会影响活跃屏幕缓冲区。

由 [**CreateFile**](https://msdn.microsoft.com/library/windows/desktop/aa363858) 和 [**CreateConsoleScreenBuffer**](https://docs.microsoft.com/en-us/windows/console/createconsolescreenbuffer) 返回的控制台句柄可以用在任何需要控制台输入缓冲区句柄或控制台屏幕缓冲区句柄的函数中。如果标准句柄没有被重定向而指向不是控制台 I/O 的东西的话，由 [**GetStdHandle**](https://docs.microsoft.com/en-us/windows/console/getstdhandle) 返回的句柄可被控制台函数使用。然而，如果标准句柄被重定向而指向文件或管道，该句柄智能用在 [**ReadFile**](https://msdn.microsoft.com/library/windows/desktop/aa365467) 和 [**WriteFile**](https://msdn.microsoft.com/library/windows/desktop/aa365747) 中。

进程可以使用 [**DuplicateHandle**](https://msdn.microsoft.com/library/windows/desktop/ms724251) 函数创建一个复制的控制台句柄，与原句柄在访问级别或继承性存在不同。然而，注意，进程创建的复制控制台句柄只能供自己使用。这一点与其他种类的句柄不同（比如文件，管道，或互斥对象），使用 DuplicateHandle 产生的其他种类句柄的复制可以用于不同的进程。

要关闭控制台句柄，进程可以使用 [**CloseHandle**](https://msdn.microsoft.com/library/windows/desktop/ms724211) 函数。

## 控制台输入缓冲区

每个控制台都有一个包含一个输入事件记录队列的输入缓冲区。当控制台的窗口拥有键盘焦点时，控制台会将每个输入事件（比如单个击键，鼠标移动或鼠标单击）格式化为控制台输入缓冲区中的输入记录。

应用可以通过使用高级控制台 I/O 函数（[high-level console I/O functions](https://docs.microsoft.com/en-us/windows/console/high-level-console-input-and-output-functions)）来对控制台输入缓冲区进行间接访问，或使用低级控制台 I/O 函数（[low-level console input functions](https://docs.microsoft.com/en-us/windows/console/low-level-console-input-functions)）进行直接访问。高级函数会对输入缓冲区中的数据进行处理，只返回输入字节流。低级函数允许应用直接读取输入记录，或将输入记录放入缓冲区。要打开一个控制台输入缓冲区句柄，需在 [**CreateFile**](https://msdn.microsoft.com/library/windows/desktop/aa363858) 调用中指定 `CONIN$` 值。

输入记录（input record）是一个包含事件类型（键盘，鼠标，窗口大小改变，焦点，或菜单事件）和事件细节的结构。[**INPUT_RECORD**](https://docs.microsoft.com/en-us/windows/console/input-record-str) 中的 EventType 成员指示了记录中包含的事件类型。

控制台输入缓冲区中的焦点和菜单事件归系统内部使用，它们应该被应用忽略。

### 键盘事件

键盘事件在任意按键被按下或释放时产生；这包括了控制键。然而，`ALT` 键在没有和其他字符组合时的按下和释放对系统有特殊意义，它不会被传递给应用。同样的，如果输入句柄为已处理模式（processed mode），`CTRL`+`C` 键组合也不会被传递。

如果输入事件是一个击键，[**INPUT_RECORD**](https://docs.microsoft.com/en-us/windows/console/input-record-str) 结构的 Event 成员会是一个包含以下信息的 [**KEY_EVENT_RECORD**](https://docs.microsoft.com/en-us/windows/console/key-event-record-str) 结构：

- 一个指示键是按下或释放的布尔值

- 一个重复计数，当按键保持按下状态时，该值会大于 1

- 虚拟键码，以独立于设备的方式表示给定的按键

- 翻译后的 Unicode 或 ANSI 字符

- 一个标记值，指示控制键（`ALT` ，`CTRL` ，`SHIFT`，`NUM LOCK` ，`SCROLL LOCK` 和 `CAPS LOCK` ）的状态，并指示是否按下了增强键（enhanced key）。对 IBM® 101-key 和 102-key 键盘，增强键是指 `INS` ，`DEL`，`HOME`，`END` ，`PAGE UP` ，`PAGE DOWN` ，和方向键，以及数字键盘左侧的除法 `/` 和 `ENTER` 键

### 鼠标事件

在用户移动鼠标或按下和释放鼠标的一个按键时，鼠标事件会被生成。鼠标事件仅当以下条件满足时，才被放入输入缓冲区：

- 控制台输入模式设为 ENABLE\_MOUSE\_INPUT （默认模式）

- 控制台窗口具有键盘焦点

- 鼠标指针位于控制台窗口内

如果输入事件是一个鼠标事件，那么 [**INPUT_RECORD**](https://docs.microsoft.com/en-us/windows/console/input-record-str) 的 Event 成员是一个包含以下信息的 [**MOUSE_EVENT_RECORD**](https://docs.microsoft.com/en-us/windows/console/mouse-event-record-str) 结构：

- 鼠标指针的坐标，坐标以字符单元的高度和宽度为单位，在控制台屏幕缓冲区的坐标系统中

- 指示鼠标状态的标志值

- 指示控制键（`ALT` ，`CTRL` ，`SHIFT`，`NUM LOCK` ，`SCROLL LOCK` 和 `CAPS LOCK` ）状态的标志值，并指示是否按下了增强键（enhanced key）。对 IBM® 101-key 和 102-key 键盘，增强键是指 `INS` ，`DEL`，`HOME`，`END` ，`PAGE UP` ，`PAGE DOWN` ，和方向键，以及数字键盘左侧的除法 `/` 和 `ENTER` 键

- 指示事件是按下按键、释放事件、鼠标移动事件或双击事件的标志值

注意，鼠标位置坐标根据的是控制台屏幕缓冲区，而不是控制台窗口。屏幕缓冲区可能已经被滚动，所以窗口的原点（最左上）可能不一定是控制台屏幕缓冲区的 (0, 0) 坐标。想要直到鼠标相对于窗口的坐标值，可将鼠标的位置坐标减去窗口原点坐标。使用 [**GetConsoleScreenBufferInfo**](https://docs.microsoft.com/en-us/windows/console/getconsolescreenbufferinfo) 函数来得到窗口原点的坐标。

[**MOUSE_EVENT_RECORD**](https://docs.microsoft.com/en-us/windows/console/mouse-event-record-str) 结构的 dwButtonState 成员有一比特对应于每次的鼠标按钮。如果按键按下，这一比特为 1，否则为 0。按键释放事件可由 **MOUSE_EVENT_RECORD** 结构中的 dwEventFlags 为 0 和按钮的比特位从 1 变为 0 得知。函数 [**GetNumberOfConsoleMouseButtons**](https://docs.microsoft.com/en-us/windows/console/getnumberofconsolemousebuttons) 会检索鼠标的按键个数。

### 缓冲区大小改变事件

控制台窗口的菜单允许用户改变活跃屏幕缓冲区的大小；这个改变会生成缓冲区大小改变事件。如果控制台的输入模式被设置为 ENABLE_WINDOW_INPUT，该事件会被放进输入缓冲区。（也就是说，默认模式被仅用）

如果输入事件是缓冲区大小改变事件，[**INPUT_RECORD**](https://docs.microsoft.com/en-us/windows/console/input-record-str) 结构的 Event 成员会包含 [**WINDOW_BUFFER_SIZE_RECORD**](https://docs.microsoft.com/en-us/windows/console/window-buffer-size-record-str) 结构，其中包含着控制台屏幕缓冲区的新大小，以字符单元的行数和列数表示。

如果用户减少了控制台屏幕缓冲区的大小，位于减小区域内的数据会丢失。

由 [**SetConsoleScreenBufferSize**](https://docs.microsoft.com/en-us/windows/console/setconsolescreenbuffersize) 函数调用导致的控制台屏幕缓冲区大小改变不会生成该事件。

## 控制台屏幕缓冲区

屏幕缓冲区是一个在控制台窗口输出的字符和颜色的二维数组。控制台可以有多个屏幕缓冲区。*活跃屏幕缓冲区* 是显示在屏幕上的那一个。

系统在创建新的控制台时会为它创建屏幕缓冲区。要打开控制台的活跃屏幕缓冲区，需要在对 [**CreateFile**](https://msdn.microsoft.com/library/windows/desktop/aa363858) 的调用中指定 `CONOUT$` 值。进程可以使用 [**CreateConsoleScreenBuffer**](https://docs.microsoft.com/en-us/windows/console/createconsolescreenbuffer) 来为它的控制台创建另外的屏幕缓冲区。新的屏幕缓冲区不是活跃的，除非使用 [**SetConsoleActiveScreenBuffer**](https://docs.microsoft.com/en-us/windows/console/setconsoleactivescreenbuffer) 函数调用进行指定。然而，无论是否活跃，屏幕缓冲区都可以进行读写访问。

每个屏幕缓冲区都有它自己的字符信息记录的二位数组。每个字符的数据存储在[**CHAR_INFO**](https://docs.microsoft.com/en-us/windows/console/char-info-str) 结构中，该结构指定了字符是 Unicode 还是 ANSI，以及显示字符的前景（foreground）和背景颜色。

一些与屏幕缓冲区联系的性质可以为每个屏幕缓冲区单独设置。这意味着对活跃屏幕缓冲区的改变可以对控制台窗口的显示产生相当大的影响。与屏幕缓冲区关联的性质包括：

- 屏幕缓冲区大小，以字符行数和列数给出

- 文本属性（将由[**WriteFile**](https://msdn.microsoft.com/library/windows/desktop/aa365747) 或 [**WriteConsole**](https://docs.microsoft.com/en-us/windows/console/writeconsole) 函数写入的文本的前景和和背景颜色）

- 窗口大小和位置（在控制台窗口中显示的控制台屏幕缓冲区的矩形区域）

- 光标的位置、外观和可见性

- 输出模式（ENABLE\_PROCESSED\_OUTPUT 和 ENABLE\_WRAP\_AT\_EOL\_OUTPUT），更多信息可见于 [High-Level Console Modes](https://docs.microsoft.com/en-us/windows/console/high-level-console-modes) 

当屏幕缓冲区被创建时，它会包含空格。它的光标是可见的，并位于缓冲区原点 (0, 0)，窗口的左上角在缓冲区的原点。控制台屏幕缓冲区的大小，窗口大小，文本属性和光标外观取决于用户和系统默认。若要检索当前与控制台缓冲区关联的属性值，可以使用 [**GetConsoleScreenBufferInfo**](https://docs.microsoft.com/en-us/windows/console/getconsolescreenbufferinfo)， [**GetConsoleCursorInfo**](https://docs.microsoft.com/en-us/windows/console/getconsolecursorinfo) 和 [**GetConsoleMode**](https://docs.microsoft.com/en-us/windows/console/getconsolemode) 函数。

对控制台屏幕缓冲区属性做出任何修改的应用，要么创建它们自己的屏幕缓冲区，要么保存它一开始时继承的缓冲区状态，并在退出时进行恢复。

### 光标外观和位置

屏幕缓冲区的光标可以是可见的或隐藏的。当它可见时，它的外观可以在完全填满一个字符格的矩形到在字符格底的水平线之间变动。若要检索光标的可见性和外观信息，可以使用 [**GetConsoleCursorInfo**](https://docs.microsoft.com/en-us/windows/console/getconsolecursorinfo) 函数。该函数会报告光标的可见性，以光标填充字符格的百分比描述光标外观。要设置光标的外观和可见性，可以使用 [**SetConsoleCursorInfo**](https://docs.microsoft.com/en-us/windows/console/setconsolecursorinfo) 函数。

使用高级控制台 I/O 函数写入的字符会在当前光标位置进行写入，并将光标向后移动一格。若想要得到光标在屏幕缓冲区坐标系统中的当前位置，可以使用 [**GetConsoleScreenBufferInfo**](https://docs.microsoft.com/en-us/windows/console/getconsolescreenbufferinfo) 。你可以使用 [**SetConsoleCursorPosition**](https://docs.microsoft.com/en-us/windows/console/setconsolecursorposition) 来设置光标位置，来控制高级函数的文本写入和放置位置。如果你移动了光标，新光标位置的文本会被覆盖。

位置，外观和光标的可见性是为每个屏幕缓冲区独立设置的。

### 字符属性

字符属性可以分为两类：颜色和 DBCS。下面的属性在 Wincon.h 头文件中定义：

- FOREGROUND\_BLUE：文本颜色包含蓝色

- FOREGROUND\_GREEN：文本颜色包含绿色

- FOREGROUND\_RED：文本颜色包含红色

- FOREGROUND\_INTENSITY：文本颜色被增强

- BACKGROUND_BLUE：背景颜色包含蓝色

- BACKGROUND_GREEN：背景颜色包含绿色

- BACKGROUND_RED：背景颜色包含红色

- BACKGROUND_INTENSITY：背景颜色被增强

- COMMON_LVB_LEADING_BYTE：Leading byte.

- COMMON_LVB_TRAILING_BYTE：Trailing byte.

- COMMON_LVB_GRID_HORIZONTAL：Top horizontal.

- COMMON_LVB_GRID_LVERTICAL：Left vertical.

- COMMON_LVB_GRID_RVERTICAL：Right vertical.

- COMMON_LVB_REVERSE_VIDEO：Reverse foreground and background attributes.

- COMMON_LVB_UNDERSCORE：Underscore.

前景属性指文本颜色。背景属性指填充背景的颜色。其他的属性与 [DBCS](https://msdn.microsoft.com/library/windows/desktop/dd317794) 使用。

应用可以将前景和背景常数组合在一起来实现不同的颜色。例如，下面的组合会得到蓝色背景上的亮青色文本：

`FOREGROUND_BLUE | FOREGROUND_GREEN | FOREGROUND_INTENSITY | BACKGROUND_BLUE` 

如果没有指定背景常数，背景就是黑色的，如果没有指定前景常数，文本就是黑色的。例如，下面的组合会产生白色背景上的黑色文本：

`BACKGROUND_BLUE | BACKGROUND_GREEN | BACKGROUND_RED`

每个屏幕缓冲区的字符格会存储用于绘制该格的前景（文本）和背景的颜色属性。应用可以为每一个格子设置它自己的颜色数据，将数据存储在每个格子中的 [**CHAR_INFO**](https://docs.microsoft.com/en-us/windows/console/char-info-str) 结构的 Attributes 成员。每个屏幕缓冲区的当前文本属性被用于随后高级函数的字符写入和回显。

应用可以使用 [**GetConsoleScreenBufferInfo**](https://docs.microsoft.com/en-us/windows/console/getconsolescreenbufferinfo) 来确定屏幕缓冲区的当前文本属性，使用 [**SetConsoleTextAttribute**](https://docs.microsoft.com/en-us/windows/console/setconsoletextattribute) 来设置文本属性。对文本缓冲区属性的改变不会影响到之前写入的字符显示。这些文本属性不会影响由低级控制台 I/O 函数写入的字符（比如 [**WriteConsoleOutput**](https://docs.microsoft.com/en-us/windows/console/writeconsoleoutput) 或 [**WriteConsoleOutputCharacter**](https://docs.microsoft.com/en-us/windows/console/writeconsoleoutputcharacter) 函数），它们要么显式指定被写入每个格子的属性或对属性不做改变。

### 字体属性

函数 [**GetCurrentConsoleFont**](https://docs.microsoft.com/en-us/windows/console/getcurrentconsolefont) 会检索当前控制台字体。存储在 [**CONSOLE_FONT_INFO**](https://docs.microsoft.com/en-us/windows/console/console-font-info-str) 结构中的信息包括字体的宽度和高度信息。

[**GetConsoleFontSize**](https://docs.microsoft.com/en-us/windows/console/getconsolefontsize) 函数会检索由控制台屏幕缓冲区指定的字体的尺寸。

## 窗口和屏幕缓冲区尺寸

屏幕缓冲区尺寸是以基于字符格的坐标网格表示的。它的宽度是每一行字符格的数量，它的高度是字符格的行数。与每个屏幕缓冲区关联的窗口，是一个决定控制台缓冲区在控制台窗口中显示位置和尺寸的矩形区域的窗口。屏幕缓冲区窗口由指定字符格坐标的左上角和右下角的窗口矩形来定义。

屏幕缓冲区的尺寸是任意的，仅由可用内存限制。屏幕缓冲区的窗口的尺寸不能超过对应的控制台缓冲区尺寸或根据当前字体大小（完全由用户控制）可以适配的最大屏幕。

函数 [**GetConsoleScreenBufferInfo**](https://docs.microsoft.com/en-us/windows/console/getconsolescreenbufferinfo) 返回以下关于屏幕缓冲区和它的窗口的信息：

- 控制台屏幕缓冲区的当前尺寸

- 窗口的当前位置

- 在当前屏幕缓冲区给定下的最大窗口尺寸，当前字体尺寸，屏幕尺寸

函数 [**GetLargestConsoleWindowSize**](https://docs.microsoft.com/en-us/windows/console/getlargestconsolewindowsize) 返回依据当前字体和屏幕尺寸所得到的控制台窗口的最大尺寸。这个尺寸与 [**GetConsoleScreenBufferInfo**](https://docs.microsoft.com/en-us/windows/console/getconsolescreenbufferinfo) 所返回的最大窗口尺寸不同，因为[**GetConsoleScreenBufferInfo**](https://docs.microsoft.com/en-us/windows/console/getconsolescreenbufferinfo) 中屏幕缓冲区尺寸被忽略了。

要改变屏幕缓冲区的尺寸，使用 [**SetConsoleScreenBufferSize**](https://docs.microsoft.com/en-us/windows/console/setconsolescreenbuffersize) 函数。如果指定的尺寸比对应的控制台窗口要小，这个函数调用会失败。

若要改变屏幕缓冲区窗口的尺寸和位置，可使用 [**SetConsoleWindowInfo**](https://docs.microsoft.com/en-us/windows/console/setconsolewindowinfo) 函数。如果指定的窗口角坐标超过控制台屏幕缓冲区或屏幕的限制，函数会失败。对活跃屏幕缓冲区窗口尺寸的改变会改变在屏幕上显示的控制台窗口的尺寸。

进程可以改变控制台输入模式来允许窗口输入，这样一来进程在用户改变控制台屏幕缓冲区尺寸时接收输入。如果应用允许窗口输入，它可以使用 [**GetConsoleScreenBufferInfo**](https://docs.microsoft.com/en-us/windows/console/getconsolescreenbufferinfo) 在开始时检索窗口和屏幕缓冲区的尺寸。得到的信息可被用于决定数据在窗口显示的方式。如果用户改变了控制台屏幕缓冲区尺寸，应用可以通过改变数据显示的方式来做出响应。例如，如果每行的字符数发生变化，应用程序可以调整文本换行的方式。如果应用没有允许窗口输入，它必须要么使用继承的窗口和屏幕缓冲区尺寸，要么在开始时将它们设置为想要的尺寸，并在退出时恢复到继承时的样子。有关更多的窗口输入模式的信息，可见于 [Low-Level Console Modes](https://docs.microsoft.com/en-us/windows/console/low-level-console-modes) 。

## 控制台的选取

辅助功能（accessibility）应用需要用户对控制台的选择信息。要检索当前选择的控制台，调用 [**GetConsoleSelectionInfo**](https://docs.microsoft.com/en-us/windows/console/getconsoleselectioninfo) 函数，[**CONSOLE_SELECTION_INFO**](https://docs.microsoft.com/en-us/windows/console/console-selection-info-str) 结构中包含选择信息，例如锚点，坐标和状态。



# Windows 中的控制台应用

## 什么是控制台应用

控制台应用，也叫字符模式（character mode）应用，是指通过“控制台”（或者叫“终端”）与用户端进行沟通的应用程序。控制台从键盘、鼠标、触摸板、笔等设备转换用户输入，并将其发送到控制台应用的标准输入流（stdin）。控制台也可以将控制台应用的输出显示在用户的屏幕上。

在 Windows 中，控制台是系统内置的，系统提供了一系列的 API 以供控制台应用与用户进行交互。

控制台应用的工作：

- 【可选】从标准输入流读入数据

- 进行”工作“

- 【可选】向标准输出流或标准错误流写入数据

## 控制台应用的 I/O

有两种方式来进行控制台的 I/O，方法的选择取决于应用所需要的灵活性和控制程度。高级方法即使用字符流 I/O，这种方法限制了对控制台输入缓冲和屏幕缓冲的访问。低级方法需要开发者编写更多的代码，并在更大的范围内选取函数，但这种方法使得应用更加灵活。

应用可以使用文件 I/O 函数 [**ReadFile**](https://msdn.microsoft.com/library/windows/desktop/aa365467) 和 [**WriteFile**](https://msdn.microsoft.com/library/windows/desktop/aa365747)，控制台函数 [**ReadConsole**](https://docs.microsoft.com/en-us/windows/console/readconsole) 和 [**WriteConsole**](https://docs.microsoft.com/en-us/windows/console/writeconsole)，来进行高层 I/O。高级输入函数会对控制台缓冲区中的输入进行过滤和处理，将输入作为字符流返回，丢弃鼠标信息和缓冲区大小调整信息。类似地，高级输出函数将一个字符流写入屏幕缓冲区中光标当前位置。通过设置控制台 I/O 模式可以控制这些函数的行为。

低级 I/O 函数提供了之间访问控制台输入缓冲和屏幕缓冲的函数，让应用能够访问鼠标和缓冲区大小调整信息，以及键盘事件的扩展信息。低级 I/O 函数让应用能够从屏幕缓冲区读入或写入指定数量的连续字符块，或是在屏幕缓冲区的特定区间内读入或写入矩形字符块。控制台的输入模式通过指定是否处理鼠标和缓冲区大小调整消息来影响低级 I/O。控制台的输出模式对低级输出没有影响。

高级和低级 I/O 方法不是互斥的，应用可以同时对其进行使用。不过一般而言，应用只会使用一种方法。

## 控制台的代码页

**代码页**是一个由 256 个字符值到字符的映射。不同的代码也包含不同的特殊字符，特殊字符通常是一种或一组语言自定义的。

与控制台联系的有两个代码页：分别用于输入和输出。控制台使用输入代码页将从键盘输入的字符翻译为相应的字符值，它使用输出代码页将由输出函数写入的字符值翻译为在控制台窗口中显示的字符图像。应用程序可使用 [**SetConsoleCP**](https://docs.microsoft.com/en-us/windows/console/setconsolecp) 和 [**GetConsoleCP**](https://docs.microsoft.com/en-us/windows/console/getconsolecp) 函数来设置和检索控制台的输入代码页，使用[**SetConsoleOutputCP**](https://docs.microsoft.com/en-us/windows/console/setconsoleoutputcp) and [**GetConsoleOutputCP**](https://docs.microsoft.com/en-us/windows/console/getconsoleoutputcp) 来设置和检索输出代码页。

## 控制台的控制处理程序

每个控制台进程都有拥有自己的控制处理函数表，它们在进程接收到 [CTRL+C](https://docs.microsoft.com/en-us/windows/console/ctrl-c-and-ctrl-break-signals), [CTRL+BREAK](https://docs.microsoft.com/en-us/windows/console/ctrl-c-and-ctrl-break-signals)，或 [CTRL+CLOSE](https://docs.microsoft.com/en-us/windows/console/ctrl-close-signal) 信号时会被系统调用。初始条件下，每个进程的控制处理表只包含一个默认处理函数，那就是 [**ExitProcess**](https://msdn.microsoft.com/library/windows/desktop/ms682658) 。通过调用[**SetConsoleCtrlHandler**](https://docs.microsoft.com/en-us/windows/console/setconsolectrlhandler) 函数，控制台进程可以添加或去除额外的处理函数（[**HandlerRoutine**](https://docs.microsoft.com/en-us/windows/console/handlerroutine)），该函数不会影响其他进程的控制处理表。当控制台进程接收到任何控制信号时，它会根据后注册先调用（last-registered，first-called）的规则对处理函数进行调用，直到一个处理函数返回 TRUE 为止。如果没有处理函数返回 TRUE，默认处理函数会被调用。

## 控制台缓冲区安全属性和访问权

Windows 安全模式允许你控制对控制台输入缓冲区和输出缓冲区的访问。更多安全属性的信息可见于 [Access-Control Model](https://msdn.microsoft.com/library/windows/desktop/aa374876)。

当你调用[**CreateFile**](https://msdn.microsoft.com/library/windows/desktop/aa363858) 或 [**CreateConsoleScreenBuffer**](https://docs.microsoft.com/en-us/windows/console/createconsolescreenbuffer) 函数时，你可以为你的控制台输入输出缓冲区指定一个安全描述符（[security descriptor](https://msdn.microsoft.com/library/windows/desktop/aa379563)）。如果你使用 NULL，对象会得到默认安全描述符。

由 [**CreateFile**](https://msdn.microsoft.com/library/windows/desktop/aa363858)，[**CreateConsoleScreenBuffer**](https://docs.microsoft.com/en-us/windows/console/createconsolescreenbuffer) 和 [**GetStdHandle**](https://docs.microsoft.com/en-us/windows/console/getstdhandle) 返回的句柄有 GENERIC\_READ 和 GENERIC\_WRITE 的访问权力。

# 参考资料

【1】Console：https://en.wikipedia.org/wiki/Console

【2】Computer terminal：https://en.wikipedia.org/wiki/Computer_terminal

【3】What is the difference between Terminal, Console, Shell, and Command Line?：https://askubuntu.com/questions/506510/what-is-the-difference-between-terminal-console-shell-and-command-line

【4】Terminal 和 Console 的区别是什么？：https://www.zhihu.com/question/20388511/answer/985945219

【5】 What is a terminal emulator：https://appuals.com/what-is-a-terminal-emulator/

【6】Microsoft windows docs, console：https://docs.microsoft.com/en-us/windows/console/
