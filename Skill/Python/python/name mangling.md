##### 介绍
在Python中，私有变量和方法（即以两个下划线`__`开头的变量和方法）的设计目的是为了防止它们被子类继承和访问，从而确保了类的封装性。这意味着，从技术上讲，私有变量和方法不会被子类继承，子类无法直接访问父类的私有变量和方法。

Python实际上通过一个简单的命名改写（name mangling）机制来实现这种访问控制。
当你定义一个以两个下划线开头的属性或方法时，Python内部将其名称改写为`_ClassName__attribute`或`_ClassName__method`。
##### 示例
```python
class Animal:
    def __init__(self):
        self.__privateVar = "I am a private variable"

    def __privateMethod(self):
        return "This is a private method"

class Dog(Animal):
    def access_private(self):
        # 尝试直接访问父类的私有属性和方法
        # print(self.__privateVar)  # 这将导致错误
        # print(self.__privateMethod())  # 这也将导致错误
        
        # 使用改写后的名称来访问
        print(self._Animal__privateVar)
        print(self._Animal__privateMethod())

```