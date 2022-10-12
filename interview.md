# Interview
本文档记录一些面试题。

## 1. 基本概念
- 面向过程和面向对象
  - 面向过程：将程序功能分割成功能小块，然后通过一定的顺序组织这些功能小块完成任务（程序按照顺序做什么？）。
  - 面向对象：
    - 类
    - 组件
      - 类可以由许多组件组成。
    - 属性
    - 行为
      - 对象做什么？能对对象做什么？
- “有一个”关系和“是一个”关系
  - “有一个”关系：某个对象是另一个对象的一部分
  - “是一个关系”（继承）：派生类，子类
    - 里氏替换原则：派生类是一个基类。
- new、delete 和 malloc、free 的区别？
- 重载的方式有哪些？
  - 参数类型不同，参数个数不同
  - const 重载

## 2. 简短的问题
- 求数组大小
    ```cpp
    int* array;
    // uint32_t array_size = sizeof(array) / sizeof(array[0])
    // uint32_t array_size = std::size(array); // c++17, #include <array>
    ```
- std::array 和 std::vector 有什么区别？
  - std::array 用于具有固定大小的数组
  - std::vector 用于非固定大小的数组
- sizeof() 和 strlen() 的区别？
  - 操作符、函数
  - 返回 C 风格字符串数组的大小

## 3. 一起来找茬
- 下面代码有什么问题？
    ```cpp
    void func(char* str)
    {
        std::cout << str << std::endl;
    }
    void func(int i)
    {
        std::cout << i << std::endl;
    }
    func(NULL)
    ```
- 下面代码有什么问题？
    ```cpp
    char* ptr = "hello";
    ptr[1] = 'a';

    char arr[] = "hello";
    arr[1] = 'a';
    ```
- 下面代码有什么问题？
    ```cpp
    char* a  = "12";
    char b[] = "12";

    if (a == b)
    {
    }

    if (0 == strcmp(a, b))
    {
    }
    ```
- 下面代码有什么问题？
  - 如果在 a->go() 抛出异常？
    ```cpp
    void func()
    {
        Simple* a = new Simple();
        a->go();
        delete a;
        a = nullptr;
    }
    ```
- 下面代码有什么问题？
    ```cpp
    void func()
    {
        Simple* a = new Simple();
        std::shared_ptr<Simple> s1(a);
        std::shared_ptr<Simple> s2(a);
    }

    // no double delete
    void func2()
    {
        auto s1 = make_shared<Simple>();
        shared_ptr<Simple> s2(s1);
    }
    ```
- 下面代码有什么问题？
    ```cpp
    // 有问题的版本
    class Foo
    {
    public:
        shared_ptr<Foo> get_pointer()
        {
            return shared_ptr<Foo>(this);
        }   
    };

    // 没有问题的版本
    class Foo : public enable_shared_from_this<Foo>
    {
    public:
        shared_ptr<Foo> get_pointer()
        {
            return shared_from_this();
        }
    };

    int main()
    {
        auto p1 = make_shared<Foo>();
        auto p2 = p1->get_pointer();
    }
    ```

## 4. 解答题
- 下面两个 变量的类型是什么？
    ```cpp
    auto str1 = "hello";
    auto str2 = "hello"s;
    ```
## 5. 算法题
- 给定一个 int 数组，将其分成两个数组，一个是偶数数组，一个是奇数数组
    ```cpp
    int arry[] = {1, 2, 3, 4, 5, 6, 7, 8, 9, 10};
    int* odd_nums = nullptr;
    int& even_nums = nullptr;
    size_t num_odds = 0;
    size_t num_evens = 0;
    // 方法一: 传递两个指针，然后在内部计算出偶数和奇数的个数后 new 内存
    void separate_odds_and_evens(arry, std::size(arry), &odd_nums, &num_odds, &even_nums, &num_evens);

    // 方法二：传递指针引用
    void separate_odds_and_evens(const int arry[], size_t size, int*& odds, size_t num_odds, int*& evens, size_t num_evens);

    // 方法三：使用 vector
    void separate_odds_and_evens(const std::vector<int>& arry, std::vector<int>& odds, std::vector<int>& evens);

    // 方法四：使用 C++ 17 结构化绑定
    std::pair<std::vector<int>, std::vector<int>> separate_odds_and_evens(const std::vector<int>& arry);
    ```