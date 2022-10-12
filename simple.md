# simple
本文档记录一些常用的代码片段

- const 重载
    ```cpp
    const A& func() const
    {
    }

    A& func()
    {
        return const_cast<A&>(std::as_const(*this).func());
    }
    ```
- 移动构造和移动赋值
    ```cpp
    A::A(A&& src) noexcept
    {
        std::swap(*this, src);
    }

    A& A::operator=(A&& rhs) noexcept
    {
        A tmp(std::move(rhs));
        std::swap(*this, tmp);

        return *this;
    }
    ```
- 使用接口类和实现类
    ```cpp
    class A
    {
    private:
        class Impl;
        std::unique_ptr<Impl> m_impl;
    };
    ```