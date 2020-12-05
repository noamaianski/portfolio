## Dr. Ignaz Semmelweis
Here, I reanalyzed the medical data Dr. Ignaz Semmelweis collected to show the necessity of hand-washing. I followed instructions written by Rasmus Bååth from DataCamp Projects. 

## Load in the Dataset
The table below shows the number of births and deaths, from 1841 to 1846, at the two clinics in Vienna General Hospital. 


```python
import pandas as pd
yearly = pd.read_csv("yearly_deaths_by_clinic.csv")
print(yearly)
```

        year  births  deaths    clinic
    0   1841    3036     237  clinic 1
    1   1842    3287     518  clinic 1
    2   1843    3060     274  clinic 1
    3   1844    3157     260  clinic 1
    4   1845    3492     241  clinic 1
    5   1846    4010     459  clinic 1
    6   1841    2442      86  clinic 2
    7   1842    2659     202  clinic 2
    8   1843    2739     164  clinic 2
    9   1844    2956      68  clinic 2
    10  1845    3241      66  clinic 2
    11  1846    3754     105  clinic 2


### Proportion of Deaths


```python
# Calculate proportion of deaths per number of births and add this data as a new column to the tables below: 
yearly["proportion_deaths"] = yearly["deaths"] / yearly["births"]
```


```python
# Extract clinic 1 data into yearly1
yearly1 = yearly[yearly["clinic"] == "clinic 1"]

# Print out yearly1
yearly1
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
      <th>year</th>
      <th>births</th>
      <th>deaths</th>
      <th>clinic</th>
      <th>proportion_deaths</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1841</td>
      <td>3036</td>
      <td>237</td>
      <td>clinic 1</td>
      <td>0.078063</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1842</td>
      <td>3287</td>
      <td>518</td>
      <td>clinic 1</td>
      <td>0.157591</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1843</td>
      <td>3060</td>
      <td>274</td>
      <td>clinic 1</td>
      <td>0.089542</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1844</td>
      <td>3157</td>
      <td>260</td>
      <td>clinic 1</td>
      <td>0.082357</td>
    </tr>
    <tr>
      <th>4</th>
      <td>1845</td>
      <td>3492</td>
      <td>241</td>
      <td>clinic 1</td>
      <td>0.069015</td>
    </tr>
    <tr>
      <th>5</th>
      <td>1846</td>
      <td>4010</td>
      <td>459</td>
      <td>clinic 1</td>
      <td>0.114464</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Extract clinic 2 data into yearly2
yearly2 = yearly[yearly["clinic"] == "clinic 2"]

# Print out yearly2
yearly2
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
      <th>year</th>
      <th>births</th>
      <th>deaths</th>
      <th>clinic</th>
      <th>proportion_deaths</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>6</th>
      <td>1841</td>
      <td>2442</td>
      <td>86</td>
      <td>clinic 2</td>
      <td>0.035217</td>
    </tr>
    <tr>
      <th>7</th>
      <td>1842</td>
      <td>2659</td>
      <td>202</td>
      <td>clinic 2</td>
      <td>0.075968</td>
    </tr>
    <tr>
      <th>8</th>
      <td>1843</td>
      <td>2739</td>
      <td>164</td>
      <td>clinic 2</td>
      <td>0.059876</td>
    </tr>
    <tr>
      <th>9</th>
      <td>1844</td>
      <td>2956</td>
      <td>68</td>
      <td>clinic 2</td>
      <td>0.023004</td>
    </tr>
    <tr>
      <th>10</th>
      <td>1845</td>
      <td>3241</td>
      <td>66</td>
      <td>clinic 2</td>
      <td>0.020364</td>
    </tr>
    <tr>
      <th>11</th>
      <td>1846</td>
      <td>3754</td>
      <td>105</td>
      <td>clinic 2</td>
      <td>0.027970</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Plot the yearly proportion of deaths at both clinics (clinic 1 and clinic 2)
ax = yearly1.plot(x="year", y="proportion_deaths", label="Clinic 1")
yearly2.plot(x="year", y="proportion_deaths", label="Clinic 2", ax=ax, color='red')
ax.set_title('Proportion of Deaths in Vienna General Hospital')
ax.set_ylabel("Proportion deaths")
```




    Text(0, 0.5, 'Proportion deaths')






    
![png](handwashing_files/handwashing_7_1.png)
    



## Clinic 1

Note from the above figure that the yearly proportion of deaths in Clinic 1 is much higher than in Clinic 2. There was one difference between the two clinics: medical students worked in Clinic 1, while midwives students worked in Clinic 2. Midwives exclusively assisted women giving birth, but the medical students also studied corpses. Dr. Semmelweis hypothesized that the medical students are spreading something from the corpses, and that this thing is causing an alarming amount of women to die. In the summer of 1847 (1847-06-01), Dr. Semmelweis decided to make washing hands mandatory – which was a controversial decision at the time. We will now examine monthly data from Clinic 1 to see if his decision had an effect on the proprotion of deaths.



```python
# Read datasets/monthly_deaths.csv into monthly
monthly = pd.read_csv("monthly_deaths.csv", parse_dates=["date"])

# Calculate proportion of deaths per number of births
monthly["proportion_deaths"] = monthly["deaths"] / monthly["births"]

# Print out the first rows in monthly
monthly.head(10)
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
      <th>date</th>
      <th>births</th>
      <th>deaths</th>
      <th>proportion_deaths</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1841-01-01</td>
      <td>254</td>
      <td>37</td>
      <td>0.145669</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1841-02-01</td>
      <td>239</td>
      <td>18</td>
      <td>0.075314</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1841-03-01</td>
      <td>277</td>
      <td>12</td>
      <td>0.043321</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1841-04-01</td>
      <td>255</td>
      <td>4</td>
      <td>0.015686</td>
    </tr>
    <tr>
      <th>4</th>
      <td>1841-05-01</td>
      <td>255</td>
      <td>2</td>
      <td>0.007843</td>
    </tr>
    <tr>
      <th>5</th>
      <td>1841-06-01</td>
      <td>200</td>
      <td>10</td>
      <td>0.050000</td>
    </tr>
    <tr>
      <th>6</th>
      <td>1841-07-01</td>
      <td>190</td>
      <td>16</td>
      <td>0.084211</td>
    </tr>
    <tr>
      <th>7</th>
      <td>1841-08-01</td>
      <td>222</td>
      <td>3</td>
      <td>0.013514</td>
    </tr>
    <tr>
      <th>8</th>
      <td>1841-09-01</td>
      <td>213</td>
      <td>4</td>
      <td>0.018779</td>
    </tr>
    <tr>
      <th>9</th>
      <td>1841-10-01</td>
      <td>236</td>
      <td>26</td>
      <td>0.110169</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Date when handwashing was made mandatory
handwashing_start = pd.to_datetime('1847-06-01')

# Split monthly into before and after handwashing_start
before_washing = monthly[monthly["date"] < handwashing_start]
after_washing = monthly[monthly["date"] >= handwashing_start]

# Plot monthly proportion of deaths before and after handwashing
ax = before_washing.plot(x="date", y="proportion_deaths",
                         label="Before handwashing")
after_washing.plot(x="date", y="proportion_deaths",
                   label="After handwashing", ax=ax, color='green')
ax.set_title('Proportion of Deaths in Clinic 1 of the Vienna General Hospital')
ax.set_ylabel("Proportion deaths")
```




    Text(0, 0.5, 'Proportion deaths')






    
![png](handwashing_files/handwashing_10_1.png)
    




```python
# Difference in mean monthly proportion of deaths due to handwashing
before_proportion = before_washing["proportion_deaths"]
after_proportion = after_washing["proportion_deaths"]
mean_diff = after_proportion.mean() - before_proportion.mean()
mean_diff
```




    -0.0839566075118334



## Conclusion
The figure in cell 11, shows that handwashing had a huge effect on the proportion of deaths. On average, it reduced the monthly proportion of deaths by 8 percentage points. 
