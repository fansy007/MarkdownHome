# numpy
build np array

```python
import numpy as np
arr = np.array([[5,10,15],[20,25,30],[35,40,45]])
arr2 = np.array(range(0,10))
arr.shape
```

## select a range of np array
[start:end:step]

```python
arr[:2:]

#output
array([[ 5, 10, 15],
       [20, 25, 30]])

arr[:2,1:]

#output
array([[10, 15],
       [25, 30]])
```


## broadcase
```python
arr>20

#output
array([[False, False, False],
       [False,  True,  True],
       [ True,  True,  True]])

arr[arr>25]
#output
array([30, 35, 40, 45])
```

## sum rows columns
axis=0 sum by row
axis=1 sum by column

![[Pasted image 20240907200140.png|475]]


## generate matrixs
np.arange(9).reshape(3,3)
array([[0, 1, 2],
       [3, 4, 5],
       [6, 7, 8]])

np.eye(3)
array([[1., 0., 0.],
       [0., 1., 0.],
       [0., 0., 1.]])

np.random.randn(25).reshape(5,5)
array([[ 1.01759906, -1.37630242, -0.52189072,  1.49589861,  0.39343685],
       [-0.63067222, -1.69252685, -0.92267584,  0.6100594 ,  0.76127473],
       [-2.16502382, -0.72028519, -0.12736635,  1.79848195,  0.4819558 ],
       [-0.83446886,  0.59556591, -1.13219992, -0.38858924,  0.09827136],
       [ 2.83581351,  0.24337261,  0.05126133, -0.78186919,  0.78654376]])

np.linspace(0,1,20) -- 20 numbers between 0->1
array([0.        , 0.05263158, 0.10526316, 0.15789474, 0.21052632,
       0.26315789, 0.31578947, 0.36842105, 0.42105263, 0.47368421,
       0.52631579, 0.57894737, 0.63157895, 0.68421053, 0.73684211,
       0.78947368, 0.84210526, 0.89473684, 0.94736842, 1.        ])

## Get sub matrixs or value from a matrics
array([[ 1,  2,  3,  4,  5],
       [ 6,  7,  8,  9, 10],
       [11, 12, 13, 14, 15],
       [16, 17, 18, 19, 20],
       [21, 22, 23, 24, 25]])

mat[3,4]
20

mat[-1,:] -- -1 拿最后一行， ：拿所有
array([21, 22, 23, 24, 25])

## matrix sum std
sum 求和
std 标准差


