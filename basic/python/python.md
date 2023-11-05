# function

```python
def sum(num1, num2):
    return num1 + num2
print(sum(5,6))
```

# class

```python
class Person:
    def __init__(self,name,height,weight):
        self.name = name
        self.height = height
        self.weight = weight

    def say_name(self):
        print("my name:" + self.name)

person1 = Person("Tom",170,100)
person1.say_name()
```



# number

```python
print (float(9)//2) #4.0
print(round(2.5)) #2 五舍六入
print(pow(2,10)) #1024

import math
print(math.ceil(2.8)) #3
```



# string

```python
word = "hello"
print(word[len(word)-1])
print(word.capitalize())
```

# list tuple map

```python
list1 = [1,2,3,4,5]
print(list1[0])

tuple1 = (1,2,3,4)
print(tuple1)

mp1 = {"key1":"value1","key2":"value2"}
print(mp1)
print(mp1.get("key2"))

set1 = {1,2,2,3}
print(set1)
```

# condition

```python
age = 20

if(age<18):
    print("child")
elif(age<30):
    print("young man")
else:
    print("adult")
```

# loop

```python
i = 1
sum2=0
while i<=100:
    sum2 = sum2 + i
    i = i + 1
print(sum2)

sum3=0
for ix in range(1,101):
    sum3 = sum3 + ix
print(sum3)
```

# module

```python
from sys import path
for item in path:
    print(item)
```



