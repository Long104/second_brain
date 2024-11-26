---
date: 2024-11-26T00:00:00.000Z
tags:
  - null
hubs:
  - '[[]]'
urls:
  - null
---
# week2

## python

```python
list_a = ["Bulbasaur","Charmander","Squirtle","Charmander"]
list_b = ["Caterpie","Pidgey","Squirtle"]
set_a = set(list_a)
set_b = set(list_b)

print("1: Set a - i.e., no duplicates:", set_a)

print("2: set intersection:", set_a.intersection(set_b))
print("3: a - b:", set_a.difference(set_b))
print("4: set b - a",set_b.difference(set_a))
print("5: set (a-b) + (b-a)", set_a.symmetric_difference(set_b))
print("6: set a u b:", set_a.union(set_b))
```
