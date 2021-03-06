##C++ 中的多态

多态性意味着有多种形式。通常，多态发生在类之间存在层级关系时并且这些类通过继承相联系的时候。

C++ 多态性意味着对一个成员函数的调用是根据调用函数的对象的类型的不同，不同的函数被执行。

考虑下面的例子，一个基类派生了其他的两类：

    #include <iostream> 
    using namespace std;
     
    class Shape {
       protected:
      int width, height;
       public:
      Shape( int a=0, int b=0)
      {
     width = a;
     height = b;
      }
      int area()
      {
     cout << "Parent class area :" <<endl;
     return 0;
      }
    };
    class Rectangle: public Shape{
       public:
      Rectangle( int a=0, int b=0):Shape(a, b) { }
      int area ()
      { 
     cout << "Rectangle class area :" <<endl;
     return (width * height); 
      }
    };
    class Triangle: public Shape{
       public:
      Triangle( int a=0, int b=0):Shape(a, b) { }
      int area ()
      { 
     cout << "Triangle class area :" <<endl;
     return (width * height / 2); 
      }
    };
    // Main function for the program
    int main( )
    {
       Shape *shape;
       Rectangle rec(10,7);
       Triangle  tri(10,5);
    
       // store the address of Rectangle
       shape = &rec;
       // call rectangle area.
       shape->area();
    
       // store the address of Triangle
       shape = &tri;
       // call triangle area.
       shape->area();
       
       return 0;
    }

上面的代码编译和执行时，它产生以下结果：

    Parent class area
    Parent class area

输出结果不正确的原因是对函数 area() 的调用被编译器设置了一次，即在基类中定义的版本，这被称为对函数调用的静态分辨或者静态链接，静态链接就是在程序被执行之前函数调用是确定的。这有时也被称为早期绑定，因为函数 area() 在编译程序期间是固定的。

但是现在，让我们对程序做略微修改，并在 Shape 类中 area() 的声明之前加关键字 **virtual** ，它看起来像这样：

    class Shape {
       protected:
      int width, height;
       public:
      Shape( int a=0, int b=0)
      {
     width = a;
     height = b;
      }
      virtual int area()
      {
     cout << "Parent class area :" <<endl;
     return 0;
      }
    };

这轻微的修改后，前面的示例代码编译和执行时，它会产生以下结果：

    Rectangle class area
    Triangle class area

这一次，编译器关注的是指针的内容而不是它的类型。因此,由于三角形和矩形类对象的地址被存储在形状类中，各自的 area() 函数可以被调用。

正如你所看到的，每个子类都有一个对 area() 函数的实现。通常多态就是这样使用的。你有不同的类，它们都有一个的相同名字的函数，甚至有相同的参数，但是对这个函数有不同的实现。

###虚函数

基类中的虚函数是一个使用关键字 **virtual** 声明的函数。派生类中已经对函数进行定义的情况下，定义一个基类的虚函数，就是要告诉编译器我们不想对这个函数进行静态链接。

我们所希望的是根据调用函数的对象的类型对程序中在任何给定指针中被调用的函数的选择。这种操作被称为动态链接，或者后期绑定。

###纯虚函数

可能你想把虚函数包括在基类中，以便它可以在派生类中根据该类的对象对函数进行重新定义，但在许多情况下，在基类中不能对虚函数给出有意义的实现。

我们可以改变基类中的虚函数 area() 如下：

    class Shape {
       protected:
      int width, height;
       public:
      Shape( int a=0, int b=0)
      {
     width = a;
     height = b;
      }
      // pure virtual function
      virtual int area() = 0;
    };

area() = 0 就是告诉编译器上面的函数没有函数体。上面的虚函数就被称为纯虚函数。