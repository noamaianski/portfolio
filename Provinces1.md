## Creating a DataFrame from a Dictionary
#### Below is a dictionary I made of the provinces of Canada, their respective capital city, their total area (sum of land area and internal water area; in square kilometres), their population (from 2016), and the count of active cases of COVID-19 as of October 31, 2020. 
##### Note: the data was taken from the Government of Canada's website and Wikipedia. 


```python
dict = {
	"Province":["Alberta", "British Columbia", "Manitoba", "New Brunswick", "Newfoundland and Labrador", "Nova Scotia", "Ontario", "Prince Edward Island", "Quebec", "Saskatchewan"],
	"Capital":["Edmonton", "Victoria", "Winnipeg", "Fredericton", "St. John's", "Halifax", "Toronto", "Charlottetown", "Québec City", "Regina"],
	"Area":[661848, 944735, 647797, 72908, 405212, 55284, 1076395, 5660, 1542056, 651036],
	"Population": [4067175, 4648055, 1278365, 747101, 519716, 923598, 13448494, 142907, 8164361, 1098352],
	"Active cases": [5172, 2448, 3010, 38, 3, 11, 7877, 0, 9194, 739] }

```

#### It's difficult to read data in this format, and so I have converted the dictionary in to a DataFrame, with the index set as the province. 


```python
import pandas as pd
province = pd.DataFrame(dict)
```


```python
province.index=province["Province"]
del province["Province"]
```


```python
print(province)
```

                                     Capital     Area  Population  Active cases
    Province                                                                   
    Alberta                         Edmonton   661848     4067175          5172
    British Columbia                Victoria   944735     4648055          2448
    Manitoba                        Winnipeg   647797     1278365          3010
    New Brunswick                Fredericton    72908      747101            38
    Newfoundland and Labrador     St. John's   405212      519716             3
    Nova Scotia                      Halifax    55284      923598            11
    Ontario                          Toronto  1076395    13448494          7877
    Prince Edward Island       Charlottetown     5660      142907             0
    Quebec                       Québec City  1542056     8164361          9194
    Saskatchewan                      Regina   651036     1098352           739



```python

```
