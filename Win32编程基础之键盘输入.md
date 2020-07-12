应用应该能够接收来自用户的键盘输入。键盘输入以投递的方式让应用进行接收。

# 键盘的输入模式

通过为当前键盘安装合适的键盘设备驱动，系统提供了设备独立的键盘支持。通过使用语言特定的键盘布局，系统提供了语言独立的键盘布局（keyboard layout）支持，这个可以由用户或应用设置。键盘设备驱动从键盘接收扫描码，它被发送到键盘布局，在那里它被翻译为消息并投递到应用合适的窗口中。

分配给键盘上每个键的是一个个唯一的扫描码（scan code），它是键盘按键的设备独立标识符。键盘在用户按下一个键时生成两个扫描码 —— 用户按下和释放按键。

键盘设备驱动解释扫描码并将它翻译（映射）为一个虚拟键码（virtual-key code），这是系统定义的设备独立值，它标明了键盘的按键。在翻译扫描码后，键盘布局会创建一个包含扫描码、虚拟键码和其他关于击键信息的消息，随后将消息放入系统队列中。系统将它从系统队列中移除并投递到合适线程的消息队列。最终，线程的消息循环移除该消息并将他传递到合适的窗口过程进行处理。

# 键盘焦点与活跃窗口

系统将键盘消息投递到创建了窗口且窗口带有键盘焦点的线程的消息队列中。*键盘焦点* 是窗口的一个暂时属性。系统通过移动键盘焦点来让所有显示的窗口共享键盘，它根据用户的指令，从一个窗口移动到另一个。拥有键盘焦点的窗口接收所有的键盘消息（从创建它的线程的消息队列中）直到焦点移动到了另一个窗口。

线程可以调用 [**GetFocus**](https://docs.microsoft.com/en-us/windows/win32/api/winuser/nf-winuser-getfocus) 函数来得知它的哪一个窗口（如果有的话）现在拥有键盘焦点。线程可以通过调用 [**SetFocus**](https://docs.microsoft.com/en-us/windows/win32/api/winuser/nf-winuser-setfocus) 函数来将键盘焦点交给它的一个窗口。当键盘焦点从一个窗口变化到另一个时，系统会向丢失焦点的窗口发送 [**WM_KILLFOCUS**](https://docs.microsoft.com/en-us/windows/win32/inputdev/wm-killfocus) 消息，并向获得焦点的窗口发送 [**WM_SETFOCUS**](https://docs.microsoft.com/en-us/windows/win32/inputdev/wm-setfocus) 消息。

键盘焦点的概念与活跃窗口是相关的。*活跃窗口* 是用户正在工作的顶级窗口。拥有键盘焦点的窗口要么是活跃窗口，要么是活跃窗口的子窗口。为了帮助用户识别活跃窗口，系统将活跃窗口放在 Z order 的最前面并将它的标题栏和边框高亮。

用户可以通过点击、使用 `ALT + TAB` 或 `ALT + ESC` 组合键来激活一个顶级窗口。线程可以通过使用 [**SetActiveWindow**](https://docs.microsoft.com/en-us/windows/win32/api/winuser/nf-winuser-setactivewindow) 函数来激活一个顶级窗口。它也可以通过 [**GetActiveWindow**](https://docs.microsoft.com/en-us/windows/win32/api/winuser/nf-winuser-getactivewindow) 函数来判断他创建的哪个顶级窗口处于激活状态。

当一个窗口被停用而另一个窗口被激活时，系统会发送 [**WM_ACTIVATE**](https://docs.microsoft.com/en-us/windows/win32/inputdev/wm-activate) 消息。*wParam* 的低位字如果是 0 则说明窗口被停用，是非零则说明窗口被激活。当默认窗口过程接收到 **WM\_ACTIVATE** 消息时，它会将键盘焦点设置到活跃窗口上。

要想将键盘和鼠标输入事件从它们将要到达的窗口屏蔽掉，可以使用 [**BlockInput**](https://docs.microsoft.com/en-us/windows/win32/api/winuser/nf-winuser-blockinput) 函数。注意，**BlockInput** 函数不会一影响异步键盘输入状态表（input-state table）。这就意味着调用 [**SendInput**](https://docs.microsoft.com/en-us/windows/win32/api/winuser/nf-winuser-sendinput) 函数会改变异步键盘输入状态表。

# 击键消息

按下一个键会导致 [**WM_KEYDOWN**](https://docs.microsoft.com/en-us/windows/win32/inputdev/wm-keydown) 或 [**WM_SYSKEYDOWN**](https://docs.microsoft.com/en-us/windows/win32/inputdev/wm-syskeydown) 消息被放在拥有键盘焦点的窗口所在线程的消息队列中。释放是个键会导致 [**WM_KEYUP**](https://docs.microsoft.com/en-us/windows/win32/inputdev/wm-keyup) 或 [**WM_SYSKEYUP**](https://docs.microsoft.com/en-us/windows/win32/inputdev/wm-syskeyup) 消息放在队列中。

按下键和放开键一般是成对出现的，但是如果用户长时间按住一个键，来使用键盘的自动重复特性，系统会连续生成大量的 [**WM_KEYDOWN**](https://docs.microsoft.com/en-us/windows/win32/inputdev/wm-keydown) 或 [**WM_SYSKEYDOWN**](https://docs.microsoft.com/en-us/windows/win32/inputdev/wm-syskeydown) 消息。它会在用户释放键时生成一个  [**WM_KEYUP**](https://docs.microsoft.com/en-us/windows/win32/inputdev/wm-keyup) 或 [**WM_SYSKEYUP**](https://docs.microsoft.com/en-us/windows/win32/inputdev/wm-syskeyup) 消息。

## 系统和非系统击键

系统区分系统和非系统击键。系统击键会产生系统击键消息，[**WM_SYSKEYDOWN**](https://docs.microsoft.com/en-us/windows/win32/inputdev/wm-syskeydown) 和 [**WM_SYSKEYUP**](https://docs.microsoft.com/en-us/windows/win32/inputdev/wm-syskeyup)。非系统击键会产生非系统击键消息， [**WM_KEYDOWN**](https://docs.microsoft.com/en-us/windows/win32/inputdev/wm-keydown) 和 [**WM_KEYUP**](https://docs.microsoft.com/en-us/windows/win32/inputdev/wm-keyup)。

如果你的窗口过程必须处理一个系统击键消息，确保在处理消息后将它传递给 **DefWindowProc** 函数。否则，所有包括 ALT 键的系统操作会在这个窗口拥有键盘焦点时失效。也就是说，用户不能够使用窗口的菜单或系统菜单，或使用 `ALT + ESC` 或 `ALT + TAB` 之类的组合键来激活其他窗口。

系统击键消息一般给系统而不是应用使用。系统使用它们来提供系统的内建的菜单键盘接口，并允许用户控制窗口的活跃。系统击键消息会在用户按下带有 `ALT` 的组合键时生成，或是在没有窗口拥有键盘焦点时用户进行击键（例如，在活跃窗口被最小化时）。这种情况下，消息会被投递到活跃窗口的消息队列中。

非系统击键消息是给应用窗口使用的；**DefWindowProc** 函数不会对它们做出任何响应。窗口过程可以丢弃它不需要的任何非系统击键消息。

## 虚拟键码

击键消息的 *wParam* 参数包含着一个被按压或释放的按键的虚拟键码。窗口过程可以根据虚拟键码的值来处理或忽略击键消息。

一般窗口过程只处理少部分的击键消息，它会忽略掉其他剩余的。例如，窗口过程可能只处理 [**WM_KEYDOWN**](https://docs.microsoft.com/en-us/windows/win32/inputdev/wm-keydown) 击键消息，并且只处理那些光标移动键，shift 键和功能键。一般的窗口过程不会处理来自字符键的击键消息。取而代之的是，它使用 [**TranslateMessage**](https://docs.microsoft.com/en-us/windows/desktop/api/winuser/nf-winuser-translatemessage) 函数将击键消息转化为字符消息。

## 击键消息标志

击键消息的 *lParam* 参数包含生成消息的击键的额外信息。这个信息包括重复计数（repeat count），扫描码（scan code），拓展键标志（extended-key flag），文本码（context code），之前的键状态标志（previous key-state flag），和过渡状态标志（transition-state flag）。下面的插图展示了这些标志的在 *lParam* 中的位置。

<img title="" src="https://docs.microsoft.com/en-us/windows/win32/inputdev/images/csinp-02.png" alt="avater" width="408" data-align="inline">

应用可以使用下面的值来操纵击键标志

- **KF_ALTDOWN**，操纵 ALT 键标志，它指明 ALT 键是否按下

- **KF_DLGMODE**，操纵对话框模式标志，它指明对话框是否是活跃的

- **KF_EXTENDED**，操纵拓展键标志

- **KF_MENUMODE**，操纵菜单模式标志，它指明菜单是否是活跃的

- **KF_REPEAT**，操纵重复计数

- **KF_UP**，操纵过渡状态标志

### 重复计数

你可以检查重复计数来判断击键消息是否表示多于一个击键。系统在键盘生成 [**WM_KEYDOWN**](https://docs.microsoft.com/en-us/windows/win32/inputdev/wm-keydown) 或 [**WM_SYSKEYDOWN**](https://docs.microsoft.com/en-us/windows/win32/inputdev/wm-syskeydown) 消息快于应用处理速度时会增加这个计数。这通常发生在用户按住一个键足够长的事件开启键盘自动重复特性时。系统不会将生成的按键消息填满系统消息队列，而是将消息组合成一个按键消息并增加重复计数。对按键释放不会启动自动重复特性，因此 [**WM_KEYUP**](https://docs.microsoft.com/en-us/windows/win32/inputdev/wm-keyup) 和 [**WM_SYSKEYUP**](https://docs.microsoft.com/en-us/windows/win32/inputdev/wm-syskeyup) 消息的重复计数值总是 1。

### 扫描码

扫描码是键盘硬件在用户按下键时生成的值。它是与设备相关的值，用于标识按下的键，而不是键所代表的字符。应用一般忽略扫描码，使用设备独立的虚拟键代码来解释击键消息。

### 拓展键标志

拓展键标志指明了击键消息是否来自增强键盘上额外的键。拓展键包括：键盘右手边的 ALT 和 CTRL 键；INS，DEL，HOME，END，PAGE UP，PAGE DOWN，数字小键盘中的箭头键；NUM LOCK；BREAK 键；PRINT SCAN 键；以及在数字小键盘上的除号键（/）和 ENTER 键。如果按键是一个拓展键的话，拓展键标志会被设置。

### 文本码

文本码指明在击键消息生成时是否按下了 ALT 键。如果按下了则文本码为 1，否则为 0。

### 先前键状态标志

先前键状态标志指明生成击键消息的按钮之前是按下还是放起的状态。如果它的值是 1 则说明之前是按下状态，是 0 则说明是放起状态。你可以使用这个标志来判断消息是否是由键盘自动重复特性生成的击键消息。对由自动重复特性生成的 [**WM_KEYDOWN**](https://docs.microsoft.com/en-us/windows/win32/inputdev/wm-keydown) 和 [**WM_SYSKEYDOWN**](https://docs.microsoft.com/en-us/windows/win32/inputdev/wm-syskeydown)，这个标志被设为 1。对于 [**WM_KEYUP**](https://docs.microsoft.com/en-us/windows/win32/inputdev/wm-keyup) 和 [**WM_SYSKEYUP**](https://docs.microsoft.com/en-us/windows/win32/inputdev/wm-syskeyup) 消息，它总是被设为 0。

### 过渡状态标志

过渡状态标志指明是按下或释放一个键生成了击键消息。对于 [**WM_KEYDOWN**](https://docs.microsoft.com/en-us/windows/win32/inputdev/wm-keydown) 和 [**WM_SYSKEYDOWN**](https://docs.microsoft.com/en-us/windows/win32/inputdev/wm-syskeydown) 消息它总是 0；对于 [**WM_KEYUP**](https://docs.microsoft.com/en-us/windows/win32/inputdev/wm-keyup) 和 [**WM_SYSKEYUP**](https://docs.microsoft.com/en-us/windows/win32/inputdev/wm-syskeyup) 消息，它总是 1。

# 字符消息

击键消息提供了许多关于击键的消息，但是它们没有提供字符击键的字符代码。要想得到字符码，应用必须使用 **TranslateMessage** 函数。**TranslateMessage** 将 [**WM_KEYDOWN**](https://docs.microsoft.com/en-us/windows/win32/inputdev/wm-keydown) 或 [**WM_SYSKEYDOWN**](https://docs.microsoft.com/en-us/windows/win32/inputdev/wm-syskeydown) 消息传递给键盘布局。键盘布局会测试消息的虚拟键代码，如果它对应与一个字符键的话，则提供等效的字符码（它会考虑按下 SHIFT 和 CAPS LOCK 按键的情况）。它随后生成一个包括字符码的字符消息，并放在消息队列的最前面。下一次的消息循环迭代会从队列移除字符消息并将消息分派到合适的窗口过程。

## 非系统字符消息

窗口过程可以接收这些字符消息：[**WM_CHAR**](https://docs.microsoft.com/en-us/windows/win32/inputdev/wm-char)，[**WM_DEADCHAR**](https://docs.microsoft.com/en-us/windows/win32/inputdev/wm-deadchar)，[**WM_SYSCHAR**](https://docs.microsoft.com/en-us/windows/desktop/menurc/wm-syschar), [**WM_SYSDEADCHAR**](https://docs.microsoft.com/en-us/windows/win32/inputdev/wm-sysdeadchar)，和 [**WM_UNICHAR**](https://docs.microsoft.com/en-us/windows/win32/inputdev/wm-unichar)。**TranslateMessage** 函数在处理 [**WM_KEYDOWN**](https://docs.microsoft.com/en-us/windows/win32/inputdev/wm-keydown) 消息时会生成 **WM_CHAR** 或 **WM_DEADCHAR** 消息。类似地，他会在处理 [**WM_SYSKEYDOWN**](https://docs.microsoft.com/en-us/windows/win32/inputdev/wm-syskeydown) 消息时生成 **WM_SYSCHAR** 或 **WM_SYSDEADCHAR** 消息。

处理键盘输入的应用一般会忽略除了 [**WM_CHAR**](https://docs.microsoft.com/en-us/windows/win32/inputdev/wm-char) 和 [**WM_UNICHAR**](https://docs.microsoft.com/en-us/windows/win32/inputdev/wm-unichar) 消息之外的其他键盘消息，将其他的消息传递给 **DefWindowProc** 函数。注意到 **WM\_CHAR** 使用的是 16 位 Unicode 传输格式（UTF）而 **WM\_UNICHAR** 使用的是 UTF-32。系统使用 [**WM_SYSCHAR**](https://docs.microsoft.com/en-us/windows/desktop/menurc/wm-syschar) 和 [**WM_SYSDEADCHAR**](https://docs.microsoft.com/en-us/windows/win32/inputdev/wm-sysdeadchar) 来实现菜单助记符（menu mnemonics）。

所有字符消息的 *wParam* 参数包含这按下的字符键的字符码。字符码的值取决于收到消息窗口的窗口类。如果使用了 Unicode 版本的 **RegisterClass** 函数来注册窗口类，系统会为该类的所有窗口提供 Unicode 字符。否则，系统会提供 ASCII 字符码。更多信息可见于 [Unicode and Character Sets](https://docs.microsoft.com/en-us/windows/desktop/Intl/unicode-and-character-sets)。

字符消息的 *lParam* 参数与击键消息的 *lParam* 是相同的。

## 死字符消息

一些非英语键盘包含一些不被期望产生字符的键，它们被用于为后续击键的字符添加变音符号。这些键被叫做 *死键*。德语键盘上的抑扬琴键（circumflex）是一个例子。要想输入一个由 "o" 和抑扬符组成的字符，德国用户会按一次抑扬键，并随后按一次 "o" 键。拥有键盘焦点的窗口会收到以下字符序列：

1. [**WM_KEYDOWN**](https://docs.microsoft.com/en-us/windows/win32/inputdev/wm-keydown)
2. [**WM_DEADCHAR**](https://docs.microsoft.com/en-us/windows/win32/inputdev/wm-deadchar)
3. [**WM_KEYUP**](https://docs.microsoft.com/en-us/windows/win32/inputdev/wm-keyup)
4. [**WM_KEYDOWN**](https://docs.microsoft.com/en-us/windows/win32/inputdev/wm-keydown)
5. [**WM_CHAR**](https://docs.microsoft.com/en-us/windows/win32/inputdev/wm-char)
6. [**WM_KEYUP**](https://docs.microsoft.com/en-us/windows/win32/inputdev/wm-keyup)

**TranslateMessage** 会在它处理来自死键的 [**WM_KEYDOWN**](https://docs.microsoft.com/en-us/windows/win32/inputdev/wm-keydown) 消息时生成 [**WM_DEADCHAR**](https://docs.microsoft.com/en-us/windows/win32/inputdev/wm-deadchar) 消息。
