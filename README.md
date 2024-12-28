## 請說明下面兩種判斷式寫法執行步驟為如何？ 並說明兩種寫法差異？

### 請舉例說明

### Case 1

```py
if "condition1":
...
if "condition2":
...
if "condition3":
...

# 即使前面條件為 True 或是 False 也會執行後面的條件
# 適用多個條件獨立的情況
```

### Case 2

```py
if "condition1":
    ...
elif "condition2":
    ...
elif "condition3":
    ...
else:
    ...

# 只要一個條件為 True 就不會執行後續條件
# 如果全部條件都為 False 就會執行 else
# 適用多個條件互斥的情況
```

## 請說明 \*args 與 \*\*kwargs 代表什麼意思？

```py
def normal_func(arg1, arg2, *args, **kwargs):
    print(arg1, arg2, args, kwargs)

# args 用於接受可變數量的位置引數
# 在函數內會被封裝成 Tuple

# kwargs 用於接收可變數量的關鍵字引數
# 在函數內會被封裝成 Dict
```

## 請說明以下例子分別會輸出什麼？

### Case 1

```py
normal_func(1, 2, [3, 4, 5])

# arg1 = 1, arg2 = 2, args = [3, 4, 5]
# args = (3, 4, 5) 會被當作第三個參數
# kwargs = {}

# 輸出 1 2 ([3, 4, 5],) {}
```

### Case 2

```py
normal_func(1, 2, *[3, 4, 5])

# arg1 = 1, arg2 = 2, args = [3, 4, 5]
# *args = (*[3, 4, 5]) 將 list 拆成單個值
# kwargs = {}

# 輸出 1 2 (3, 4, 5) {}
```

### Case 3

```py
normal_func(1, 2, **{"a": 3, "b": 4})

# arg1 = 1, arg2 = 2
# *args = ()
# kwargs = {"a": 3, "b": 4}

# 輸出 1 2 () {'a': 3, 'b': 4'}
```

### Case 4

```py
normal_func(1, 2, *[3, 4], **{"a": 5, "b": 6})

# arg1 = 1, arg2 = 2
# *args = (3, 4)
# kwargs = {"a": 5, "b": 6}

# 輸出 1 2 (3, 4) {'a': 5, 'b': 6'}
```

### Case 5

```py
normal_func(**{"arg1": 1, "arg2": 2, "args3": 3})

# arg1 = 1, arg2 = 2
# *args = ()
# kwargs = {"args3": 3}

# 輸出1 2 () {'args3': 3}
```

## 如何讓 `instance` 這個物件能夠被迭代(最簡單的方式)？或是能夠使用 list(instance)?

```py
class A:
    pass


instance = A()

for i in instance:
    print(i)
```

```py
class A:
    def __init__(self):
        self.data = [1, 2, 3]

    def __iter__(self):
        return iter(self.data)


instance = A()
for i in instance:
    print(i)
```

## OOP basic (Object Oriented Programming - 物件導向基礎)

```py
class A:
    a = 1
    b = 2

    def __init__(self):
        self.c = 3
        self.d = 4

    def normal_method(self, val):
        self.c = val

    @staticmethod
    def static_method(): ...

    @classmethod
    def class_method(cls, val):
        cls.a = val

# 實例化兩個物件
a1 = A()
a2 = A()
```

### 請回答下列問題

```py
a1.normal_method == a2.normal_method

# False
# 雖然是綁定同個方法，但是是綁定不同的物件
# a1 和 a2 的記憶體會位置會不同
```

```py
a1.static_method == a2.static_method

# True
# 靜態方法不依賴具體物件
# 所以記憶體位置會相同
```

```py
a1.class_method(10)

# 修改了 A.a 的值為 10，但是 class 方法操作是 class 本身
# a1.a 和 a2.a 都會變更
```

```py
a1.a == a2.a

# True
# a1.a 和 a2.a 都指向 class 屬性 A.a
```

```py
a1.normal_method(100)

# 修改了 a1.c 的值為 100，但不影響 a2.c
```

```py
a1.c == a2.c

# False
# 因為 a1.c 為 100，a2.c 仍然為 3
```

## multi inheritance (多繼承)

```py
class A:
    def func(self): ...
    def func2(self): ...
class B:
    def func(self): ...
    def func2(self): ...


class C(A, B):
    def func(self): ...

# 實例化一個物件
instance = C()

# 請回答下列問題
instance.func()
instance.func2()

# instance.func() 執行了 C.func()
# 因為 C.func() 覆蓋了 A.func() 與 B.func()，所以會優先執行

# instance.func2() 執行了 C.func2()
# 因為 Python 使用了方法解析順序(MRO)，所以會優先執行 A.func2()
# 對於 C，MRO 是 [C, A, B, object]，因此先從 A 查找 func2()
```
