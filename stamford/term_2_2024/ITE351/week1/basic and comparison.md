---
date: 2024-11-19T00:00:00.000Z
tags:
  - null
hubs:
  - '[[]]'
urls:
  - null
---
# basic and comparison

## format

```python
code = "ITE351"

print("i am taking {} course".format(code))
```

## f

```python
code = "ITE351"

print(f"i am taking {code} course")
```

## sep

```python
print(" User", "Desktop", "Home", sep="/")
```

## end

- to connect the current and below line (disable new line)

```python
print("Hello", end= " ")
print("world!")
```

## raw

- \n will not work

```python
print(r"6: \n is used for newline")
```

## c format style

```python
print("8: c style printing = %f" % 1.0)
print("9: Casting with c style: value1 = %.2f value2 = %d" % (3.1415,1.5))
print("my name is %s and my gpa is %.1f" % ("pantorn" , 3.7))
```

## type checking

```python
a = True
a2 = 10
b = False
b2 = 0
print(type(b))
print(type(b2))
print("1: is a boolean: ", type(a) is bool)
print("2: is a2 int: ", isinstance(a2,int))
print("1: is a boolean: ", type(b) is bool)
print("2: is a2 int: ", isinstance(b2,int))
```

## operator

```python
print("4: True and False: ", True and False)
print("5: True or False: ", True or False)
print("6: not False: ",  not False)
print("7: not 0: ", not 0)
print("8: not 1: ", not 1)
```

```python
print("1: 3+3 -->", 3+3)
print("2: 3/3 -->",3/3)
print("3: 4//3 -->", 4//3)
print("4: 4 % 3 --> " ,5 % 3)
print("5: 4 * 2 -->", 4*2)
print("5: 4 ^ 2 -->", 4**2)
```

## input

```python
a = input()
if int(a) > 0:
    print(f"user number is more than 0 and is {a}")
else:
    print("user number is less than 1")
```

## concatenate

```python
a,b,c = "Alice", "Bob", "Charlie"
print(a,b,c,sep = ",")

concatenate = a + "," + b + "," + c
print(concatenate)
```

## random math

```python
import random
import math

num = math.floor(random.random() * 10)


user = input()
if int(user) > num :
  print("your guess is higher")
elif int(user) < num:
  print("your guess is lower")
else :
  print("your number is equal")
print("the number is  ",num)
```


