在正式开始介绍控制台应用之前，先看看什么是控制台和终端（物理意义上）。

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

但它们又是不同的。一台主机可以有多个终端，但在主机的系统完成启动之前，终端无法连接到主机上。为了能够记录主机开机日志，需要有控制台。一个主机只能有一个控制台。

## 作为软件的 console 和 terminal



# 什么是控制台应用

控制台应用，也叫字符模式（character mode）应用，是指通过“控制台”（或者叫“终端”）与用户端进行沟通的应用程序。控制台从键盘、鼠标、触摸板、笔等设备转换用户输入，并将其发送到控制台应用的标准输入流（stdin）。控制台也可以将控制台应用的输出显示在用户的屏幕上。



# 参考资料

Console：https://en.wikipedia.org/wiki/Console

Computer terminal：https://en.wikipedia.org/wiki/Computer_terminal

What is the difference between Terminal, Console, Shell, and Command Line?：https://askubuntu.com/questions/506510/what-is-the-difference-between-terminal-console-shell-and-command-line

Terminal 和 Console 的区别是什么？：https://www.zhihu.com/question/20388511/answer/985945219




