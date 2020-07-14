控件是子窗口，应用将它与其他的窗口结合使用来与用户进行交互。控件多数时候都用在对话框中，但它们也可以用在其他窗口中。对话框内的控件为用户提供了文本输入、选项选择和初始化等功能。其他窗口中的控制台可以提供一系列的服务，比如让用户选择命令、观察状态以及编辑和阅读文本。

# 一些窗口函数

既然控件是子窗口，那么有必要介绍一些对窗口进行操作的函数。除了 **CreateWindow** 函数用来创建窗口外，其他的一些窗口函数可以移动窗口、隐藏或显示窗口、禁用或启用窗口、更新窗口，等等。

## CreateWinodwEx

[**CreateWindowEx**](https://docs.microsoft.com/en-us/windows/win32/api/winuser/nf-winuser-createwindowexa) 函数创建一个带有拓展窗口风格的窗口。除了拓展风格这一点，它的功能与 **CreateWindow** 是一样的。

函数的原型如下：

```c
HWND CreateWindowExA(
  DWORD     dwExStyle,
  LPCSTR    lpClassName,
  LPCSTR    lpWindowName,
  DWORD     dwStyle,
  int       X,
  int       Y,
  int       nWidth,
  int       nHeight,
  HWND      hWndParent,
  HMENU     hMenu,
  HINSTANCE hInstance,
  LPVOID    lpParam
);
```

*dwExStyle* 参数是创建窗口的拓展窗口风格，可以参阅 [Extended Window Styles](https://docs.microsoft.com/en-us/windows/desktop/winmsg/extended-window-styles) 获取更多信息。

*lpClassName* 是注册窗口类的类名，或是一个由 **RegisterClass** 或 **RegisterClass** 返回的原子值。如果使用原子值，那么它必须在 *lpClassName* 的低位字，*lpClassName* 的高位字必须是 0。如果 *lpClassName* 是一个字符串，它应该指定一个窗口类名。窗口类名可以是预定义的 [system class](https://docs.microsoft.com/en-us/windows/desktop/winmsg/about-window-classes)。

*lpWindowName* 是窗口的名字。如果窗口风格中指定了一个标题栏，那么窗口标题会显示在标题栏上。使用 **CreateWindowEx** 创建像是按钮、组框和静态类的控件时，*lpWindowName* 是控件的文本。使用 **SS\_ICON** 创建静态控件时，可以使用 *lpWindowName* 来指定图标的名字或标识符。要指定标识符，可以使用 "#num" 的语法。

*dwStyle* 是所创建窗口的风格。这个参数可以是一系列  [window style values](https://docs.microsoft.com/en-us/windows/desktop/winmsg/window-styles) 值的组合，还可以加上控件的风格。

*X* 是窗口的初始水平位置。对于重叠窗口或弹出窗口（overlapped and pup-up），x 参数是窗口的左上角的 x 坐标，在屏幕坐标系中。对于子窗口， x 是相对于父窗口客户区左上角的坐标，是子窗口左上角的坐标。如果 x 被设为 **CW\_USEDEFAULT**，系统会选择默认位置来作为窗口左上角的坐标，并忽略 *Y* 参数。**CW\_USEDEFAULT** 只对重叠窗口有效；如果对弹出窗口使用这个值， x 和 y 参数会被设为 0。

*Y* 参数是窗口初始垂直位置。对于重叠或弹出窗口，这是窗口左上角的坐标，在屏幕坐标系中。对子窗口，这是子窗口的左上角的坐标，在父窗口的客户区坐标系中。如果重叠窗口使用了 **WS\_VISIBLE** 风格并对 x 参数使用了 **CW\_USEDEFAULT**，y 参数就决定了窗口的显示。如果 y 参数被设为 **CW\_USEDEFAULT**，之后窗口管理器会使用 **SW_SHOW** 标志在窗口创建后调用 [ShowWindow](https://docs.microsoft.com/en-us/windows/desktop/api/winuser/nf-winuser-showwindow) 函数。如果 y 参数是其他的值，窗口管理器会使用 *nCmdShow* 来调用 **ShowWindow**。

*nWidth* 参数是窗口的宽度，以设备单元为单位。对重叠窗口，*nWidth* 是窗口的宽度，以屏幕为坐标系。如果 *nWidth* 是 **CW\_USEDEFAULT**，系统会为窗口选择默认宽度和高度。


