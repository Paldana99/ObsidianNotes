# TP n°2: Descente de gradient

# Exercice 1:

## Partie 1:

### 1:


```python
import tensorflow as tf
from numpy.linalg import norm
import matplotlib.pyplot as plt
import pandas as pd
import seaborn as sns
import numpy as np
from tqdm import tqdm
```


```python
def descenteGradient1(x: list, maxIter : int, pas : float, epsilon : float):
    x = tf.Variable(x, name='x')

    for i in range(maxIter):
        with tf.GradientTape() as tape:
            z = 4*(x[0]-1.0)**2+(0.5)*(tf.math.exp(x[1]-3.0)-1)**2
        
        x1 = x - pas * tape.gradient(z, x)
        
        if (tf.norm(x-x1, ord=2) < epsilon):
            return x, i
        
        x = tf.Variable(x1, name='x')
    
    return x, i
```


```python
x0 = 2.0
y0 = 1.0
descenteGradient1([x0, y0], maxIter=500, pas=0.22, epsilon=0.000001)
```

    2022-06-03 18:49:53.018028: W tensorflow/stream_executor/platform/default/dso_loader.cc:64] Could not load dynamic library 'libcuda.so.1'; dlerror: libcuda.so.1: cannot open shared object file: No such file or directory
    2022-06-03 18:49:53.018062: W tensorflow/stream_executor/cuda/cuda_driver.cc:269] failed call to cuInit: UNKNOWN ERROR (303)
    2022-06-03 18:49:53.018085: I tensorflow/stream_executor/cuda/cuda_diagnostics.cc:156] kernel driver does not appear to be running on this host (asus): /proc/driver/nvidia/version does not exist
    2022-06-03 18:49:53.019299: I tensorflow/core/platform/cpu_feature_guard.cc:193] This TensorFlow binary is optimized with oneAPI Deep Neural Network Library (oneDNN) to use the following CPU instructions in performance-critical operations:  AVX2 FMA
    To enable them in other operations, rebuild TensorFlow with the appropriate compiler flags.





    (<tf.Variable 'x:0' shape=(2,) dtype=float32, numpy=array([1.0000001, 2.9999952], dtype=float32)>,
     88)



### 2: Déterminer le pas constant optimal

Pour determiner le pas constant optimal il nous faut trouver les valeurs propres de la matrice hessienne du grad(f)

Ou:
$$f(x) = 4(x − 1)^2 +  \frac{1}{2}(e^{(y−3)} − 1)^2$$

On retrouve comme matrice:
$$
H=
\begin{bmatrix} 8 & 0 \\
    0 & 2e^{2y-6}-e^{y-3} \\ \end{bmatrix}
$$
Si on évalue dans le point $x=1 \text{ et } y=3$:

$$
H=
\begin{bmatrix}
8 & 0 \\
0 & 1 \\ \end{bmatrix}
$$

On calcule les valeurs propres et on retrouve:
$$\lambda_1=8 \quad \lambda_2=1$$
Alors le pas optimal est:
$$
h = \frac{2}{l+L} = \frac{2}{1+8} = 0.\bar2 
$$


### 3: Verifier numeriquement


```python
iters = []
for i in range(0, 100):
    x0 = tf.Variable(2.0, name='x')
    y0 = tf.Variable(1.0, name='y')
    iters.append(descenteGradient1((x0, y0), maxIter=500, pas=i/100, epsilon=0.000001)[1])

```


```python
plt.plot([x/100 for x in range(100)], iters)
plt.show()
```


    
![png](output_9_0.png)
    



```python
top = 30
plt.plot([x/100 for x in range(1,top)], iters[1:top])
plt.axvline(x=0.23, color='red', linestyle='--')
plt.rc('font', size=15)
plt.show()
```


    
![png](output_10_0.png)
    



```python
x0 = 2.0
y0 = 1.0
descenteGradient1([x0, y0], maxIter=500, pas=0.23, epsilon=0.000001)
```




    (<tf.Variable 'x:0' shape=(2,) dtype=float32, numpy=array([0.9999997, 2.9999964], dtype=float32)>,
     85)



Avec un pas de 0.23, on realise 85 iteration.

## Partie 2:

### 4:


```python
def descenteGradient2(x: list, maxIter : int, pas : float, epsilon : float, m : float):
    x = tf.Variable(x, name='x')
    x_1 = tf.Variable(x, name='x_1')

    for i in range(maxIter):
        with tf.GradientTape() as tape:
            z = 4*(x[0]-1.0)**2+(0.5)*(tf.math.exp(x[1]-3.0)-1)**2

        x1 = x + m * (x - x_1) - pas * tape.gradient(z, x)
        
        if (tf.norm(x-x1, ord=2) < epsilon):
            return x, i
        
        x_1 = tf.Variable(x, name='x_1')
        x = tf.Variable(x1, name='x')
    
    return x, i
```


```python
x0 = 2.0
y0 = 1.0
descenteGradient2([x0, y0], maxIter=500, pas=0.22, epsilon=0.000001, m=0.31)
```




    (<tf.Variable 'x:0' shape=(2,) dtype=float32, numpy=array([1.       , 3.0000086], dtype=float32)>,
     48)



### 5:


```python
iters2 = []
for i in range(0, 100):
    x0 = 2.0
    y0 = 1.0
    iters2.append(descenteGradient2((x0, y0), maxIter=500, pas=0.22, epsilon=0.000001, m=i/100)[1])

```


```python
plt.plot([x/100 for x in range(100)], iters2)
plt.show()
```


    
![png](output_18_0.png)
    



```python
top = [20,50]
plt.plot([x/100 for x in range(top[0], top[1])], iters2[top[0]:top[1]])
plt.axvline(x=0.37, color='red', linestyle='--')
plt.rc('font', size=15)
plt.show()
```


    
![png](output_19_0.png)
    



```python
x0 = 2.0
y0 = 1.0
descenteGradient2([x0, y0], maxIter=500, pas=0.22, epsilon=0.000001, m=0.37)
```




    (<tf.Variable 'x:0' shape=(2,) dtype=float32, numpy=array([1.       , 2.9999907], dtype=float32)>,
     47)



On retrouve que la meilleur valeur du moment est $m=0.37$ qui va permettre faire 47 iteration.

### 6:


```python
def descenteGradient3(x: list, maxIter : int, pas : float, epsilon : float, m : float):
    x = tf.Variable(x, name='x')
    x_1 = tf.Variable(x, name='x_1')

    for i in range(maxIter):
        x = x + m * (x - x_1)
        x = tf.Variable(x)
        
        with tf.GradientTape() as tape:
            z = 4*(x[0]-1.0)**2+(0.5)*(tf.math.exp(x[1]-3.0)-1)**2
        
        x1 = x + m * (x - x_1) - pas * tape.gradient(z, x)
        
        if (tf.norm(x-x1, ord=2) < epsilon):
            return x, i
        
        x_1 = tf.Variable(x, name='x_1')
        x = tf.Variable(x1, name='x')
    
    return x, i
```


```python
x0 = 2.0
y0 = 1.0
descenteGradient3([x0, y0], maxIter=500, pas=0.22, epsilon=0.000001, m=0.31)
```




    (<tf.Variable 'Variable:0' shape=(2,) dtype=float32, numpy=array([0.9999998, 3.000042 ], dtype=float32)>,
     38)




```python
iters3 = []
x0 = 2.0
y0 = 1.0
for i in range(0, 100):
    iters3.append(descenteGradient3((x0, y0), maxIter=500, pas=0.22, epsilon=0.000001, m=i/100)[1])

```


```python
plt.plot([x/100 for x in range(100)], iters3)
plt.show()
```


    
![png](output_26_0.png)
    



```python
top = [10,40]
plt.plot([x/100 for x in range(top[0], top[1])], iters3[top[0]:top[1]])
plt.axvline(x=0.37, color='green', linestyle='--')
plt.rc('font', size=15)
plt.axvline(x=0.31, color='red', linestyle='--')
plt.rc('font', size=15)
plt.show()
```


    
![png](output_27_0.png)
    



```python
x0 = 2.0
y0 = 1.0
descenteGradient3((x0, y0), maxIter=500, pas=0.22, epsilon=0.000001, m=0.31)
```




    (<tf.Variable 'Variable:0' shape=(2,) dtype=float32, numpy=array([0.9999998, 3.000042 ], dtype=float32)>,
     38)



On observe que avec la methode de Yurii Nesterov, avec une valeur de $m=0.31$, on fait un quantite de 38 iteration, une amelioration face a la methode du moment normal.

# Exercice 2

## 1:


```python
data = pd.read_csv("isolation.csv", delimiter=';', decimal=',')
data
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>cout_total_ht</th>
      <th>annee_travaux</th>
      <th>Code Région</th>
      <th>region</th>
      <th>poste_isolation</th>
      <th>isolant</th>
      <th>epaisseur</th>
      <th>resistance</th>
      <th>surface</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>156.000000</td>
      <td>2016</td>
      <td>53</td>
      <td>BRE</td>
      <td>ITI</td>
      <td>LAINE MINERALE</td>
      <td>120</td>
      <td>3.8</td>
      <td>4.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>237.914692</td>
      <td>2016</td>
      <td>75</td>
      <td>NAQ</td>
      <td>RAMPANTS</td>
      <td>LAINE MINERALE</td>
      <td>120</td>
      <td>6.0</td>
      <td>35.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>395.000000</td>
      <td>2016</td>
      <td>53</td>
      <td>BRE</td>
      <td>COMBLES PERDUES</td>
      <td>LAINE MINERALE</td>
      <td>320</td>
      <td>7.1</td>
      <td>11.5</td>
    </tr>
    <tr>
      <th>3</th>
      <td>399.000000</td>
      <td>2018</td>
      <td>84</td>
      <td>ARA</td>
      <td>COMBLES PERDUES</td>
      <td>LAINE MINERALE</td>
      <td>335</td>
      <td>7.0</td>
      <td>70.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>447.000000</td>
      <td>2018</td>
      <td>27</td>
      <td>BFC</td>
      <td>COMBLES PERDUES</td>
      <td>LAINE VEGETALE</td>
      <td>430</td>
      <td>7.5</td>
      <td>11.0</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>483</th>
      <td>29749.000000</td>
      <td>2017</td>
      <td>24</td>
      <td>CVL</td>
      <td>ITE</td>
      <td>PLASTIQUES</td>
      <td>140</td>
      <td>4.1</td>
      <td>172.0</td>
    </tr>
    <tr>
      <th>484</th>
      <td>29881.516590</td>
      <td>2016</td>
      <td>53</td>
      <td>BRE</td>
      <td>ITE</td>
      <td>PLASTIQUES</td>
      <td>120</td>
      <td>3.8</td>
      <td>211.0</td>
    </tr>
    <tr>
      <th>485</th>
      <td>32383.000000</td>
      <td>2013</td>
      <td>28</td>
      <td>NOR</td>
      <td>ITE</td>
      <td>LAINE MINERALE</td>
      <td>120</td>
      <td>4.0</td>
      <td>194.0</td>
    </tr>
    <tr>
      <th>486</th>
      <td>37486.000000</td>
      <td>2018</td>
      <td>76</td>
      <td>OCC</td>
      <td>ITE</td>
      <td>PLASTIQUES</td>
      <td>140</td>
      <td>3.0</td>
      <td>249.0</td>
    </tr>
    <tr>
      <th>487</th>
      <td>62597.000000</td>
      <td>2017</td>
      <td>93</td>
      <td>PAC</td>
      <td>ITE</td>
      <td>PLASTIQUES</td>
      <td>120</td>
      <td>3.9</td>
      <td>355.0</td>
    </tr>
  </tbody>
</table>
<p>488 rows × 9 columns</p>
</div>




```python
data.dtypes
```




    cout_total_ht      float64
    annee_travaux        int64
    Code Région          int64
    region              object
    poste_isolation     object
    isolant             object
    epaisseur            int64
    resistance         float64
    surface            float64
    dtype: object




```python
data.corr()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>cout_total_ht</th>
      <th>annee_travaux</th>
      <th>Code Région</th>
      <th>epaisseur</th>
      <th>resistance</th>
      <th>surface</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>cout_total_ht</th>
      <td>1.000000</td>
      <td>0.043095</td>
      <td>-0.137020</td>
      <td>-0.419655</td>
      <td>-0.383402</td>
      <td>0.484789</td>
    </tr>
    <tr>
      <th>annee_travaux</th>
      <td>0.043095</td>
      <td>1.000000</td>
      <td>0.042536</td>
      <td>-0.048969</td>
      <td>-0.039561</td>
      <td>0.019415</td>
    </tr>
    <tr>
      <th>Code Région</th>
      <td>-0.137020</td>
      <td>0.042536</td>
      <td>1.000000</td>
      <td>0.330998</td>
      <td>0.289447</td>
      <td>0.054207</td>
    </tr>
    <tr>
      <th>epaisseur</th>
      <td>-0.419655</td>
      <td>-0.048969</td>
      <td>0.330998</td>
      <td>1.000000</td>
      <td>0.909575</td>
      <td>-0.089866</td>
    </tr>
    <tr>
      <th>resistance</th>
      <td>-0.383402</td>
      <td>-0.039561</td>
      <td>0.289447</td>
      <td>0.909575</td>
      <td>1.000000</td>
      <td>-0.135494</td>
    </tr>
    <tr>
      <th>surface</th>
      <td>0.484789</td>
      <td>0.019415</td>
      <td>0.054207</td>
      <td>-0.089866</td>
      <td>-0.135494</td>
      <td>1.000000</td>
    </tr>
  </tbody>
</table>
</div>




```python
sns.pairplot(data, hue="isolant")
```




    <seaborn.axisgrid.PairGrid at 0x7f4398108820>




    
![png](output_34_1.png)
    


On retrouve que eppaiseur et resistance sont tres identiques (une correlation de 0.9). Cela par le materieux, plus eppais, plus resistant.

## 2:


```python
data[['resistance', 'surface', 'cout_total_ht']]
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>resistance</th>
      <th>surface</th>
      <th>cout_total_ht</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>3.8</td>
      <td>4.0</td>
      <td>156.000000</td>
    </tr>
    <tr>
      <th>1</th>
      <td>6.0</td>
      <td>35.0</td>
      <td>237.914692</td>
    </tr>
    <tr>
      <th>2</th>
      <td>7.1</td>
      <td>11.5</td>
      <td>395.000000</td>
    </tr>
    <tr>
      <th>3</th>
      <td>7.0</td>
      <td>70.0</td>
      <td>399.000000</td>
    </tr>
    <tr>
      <th>4</th>
      <td>7.5</td>
      <td>11.0</td>
      <td>447.000000</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>483</th>
      <td>4.1</td>
      <td>172.0</td>
      <td>29749.000000</td>
    </tr>
    <tr>
      <th>484</th>
      <td>3.8</td>
      <td>211.0</td>
      <td>29881.516590</td>
    </tr>
    <tr>
      <th>485</th>
      <td>4.0</td>
      <td>194.0</td>
      <td>32383.000000</td>
    </tr>
    <tr>
      <th>486</th>
      <td>3.0</td>
      <td>249.0</td>
      <td>37486.000000</td>
    </tr>
    <tr>
      <th>487</th>
      <td>3.9</td>
      <td>355.0</td>
      <td>62597.000000</td>
    </tr>
  </tbody>
</table>
<p>488 rows × 3 columns</p>
</div>




```python
a = tf.Variable(tf.random.normal((3,1)), name='a')
a
```




    <tf.Variable 'a:0' shape=(3, 1) dtype=float32, numpy=
    array([[ 0.8329525 ],
           [-0.57221955],
           [-0.56555384]], dtype=float32)>




```python
a = np.zeros((3,1))
a[0] = 1
a[1] = 30
a[2] = 80
a = tf.Variable(a, name='a')
a
```




    <tf.Variable 'a:0' shape=(3, 1) dtype=float64, numpy=
    array([[ 1.],
           [30.],
           [80.]])>




```python
X = data[['resistance', 'surface']]
X = X.assign(bias=1)
X = X[["bias", "resistance", "surface"]]
X.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>bias</th>
      <th>resistance</th>
      <th>surface</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>3.8</td>
      <td>4.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>6.0</td>
      <td>35.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1</td>
      <td>7.1</td>
      <td>11.5</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1</td>
      <td>7.0</td>
      <td>70.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>1</td>
      <td>7.5</td>
      <td>11.0</td>
    </tr>
  </tbody>
</table>
</div>




```python
Y = data['cout_total_ht']
Y.head()
```




    0    156.000000
    1    237.914692
    2    395.000000
    3    399.000000
    4    447.000000
    Name: cout_total_ht, dtype: float64




```python
def descenteGradient(a, X, Y, maxIter : int, pas : float, epsilon : float):
    for i in tqdm(range(maxIter)):
        #print(i, x0, y0)
        with tf.GradientTape() as tape:
            z = tf.norm(X.to_numpy() @ a - Y.to_numpy(), 2)
        grad = tape.gradient(z, a)
        norm = np.linalg.norm(grad, 2)
        
        if norm > 100:
            grad /= 10
            
        a1 = a - pas * grad
        
        if (tf.norm(a-a1, ord=2) < epsilon):
            return a, i
        
        a = tf.Variable(a1, name='a')
    
    return a, i
```


```python
res = descenteGradient(a, X, Y, maxIter=10000, pas=0.1, epsilon=0.01)
res
```

    100%|██████████████████████████████████████████████████████| 10000/10000 [01:06<00:00, 150.70it/s]





    (<tf.Variable 'a:0' shape=(3, 1) dtype=float64, numpy=
     array([[633.47493284],
            [589.50098332],
            [237.44717842]])>,
     9999)




```python
y_predict = X.to_numpy() @ res[0].numpy()
Y_res = np.resize(Y, (488))
y_predict = np.resize(y_predict, (488))
score = np.linalg.norm((Y_res - y_predict)**2, 2)
print(score)
len(str(score))
```

    15708966492.3896





    16



On retrove que le modele ne reussit pas a predire bien les valeurs.


```python
def descenteGradient3(a, X, Y, maxIter : int, pas : float, epsilon : float, m : float):
    a = tf.Variable(a, name='a')
    a_1 = tf.Variable(a, name='a_1')

    for i in range(maxIter):
        a = a + m * (a - a_1)
        a = tf.Variable(a)
        
        with tf.GradientTape() as tape:
            z = tf.norm(X.to_numpy() @ a - Y.to_numpy(), 2)
            
        a1 = a + m * (a - a_1) - pas * tape.gradient(z, a)
        
        if (tf.norm(a-a1, ord=2) < epsilon):
            return a, i
        
        a_1 = tf.Variable(a, name='a_1')
        a = tf.Variable(a1, name='a')
    
    return a, i
```


```python
res = descenteGradient3(a, X, Y, maxIter=1000, pas=0.22, epsilon=0.000001, m=0.2)
res
```




    (<tf.Variable 'a:0' shape=(3, 1) dtype=float64, numpy=
     array([[ 215.94537517],
            [ 843.99169633],
            [4028.62621758]])>,
     999)




```python

```
