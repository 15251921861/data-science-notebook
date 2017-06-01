# ���� NumPy ģ��

```py
# ��Դ��NumPy Biginner's Guide 2e ch6
```

## �������

```py
import numpy as np

A = np.mat("0 1 2;1 0 3;4 -3 8")
print "A\n", A
'''
A
[[ 0  1  2]
 [ 1  0  3]
 [ 4 -3  8]]
'''

# ��������棬������ᱨ��
inverse = np.linalg.inv(A)
print "inverse of A\n", inverse
'''
inverse of A
[[-4.5  7.  -1.5]
 [-2.   4.  -1. ]
 [ 1.5 -2.   0.5]]
'''

print "Check\n", A * inverse
'''
Check
[[ 1.  0.  0.]
 [ 0.  1.  0.]
 [ 0.  0.  1.]]
'''
```

## ������Է�����

```py
import numpy as np

A = np.mat("1 -2 1;0 2 -8;-4 5 9")
print "A\n", A
'''
A
[[ 1 -2  1]
 [ 0  2 -8]
 [-4  5  9]]
'''

b = np.array([0, 8, -9])
print "b\n", b
'''
b
[ 0  8 -9]
'''

# solve ������� x��ʹ Ax = b
# �ڲ�ʹ�� np.dot(A.I, b) ������
# ���� A ������ʱ����
x = np.linalg.solve(A, b)
print "Solution", x
'''
Solution [ 29.  16.   3.]
'''

print "Check\n", np.dot(A , x)
'''
Check
[[ 0.  8. -9.]]
'''
```

## ����ֵ����������

```py

# ��� Ax = ��x������ x ����
# �� �� �� A ������ֵ��x �� A ���� �� ����������
import numpy as np

A = np.mat("3 -2;1 0")
print "A\n", A
'''
A
[[ 3 -2]
 [ 1  0]]
'''

# eigvals �����������ֵ
print "Eigenvalues", np.linalg.eigvals(A)
# Eigenvalues [ 2.  1.]

# eig �������ֵ����������
# �����������������
eigenvalues, eigenvectors = np.linalg.eig(A)
print "First tuple of eig", eigenvalues
print "Second tuple of eig\n", eigenvectors
'''
First tuple of eig [ 2.  1.]
Second tuple of eig
[[ 0.89442719  0.70710678]
 [ 0.4472136   0.70710678]]
'''

for i in range(len(eigenvalues)):
    print "Left", np.dot(A, eigenvectors[:,i])
    print "Right", eigenvalues[i] * eigenvectors[:,i]
    print
'''
Left [[ 1.78885438]
 [ 0.89442719]]
Right [[ 1.78885438]
 [ 0.89442719]]
Left [[ 0.70710678]
 [ 0.70710678]]
Right [[ 0.70710678]
 [ 0.70710678]]
'''
```

## ����ֵ�ֽ�

```py
# ����ֵ�� A * A.T ����ֵ������ƽ����
# �� A �� mxn �׾���
# ����ֵ�ֽ⽫ A �ֽ�� USV
# U �� mxm �ס�S �� mxm �׶ԽǾ���������ֵ����
# V �� mxn ��

import numpy as np

A = np.mat("4 11 14;8 7 -2")
print "A\n", A
'''
A
[[ 4 11 14]
 [ 8  7 -2]]
'''

# linalg.svd �������ֵ
U, Sigma, V = np.linalg.svd(A, full_matrices=False)

print "U"
print U
'''
U
[[-0.9486833  -0.31622777]
 [-0.31622777  0.9486833 ]]
'''

print "Sigma"
print Sigma
'''
Sigma
[ 18.97366596   9.48683298]
'''

print "V"
print V
'''
V
[[-0.33333333 -0.66666667 -0.66666667]
 [ 0.66666667  0.33333333 -0.66666667]]
'''

print "Product\n", U * np.diag(Sigma) * V
'''
Product
[[  4.  11.  14.]
 [  8.   7.  -2.]]
'''

print np.linalg.eigvals(A * A.T) ** 0.5
'''
[ 18.97366596   9.48683298]
'''

```

## ���������

```py
# ������Ψһ���� M������
# AMA = A��MAM = M��AM �� MA ��Ϊ�Գƾ���
# �� M �� A �Ĺ��������

import numpy as np

A = np.mat("4 11 14;8 7 -2")
print "A\n", A
'''
A
[[ 4 11 14]
 [ 8  7 -2]]
'''

# linalg.pinv ��������
pseudoinv = np.linalg.pinv(A)
print "Pseudo inverse\n", pseudoinv
'''
Pseudo inverse
[[-0.00555556  0.07222222]
 [ 0.02222222  0.04444444]
 [ 0.05555556 -0.05555556]]
'''

print "Check", A * pseudoinv
'''
Check [[  1.00000000e+00   0.00000000e+00]
 [  8.32667268e-17   1.00000000e+00]]
'''
```

## �����������ʽ

```py
import numpy as np

A = np.mat("3 4;5 6")
print "A\n", A
'''
A
[[ 3.  4.]
 [ 5.  6.]]
'''

# linalg.det �������ʽ
# ���ڶ��׾���
# det(A) = A[0][0] * A[1][1] - A[0][1] * A[1][0]
print "Determinant", np.linalg.det(A)
# Determinant -2.0
```

## ���ٸ���Ҷ�任��FFT��

```py
import numpy as np
from matplotlib.pyplot import plot, show

# ���� 30 ��������Ҳ�
x =  np.linspace(0, 2 * np.pi, 30)
wave = np.cos(x)

# ʹ�� fft �����任���Ҳ�
transformed = np.fft.fft(wave)

# ��֤�Ƿ��ܹ���ԭ����
print np.all(np.abs(np.fft.ifft(transformed) - wave) < 10 ** -9)
# True

# ���Ʊ任����ź�
plot(transformed)
show()
```

![](http://upload-images.jianshu.io/upload_images/118142-225ebdf16fd50ecb.jpg)

## ����Ƶ��

```py
import numpy as np
from matplotlib.pyplot import plot, show

# ���� 30 ��������Ҳ�
x =  np.linspace(0, 2 * np.pi, 30)
wave = np.cos(x)

# ʹ�� fft �����任���Ҳ�
transformed = np.fft.fft(wave)

# ʹ�� fftshift  ���������ź�
shifted = np.fft.fftshift(transformed)

# ����Ƿ���Ի�ԭ
print np.all(np.abs(np.fft.ifftshift(shifted) - transformed) < 10 ** -9)

# �����ź�
plot(transformed, lw=2)
plot(shifted, lw=3)
show()
```

![](http://upload-images.jianshu.io/upload_images/118142-0c289ee5b6981ff2.jpg)

## �������

```py
import numpy as np
from matplotlib.pyplot import plot, show

# ������СΪ 10000 ���������
# ��ʼ���Ϊ 1000
cash = np.zeros(10000)
cash[0] = 1000

# �����������������������ֲ� B(n = 9, p = 0.5)
# P(x = k) = C(n, k) * p ** k * (1 - p) ** (n - k)
# x: 0 ~ 9
outcome = np.random.binomial(9, 0.5, size=len(cash))

for i in range(1, len(cash)):

    # ��������С�� 5������һ�������һ
    # p = 0.5 ʱ������ֲ��ǶԳƵ�
    # ����С�� 5 �ĸ���Ӧ���� 0.5
    if outcome[i] < 5:
      cash[i] = cash[i - 1] - 1
    elif outcome[i] < 10:
      cash[i] = cash[i - 1] + 1
    else:
      raise AssertionError("Unexpected outcome " + outcome)

print outcome.min(), outcome.max()
# 0 9

# �������仯���
plot(np.arange(len(cash)), cash)
show()
```

![](http://upload-images.jianshu.io/upload_images/118142-a2a55d780cdc27d1.jpg)

## ģ����Ϸ��Ŀ

```py
# ��Ϸ��Ŀ����һ��Ͱ�������� 25 ��������
# ��һ����ù��
# ѡ����ȷ�ش��������Ҫȡ��������
# �������������ͨ�򣬷�����һ
# �����������

import numpy as np
from matplotlib.pyplot import plot, show

# ������������
points = np.zeros(100)

# hypergeometric �������ɵ���������㳬���ηֲ�
# �����ηֲ������ˣ��������������򣬴Ӵ�����ȡ��������ȡ�� k ��һ����ĸ��ʡ�
# �����ֱ�Ϊ����ͨ��ĸ�������ù��ĸ�����ȡ���ĸ���
# �����ģ����ȡ����������ͨ��ĸ���
outcomes = np.random.hypergeometric(25, 1, 3, size=len(points))

for i in range(len(points)):
   if outcomes[i] == 3:
      # �������������ͨ�򣬷�����һ
      points[i] = points[i - 1] + 1
   elif outcomes[i] == 2:
      # ������ڵ�ù�򣬷�������
      points[i] = points[i - 1] - 6
   else:
      print outcomes[i]

# ���Ʒ����仯���
plot(np.arange(len(points)), points)
show()
```

![](http://upload-images.jianshu.io/upload_images/118142-43e3c61f417e7a60.jpg)

## ������̬�ֲ�

![](https://imgsa.baidu.com/baike/s%3D205/sign=2abf505a42166d223c77129473220945/342ac65c1038534384b650b09213b07eca808822.jpg)

```py
import numpy as np
import matplotlib.pyplot as plt

N=10000

# ����������������������̬�ֲ� N(mu = 0, sigma = 1)
normal_values = np.random.normal(size=N)

# ����ֱ��ͼ�������Ƿ��飬�����ǳ���Ƶ��
# �ڶ���������ʾ 100 ���飨Ĭ�� 10 ����
# bins ������ֵ
dummy, bins, dummy = plt.hist(normal_values, np.sqrt(N), normed=True, lw=1)

# ������̬�ֲ������ܶȺ���
sigma = 1
mu = 0
plt.plot(bins, 1/(sigma * np.sqrt(2 * np.pi)) * np.exp( - (bins - mu)**2 / (2 * sigma**2) ),lw=2)
plt.show()
```

![](http://upload-images.jianshu.io/upload_images/118142-aa1c1a58015cecc4.jpg)

## ���ƶ�����̬�ֲ�

![](https://imgsa.baidu.com/baike/s%3D163/sign=966dfaa16009c93d03f20af1ac3cf8bb/43a7d933c895d143f231548c74f082025baf07dd.jpg)

```py
# ����һ�δ������һ��

import numpy as np
import matplotlib.pyplot as plt

N=10000

# ������ĳ� lognormal �����ɶ�����̬�ֲ��������
lognormal_values = np.random.lognormal(size=N)

dummy, bins, dummy = plt.hist(lognormal_values, np.sqrt(N), normed=True, lw=1)

sigma = 1
mu = 0
x = np.linspace(min(bins), max(bins), len(bins))
# �޸�����Ĺ�ʽ
pdf = np.exp(-(np.log(x) - mu)**2 / (2 * sigma**2))/ (x * sigma * np.sqrt(2 * np.pi))
plt.plot(x, pdf,lw=3)
plt.show()
```

![](http://upload-images.jianshu.io/upload_images/118142-b5562aa3bc7ef728.jpg)