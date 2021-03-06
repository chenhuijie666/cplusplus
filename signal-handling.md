# C++ 信号处理 #

信号是由操作系统传递到进程的中断，它可以提前终止一个程序。在 UNIX，LINUX，Mac OS X 或 Windows 系统上，你可以通过按 Ctrl+C 产生一个中断。

有的信号不能被程序捕获到，但是下面列出的信号，你可以在程序中捕捉它们，并且可以基于这些信号进行相应的操作。这些信号定义在 C++ 头文件 <csignal> 中。

<table>
<tr>
<th align="left">信号</th>
<th align="left">描述</th>
</tr>
   <tr>
      <td>SIGABRT</td>
      <td>程序的异常终止，例如调用 abort </td>
   </tr>
   <tr>
      <td>SIGFPE</td>
      <td>一个错误的算术运算，例如除以零或运算结果溢出。</td>
   <tr>
      <td>SIGILL</td>
      <td>检测到非法指令。</td>
   </tr>
   <tr>
      <td>SIGINT</td>
      <td>接收到交互注意信号。</td>
   </tr>
   <tr>
      <td>SIGSEGV</td>
      <td>一个非法的存储访问。</td>
   </tr>
   <tr>
      <td>SIGTERM</td>
      <td>发送给程序的终止请求信号。</td>
   </tr>
</table>


## signal() 函数： ##

C++ 信号处理库提供 **signal** 函数来捕获意外事件。以下是 signal() 函数的语法：

    void (*signal (int sig, void (*func)(int)))(int); 

简单来说，这个函数接收两个参数：第一个参数是一个整数，表示信号号码；第二个参数是一个指向信号处理函数的指针。

让我们用 signal() 函数写一个简单的 C++ 程序，用它来捕捉 SIGINT 信号。不管你想在程序中捕获什么信号，你必须使用 **signal** 函数注册该信号，并将其与信号处理程序相关联。
例子如下所示：

    #include <iostream>
    #include <csignal>
    
    using namespace std;
    
    void signalHandler( int signum )
    {
    cout << "Interrupt signal (" << signum << ") received.\n";
    
    // cleanup and close up stuff here  
    // terminate program  
    
       exit(signum);  
    
    }
    
    int main ()
    {
    // register signal SIGINT and signal handler  
    signal(SIGINT, signalHandler);  
    
    while(1){
       cout << "Going to sleep...." << endl;
       sleep(1);
    }
    
    return 0;
    }


当上述代码编译和执行后，将会产生以下的结果：

    Going to sleep....
    Going to sleep....
    Going to sleep....

现在，按 Ctrl+C 来中断这个程序，你会看到程序将捕获的信号，并会通过打印展示出来，如下所示：

    Going to sleep....
    Going to sleep....
    Going to sleep....
    Interrupt signal (2) received.

## raise() 函数 ##

您可以通过 **raise()** 函数生成信号，它用一个整数的信号编号作为参数，语法如下所示。

    int raise (signal sig);

这里的 **sig** 是要发送的信号编号，这些信号是：SIGINT，SIGABRT，SIGFPE，SIGILL，SIGSEGV，SIGTERM，SIGHUP。以下是我们使用 raise() 函数从程序内部发出一个信号的例子：

    #include <iostream>
    #include <csignal>
    
    using namespace std;
    
    void signalHandler( int signum )
    {
    cout << "Interrupt signal (" << signum << ") received.\n";
    
    // cleanup and close up stuff here  
    // terminate program  
    
       exit(signum);  
    
    }
    
    int main ()
    {
    int i = 0;
    // register signal SIGINT and signal handler  
    signal(SIGINT, signalHandler);  
    
    while(++i){
       cout << "Going to sleep...." << endl;
       if( i == 3 ){
      raise( SIGINT);
       }
       sleep(1);
    }
    
    return 0;
    }

当上述代码编译和执行后，将会产生以下的结果，并且这些结果会自动出现：

    Going to sleep....
    Going to sleep....
    Going to sleep....
    Interrupt signal (2) received.
