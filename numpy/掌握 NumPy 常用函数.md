# ���� NumPy ���ú���

## 쳲��������ĵ� n ��

```py
# ��Դ��NumPy Cookbook 2e Ch3.1

import numpy as np

# 쳲��������е�ÿ�������֮ǰ��������Ӷ���
# �� 1 �� 2 ��ʼ��ǰ 10 ��Ϊ��
# 1, 2, 3, 5, 8, 13, 21, 34, 55, 89, ...

# 쳲��������е�ͨ�ʽΪ��
# fn = (phi ** n - (-phi) ** (-n)) / 5 ** 0.5
# ���� phi �ǻƽ������phi = (1 + 5 ** 0.5) / 2

# ����һ��쳲��������У�ÿһ���ֵ�������İ���
# ���ֵΪż������ĺ�

# 1. ���� phi
phi = (1 + np.sqrt(5))/2 
print("Phi", phi)
# Phi 1.61803398875

# 2. Ѱ��С���İ�����������
n = np.log(4 * 10 ** 6 * np.sqrt(5) + 0.5)/np.log(phi) 
print(n)
# 33.2629480359

# 3. ���� 1 ~ n ������
n = np.arange(1, n) 
print(n)

# 4. ����쳲�������
fib = (phi**n - (-1/phi)**n)/np.sqrt(5) 
print("First 9 Fibonacci Numbers", fib[:9])
# First 9 Fibonacci Numbers [  1.   1.   2.   3.   5.   8.  13.  21.  34.] 

# 5. ת��Ϊ��������ѡ��
fib = fib.astype(int) 
print("Integers", fib)
'''
Integers [      1       1       2       3       5       8      13      21      34
  ... snip ... snip ...
  317811  514229  832040 1346269 2178309 3524578] 
'''

# 6. ѡ��ֵΪż������
eventerms = fib[fib % 2 == 0] 
print(eventerms)
# [      2       8      34     144     610    2584   10946   46368  196418  832040 3524578]

# 7. ���
print(eventerms.sum())
# 4613732
```

## Ѱ��������

```py
# ��Դ��NumPy Cookbook 2e Ch3.2

from __future__ import print_function 
import numpy as np

# 13195 ���������� 5, 7, 13 �� 29
# 600851475143 ������������Ƕ����أ�

N = 600851475143 
LIM = 10 ** 6


def factor(n): 
    # 1. ����������Χ������
    # a �� sqrtn ~ sqrtn + lim - 1 ������
    # ���� sqrtn �� n ƽ��������ȡ��
    # lim �� sqrtn �� 10e6 �Ľ�Сֵ
    a = np.ceil(np.sqrt(n))   
    lim = min(n, LIM)   
    a = np.arange(a, a + lim)   
    b2 = a ** 2 - n
    
    # 2. ��� b �Ƿ���ƽ����
    # modf ����ȡС������
    fractions = np.modf(np.sqrt(b2))[0]
    
    # 3. Ѱ��û��С�����ֵĵط�
    # ����� b Ϊƽ����
    indices = np.where(fractions == 0)
    
    # 4. Ѱ�� b Ϊƽ����ʱ��a ��ֵ����ȡ����һ��
    a = np.ravel(np.take(a, indices))[0]
    # ���� a = a[indices][0]
    
    # ��� c �� d
    a = int(a)   
    b = np.sqrt(a ** 2 - n)    
    b = int(b)   
    c = a + b   
    d = a - b
    
    # ������ֹ�����򷵻�
    if c == 1 or d == 1:      
        return
    
    # ��ӡ��ǰ c �� d ���ݹ�
    print(c, d)   
    factor(c)   
    factor(d)

factor(N)
'''
1234169 486847 
1471 839 
6857 71
'''
```

## Ѱ�һ�����

```py
# ��Դ��NumPy Cookbook 2e Ch3.3

# ���������Ŷ����Ƿ��Ŷ���һ��
# ��������λ���ĳ˻����ɵ����������� 9009 = 91 x 99
# Ѱ��������λ���˻����ɵ���������

# 1. ������λ��������
a = np.arange(100, 1000) 
np.testing.assert_equal(100, a[0]) np.testing.assert_equal(999, a[-1])

# 2. ��������������Ԫ�صĳ˻�
# outer ��������������Ҳ���� a[i] x a[j] �ľ���
# ravel ����չ��֮�󣬾���ÿ��Ԫ�س˻���������
numbers = np.outer(a, a) 
numbers = np.ravel(numbers) 
numbers.sort() 
np.testing.assert_equal(810000, len(numbers)) 
np.testing.assert_equal(10000, numbers[0]) 
np.testing.assert_equal(998001, numbers[-1])

#3. Ѱ�����Ļ�����
for number in numbers[::-1]:   
    s = str(numbers[i])
    if s == s[::-1]:
        print(s)     
        break
```