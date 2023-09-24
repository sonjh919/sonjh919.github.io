---
title: Python Error 모음집
date: 2023-09-16 +0800
categories: [Area, Python, Error]
tags: [Python]
---

---

<br>
Python으로 코딩 테스트 준비를 하면서 겪었던 Error들을 모아봤다. Ctrl+F로 찾아보자.

<br>

---

### **TypeError: list indices must be integers or slices, not str**

**Why**

- 리스트의 인덱스를 정수형이 아닌 문자열으로 사용했다.
- 주로 리스트를 for in 반복문에서 사용할 때 발생한다.

**Soln**

- range와 len을 활용하여 인덱스가 정수형이 되게 바꾸자

```python
ex_list = ['a', 'b', 'c', 'd', 'e']

# Error
for i in ex_list:
  print(ex_list[i])

# Solution
for i in range(len(ex_list)):
  print(ex_list[i])
```

<br>

---

<br>

### **TypeError: sequence item 0: expected str instance, int found**

**Why**

- join을 시도할 때 list의 요소가 string이여야 하나 int이여서 join이 되지 않는다.

**Soln**

- map을 활용하여 요소를 string으로 명시적 형변환을 해주자.

```python
ex_list = [1, 2, 3, 4, 5]

# Error
res = ''join(ex_list)

# Solution
res = ''.join(map(str, ex_list))
```

<br>

---

<br>

### IndexError: list assignment index out of range

**Why**

- 빈 리스트에 인덱스를 지정했다.

**Soln**

- append()로 넣거나, 길이만큼의 리스트를 미리 만들어둔다.

```python
# error
a = []
a[1] = 1

# sol
# 1. list를 미리 지정
a = [0,0]
a = [0 for i in range(n)] # list comprehension
a[1] = 1

# 2. append 또는 insert 사용
a = []
a.append('hi')
a.insert(1, 'hi') # 인덱스 지정 가능

```
