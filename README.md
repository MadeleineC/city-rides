
Trends

1: Relative to suburban and rural communities, there are more rides in urban areas and the average fare is cheaper.  Similarly, suburban communities have cheaper average fares and more rides compared to their rural counterparts.

2: The number of drivers in urban areas were disproportionately greater (77.9%) as compared to the percentage of rides that were provided in urban areas (68.4%).  On the other hand, a smaller percentage of drivers provided a larger percentage of rides in suburban and rural areas.

3: Just under 2/3 of revenue (63%) comes from rides provided in urban areas, 30% from rides provided in suburban areas and only 6.7% from rides provided in rural areas.




```python
import matplotlib.pyplot as plt
import pandas as pd
import numpy as np
import os
import seaborn as sns
```


```python
city_data = pd.read_csv("raw_data/city_data.csv")
#city_data.head()
city_data = city_data.drop(city_data.index[[100]])
city_data = city_data.sort_values("city")
city_data = city_data.set_index('city')
city_data.head()
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
      <th>driver_count</th>
      <th>type</th>
    </tr>
    <tr>
      <th>city</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Alvarezhaven</th>
      <td>21</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>Alyssaberg</th>
      <td>67</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>Anitamouth</th>
      <td>16</td>
      <td>Suburban</td>
    </tr>
    <tr>
      <th>Antoniomouth</th>
      <td>21</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>Aprilchester</th>
      <td>49</td>
      <td>Urban</td>
    </tr>
  </tbody>
</table>
</div>




```python
# city_data["ride_count"] = ""
# city_data["mean_fare"] = ""
city_data["color"] = ""
city_data.head()
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
      <th>driver_count</th>
      <th>type</th>
      <th>color</th>
    </tr>
    <tr>
      <th>city</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Alvarezhaven</th>
      <td>21</td>
      <td>Urban</td>
      <td></td>
    </tr>
    <tr>
      <th>Alyssaberg</th>
      <td>67</td>
      <td>Urban</td>
      <td></td>
    </tr>
    <tr>
      <th>Anitamouth</th>
      <td>16</td>
      <td>Suburban</td>
      <td></td>
    </tr>
    <tr>
      <th>Antoniomouth</th>
      <td>21</td>
      <td>Urban</td>
      <td></td>
    </tr>
    <tr>
      <th>Aprilchester</th>
      <td>49</td>
      <td>Urban</td>
      <td></td>
    </tr>
  </tbody>
</table>
</div>




```python
color_dict = {"Rural":"Gold", "Suburban": "lightskyblue", "Urban":"lightcoral"}
for index, row in city_data.iterrows():
    if row["type"] == "Urban":
        city_data["color"][index] = color_dict["Urban"]
    elif row["type"] == "Suburban":
        city_data["color"][index] = color_dict["Suburban"]
    else:
        city_data["color"][index] = color_dict["Rural"]
city_data.head()
        
```

    /Users/Madeleine/anaconda3/envs/PythonData/lib/python3.6/site-packages/ipykernel/__main__.py:4: SettingWithCopyWarning: 
    A value is trying to be set on a copy of a slice from a DataFrame
    
    See the caveats in the documentation: http://pandas.pydata.org/pandas-docs/stable/indexing.html#indexing-view-versus-copy
    /Users/Madeleine/anaconda3/envs/PythonData/lib/python3.6/site-packages/ipykernel/__main__.py:6: SettingWithCopyWarning: 
    A value is trying to be set on a copy of a slice from a DataFrame
    
    See the caveats in the documentation: http://pandas.pydata.org/pandas-docs/stable/indexing.html#indexing-view-versus-copy
    /Users/Madeleine/anaconda3/envs/PythonData/lib/python3.6/site-packages/ipykernel/__main__.py:8: SettingWithCopyWarning: 
    A value is trying to be set on a copy of a slice from a DataFrame
    
    See the caveats in the documentation: http://pandas.pydata.org/pandas-docs/stable/indexing.html#indexing-view-versus-copy





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
      <th>driver_count</th>
      <th>type</th>
      <th>color</th>
    </tr>
    <tr>
      <th>city</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Alvarezhaven</th>
      <td>21</td>
      <td>Urban</td>
      <td>lightcoral</td>
    </tr>
    <tr>
      <th>Alyssaberg</th>
      <td>67</td>
      <td>Urban</td>
      <td>lightcoral</td>
    </tr>
    <tr>
      <th>Anitamouth</th>
      <td>16</td>
      <td>Suburban</td>
      <td>lightskyblue</td>
    </tr>
    <tr>
      <th>Antoniomouth</th>
      <td>21</td>
      <td>Urban</td>
      <td>lightcoral</td>
    </tr>
    <tr>
      <th>Aprilchester</th>
      <td>49</td>
      <td>Urban</td>
      <td>lightcoral</td>
    </tr>
  </tbody>
</table>
</div>




```python
ride_data = pd.read_csv("raw_data/ride_data.csv")
#drop extra data point
ride_data.head()
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
      <th>city</th>
      <th>date</th>
      <th>fare</th>
      <th>ride_id</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Sarabury</td>
      <td>2016-01-16 13:49:27</td>
      <td>38.35</td>
      <td>5403689035038</td>
    </tr>
    <tr>
      <th>1</th>
      <td>South Roy</td>
      <td>2016-01-02 18:42:34</td>
      <td>17.49</td>
      <td>4036272335942</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Wiseborough</td>
      <td>2016-01-21 17:35:29</td>
      <td>44.18</td>
      <td>3645042422587</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Spencertown</td>
      <td>2016-07-31 14:53:22</td>
      <td>6.87</td>
      <td>2242596575892</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Nguyenbury</td>
      <td>2016-07-09 04:42:44</td>
      <td>6.28</td>
      <td>1543057793673</td>
    </tr>
  </tbody>
</table>
</div>




```python
grouped_ride_data = ride_data.groupby("city")
city_data["mean_fare"] = grouped_ride_data["fare"].mean()
city_data["ride_count"] = grouped_ride_data["ride_id"].count()
city_data.head()
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
      <th>driver_count</th>
      <th>type</th>
      <th>color</th>
      <th>mean_fare</th>
      <th>ride_count</th>
    </tr>
    <tr>
      <th>city</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Alvarezhaven</th>
      <td>21</td>
      <td>Urban</td>
      <td>lightcoral</td>
      <td>23.928710</td>
      <td>31</td>
    </tr>
    <tr>
      <th>Alyssaberg</th>
      <td>67</td>
      <td>Urban</td>
      <td>lightcoral</td>
      <td>20.609615</td>
      <td>26</td>
    </tr>
    <tr>
      <th>Anitamouth</th>
      <td>16</td>
      <td>Suburban</td>
      <td>lightskyblue</td>
      <td>37.315556</td>
      <td>9</td>
    </tr>
    <tr>
      <th>Antoniomouth</th>
      <td>21</td>
      <td>Urban</td>
      <td>lightcoral</td>
      <td>23.625000</td>
      <td>22</td>
    </tr>
    <tr>
      <th>Aprilchester</th>
      <td>49</td>
      <td>Urban</td>
      <td>lightcoral</td>
      <td>21.981579</td>
      <td>19</td>
    </tr>
  </tbody>
</table>
</div>




```python
grouped_bytype = city_data.groupby('type')

for key, grp in grouped_bytype:    
    plt.scatter(x=grp["ride_count"],y=grp["mean_fare"],
            c=grp.color, 
            label=key,
            alpha=0.5,
            s=(grp.driver_count*4),
            edgecolors='bk',linewidths=.5)
    
plt.title("Ride Sharing Data")
plt.xlabel("Number of Rides (PerCity)")
plt.ylabel("Average Fare")

plt.legend();
plt.show()
```


![png](output_7_0.png)



```python
merged_data = pd.merge(city_data,ride_data, left_index=True, right_on="city", how="outer")
merged_data.head()
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
      <th>driver_count</th>
      <th>type</th>
      <th>color</th>
      <th>mean_fare</th>
      <th>ride_count</th>
      <th>city</th>
      <th>date</th>
      <th>fare</th>
      <th>ride_id</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>117</th>
      <td>21</td>
      <td>Urban</td>
      <td>lightcoral</td>
      <td>23.92871</td>
      <td>31</td>
      <td>Alvarezhaven</td>
      <td>2016-04-18 20:51:29</td>
      <td>31.93</td>
      <td>4267015736324</td>
    </tr>
    <tr>
      <th>125</th>
      <td>21</td>
      <td>Urban</td>
      <td>lightcoral</td>
      <td>23.92871</td>
      <td>31</td>
      <td>Alvarezhaven</td>
      <td>2016-08-01 00:39:48</td>
      <td>6.42</td>
      <td>8394540350728</td>
    </tr>
    <tr>
      <th>155</th>
      <td>21</td>
      <td>Urban</td>
      <td>lightcoral</td>
      <td>23.92871</td>
      <td>31</td>
      <td>Alvarezhaven</td>
      <td>2016-09-01 22:57:12</td>
      <td>18.09</td>
      <td>1197329964911</td>
    </tr>
    <tr>
      <th>250</th>
      <td>21</td>
      <td>Urban</td>
      <td>lightcoral</td>
      <td>23.92871</td>
      <td>31</td>
      <td>Alvarezhaven</td>
      <td>2016-08-18 07:12:06</td>
      <td>20.74</td>
      <td>357421158941</td>
    </tr>
    <tr>
      <th>340</th>
      <td>21</td>
      <td>Urban</td>
      <td>lightcoral</td>
      <td>23.92871</td>
      <td>31</td>
      <td>Alvarezhaven</td>
      <td>2016-04-04 23:45:50</td>
      <td>14.25</td>
      <td>6431434271355</td>
    </tr>
  </tbody>
</table>
</div>




```python
merged_groupby_type = merged_data.groupby("type")
```


```python
# % of Total Fares by City Type
#Find total fares 
total_fares = merged_data['fare'].sum()

#Find total fares 
total_fares_by_type = merged_groupby_type["fare"].sum()
percent_fares_by_type = total_fares_by_type/total_fares*100
percent_fares_by_type

types = ["Rural", "Suburban","Urban"]
colors = ["Gold", "lightskyblue", "lightcoral"]
explode = (0.05, 0.05, 0)

plt.title("% Total Fares by City Type")
plt.pie(percent_fares_by_type, labels=types, colors=colors, autopct="%1.1f%%",startangle=90, shadow=True, explode=explode)
plt.axis("equal")
plt.show()
```


![png](output_10_0.png)



```python
# % of Total Rides by City Type
total_rides = ride_data["fare"].count()

#Find total fares 
total_rides_by_type = merged_groupby_type["fare"].count()
percent_rides_by_type = total_rides_by_type/total_rides*100
percent_rides_by_type

types = ["Rural", "Suburban","Urban"]
colors = ["Gold", "lightskyblue", "lightcoral"]
explode = (0.05, 0.05, 0)

plt.title("% Rides by City Type")
plt.pie(percent_rides_by_type, labels=types, colors=colors, autopct="%1.1f%%",startangle=90, shadow=True, explode=explode)
plt.axis("equal")
plt.show()

```


![png](output_11_0.png)



```python
# % of Total Drivers by City Type
# groupby_type = merged_data.groupby(["type", "city"])
# driver_count = groupby_type["driver_count"].first()
# driver_count


total_drivers = city_data["driver_count"].sum()
total_drivers

total_drivers_by_type = grouped_bytype["driver_count"].sum()
total_drivers_by_type
percent_drivers_by_type = total_drivers_by_type/total_drivers*100
percent_drivers_by_type

types = ["Rural", "Suburban","Urban"]
colors = ["Gold", "lightskyblue", "lightcoral"]
explode = (0.05, 0.05, 0)

plt.title("% Drivers by City Type")
plt.pie(percent_drivers_by_type, labels=types, colors=colors, autopct="%1.1f%%",startangle=90, shadow=True, explode=explode)
plt.axis("equal")
plt.show()
```


![png](output_12_0.png)

