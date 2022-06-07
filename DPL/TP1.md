	# TP1 n1: Introduction au calcul scientifique avec numpy
## Pablo Aldana
### 13 Mai 2022


```python
import numpy as np
import matplotlib.pyplot as plt
from time import time
from numpy.polynomial import Polynomial as P
import pandas as pd
import seaborn as sns
```

# Exercice 1:



```python
n = 100
M1 = np.random.randn(n,n)
M2 = np.random.randn(n,n)
```


```python
# Fonction par defaut de numpy
def numpy_add(M1, M2):
    return np.add(M1, M2)
```


```python
# Fonction par une double iteration, on fait l'addition pour chaque cellule de la matrice.
def personal_add(M1, M2):
    M3 = np.empty((n,n))
    for i in range(n):
        for j in range(n):
            M3[i,j] = M1[i,j] + M2[i,j]
    return M3
```


```python
# On prend le temps 
personal_time = []
numpy_time = []
n_list = []
for n in range(2, 1000, 10):
    n_list.append(n)
    M1 = np.random.randn(n,n)
    M2 = np.random.randn(n,n)
    # Numpy Add
    start_time = time()
    M11 = numpy_add(M1, M2)
    end_time_numpy = time() - start_time
    numpy_time.append(end_time_numpy)
    # Personal Algorithme
    start_time = time()
    M12 = personal_add(M1, M2)
    end_time_personal = time() - start_time
    personal_time.append(end_time_personal)
    
```


```python
fig, ax = plt.subplots()

fig.set_figheight(15)
fig.set_figwidth(15)

ax.plot(n_list, personal_time, linewidth=2.0, label='Personal')
ax.plot(n_list, numpy_time, linewidth=2.0, label="Numpy")
ax.set_xlabel("Size of matrix")
ax.set_ylabel("Time (ms)")
ax.legend(('Personal','Numpy'),loc='upper right')
plt.show()
```


    
![png](output_7_0.png)
    


# Exercice 2:


```python
p=P([1,-2,0,1, 3, 5])
```


```python
def matrice_compagnon(polynome):
    degree = polynome.degree() 
    coef = p.coef * -1
    identite = np.eye(degree - 1)
    M = np.vstack((np.zeros(degree-1), identite))
    M = np.column_stack((M, coef[:len(coef)-1]))
    return M
    
```


```python
matrice_compagnon(p)
```




    array([[ 0.,  0.,  0.,  0., -1.],
           [ 1.,  0.,  0.,  0.,  2.],
           [ 0.,  1.,  0.,  0., -0.],
           [ 0.,  0.,  1.,  0., -1.],
           [ 0.,  0.,  0.,  1., -3.]])



# Exercice 3:


```python
df1 = pd.read_csv("archive/all_womens_foil_fencer_bio_data_May_13_2021_cleaned.csv")
df1
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
      <th>id</th>
      <th>name</th>
      <th>country_code</th>
      <th>country</th>
      <th>hand</th>
      <th>age</th>
      <th>url</th>
      <th>date_accessed</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>28761</td>
      <td>DVORKIN Mary</td>
      <td>ISR</td>
      <td>ISRAEL</td>
      <td>Left</td>
      <td>24</td>
      <td>https://fie.org/athletes/28761</td>
      <td>2021-05-13 21:42:17</td>
    </tr>
    <tr>
      <th>1</th>
      <td>43803</td>
      <td>SHI Yue</td>
      <td>CHN</td>
      <td>CHINA</td>
      <td>Right</td>
      <td>22</td>
      <td>https://fie.org/athletes/43803</td>
      <td>2021-05-13 21:35:13</td>
    </tr>
    <tr>
      <th>2</th>
      <td>46080</td>
      <td>TANG Nga Hei</td>
      <td>MAC</td>
      <td>MACAO, CHINA</td>
      <td>Right</td>
      <td>20</td>
      <td>https://fie.org/athletes/46080</td>
      <td>2021-05-13 21:46:21</td>
    </tr>
    <tr>
      <th>3</th>
      <td>46481</td>
      <td>WONAME Kelsey Victoria Afriyie</td>
      <td>GHA</td>
      <td>GHANA</td>
      <td>Right</td>
      <td>17</td>
      <td>https://fie.org/athletes/46481</td>
      <td>2021-05-13 21:48:14</td>
    </tr>
    <tr>
      <th>4</th>
      <td>47075</td>
      <td>BRECHERET Carolina</td>
      <td>BRA</td>
      <td>BRAZIL</td>
      <td>Right</td>
      <td>16</td>
      <td>https://fie.org/athletes/47075</td>
      <td>2021-05-13 21:50:07</td>
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
    </tr>
    <tr>
      <th>2103</th>
      <td>51177</td>
      <td>SAAVEDRA Ana</td>
      <td>MEX</td>
      <td>MEXICO</td>
      <td>Right</td>
      <td>16</td>
      <td>https://fie.org/athletes/51177</td>
      <td>2021-05-13 21:30:50</td>
    </tr>
    <tr>
      <th>2104</th>
      <td>40429</td>
      <td>MORE CHAVEZ Karine</td>
      <td>CUB</td>
      <td>CUBA</td>
      <td>Right</td>
      <td>25</td>
      <td>https://fie.org/athletes/40429</td>
      <td>2021-05-13 21:55:53</td>
    </tr>
    <tr>
      <th>2105</th>
      <td>51183</td>
      <td>ADALID Maria</td>
      <td>MEX</td>
      <td>MEXICO</td>
      <td>Right</td>
      <td>17</td>
      <td>https://fie.org/athletes/51183</td>
      <td>2021-05-13 21:30:51</td>
    </tr>
    <tr>
      <th>2106</th>
      <td>51186</td>
      <td>ESPINOSA Frida</td>
      <td>MEX</td>
      <td>MEXICO</td>
      <td>Right</td>
      <td>15</td>
      <td>https://fie.org/athletes/51186</td>
      <td>2021-05-13 21:30:52</td>
    </tr>
    <tr>
      <th>2107</th>
      <td>51193</td>
      <td>MARTINEZ Maggie</td>
      <td>MEX</td>
      <td>MEXICO</td>
      <td>Right</td>
      <td>18</td>
      <td>https://fie.org/athletes/51193</td>
      <td>2021-05-13 21:30:55</td>
    </tr>
  </tbody>
</table>
<p>2108 rows × 8 columns</p>
</div>




```python
# On filtre par pays (France)
df1 = df1[df1.country == "FRANCE"][["id", "name"]]
df1
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
      <th>id</th>
      <th>name</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>11</th>
      <td>20514</td>
      <td>THIBUS Ysaora</td>
    </tr>
    <tr>
      <th>52</th>
      <td>48818</td>
      <td>MARECHAL Jade</td>
    </tr>
    <tr>
      <th>55</th>
      <td>16054</td>
      <td>BLAZE Anita</td>
    </tr>
    <tr>
      <th>64</th>
      <td>39140</td>
      <td>CATARZI Constance</td>
    </tr>
    <tr>
      <th>80</th>
      <td>2860</td>
      <td>GUYART Astrid</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>1844</th>
      <td>32685</td>
      <td>OLIVIERO NATUREL Marguerite</td>
    </tr>
    <tr>
      <th>1914</th>
      <td>3072</td>
      <td>WILLARD Antoinette</td>
    </tr>
    <tr>
      <th>1978</th>
      <td>3048</td>
      <td>TISSIER Nicole</td>
    </tr>
    <tr>
      <th>1982</th>
      <td>38641</td>
      <td>VALLET-MODAINE Laurence</td>
    </tr>
    <tr>
      <th>2099</th>
      <td>26069</td>
      <td>ROUAS Maud</td>
    </tr>
  </tbody>
</table>
<p>88 rows × 2 columns</p>
</div>




```python
df2 = pd.read_csv("archive/all_womens_foil_fencer_rankings_data_May_13_2021_cleaned.csv")
df2
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
      <th>id</th>
      <th>weapon</th>
      <th>category</th>
      <th>season</th>
      <th>rank</th>
      <th>points</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>164</td>
      <td>Foil</td>
      <td>Veterans</td>
      <td>2016/2017</td>
      <td>78</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>164</td>
      <td>Foil</td>
      <td>Veterans</td>
      <td>2016/2017</td>
      <td>78</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>164</td>
      <td>Foil</td>
      <td>Veterans</td>
      <td>2017/2018</td>
      <td>37</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>164</td>
      <td>Foil</td>
      <td>Veterans</td>
      <td>2017/2018</td>
      <td>37</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>234</td>
      <td>Foil</td>
      <td>Senior</td>
      <td>2007/2008</td>
      <td>52</td>
      <td>56.0</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>10932</th>
      <td>53148</td>
      <td>Foil</td>
      <td>Cadet</td>
      <td>2021/2022</td>
      <td>25</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>10933</th>
      <td>53148</td>
      <td>Foil</td>
      <td>Junior</td>
      <td>2021/2022</td>
      <td>213</td>
      <td>2.5</td>
    </tr>
    <tr>
      <th>10934</th>
      <td>53151</td>
      <td>Foil</td>
      <td>Cadet</td>
      <td>2021/2022</td>
      <td>8</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>10935</th>
      <td>53161</td>
      <td>Foil</td>
      <td>Junior</td>
      <td>2021/2022</td>
      <td>287</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>10936</th>
      <td>53162</td>
      <td>Foil</td>
      <td>Junior</td>
      <td>2021/2022</td>
      <td>321</td>
      <td>0.0</td>
    </tr>
  </tbody>
</table>
<p>10937 rows × 6 columns</p>
</div>




```python
# On prend seulement les top ranking (8), qui utilisent le foil
df2 = df2[(~df2.season.isin(["2002/2003"])) & (df2["rank"] <= 8) & (df2["weapon"] == "Foil")][["id", "rank", "season"]]
df2
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
      <th>id</th>
      <th>rank</th>
      <th>season</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>144</th>
      <td>2839</td>
      <td>5</td>
      <td>2004/2005</td>
    </tr>
    <tr>
      <th>159</th>
      <td>2860</td>
      <td>7</td>
      <td>2003/2004</td>
    </tr>
    <tr>
      <th>169</th>
      <td>2860</td>
      <td>5</td>
      <td>2012/2013</td>
    </tr>
    <tr>
      <th>173</th>
      <td>2860</td>
      <td>8</td>
      <td>2016/2017</td>
    </tr>
    <tr>
      <th>180</th>
      <td>2928</td>
      <td>8</td>
      <td>2005/2006</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>10624</th>
      <td>51088</td>
      <td>2</td>
      <td>2021/2022</td>
    </tr>
    <tr>
      <th>10894</th>
      <td>52436</td>
      <td>4</td>
      <td>2021/2022</td>
    </tr>
    <tr>
      <th>10929</th>
      <td>53007</td>
      <td>1</td>
      <td>2021/2022</td>
    </tr>
    <tr>
      <th>10931</th>
      <td>53107</td>
      <td>7</td>
      <td>2021/2022</td>
    </tr>
    <tr>
      <th>10934</th>
      <td>53151</td>
      <td>8</td>
      <td>2021/2022</td>
    </tr>
  </tbody>
</table>
<p>490 rows × 3 columns</p>
</div>




```python
df3 = pd.read_csv("archive/all_womens_foil_tournament_data_May_13_2021_cleaned.csv")
df3
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
      <th>competition_ID</th>
      <th>season</th>
      <th>name</th>
      <th>category</th>
      <th>country</th>
      <th>start_date</th>
      <th>end_date</th>
      <th>weapon</th>
      <th>gender</th>
      <th>timezone</th>
      <th>url</th>
      <th>unique_ID</th>
      <th>missing_results_flag</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>121</td>
      <td>2021</td>
      <td>Grand Prix</td>
      <td>Senior</td>
      <td>QATAR</td>
      <td>2021-03-26</td>
      <td>2021-03-28</td>
      <td>Foil</td>
      <td>Womens</td>
      <td>Asia/Qatar</td>
      <td>https://fie.org/competitions/2021/121</td>
      <td>2021-121</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1</th>
      <td>41</td>
      <td>2017</td>
      <td>Tournoi international</td>
      <td>Junior</td>
      <td>GERMANY</td>
      <td>2016-10-28</td>
      <td>2016-10-28</td>
      <td>Foil</td>
      <td>Womens</td>
      <td>Europe/Berlin</td>
      <td>https://fie.org/competitions/2017/41</td>
      <td>2017-41</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>2</th>
      <td>800</td>
      <td>2015</td>
      <td>Championnats Panaméricains</td>
      <td>Senior</td>
      <td>CHILE</td>
      <td>2015-04-17</td>
      <td>2015-04-26</td>
      <td>Foil</td>
      <td>Womens</td>
      <td>America/Santiago</td>
      <td>https://fie.org/competitions/2015/800</td>
      <td>2015-800</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>3</th>
      <td>243</td>
      <td>2019</td>
      <td>Championnats du Monde</td>
      <td>Senior</td>
      <td>HUNGARY</td>
      <td>2019-07-16</td>
      <td>2019-07-19</td>
      <td>Foil</td>
      <td>Womens</td>
      <td>Europe/Budapest</td>
      <td>https://fie.org/competitions/2019/243</td>
      <td>2019-243</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>4</th>
      <td>237</td>
      <td>2016</td>
      <td>Championnats du monde juniors-cadets</td>
      <td>Cadet</td>
      <td>FRANCE</td>
      <td>2016-04-01</td>
      <td>2016-04-01</td>
      <td>Foil</td>
      <td>Womens</td>
      <td>Europe/Paris</td>
      <td>https://fie.org/competitions/2016/237</td>
      <td>2016-237</td>
      <td>NaN</td>
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
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>213</th>
      <td>118</td>
      <td>2015</td>
      <td>Coupe du Monde</td>
      <td>Senior</td>
      <td>FRANCE</td>
      <td>2014-11-07</td>
      <td>2014-11-08</td>
      <td>Foil</td>
      <td>Womens</td>
      <td>Europe/Paris</td>
      <td>https://fie.org/competitions/2015/118</td>
      <td>2015-118</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>214</th>
      <td>1014</td>
      <td>2015</td>
      <td>Championnats asiatiques</td>
      <td>Senior</td>
      <td>SINGAPORE</td>
      <td>2015-06-25</td>
      <td>2015-06-30</td>
      <td>Foil</td>
      <td>Womens</td>
      <td>Asia/Singapore</td>
      <td>https://fie.org/competitions/2015/1014</td>
      <td>2015-1014</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>215</th>
      <td>122</td>
      <td>2018</td>
      <td>Reinhold-Würth-Cup</td>
      <td>Senior</td>
      <td>GERMANY</td>
      <td>2018-04-27</td>
      <td>2018-04-28</td>
      <td>Foil</td>
      <td>Womens</td>
      <td>Europe/Berlin</td>
      <td>https://fie.org/competitions/2018/122</td>
      <td>2018-122</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>216</th>
      <td>127</td>
      <td>2016</td>
      <td>The Artus Court PKO BP</td>
      <td>Senior</td>
      <td>POLAND</td>
      <td>2016-01-15</td>
      <td>2016-01-16</td>
      <td>Foil</td>
      <td>Womens</td>
      <td>Europe/Warsaw</td>
      <td>https://fie.org/competitions/2016/127</td>
      <td>2016-127</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>217</th>
      <td>1218</td>
      <td>2018</td>
      <td>Tournoi satellite</td>
      <td>Senior</td>
      <td>TURKEY</td>
      <td>2017-12-09</td>
      <td>2017-12-09</td>
      <td>Foil</td>
      <td>Womens</td>
      <td>Europe/Istanbul</td>
      <td>https://fie.org/competitions/2018/1218</td>
      <td>2018-1218</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
<p>218 rows × 13 columns</p>
</div>




```python
# On prend seulement les competitions "Senior"
df3 = df3[df3.category == "Senior"]
df3 = df3[["category", "unique_ID"]]
df3.columns=["category", "tournament_ID"]
df3
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
      <th>category</th>
      <th>tournament_ID</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Senior</td>
      <td>2021-121</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Senior</td>
      <td>2015-800</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Senior</td>
      <td>2019-243</td>
    </tr>
    <tr>
      <th>6</th>
      <td>Senior</td>
      <td>2018-586</td>
    </tr>
    <tr>
      <th>7</th>
      <td>Senior</td>
      <td>2021-1061</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>213</th>
      <td>Senior</td>
      <td>2015-118</td>
    </tr>
    <tr>
      <th>214</th>
      <td>Senior</td>
      <td>2015-1014</td>
    </tr>
    <tr>
      <th>215</th>
      <td>Senior</td>
      <td>2018-122</td>
    </tr>
    <tr>
      <th>216</th>
      <td>Senior</td>
      <td>2016-127</td>
    </tr>
    <tr>
      <th>217</th>
      <td>Senior</td>
      <td>2018-1218</td>
    </tr>
  </tbody>
</table>
<p>115 rows × 2 columns</p>
</div>




```python
df4 = pd.read_csv("archive/all_womens_foil_bout_data_May_13_2021_cleaned.csv")
df4
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
      <th>fencer_ID</th>
      <th>opp_ID</th>
      <th>fencer_age</th>
      <th>opp_age</th>
      <th>fencer_score</th>
      <th>opp_score</th>
      <th>winner_ID</th>
      <th>fencer_curr_pts</th>
      <th>opp_curr_pts</th>
      <th>tournament_ID</th>
      <th>pool_ID</th>
      <th>upset</th>
      <th>date</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>36796</td>
      <td>19574</td>
      <td>23</td>
      <td>28</td>
      <td>5</td>
      <td>1</td>
      <td>36796</td>
      <td>12.5</td>
      <td>7.50</td>
      <td>2021-121</td>
      <td>1</td>
      <td>False</td>
      <td>2021-03-26</td>
    </tr>
    <tr>
      <th>1</th>
      <td>36796</td>
      <td>42147</td>
      <td>23</td>
      <td>19</td>
      <td>5</td>
      <td>2</td>
      <td>36796</td>
      <td>12.5</td>
      <td>0.75</td>
      <td>2021-121</td>
      <td>1</td>
      <td>False</td>
      <td>2021-03-26</td>
    </tr>
    <tr>
      <th>2</th>
      <td>36796</td>
      <td>49116</td>
      <td>23</td>
      <td>21</td>
      <td>5</td>
      <td>2</td>
      <td>36796</td>
      <td>12.5</td>
      <td>22.25</td>
      <td>2021-121</td>
      <td>1</td>
      <td>True</td>
      <td>2021-03-26</td>
    </tr>
    <tr>
      <th>3</th>
      <td>36796</td>
      <td>39631</td>
      <td>23</td>
      <td>18</td>
      <td>5</td>
      <td>4</td>
      <td>36796</td>
      <td>12.5</td>
      <td>23.00</td>
      <td>2021-121</td>
      <td>1</td>
      <td>True</td>
      <td>2021-03-26</td>
    </tr>
    <tr>
      <th>4</th>
      <td>36796</td>
      <td>23447</td>
      <td>23</td>
      <td>27</td>
      <td>4</td>
      <td>5</td>
      <td>23447</td>
      <td>12.5</td>
      <td>79.00</td>
      <td>2021-121</td>
      <td>1</td>
      <td>False</td>
      <td>2021-03-26</td>
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
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>49126</th>
      <td>45679</td>
      <td>32336</td>
      <td>34</td>
      <td>25</td>
      <td>5</td>
      <td>2</td>
      <td>45679</td>
      <td>0.0</td>
      <td>0.00</td>
      <td>2018-1218</td>
      <td>5</td>
      <td>False</td>
      <td>2017-12-09</td>
    </tr>
    <tr>
      <th>49127</th>
      <td>45679</td>
      <td>35935</td>
      <td>34</td>
      <td>22</td>
      <td>4</td>
      <td>5</td>
      <td>35935</td>
      <td>0.0</td>
      <td>3.00</td>
      <td>2018-1218</td>
      <td>5</td>
      <td>False</td>
      <td>2017-12-09</td>
    </tr>
    <tr>
      <th>49128</th>
      <td>36591</td>
      <td>32336</td>
      <td>22</td>
      <td>25</td>
      <td>2</td>
      <td>5</td>
      <td>32336</td>
      <td>0.0</td>
      <td>0.00</td>
      <td>2018-1218</td>
      <td>5</td>
      <td>False</td>
      <td>2017-12-09</td>
    </tr>
    <tr>
      <th>49129</th>
      <td>36591</td>
      <td>35935</td>
      <td>22</td>
      <td>22</td>
      <td>1</td>
      <td>5</td>
      <td>35935</td>
      <td>0.0</td>
      <td>3.00</td>
      <td>2018-1218</td>
      <td>5</td>
      <td>False</td>
      <td>2017-12-09</td>
    </tr>
    <tr>
      <th>49130</th>
      <td>32336</td>
      <td>35935</td>
      <td>25</td>
      <td>22</td>
      <td>0</td>
      <td>5</td>
      <td>35935</td>
      <td>0.0</td>
      <td>3.00</td>
      <td>2018-1218</td>
      <td>5</td>
      <td>False</td>
      <td>2017-12-09</td>
    </tr>
  </tbody>
</table>
<p>49131 rows × 13 columns</p>
</div>




```python
df4 = df4[["fencer_ID", "tournament_ID"]]
df4.columns = ["id", "tournament_ID"]

```


```python
# On merge les 4 DF, pour avoir 1 qui nous permet faire le graphique.
df = pd.merge(df1, df2, on="id")[["id", "name", "rank", "season"]]
df22 = pd.merge(df3, df4, on="tournament_ID")
df = pd.merge(df22, df, on="id")
df = df[["name", "rank", "season"]]
df.drop_duplicates(subset=None, keep="first", inplace=True)
df = df.sort_values(by=["name", "season"])
df["season"] = pd.Categorical(df.season)
df["season_cat"] = df.season.cat.codes
df
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
      <th>name</th>
      <th>rank</th>
      <th>season</th>
      <th>season_cat</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>88</th>
      <td>BLAZE Anita</td>
      <td>7</td>
      <td>2010/2011</td>
      <td>5</td>
    </tr>
    <tr>
      <th>902</th>
      <td>GEBET Gaelle</td>
      <td>5</td>
      <td>2004/2005</td>
      <td>1</td>
    </tr>
    <tr>
      <th>946</th>
      <td>GUILLAUME Meredith</td>
      <td>1</td>
      <td>2014/2015</td>
      <td>9</td>
    </tr>
    <tr>
      <th>210</th>
      <td>GUYART Astrid</td>
      <td>7</td>
      <td>2003/2004</td>
      <td>0</td>
    </tr>
    <tr>
      <th>211</th>
      <td>GUYART Astrid</td>
      <td>5</td>
      <td>2012/2013</td>
      <td>7</td>
    </tr>
    <tr>
      <th>212</th>
      <td>GUYART Astrid</td>
      <td>8</td>
      <td>2016/2017</td>
      <td>10</td>
    </tr>
    <tr>
      <th>866</th>
      <td>HUIN Julie</td>
      <td>3</td>
      <td>2005/2006</td>
      <td>2</td>
    </tr>
    <tr>
      <th>867</th>
      <td>HUIN Julie</td>
      <td>8</td>
      <td>2006/2007</td>
      <td>3</td>
    </tr>
    <tr>
      <th>0</th>
      <td>LACHERAY Eva</td>
      <td>5</td>
      <td>2018/2019</td>
      <td>12</td>
    </tr>
    <tr>
      <th>1</th>
      <td>LACHERAY Eva</td>
      <td>4</td>
      <td>2020/2021</td>
      <td>13</td>
    </tr>
    <tr>
      <th>408</th>
      <td>LUMINET Clarisse</td>
      <td>7</td>
      <td>2012/2013</td>
      <td>7</td>
    </tr>
    <tr>
      <th>965</th>
      <td>MAITREJEAN Corinne</td>
      <td>8</td>
      <td>2005/2006</td>
      <td>2</td>
    </tr>
    <tr>
      <th>966</th>
      <td>MAITREJEAN Corinne</td>
      <td>7</td>
      <td>2008/2009</td>
      <td>4</td>
    </tr>
    <tr>
      <th>967</th>
      <td>MAITREJEAN Corinne</td>
      <td>6</td>
      <td>2010/2011</td>
      <td>5</td>
    </tr>
    <tr>
      <th>968</th>
      <td>MAITREJEAN Corinne</td>
      <td>8</td>
      <td>2011/2012</td>
      <td>6</td>
    </tr>
    <tr>
      <th>969</th>
      <td>MAITREJEAN Corinne</td>
      <td>7</td>
      <td>2012/2013</td>
      <td>7</td>
    </tr>
    <tr>
      <th>434</th>
      <td>MIENVILLE Julie</td>
      <td>6</td>
      <td>2013/2014</td>
      <td>8</td>
    </tr>
    <tr>
      <th>526</th>
      <td>MPAH-NJANGA Jeromine</td>
      <td>8</td>
      <td>2013/2014</td>
      <td>8</td>
    </tr>
    <tr>
      <th>612</th>
      <td>RANVIER Pauline</td>
      <td>8</td>
      <td>2012/2013</td>
      <td>7</td>
    </tr>
    <tr>
      <th>613</th>
      <td>RANVIER Pauline</td>
      <td>3</td>
      <td>2014/2015</td>
      <td>9</td>
    </tr>
    <tr>
      <th>830</th>
      <td>THIBUS Ysaora</td>
      <td>8</td>
      <td>2011/2012</td>
      <td>6</td>
    </tr>
    <tr>
      <th>831</th>
      <td>THIBUS Ysaora</td>
      <td>5</td>
      <td>2016/2017</td>
      <td>10</td>
    </tr>
    <tr>
      <th>832</th>
      <td>THIBUS Ysaora</td>
      <td>5</td>
      <td>2017/2018</td>
      <td>11</td>
    </tr>
    <tr>
      <th>833</th>
      <td>THIBUS Ysaora</td>
      <td>6</td>
      <td>2018/2019</td>
      <td>12</td>
    </tr>
    <tr>
      <th>834</th>
      <td>THIBUS Ysaora</td>
      <td>6</td>
      <td>2020/2021</td>
      <td>13</td>
    </tr>
    <tr>
      <th>835</th>
      <td>THIBUS Ysaora</td>
      <td>3</td>
      <td>2021/2022</td>
      <td>14</td>
    </tr>
  </tbody>
</table>
</div>




```python
# On regroupe selon le name
d = dict(list(df.groupby("name")))
d["THIBUS Ysaora"].sort_values(by="season_cat")
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
      <th>name</th>
      <th>rank</th>
      <th>season</th>
      <th>season_cat</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>830</th>
      <td>THIBUS Ysaora</td>
      <td>8</td>
      <td>2011/2012</td>
      <td>6</td>
    </tr>
    <tr>
      <th>831</th>
      <td>THIBUS Ysaora</td>
      <td>5</td>
      <td>2016/2017</td>
      <td>10</td>
    </tr>
    <tr>
      <th>832</th>
      <td>THIBUS Ysaora</td>
      <td>5</td>
      <td>2017/2018</td>
      <td>11</td>
    </tr>
    <tr>
      <th>833</th>
      <td>THIBUS Ysaora</td>
      <td>6</td>
      <td>2018/2019</td>
      <td>12</td>
    </tr>
    <tr>
      <th>834</th>
      <td>THIBUS Ysaora</td>
      <td>6</td>
      <td>2020/2021</td>
      <td>13</td>
    </tr>
    <tr>
      <th>835</th>
      <td>THIBUS Ysaora</td>
      <td>3</td>
      <td>2021/2022</td>
      <td>14</td>
    </tr>
  </tbody>
</table>
</div>




```python
fig, ax = plt.subplots()
fig.set_figheight(15)
fig.set_figwidth(15)

labels = list(df.sort_values(by="season")["season"].unique())


for key, data in d.items():
    data =  data.sort_values(by=["season_cat"])
    ax.plot(data.season_cat, data["rank"], linewidth=2.0, label=data.name)

plt.xticks(range(0,len(labels)), labels, rotation ='vertical')

ax.set_xlabel("Year Competition")
ax.set_ylabel("Rank")
ax.plot
ax.legend(df.name.unique(),loc='upper right')
# On inverse pour avoir le rank 1 en premier
plt.gca().invert_yaxis()
plt.show()
```


    
![png](output_23_0.png)
    


# Exercice 4

## Exercice 1:


```python
pingouins = sns.load_dataset("penguins")
```


```python
pingouins
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
      <th>species</th>
      <th>island</th>
      <th>bill_length_mm</th>
      <th>bill_depth_mm</th>
      <th>flipper_length_mm</th>
      <th>body_mass_g</th>
      <th>sex</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Adelie</td>
      <td>Torgersen</td>
      <td>39.1</td>
      <td>18.7</td>
      <td>181.0</td>
      <td>3750.0</td>
      <td>Male</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Adelie</td>
      <td>Torgersen</td>
      <td>39.5</td>
      <td>17.4</td>
      <td>186.0</td>
      <td>3800.0</td>
      <td>Female</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Adelie</td>
      <td>Torgersen</td>
      <td>40.3</td>
      <td>18.0</td>
      <td>195.0</td>
      <td>3250.0</td>
      <td>Female</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Adelie</td>
      <td>Torgersen</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Adelie</td>
      <td>Torgersen</td>
      <td>36.7</td>
      <td>19.3</td>
      <td>193.0</td>
      <td>3450.0</td>
      <td>Female</td>
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
    </tr>
    <tr>
      <th>339</th>
      <td>Gentoo</td>
      <td>Biscoe</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>340</th>
      <td>Gentoo</td>
      <td>Biscoe</td>
      <td>46.8</td>
      <td>14.3</td>
      <td>215.0</td>
      <td>4850.0</td>
      <td>Female</td>
    </tr>
    <tr>
      <th>341</th>
      <td>Gentoo</td>
      <td>Biscoe</td>
      <td>50.4</td>
      <td>15.7</td>
      <td>222.0</td>
      <td>5750.0</td>
      <td>Male</td>
    </tr>
    <tr>
      <th>342</th>
      <td>Gentoo</td>
      <td>Biscoe</td>
      <td>45.2</td>
      <td>14.8</td>
      <td>212.0</td>
      <td>5200.0</td>
      <td>Female</td>
    </tr>
    <tr>
      <th>343</th>
      <td>Gentoo</td>
      <td>Biscoe</td>
      <td>49.9</td>
      <td>16.1</td>
      <td>213.0</td>
      <td>5400.0</td>
      <td>Male</td>
    </tr>
  </tbody>
</table>
<p>344 rows × 7 columns</p>
</div>



## Exercice 2:


```python
pingouins.describe()
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
      <th>bill_length_mm</th>
      <th>bill_depth_mm</th>
      <th>flipper_length_mm</th>
      <th>body_mass_g</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>count</th>
      <td>342.000000</td>
      <td>342.000000</td>
      <td>342.000000</td>
      <td>342.000000</td>
    </tr>
    <tr>
      <th>mean</th>
      <td>43.921930</td>
      <td>17.151170</td>
      <td>200.915205</td>
      <td>4201.754386</td>
    </tr>
    <tr>
      <th>std</th>
      <td>5.459584</td>
      <td>1.974793</td>
      <td>14.061714</td>
      <td>801.954536</td>
    </tr>
    <tr>
      <th>min</th>
      <td>32.100000</td>
      <td>13.100000</td>
      <td>172.000000</td>
      <td>2700.000000</td>
    </tr>
    <tr>
      <th>25%</th>
      <td>39.225000</td>
      <td>15.600000</td>
      <td>190.000000</td>
      <td>3550.000000</td>
    </tr>
    <tr>
      <th>50%</th>
      <td>44.450000</td>
      <td>17.300000</td>
      <td>197.000000</td>
      <td>4050.000000</td>
    </tr>
    <tr>
      <th>75%</th>
      <td>48.500000</td>
      <td>18.700000</td>
      <td>213.000000</td>
      <td>4750.000000</td>
    </tr>
    <tr>
      <th>max</th>
      <td>59.600000</td>
      <td>21.500000</td>
      <td>231.000000</td>
      <td>6300.000000</td>
    </tr>
  </tbody>
</table>
</div>




```python
pingouins.info()
```

    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 344 entries, 0 to 343
    Data columns (total 7 columns):
     #   Column             Non-Null Count  Dtype  
    ---  ------             --------------  -----  
     0   species            344 non-null    object 
     1   island             344 non-null    object 
     2   bill_length_mm     342 non-null    float64
     3   bill_depth_mm      342 non-null    float64
     4   flipper_length_mm  342 non-null    float64
     5   body_mass_g        342 non-null    float64
     6   sex                333 non-null    object 
    dtypes: float64(4), object(3)
    memory usage: 18.9+ KB


## Exercice 3:


```python
pingouins.corr()
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
      <th>bill_length_mm</th>
      <th>bill_depth_mm</th>
      <th>flipper_length_mm</th>
      <th>body_mass_g</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>bill_length_mm</th>
      <td>1.000000</td>
      <td>-0.235053</td>
      <td>0.656181</td>
      <td>0.595110</td>
    </tr>
    <tr>
      <th>bill_depth_mm</th>
      <td>-0.235053</td>
      <td>1.000000</td>
      <td>-0.583851</td>
      <td>-0.471916</td>
    </tr>
    <tr>
      <th>flipper_length_mm</th>
      <td>0.656181</td>
      <td>-0.583851</td>
      <td>1.000000</td>
      <td>0.871202</td>
    </tr>
    <tr>
      <th>body_mass_g</th>
      <td>0.595110</td>
      <td>-0.471916</td>
      <td>0.871202</td>
      <td>1.000000</td>
    </tr>
  </tbody>
</table>
</div>



- body_mass_g et flipper_lenght_mm ont le taux de correlation le plus haut (0.87)
- flipper_length_mm et bill_lenght_mm ont une correlation de (0.65)

## Exercice 4


```python
pingouins.species.unique()
```




    array(['Adelie', 'Chinstrap', 'Gentoo'], dtype=object)




```python
pingouins.columns
```




    Index(['species', 'island', 'bill_length_mm', 'bill_depth_mm',
           'flipper_length_mm', 'body_mass_g', 'sex'],
          dtype='object')




```python
data = pingouins[["species", "bill_length_mm", "bill_depth_mm", "flipper_length_mm"]]
```


```python
sns.pairplot(data, hue="species")
```




    <seaborn.axisgrid.PairGrid at 0x7f2500b97940>




    
![png](output_38_1.png)
    


- On voit en premier que les especes ne sont pas represente en meme quantites dans le DataSet.
- Dans le graphique entre bill_depth_mm et flipper_lenght_mm, on voit que les especes Adelie et Chinstrap, son tres rassemblente. 
- On voit une difference notable entre Gentoo et Adelie dans tous les aspects.
