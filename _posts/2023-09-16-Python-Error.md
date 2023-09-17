---
title: Python Error 모음집
date: 2023-09-16 +0800
categories: [코딩테스트, Error]
tags: [Python]
---

---

Python으로 코딩 테스트 준비를 하면서 겪었던 Error들을 모아봤다. Ctrl+F로 찾아보자.

---

### **TypeError: list indices must be integers or slices, not str**

**Why**

- 리스트의 인덱스를 정수형이 아닌 문자열으로 사용했다.
- 주로 리스트를 for in 반복문에서 사용할 때 발생한다.

**Soln**

- range와 len을 활용하여 인덱스가 정수형이 되게 바꾸자.

```python
a = ['a', 'b', 'c', 'd', 'e']

# Error
for i in a:
  print(a[i])

# Solution
for i in range(len(a)):
  print(a[i])
```

---
