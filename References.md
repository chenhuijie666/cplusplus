## C++ 引用

引用变量是一个别名，即已经存在的变量的另一个名称。一旦用一个变量初始化引用，变量名称和引用名称都可以用来指示变量。

### C++ 引用 VS 指针

引用与指针非常容易混淆，但引用和指针有三个主要区别：    

- 空引用不可能存在。你必须始终能够假定一个引用被连接到一个合法的存储块。   
- 一旦一个引用被初始化为一个对象，它就不能改变去指示另一个对象。指针可以随时改变指向另一个不同的对象。  
- 引用必须在它被创建时就初始化。指针可以在任何时候初始化。

### 在 c++ 中创建引用:
考虑到一个变量名是一个附加到该变量在内存中的位置的标签。你可以认为一个引用是附加到该内存位置的第二个标签。因此,您可以通过原始变量名或引用来访问变量的内容。例如，我们假设有下面的例子：
     
	int i = 17;   

我们可以为 i 声明引用变量，如下所示。

	int& r = i;

在这些声明中将 & 理解为引用（**reference**）。因此，第一个声明理解为 “ r 是一个整数引用，初始化为 i ” 和第二声明理解为 “ s 是一个双引用，初始化为 d ”。下面的例子使用了 int 和 double 引用：

    #include <iostream>
   
    using namespace std;
     
    int main ()
    {
       // declare simple variables
       inti;
       double d;
     
       // declare reference variables
       int&r = i;
       double& s = d;
       
       i = 5;
       cout << "Value of i : " << i << endl;
       cout << "Value of i reference : " << r  << endl;
     
       d = 11.7;
       cout << "Value of d : " << d << endl;
       cout << "Value of d reference : " << s  << endl;
       
       return 0;
    }

将上面的代码放在一起编译、执行，执行结果如下 ：

    Value of i : 5
    Value of i reference : 5
    Value of d : 11.7
    Value of d reference : 11.7

引用通常用于函数参数列表和函数返回值。以下是与 c++ 引用有关的两个重要的方面，一个 c++ 程序员应该明确了解：

<table>
<tr>
<th>内容</th>
<th>描述</th>
</tr>
<tr>
<td><a href="http://www.tutorialspoint.com/cplusplus/passing_parameters_by_references.htm" title="在 c++ 中通过引用传递参数
">引用作为参数</a></td>
<td>c++ 支持引用作为函数参数传递，它比直接传递参数更安全。</td>
</tr>
<tr>
<td><a href="http://www.tutorialspoint.com/cplusplus/returning_values_by_reference.htm" title="在 c++ 中通过引用得到函数返回值">引用作为返回值</a></td>
<td>可以从一个 c++ 函数返回引用，就像返回任何其他数据类型。</td>
</tr>
</table>
