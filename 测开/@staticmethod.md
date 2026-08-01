```python
class Car:
    brand = "通用"  # 类属性

    def __init__(self, model):
        self.model = model  # 实例属性

    @staticmethod
    def calc_speed(velocity, time):
        return velocity * time  # 没有 self，不依赖对象状态

# 1. 类可以直接调用（属于类的标志）
print(Car.calc_speed(10, 2))  # 输出 20

# 2. 实例虽然能调，但没用到自身任何数据
my_car = Car("Model S")
print(my_car.calc_speed(10, 2))  # 也是 20（my_car的model属性完全没用上）

# 3. 终极证据：看内存归属
print("类字典里包含:", "calc_speed" in Car.__dict__)  # True
print("实例字典里只有:", my_car.__dict__)  # 输出 {'model': 'Model S'}，根本没有 calc_speed
```

> 静态方法内存只存一份，挂在类上，所有实例共享。
>
> 实例能调用只是 Python 语法糖（自动帮你找到类去执行），" 但**所有权**永远属于类，不属于任何一个对象" 。