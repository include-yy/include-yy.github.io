本文翻译自 *Writing a C library part 2*

作者：davidz

作者主页：https://www.blogger.com/profile/18166813552495508964

文章源地址：davidz25.blogspot.com/2011/07/writing-c-library-part-4.html前篇：[part one](davidz25.blogspot.com/2011/06/writing-c-library-part-1.html) [part two](http://davidz25.blogspot.com/2011/06/writing-c-library-part-2.html) [part three](http://davidz25.blogspot.com/2011/06/writing-c-library-part-3.html) 



# 辅助（Helper）和守护进程

有时，程序或库调用外部进程完成工作是非常有用的。这样做的原因有很多 —— 例如，你想要使用的代码：

- 可能在 C 语言中用起来不是很容易 —— 它可以用 [python](http://en.wikipedia.org/wiki/Python_(programming_language)，或 gosh，或 [bash](http://en.wikipedia.org/wiki/Bash_(Unix_shell) 写

- 可能和信号处理程序或其他全局进程状态搞混

- 不是线程安全的，或者会泄露或仅仅是膨胀（bloated）

- 错误处理你的库所使用的方式不兼容

- 需要提权

- 你感觉很糟糕，但是又不值得自己重新实现一遍

第一种方式是直接调用 [fork(2)](http://www.kernel.org/doc/man-pages/online/pages/man2/fork.2.html) 并在子进程中使用这个库 —— 这通常是行不通的，因为
