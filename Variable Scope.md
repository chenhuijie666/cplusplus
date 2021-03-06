# C++ 变量作用域   #


变量作用域就是指变量在程序中能够操作的区域，通常按照在程序中不同地方声明可以分为如下三类：   

1. 局部变量：在函数中或者由花括号括起来的代码块中声明。  
2. 形式变量：在函数的参数中声明，也叫形参。  
3. 全局变量：在所有函数之外声明的变量。  



关于函数及函数参数的内容我们会在后续章节中学习。这里我们首先学习关于局部变量和全部变量的相关内容。  

## 局部变量：   ##

在函数或代码块内部声明的变量称为局部变量。他们在函数体内声明后仅能被其声明的所在函数体内部的后续语句操作。局部变量不能被函数外部的访问到。下面的就是使用局部变量的例子。  

    #include <iostream>
    using namespace std;
     
    int main ()
    {
      // Local variable declaration:
      int a, b;
      int c;
     
      // actual initialization
      a = 10;
      b = 20;
      c = a + b;
     
      cout << c;
     
      return 0;
    }
    

## 全局变量： ##

全局变量通常会被声明定义在所有函数体的外面，大部分情况下是在程序的最上方定义。全部变量的生命周期就是进程从开始到程序执行结束的整个过程。  
  
全局变量可以被任何函数访问。也就是说，全局变量一旦被声明，将在程序的整个生命周期内都是有效的。下面是使用全局和局部变量的例子：

    #include <iostream>
    using namespace std;
     
    // Global variable declaration:
    int g;
     
    int main ()
    {
      // Local variable declaration:
      int a, b;
     
      // actual initialization
      a = 10;
      b = 20;
      g = a + b;
     
      cout << g;
     
      return 0;
    }

程序中的局部变量和全局变量可以有相同的变量名称。但是在局部变量所在函数体内如，使用变量名仅能访问到局部变量。比如：

    #include <iostream>
    using namespace std;
     
    // Global variable declaration:
    int g = 20;
     
    int main ()
    {
      // Local variable declaration:
      int g = 10;
     
      cout << g;
     
      return 0;
    }

上述例子中的程序被编译并执行后，将显示如下结果：  

    10



## 局部变量和全局变量的初始化 ##

局部变量被定义后，默认情况下，系统并不会对该变量进行初始化，所以需要程序员进行初始化操作。与之不同的是，全局变量定义后会被编译系统自动初始化，具体初始化的值如下：
<table>
<tbody>
<tr>
<th>数据类型</th>
<th>默认初始化的值</th>

</tr>
<tr>
<td>int</td> <td>0</td> 
</tr>

</tr>
<tr>
<td>char</td> <td>'\0'</td> 
</tr>

</tr>
<tr>
<td>float</td> <td>0</td> 
</tr>

</tr>
<tr>
<td>double</td> <td>0</td> 
</tr>

</tr>
<tr>
<td>pointer</td> <td>NULL</td> 
</tr>


</tbody>
</table>   

适如其分的给变量初始化是一个很好的编程习惯，否则，有时程序会出现很多意想不到的错误。