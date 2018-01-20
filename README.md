# Matplotlib-Homework

Analysis:
1. Urban cities had the most riders.  
2. As a driver, you can potentially make more fares a rural setting and not have to drive as much
3. Urban cities have a high density of drivers, while surban cities aren't as dense.  Therefore surban 
fares are more expensive then urban.  



```python
 # Import Dependencies
import matplotlib.pyplot as plt
import pandas as pd
import numpy as np
import os
```


```python
 # Import our data into pandas from CSV
file_name1 = os.path.join("raw_data","city_data.csv" )
file_name2 = os.path.join("raw_data","ride_data.csv" )

city_data_df = pd.read_csv(file_name1)
ride_data_df = pd.read_csv(file_name2)
```


```python
city_data_df.head()
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>city</th>
      <th>driver_count</th>
      <th>type</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Kelseyland</td>
      <td>63</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Nguyenbury</td>
      <td>8</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>2</th>
      <td>East Douglas</td>
      <td>12</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>3</th>
      <td>West Dawnfurt</td>
      <td>34</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Rodriguezburgh</td>
      <td>52</td>
      <td>Urban</td>
    </tr>
  </tbody>
</table>
</div>




```python
ride_data_df.head()
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
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
#merge 2 dataframes together
combined_data = pd.merge(city_data_df, ride_data_df, how="inner", on="city")
combined_data.head()
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>city</th>
      <th>driver_count</th>
      <th>type</th>
      <th>date</th>
      <th>fare</th>
      <th>ride_id</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Kelseyland</td>
      <td>63</td>
      <td>Urban</td>
      <td>2016-08-19 04:27:52</td>
      <td>5.51</td>
      <td>6246006544795</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Kelseyland</td>
      <td>63</td>
      <td>Urban</td>
      <td>2016-04-17 06:59:50</td>
      <td>5.54</td>
      <td>7466473222333</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Kelseyland</td>
      <td>63</td>
      <td>Urban</td>
      <td>2016-05-04 15:06:07</td>
      <td>30.54</td>
      <td>2140501382736</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Kelseyland</td>
      <td>63</td>
      <td>Urban</td>
      <td>2016-01-25 20:44:56</td>
      <td>12.08</td>
      <td>1896987891309</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Kelseyland</td>
      <td>63</td>
      <td>Urban</td>
      <td>2016-08-09 18:19:47</td>
      <td>17.91</td>
      <td>8784212854829</td>
    </tr>
  </tbody>
</table>
</div>




```python
#citycity_df = combined_data.set_index("city")
#citycity_df.head()
```


```python
#average fair per city
city_fare = combined_data.groupby(['city']).fare.mean()
city_fare.head()
```




    city
    Alvarezhaven    23.928710
    Alyssaberg      20.609615
    Anitamouth      37.315556
    Antoniomouth    23.625000
    Aprilchester    21.981579
    Name: fare, dtype: float64




```python
#number of rides per city

city_rides = combined_data.groupby('city').date.count()
city_rides.head()


```




    city
    Alvarezhaven    31
    Alyssaberg      26
    Anitamouth       9
    Antoniomouth    22
    Aprilchester    19
    Name: date, dtype: int64




```python
#Drivers per city
city_drivers = combined_data.groupby('city').driver_count.mean()
city_drivers.head()

```




    city
    Alvarezhaven    21
    Alyssaberg      67
    Anitamouth      16
    Antoniomouth    21
    Aprilchester    49
    Name: driver_count, dtype: int64




```python
#Make a new table
Scatter_Table = pd.DataFrame({"Average fair per city": city_fare,
              "Rides per City": city_rides,
              "Drivers per City": city_drivers, 
             })
Scatter_Table.head()
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Average fair per city</th>
      <th>Drivers per City</th>
      <th>Rides per City</th>
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
      <td>23.928710</td>
      <td>21</td>
      <td>31</td>
    </tr>
    <tr>
      <th>Alyssaberg</th>
      <td>20.609615</td>
      <td>67</td>
      <td>26</td>
    </tr>
    <tr>
      <th>Anitamouth</th>
      <td>37.315556</td>
      <td>16</td>
      <td>9</td>
    </tr>
    <tr>
      <th>Antoniomouth</th>
      <td>23.625000</td>
      <td>21</td>
      <td>22</td>
    </tr>
    <tr>
      <th>Aprilchester</th>
      <td>21.981579</td>
      <td>49</td>
      <td>19</td>
    </tr>
  </tbody>
</table>
</div>




```python
Scatter_Table.to_csv("Scatter_Table.csv")
```


```python
file_name3 = os.path.join("Scatter_Table.csv" )

Scatter_Table_df = pd.read_csv(file_name3)
```


```python
Scatter_Table_df.head()
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>city</th>
      <th>Average fair per city</th>
      <th>Drivers per City</th>
      <th>Rides per City</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Alvarezhaven</td>
      <td>23.928710</td>
      <td>21</td>
      <td>31</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Alyssaberg</td>
      <td>20.609615</td>
      <td>67</td>
      <td>26</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Anitamouth</td>
      <td>37.315556</td>
      <td>16</td>
      <td>9</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Antoniomouth</td>
      <td>23.625000</td>
      <td>21</td>
      <td>22</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Aprilchester</td>
      <td>21.981579</td>
      <td>49</td>
      <td>19</td>
    </tr>
  </tbody>
</table>
</div>




```python
Big_Table = pd.merge(Scatter_Table_df, city_data_df, on="city")
Big_Table.head()
```




<div>
<style>
    .dataframe thead tr:only-child th {
        text-align: right;
    }

    .dataframe thead th {
        text-align: left;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>city</th>
      <th>Average fair per city</th>
      <th>Drivers per City</th>
      <th>Rides per City</th>
      <th>driver_count</th>
      <th>type</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Alvarezhaven</td>
      <td>23.928710</td>
      <td>21</td>
      <td>31</td>
      <td>21</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Alyssaberg</td>
      <td>20.609615</td>
      <td>67</td>
      <td>26</td>
      <td>67</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Anitamouth</td>
      <td>37.315556</td>
      <td>16</td>
      <td>9</td>
      <td>16</td>
      <td>Suburban</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Antoniomouth</td>
      <td>23.625000</td>
      <td>21</td>
      <td>22</td>
      <td>21</td>
      <td>Urban</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Aprilchester</td>
      <td>21.981579</td>
      <td>49</td>
      <td>19</td>
      <td>49</td>
      <td>Urban</td>
    </tr>
  </tbody>
</table>
</div>




```python
Urban = Big_Table[Big_Table["type"] == "Urban"]
x = Urban['Rides per City']
y = Urban["Average fair per city"]
s = Urban["Drivers per City"]
plt.scatter(x,y,s, c='g', label= 'Urban')

Suburban = Big_Table[Big_Table["type"] == "Suburban"]
x2 = Suburban['Rides per City']
y2 = Suburban["Average fair per city"]
s = Suburban["Drivers per City"]
plt.scatter(x2,y2,s, c='y', label= 'Suburban')

Rural = Big_Table[Big_Table["type"] == "Rural"]
x3 = Rural['Rides per City']
y3 = Rural["Average fair per city"]
s = Rural["Drivers per City"]
plt.scatter(x3,y3,s, c='b', label= 'Rural')

plt.title("Pyber Ride Sharing Data (2016)")
plt.ylabel("Average Fare ($)")
plt.xlabel("Total Number of Rides (Per City)")
plt.legend()
plt.style.use('ggplot')
plt.grid(True)
plt.xlim(0, 40)
plt.ylim(15, 45)
plt.rcParams['lines.linewidth']
plt.rcParams["figure.figsize"]


plt.savefig('Pyber Ride Sharing Data')
plt.show()
```


![png](output_14_0.png)



```python
#% of Total FAre by City Type
Total_sum = combined_data['fare'].sum()

Total_Type = combined_data.groupby(['type']).fare.sum()

TFCT = (Total_Type/Total_sum)*100
TFCT
```




    type
    Rural        6.579786
    Suburban    31.445750
    Urban       61.974463
    Name: fare, dtype: float64




```python
 # Dataset Total Fare by City type
types = ["Rural", "Suburban", "Urban",]
fare = [6.6, 31.4, 62.0]
colors = ["yellowgreen", "red", "lightskyblue"]
explode = (0, 0, 0.05)
```


```python
plt.title("% of Total Fares by City Type")
plt.pie(fare, explode=explode, labels=types, colors=colors,
        autopct="%1.1f%%", shadow=True, startangle=90)
plt.axis("equal")

plt.savefig('% of Total Fares by City Type')
plt.show()
```


![png](output_17_0.png)



```python
#% of Total Rides by City Type
Total_Rides = combined_data['date'].count()

Total_RidesType = combined_data.groupby(['type']).date.count()

Rides = (Total_RidesType/Total_Rides)*100
Rides
```




    type
    Rural        5.193187
    Suburban    27.295388
    Urban       67.511425
    Name: date, dtype: float64




```python
 # Dataset Total Rides by City type
types = ["Rural", "Suburban", "Urban",]
rides = [5.2, 27.3, 67.5]
colors = ["yellowgreen", "red", "lightskyblue"]
explode = (0, 0, 0.05)
```


```python
plt.title("% of Total Rides by City Type")
plt.pie(rides, explode=explode, labels=types, colors=colors,
        autopct="%1.1f%%", shadow=True, startangle=90)
plt.axis("equal")

plt.savefig('% of Total Rides by City Type')
plt.show()
```


![png](output_20_0.png)



```python
#% of Total Drivers by City Type
Total_Drivers = city_data_df['driver_count'].sum()

Total_DriversType = city_data_df.groupby(['type']).driver_count.sum()

Drives = (Total_DriversType/Total_Drivers)*100
Drives
```




    type
    Rural        3.105405
    Suburban    19.050463
    Urban       77.844133
    Name: driver_count, dtype: float64




```python
 # Dataset Total Drivers by City type
types = ["Rural", "Suburban", "Urban",]
drivers = [3.1, 19.0, 77.8]
colors = ["yellowgreen", "red", "lightskyblue"]
explode = (0, 0, 0.05)
```


```python
plt.title("% of Total Drivers by City Type")
plt.pie(drivers, explode=explode, labels=types, colors=colors,
        autopct="%1.1f%%", shadow=True, startangle=90)
plt.axis("equal")

plt.savefig('% of Total Drivers by City Type')
plt.show()

{
 "cells": [
  {
   "cell_type": "code",
   "execution_count": 74,
   "metadata": {
    "collapsed": true
   },
   "outputs": [],
   "source": [
    " # Import Dependencies\n",
    "import matplotlib.pyplot as plt\n",
    "import pandas as pd\n",
    "import numpy as np\n",
    "import os"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 75,
   "metadata": {
    "collapsed": true
   },
   "outputs": [],
   "source": [
    " # Import our data into pandas from CSV\n",
    "file_name1 = os.path.join(\"raw_data\",\"city_data.csv\" )\n",
    "file_name2 = os.path.join(\"raw_data\",\"ride_data.csv\" )\n",
    "\n",
    "city_data_df = pd.read_csv(file_name1)\n",
    "ride_data_df = pd.read_csv(file_name2)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 76,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/html": [
       "<div>\n",
       "<style>\n",
       "    .dataframe thead tr:only-child th {\n",
       "        text-align: right;\n",
       "    }\n",
       "\n",
       "    .dataframe thead th {\n",
       "        text-align: left;\n",
       "    }\n",
       "\n",
       "    .dataframe tbody tr th {\n",
       "        vertical-align: top;\n",
       "    }\n",
       "</style>\n",
       "<table border=\"1\" class=\"dataframe\">\n",
       "  <thead>\n",
       "    <tr style=\"text-align: right;\">\n",
       "      <th></th>\n",
       "      <th>city</th>\n",
       "      <th>driver_count</th>\n",
       "      <th>type</th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>0</th>\n",
       "      <td>Kelseyland</td>\n",
       "      <td>63</td>\n",
       "      <td>Urban</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>1</th>\n",
       "      <td>Nguyenbury</td>\n",
       "      <td>8</td>\n",
       "      <td>Urban</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2</th>\n",
       "      <td>East Douglas</td>\n",
       "      <td>12</td>\n",
       "      <td>Urban</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>3</th>\n",
       "      <td>West Dawnfurt</td>\n",
       "      <td>34</td>\n",
       "      <td>Urban</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>4</th>\n",
       "      <td>Rodriguezburgh</td>\n",
       "      <td>52</td>\n",
       "      <td>Urban</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "</div>"
      ],
      "text/plain": [
       "             city  driver_count   type\n",
       "0      Kelseyland            63  Urban\n",
       "1      Nguyenbury             8  Urban\n",
       "2    East Douglas            12  Urban\n",
       "3   West Dawnfurt            34  Urban\n",
       "4  Rodriguezburgh            52  Urban"
      ]
     },
     "execution_count": 76,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "city_data_df.head()"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 77,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/html": [
       "<div>\n",
       "<style>\n",
       "    .dataframe thead tr:only-child th {\n",
       "        text-align: right;\n",
       "    }\n",
       "\n",
       "    .dataframe thead th {\n",
       "        text-align: left;\n",
       "    }\n",
       "\n",
       "    .dataframe tbody tr th {\n",
       "        vertical-align: top;\n",
       "    }\n",
       "</style>\n",
       "<table border=\"1\" class=\"dataframe\">\n",
       "  <thead>\n",
       "    <tr style=\"text-align: right;\">\n",
       "      <th></th>\n",
       "      <th>city</th>\n",
       "      <th>date</th>\n",
       "      <th>fare</th>\n",
       "      <th>ride_id</th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>0</th>\n",
       "      <td>Sarabury</td>\n",
       "      <td>2016-01-16 13:49:27</td>\n",
       "      <td>38.35</td>\n",
       "      <td>5403689035038</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>1</th>\n",
       "      <td>South Roy</td>\n",
       "      <td>2016-01-02 18:42:34</td>\n",
       "      <td>17.49</td>\n",
       "      <td>4036272335942</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2</th>\n",
       "      <td>Wiseborough</td>\n",
       "      <td>2016-01-21 17:35:29</td>\n",
       "      <td>44.18</td>\n",
       "      <td>3645042422587</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>3</th>\n",
       "      <td>Spencertown</td>\n",
       "      <td>2016-07-31 14:53:22</td>\n",
       "      <td>6.87</td>\n",
       "      <td>2242596575892</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>4</th>\n",
       "      <td>Nguyenbury</td>\n",
       "      <td>2016-07-09 04:42:44</td>\n",
       "      <td>6.28</td>\n",
       "      <td>1543057793673</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "</div>"
      ],
      "text/plain": [
       "          city                 date   fare        ride_id\n",
       "0     Sarabury  2016-01-16 13:49:27  38.35  5403689035038\n",
       "1    South Roy  2016-01-02 18:42:34  17.49  4036272335942\n",
       "2  Wiseborough  2016-01-21 17:35:29  44.18  3645042422587\n",
       "3  Spencertown  2016-07-31 14:53:22   6.87  2242596575892\n",
       "4   Nguyenbury  2016-07-09 04:42:44   6.28  1543057793673"
      ]
     },
     "execution_count": 77,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "ride_data_df.head()"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 78,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/html": [
       "<div>\n",
       "<style>\n",
       "    .dataframe thead tr:only-child th {\n",
       "        text-align: right;\n",
       "    }\n",
       "\n",
       "    .dataframe thead th {\n",
       "        text-align: left;\n",
       "    }\n",
       "\n",
       "    .dataframe tbody tr th {\n",
       "        vertical-align: top;\n",
       "    }\n",
       "</style>\n",
       "<table border=\"1\" class=\"dataframe\">\n",
       "  <thead>\n",
       "    <tr style=\"text-align: right;\">\n",
       "      <th></th>\n",
       "      <th>city</th>\n",
       "      <th>driver_count</th>\n",
       "      <th>type</th>\n",
       "      <th>date</th>\n",
       "      <th>fare</th>\n",
       "      <th>ride_id</th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>0</th>\n",
       "      <td>Kelseyland</td>\n",
       "      <td>63</td>\n",
       "      <td>Urban</td>\n",
       "      <td>2016-08-19 04:27:52</td>\n",
       "      <td>5.51</td>\n",
       "      <td>6246006544795</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>1</th>\n",
       "      <td>Kelseyland</td>\n",
       "      <td>63</td>\n",
       "      <td>Urban</td>\n",
       "      <td>2016-04-17 06:59:50</td>\n",
       "      <td>5.54</td>\n",
       "      <td>7466473222333</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2</th>\n",
       "      <td>Kelseyland</td>\n",
       "      <td>63</td>\n",
       "      <td>Urban</td>\n",
       "      <td>2016-05-04 15:06:07</td>\n",
       "      <td>30.54</td>\n",
       "      <td>2140501382736</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>3</th>\n",
       "      <td>Kelseyland</td>\n",
       "      <td>63</td>\n",
       "      <td>Urban</td>\n",
       "      <td>2016-01-25 20:44:56</td>\n",
       "      <td>12.08</td>\n",
       "      <td>1896987891309</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>4</th>\n",
       "      <td>Kelseyland</td>\n",
       "      <td>63</td>\n",
       "      <td>Urban</td>\n",
       "      <td>2016-08-09 18:19:47</td>\n",
       "      <td>17.91</td>\n",
       "      <td>8784212854829</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "</div>"
      ],
      "text/plain": [
       "         city  driver_count   type                 date   fare        ride_id\n",
       "0  Kelseyland            63  Urban  2016-08-19 04:27:52   5.51  6246006544795\n",
       "1  Kelseyland            63  Urban  2016-04-17 06:59:50   5.54  7466473222333\n",
       "2  Kelseyland            63  Urban  2016-05-04 15:06:07  30.54  2140501382736\n",
       "3  Kelseyland            63  Urban  2016-01-25 20:44:56  12.08  1896987891309\n",
       "4  Kelseyland            63  Urban  2016-08-09 18:19:47  17.91  8784212854829"
      ]
     },
     "execution_count": 78,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "#merge 2 dataframes together\n",
    "combined_data = pd.merge(city_data_df, ride_data_df, how=\"inner\", on=\"city\")\n",
    "combined_data.head()"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 79,
   "metadata": {
    "collapsed": true
   },
   "outputs": [],
   "source": [
    "#citycity_df = combined_data.set_index(\"city\")\n",
    "#citycity_df.head()"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 80,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "city\n",
       "Alvarezhaven    23.928710\n",
       "Alyssaberg      20.609615\n",
       "Anitamouth      37.315556\n",
       "Antoniomouth    23.625000\n",
       "Aprilchester    21.981579\n",
       "Name: fare, dtype: float64"
      ]
     },
     "execution_count": 80,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "#average fair per city\n",
    "city_fare = combined_data.groupby(['city']).fare.mean()\n",
    "city_fare.head()"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 81,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "city\n",
       "Alvarezhaven    31\n",
       "Alyssaberg      26\n",
       "Anitamouth       9\n",
       "Antoniomouth    22\n",
       "Aprilchester    19\n",
       "Name: date, dtype: int64"
      ]
     },
     "execution_count": 81,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "#number of rides per city\n",
    "\n",
    "city_rides = combined_data.groupby('city').date.count()\n",
    "city_rides.head()\n",
    "\n"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 82,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "city\n",
       "Alvarezhaven    21\n",
       "Alyssaberg      67\n",
       "Anitamouth      16\n",
       "Antoniomouth    21\n",
       "Aprilchester    49\n",
       "Name: driver_count, dtype: int64"
      ]
     },
     "execution_count": 82,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "#Drivers per city\n",
    "city_drivers = combined_data.groupby('city').driver_count.mean()\n",
    "city_drivers.head()\n"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 83,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/html": [
       "<div>\n",
       "<style>\n",
       "    .dataframe thead tr:only-child th {\n",
       "        text-align: right;\n",
       "    }\n",
       "\n",
       "    .dataframe thead th {\n",
       "        text-align: left;\n",
       "    }\n",
       "\n",
       "    .dataframe tbody tr th {\n",
       "        vertical-align: top;\n",
       "    }\n",
       "</style>\n",
       "<table border=\"1\" class=\"dataframe\">\n",
       "  <thead>\n",
       "    <tr style=\"text-align: right;\">\n",
       "      <th></th>\n",
       "      <th>Average fair per city</th>\n",
       "      <th>Drivers per City</th>\n",
       "      <th>Rides per City</th>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>city</th>\n",
       "      <th></th>\n",
       "      <th></th>\n",
       "      <th></th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>Alvarezhaven</th>\n",
       "      <td>23.928710</td>\n",
       "      <td>21</td>\n",
       "      <td>31</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>Alyssaberg</th>\n",
       "      <td>20.609615</td>\n",
       "      <td>67</td>\n",
       "      <td>26</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>Anitamouth</th>\n",
       "      <td>37.315556</td>\n",
       "      <td>16</td>\n",
       "      <td>9</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>Antoniomouth</th>\n",
       "      <td>23.625000</td>\n",
       "      <td>21</td>\n",
       "      <td>22</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>Aprilchester</th>\n",
       "      <td>21.981579</td>\n",
       "      <td>49</td>\n",
       "      <td>19</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "</div>"
      ],
      "text/plain": [
       "              Average fair per city  Drivers per City  Rides per City\n",
       "city                                                                 \n",
       "Alvarezhaven              23.928710                21              31\n",
       "Alyssaberg                20.609615                67              26\n",
       "Anitamouth                37.315556                16               9\n",
       "Antoniomouth              23.625000                21              22\n",
       "Aprilchester              21.981579                49              19"
      ]
     },
     "execution_count": 83,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "#Make a new table\n",
    "Scatter_Table = pd.DataFrame({\"Average fair per city\": city_fare,\n",
    "              \"Rides per City\": city_rides,\n",
    "              \"Drivers per City\": city_drivers, \n",
    "             })\n",
    "Scatter_Table.head()"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 84,
   "metadata": {
    "collapsed": true
   },
   "outputs": [],
   "source": [
    "Scatter_Table.to_csv(\"Scatter_Table.csv\")"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 85,
   "metadata": {
    "collapsed": true
   },
   "outputs": [],
   "source": [
    "file_name3 = os.path.join(\"Scatter_Table.csv\" )\n",
    "\n",
    "Scatter_Table_df = pd.read_csv(file_name3)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 86,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/html": [
       "<div>\n",
       "<style>\n",
       "    .dataframe thead tr:only-child th {\n",
       "        text-align: right;\n",
       "    }\n",
       "\n",
       "    .dataframe thead th {\n",
       "        text-align: left;\n",
       "    }\n",
       "\n",
       "    .dataframe tbody tr th {\n",
       "        vertical-align: top;\n",
       "    }\n",
       "</style>\n",
       "<table border=\"1\" class=\"dataframe\">\n",
       "  <thead>\n",
       "    <tr style=\"text-align: right;\">\n",
       "      <th></th>\n",
       "      <th>city</th>\n",
       "      <th>Average fair per city</th>\n",
       "      <th>Drivers per City</th>\n",
       "      <th>Rides per City</th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>0</th>\n",
       "      <td>Alvarezhaven</td>\n",
       "      <td>23.928710</td>\n",
       "      <td>21</td>\n",
       "      <td>31</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>1</th>\n",
       "      <td>Alyssaberg</td>\n",
       "      <td>20.609615</td>\n",
       "      <td>67</td>\n",
       "      <td>26</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2</th>\n",
       "      <td>Anitamouth</td>\n",
       "      <td>37.315556</td>\n",
       "      <td>16</td>\n",
       "      <td>9</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>3</th>\n",
       "      <td>Antoniomouth</td>\n",
       "      <td>23.625000</td>\n",
       "      <td>21</td>\n",
       "      <td>22</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>4</th>\n",
       "      <td>Aprilchester</td>\n",
       "      <td>21.981579</td>\n",
       "      <td>49</td>\n",
       "      <td>19</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "</div>"
      ],
      "text/plain": [
       "           city  Average fair per city  Drivers per City  Rides per City\n",
       "0  Alvarezhaven              23.928710                21              31\n",
       "1    Alyssaberg              20.609615                67              26\n",
       "2    Anitamouth              37.315556                16               9\n",
       "3  Antoniomouth              23.625000                21              22\n",
       "4  Aprilchester              21.981579                49              19"
      ]
     },
     "execution_count": 86,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "Scatter_Table_df.head()"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 87,
   "metadata": {
    "scrolled": true
   },
   "outputs": [
    {
     "data": {
      "text/html": [
       "<div>\n",
       "<style>\n",
       "    .dataframe thead tr:only-child th {\n",
       "        text-align: right;\n",
       "    }\n",
       "\n",
       "    .dataframe thead th {\n",
       "        text-align: left;\n",
       "    }\n",
       "\n",
       "    .dataframe tbody tr th {\n",
       "        vertical-align: top;\n",
       "    }\n",
       "</style>\n",
       "<table border=\"1\" class=\"dataframe\">\n",
       "  <thead>\n",
       "    <tr style=\"text-align: right;\">\n",
       "      <th></th>\n",
       "      <th>city</th>\n",
       "      <th>Average fair per city</th>\n",
       "      <th>Drivers per City</th>\n",
       "      <th>Rides per City</th>\n",
       "      <th>driver_count</th>\n",
       "      <th>type</th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>0</th>\n",
       "      <td>Alvarezhaven</td>\n",
       "      <td>23.928710</td>\n",
       "      <td>21</td>\n",
       "      <td>31</td>\n",
       "      <td>21</td>\n",
       "      <td>Urban</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>1</th>\n",
       "      <td>Alyssaberg</td>\n",
       "      <td>20.609615</td>\n",
       "      <td>67</td>\n",
       "      <td>26</td>\n",
       "      <td>67</td>\n",
       "      <td>Urban</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>2</th>\n",
       "      <td>Anitamouth</td>\n",
       "      <td>37.315556</td>\n",
       "      <td>16</td>\n",
       "      <td>9</td>\n",
       "      <td>16</td>\n",
       "      <td>Suburban</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>3</th>\n",
       "      <td>Antoniomouth</td>\n",
       "      <td>23.625000</td>\n",
       "      <td>21</td>\n",
       "      <td>22</td>\n",
       "      <td>21</td>\n",
       "      <td>Urban</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>4</th>\n",
       "      <td>Aprilchester</td>\n",
       "      <td>21.981579</td>\n",
       "      <td>49</td>\n",
       "      <td>19</td>\n",
       "      <td>49</td>\n",
       "      <td>Urban</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "</div>"
      ],
      "text/plain": [
       "           city  Average fair per city  Drivers per City  Rides per City  \\\n",
       "0  Alvarezhaven              23.928710                21              31   \n",
       "1    Alyssaberg              20.609615                67              26   \n",
       "2    Anitamouth              37.315556                16               9   \n",
       "3  Antoniomouth              23.625000                21              22   \n",
       "4  Aprilchester              21.981579                49              19   \n",
       "\n",
       "   driver_count      type  \n",
       "0            21     Urban  \n",
       "1            67     Urban  \n",
       "2            16  Suburban  \n",
       "3            21     Urban  \n",
       "4            49     Urban  "
      ]
     },
     "execution_count": 87,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "Big_Table = pd.merge(Scatter_Table_df, city_data_df, on=\"city\")\n",
    "Big_Table.head()"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 88,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "image/png": "iVBORw0KGgoAAAANSUhEUgAAAYAAAAETCAYAAAA/NdFSAAAABHNCSVQICAgIfAhkiAAAAAlwSFlz\nAAALEgAACxIB0t1+/AAAADl0RVh0U29mdHdhcmUAbWF0cGxvdGxpYiB2ZXJzaW9uIDIuMS4wLCBo\ndHRwOi8vbWF0cGxvdGxpYi5vcmcvpW3flQAAIABJREFUeJzs3Xd4FNX6wPHvbE/vIZCE0AwldKSI\nSlEpIqggeFER6RcEFUEFaQIiRUARERC9iIAKFoqicpWfIJaLFMEgvQQICek92b7z+yOysKSwIbsp\n5HyeJ8+TnTkz8+4kO2fnzDnvkWRZlhEEQRBqHEVlByAIgiBUDlEBCIIg1FCiAhAEQaihRAUgCIJQ\nQ4kKQBAEoYYSFYAgCEINJSqAKuy+++6jcePG9p9mzZrRvXt3Fi1aREFBwU23v3z5Mo0bN+b06dNu\ni/HqMa7/adq0KZ06dWLixImkpqY6vJ+NGzeWuK+OHTuyZcuWW45l//79DB06lDZt2tC6dWsef/xx\nvvvuuyKxuvJ8/PHHHzRu3Jj8/HyX7fN6N/4PtGrVikceeYQvv/yyTPvJz8/niy++KHc88+bN46uv\nvgIgOzubGTNmcM8999CxY0eef/55kpOT7WUtFgvz5s2jU6dOtG/fnnnz5mEymYrd76xZs1i0aFGR\n5d988w29evWiVatWDB48mJMnT9rXzZ07l61bt5b7PdVoslBlde/eXV69erWckpIip6SkyElJSfLv\nv/8ud+7cWZ42bdpNt4+Pj5ejo6PlU6dOuS3Gq8f4448/7HFeuXJF/vnnn+Xu3bvLI0aMsJdNT0+X\nCwoKStxXhw4d5K+++uqW4jh+/LjcokUL+f3335fPnj0rnz9/Xl67dq3ctGlT+dtvv3WI1ZXnw2g0\nyikpKbLNZnPZPq93/f9AcnKyfO7cOfnjjz+WW7ZsKX/44YdO7+fdd9+V+/fvX65YYmNj5Yceeki2\nWq2yLMvyuHHj5AEDBsh//fWXfPLkSXnEiBFy//79ZYvFIsuyLC9atEju2bOn/Oeff8p//PGH3L17\nd3nhwoVF9rtmzRo5Ojq6yLo9e/bIMTEx8meffSafP39efumll+Ru3brJBoNBlmVZTktLk7t16yZn\nZGSU633VZOIOoIrz8vIiJCSEkJAQatWqxV133cXQoUP573//W9mhOfD397fHGRYWRpcuXXjhhRf4\n9ddfycvLAyAwMBAPDw+3HH/79u20adOGMWPG0LBhQ+rXr8/w4cN55JFH+Oyzz9xyTACNRkNISAiS\nJLntGFf/B0JDQ2nQoAFDhw7llVdeYfny5aSnpzu1D9kF4z3fe+89Bg8ejEKhICMjg//7v/9j1qxZ\ntGzZksaNGzN//nyOHTvGmTNnMBqNfPbZZ0yZMoU2bdrQoUMHZsyYwaZNmzAYDABkZGTw7LPP8uGH\nH1K7du0ix1u1ahVPPPEEgwcPpn79+syePRtJkjh16hQAQUFBdOrUqdS7SqF0ogKohpRKJRqNBpPJ\nRIcOHYrc2g8dOpTly5fbX//888/cf//9tGrViueff56srCz7utTUVF544QXatGnDPffcw/Tp08nN\nzQWuNZmsXLmSjh07Mnr06DLFqdFoHC6M1zcBWa1WFi9eTKdOnejYsWOxH+L//Oc/dO/enTZt2vDE\nE09w5MiREo8lSRLnzp3jypUrDstffvnlIk0Lv/76Kw899BAtWrRg0KBBDk1CsbGxPPPMM7Rp04YW\nLVowcOBA/vzzzxLPx41NQI0bN2bLli0MGDCAVq1aMWjQIA4fPmzff2JiIiNHjqR169b07NmTzZs3\n07hxY2dPqd2AAQOQJIndu3cDUFBQwOzZs7nnnnuIiYmha9eurFy5EoAtW7awYsUKjh07RuPGjbl8\n+XKp5YsTHx/P3r176dGjBwA6nY41a9bQtGlTh78BgMFg4MSJExQUFNC+fXv7+g4dOlBQUMCJEycA\nOHfuHFqtlm3bthEZGelwvPz8fI4cOULv3r3ty7y8vPjpp59o2bKlfVnPnj357LPPMJvNZT6HgqgA\nqhWbzUZsbCwbN27kgQceQKPR0KtXL7799lt7meTkZA4cOEDfvn3tyzZu3MjcuXP59NNPSUhI4MUX\nX7Sve+6555Blmc2bN7Nq1SouXbrksB5gz549bNq0iVdeecXpWM+cOcOyZcvo0qUL3t7eRdavXLmS\nbdu28eabb/Lxxx/zww8/OFRMmzZtYv369bz22mts3bqVrl278swzzxAfH1/s8QYNGoRer6dHjx6M\nGjWK//znP5w8eZLAwEDq1KnjUHbz5s3Mnj2bLVu2IEkSM2fOBAovOqNHj6Zp06Zs376dzz//HC8v\nL1577bUynY9ly5bxwgsvsHnzZtRqNbNmzQIK28THjBmDQqHg888/Z+rUqbzzzjtOn9PreXh4EBER\nwdmzZwFYuHAhR44cYeXKlezcuZOnn36ad955h7///ps+ffowYsQImjRpwq+//krt2rVLLV+cvXv3\n0rBhQ2rVqgWAp6cnXbt2RaPR2Mt89NFHeHt707hxY5KTk/H09MTHx8e+3tvbGw8PD5KSkgBo3749\nb7/9drHf/uPj45FlGaPRyPDhw+ncuTMjRozg3LlzDuU6d+5MVlYWx44du6XzWONVchOUUIru3bvL\nMTExcuvWreXWrVvLzZo1k2NiYuTnnntOzs7OlmVZlvfv3y83bdpUTk1NlWVZlteuXSsPGDBAluVr\nbd5ff/21fZ8nTpyQo6Oj5bi4OPl///uf3Lp1a9loNNrXJyUl2dvJr26/Y8eOEmO8WqZly5b2OGNi\nYuR27drJU6dOlbOyshzez4YNG2SbzSZ37txZ3rhxo33dlStX5KZNm9qfAXTr1k3evn27w7GGDx9e\nbBvyVRcuXJCnT58u33XXXXJ0dLQcHR0tDxw4UL5w4YJDrP/973/t22zbtk1u2bKlLMuFbcpr1qyR\nzWazff3OnTvlJk2aOGx//fnYt2+fHB0dLefl5cmyLMvR0dHy+++/b1+/a9cuOTo6WjYajfIvv/wi\nx8TEyOnp6fb1n376qRwdHV3ie7p6zoozePBgefr06bIsy/LWrVvlv//+22F969at5a1bt8qyLMvL\nly93eAZws/I3mjp1qvziiy+WGOeOHTvkJk2ayJ988ol9/x06dChSrn379vK2bduKLB8yZIjD3/bA\ngQNydHS03L17d/nrr7+Wjx49Kk+aNEm+++675ZycHIdte/bsWeI5EkqnquwKSCjdv//9bx5++GEA\n1Go1wcHBDt+67rzzTsLCwti5cydDhgzhm2++sZe/qnXr1vbfGzdujFqt5uzZsyQlJaHX6+nYsWOR\n48bFxRETEwNQ5Pa8OMuXL6devXpkZmaydOlS9Ho9L774In5+fkXKZmZmkpaWRrNmzezLwsLCCA0N\nBQq/iScmJjJz5kyHb98mk8nhvd8oKiqKefPmIcsyx48f56effmL9+vWMGzfO4S6pbt269t99fX3t\nbdJBQUEMGjSITz75hJMnT3LhwgVOnDiBzWZzOM7Nzke9evXsv1+9+7FYLJw6dYrw8HACAwPt69u0\naVPqvkqTl5dn/4b98MMPs3v3brZv326Pu6CgoEjsV5W1fFpamsN5u96WLVuYMWMGzzzzDE8++SRQ\n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\nwRyXHVdkucFqYMuZLfRr0I/BjQfzfuz75Jiv9bDxUHrwUP2Hilz8i/PR8Y9KXJdvyWfP5T3lzv8j\nXONUBbBjxw727NmD2Wzmvvvu44033rhpE9DVpHF6vZ633nqLwYMHYzabuf/++2nQoAFbtmzhiy++\nYOjQ4kf7BQcHF7u8KlGpVNU6zitXtBj+yb6r03lV6nuprudy5u6ZDhf/6+Wac3lm1zP8+syvbo9r\nzSNryNuax2/xv9m7eXprvGkV2orPB32Ov678vX18cnyKrWAA1P/f3p3Hx3S2jx//zJJ9lZCdBBGp\nINYg/FCKR1G01NZ6LK2d8rRC6UIlxddWVaJK7F5KUf02qvZSbR+7BCUiIgkhiewykUxmfn/MN1OT\nmUzGEhlyv/+Sc2bOfc0tOdecc9/nui0tqFmzJuHdwwnxDSHyXCRZhVk4WDrwTuN3GN50uMEvjWX7\nMzlP/+rhUX9l/MXA5gOf7oM8gRfl9/NxmZQAEhISGDlyJEFBQahUKv7880+io6P58kvDKyOVysjI\nYPHixXTv3p0OHTrw4MED7Ow01bBCQkKIiiq/6NeLcLlV1d9aTVVenC4u8ykpmYNUao+j4+wq/Szm\n0JfGFkIvVTbOdRfWGT3mpXuXSE3TrK9b2VZ3Xs2V+1fY/PdmpBZSXvd5nVCvUJT5SjLyMyhUFrLy\n4kqOJh9FoVTgYOnA63VfZ3TQaJMGV4PsgrCSWVGgLNDb186tnbZfQl1DCe2mO7Z3/77hB97K9mdF\nD6ZZqayq5PfEHH4/TVEpt4CmTJlCfn4+P/74I7/++isKhYKePXsafU92djYRERGMGjWKJk2aAGh/\n9vf3JzY2lnr1nv6yVHhyVlb++PhsqeowqtzxlON8de4rbj+4jVwqp2GNhizosEBnIfTylC5QUp5i\nVTH3Ffefy8ymmzk3WXx2MfHZ8UikEm7ev4mV3IpW7q0oVBYydN9Q/ntPd4nJ82nn+ePOH6zrtq7C\nJGBoNbBSlzIulbvvcbSs1ZKDyQcN7pNL5IwMEutSPEsVJoA7d+6wb98+fvvtN9zc3CgqKmLVqlXY\n2hpfPGHPnj3k5+eza9cudu3SrEQ1fPhwNmzYgFwux9nZWTxMJlS5P+78wdTfpnKv4J52W2JuIkl5\nSex9Y2+5SzWWsrOwI19Z/mI7cqkcewvNKloHbh1g89+bkSBhXNNxhHo9uxlwN3Nu8s7+d3QGguOz\n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\n",
      "text/plain": [
       "<matplotlib.figure.Figure at 0x20cf42f2978>"
      ]
     },
     "metadata": {},
     "output_type": "display_data"
    }
   ],
   "source": [
    "Urban = Big_Table[Big_Table[\"type\"] == \"Urban\"]\n",
    "x = Urban['Rides per City']\n",
    "y = Urban[\"Average fair per city\"]\n",
    "s = Urban[\"Drivers per City\"]\n",
    "plt.scatter(x,y,s, c='g', label= 'Urban')\n",
    "\n",
    "Suburban = Big_Table[Big_Table[\"type\"] == \"Suburban\"]\n",
    "x2 = Suburban['Rides per City']\n",
    "y2 = Suburban[\"Average fair per city\"]\n",
    "s = Suburban[\"Drivers per City\"]\n",
    "plt.scatter(x2,y2,s, c='y', label= 'Suburban')\n",
    "\n",
    "Rural = Big_Table[Big_Table[\"type\"] == \"Rural\"]\n",
    "x3 = Rural['Rides per City']\n",
    "y3 = Rural[\"Average fair per city\"]\n",
    "s = Rural[\"Drivers per City\"]\n",
    "plt.scatter(x3,y3,s, c='b', label= 'Rural')\n",
    "\n",
    "plt.title(\"Pyber Ride Sharing Data (2016)\")\n",
    "plt.ylabel(\"Average Fare ($)\")\n",
    "plt.xlabel(\"Total Number of Rides (Per City)\")\n",
    "plt.legend()\n",
    "plt.style.use('ggplot')\n",
    "plt.grid(True)\n",
    "plt.xlim(0, 40)\n",
    "plt.ylim(15, 45)\n",
    "plt.rcParams['lines.linewidth']\n",
    "plt.rcParams[\"figure.figsize\"]\n",
    "\n",
    "\n",
    "plt.savefig('Pyber Ride Sharing Data')\n",
    "plt.show()"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "metadata": {
    "collapsed": true
   },
   "outputs": [],
   "source": []
  },
  {
   "cell_type": "code",
   "execution_count": 89,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "type\n",
       "Rural        6.579786\n",
       "Suburban    31.445750\n",
       "Urban       61.974463\n",
       "Name: fare, dtype: float64"
      ]
     },
     "execution_count": 89,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "#% of Total FAre by City Type\n",
    "Total_sum = combined_data['fare'].sum()\n",
    "\n",
    "Total_Type = combined_data.groupby(['type']).fare.sum()\n",
    "\n",
    "TFCT = (Total_Type/Total_sum)*100\n",
    "TFCT"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 90,
   "metadata": {
    "collapsed": true
   },
   "outputs": [],
   "source": [
    " # Dataset Total Fare by City type\n",
    "types = [\"Rural\", \"Suburban\", \"Urban\",]\n",
    "fare = [6.6, 31.4, 62.0]\n",
    "colors = [\"yellowgreen\", \"red\", \"lightskyblue\"]\n",
    "explode = (0, 0, 0.05)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 91,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "image/png": "iVBORw0KGgoAAAANSUhEUgAAAV0AAAD4CAYAAABPLjVeAAAABHNCSVQICAgIfAhkiAAAAAlwSFlz\nAAALEgAACxIB0t1+/AAAADl0RVh0U29mdHdhcmUAbWF0cGxvdGxpYiB2ZXJzaW9uIDIuMS4wLCBo\ndHRwOi8vbWF0cGxvdGxpYi5vcmcvpW3flQAAIABJREFUeJzt3Xd4VFX+x/H3zGRm0hskBAgllBBK\nIBTpoqIooOiuClZUxO7u/tR1FQV1besqqLsLoquIrlhAEFBUrBiKSJcOIQmpkALpddo9vz8CAyMg\nqTOZ5Pt6njzAzZ17vzNMPjlz7jnn6pRSCiGEEG6h93QBQgjRmkjoCiGEG0noCiGEG0noCiGEG0no\nCiGEG0noCiGEG0noNoIff/yRiy66iFGjRrFixQqX77300ku88cYbDT7HN998w4UXXsiAAQNITEx0\n+d6MGTPo1avXOb/mzp1b63Pk5eXVat+lS5cyatSoc35/zJgx56ynOXj99deZMmVKox7z+PHjPP/8\n84wdO5b+/ftzxRVX8Oabb2K1Wp373HTTTcyZMwcAq9XKxx9/XK9z/d7r26tXL7Zt29Yoz0k0ASUa\nxOFwqGHDhqnly5er9evXq/79+6vCwkKllFJ5eXlqzJgxqqysrMHnGTdunHriiSdUdna2qqqqcvle\naWmpys/PV/n5+Wrz5s0qNjZW7dq1y7mtvLz8vMfPyMhQsbGxKiUlpVb1fPrpp2rkyJHn/P6FF16o\n3n77bWcNp381B6+99pqaPHlyox0vMzNTjR49Wt17771qy5YtKjMzU61evVqNHj1aPfDAA879ioqK\nnP8f53sNf09BQYHz9Zw3b5665JJLXF5jq9XaKM9LND4fT4e+tyssLKSoqIgrr7wSk8lEUFAQWVlZ\nhIWF8dZbbzF16lQCAwMbfJ7S0lIGDx5Mx44dz/heUFAQQUFBABQVFQEQHh5ORERErY+vmmCOTGBg\nYJ1q8GbPPPMMsbGxzJ8/H72+5gNkp06diIiI4Oabb2bDhg2MHj2a0NDQRjlfeHi48+8BAQEYDIZW\n81p7O+leaKCwsDD8/f3ZvXs3GRkZlJSUEBUVxdGjR0lMTOSWW26p1XHS09O5//77ueCCCxg2bBiz\nZs2ivLwcgF69elFUVMSTTz7J2LFj613rrl27mDp1KgMHDmT06NG8+uqr2O127HY7l19+OQATJ05k\n/vz5AKxcuZJJkybRr18/Bg0axAMPPMDx48frff7fWrhwIZdffjn9+vVj2LBhPP7441RWVgI1H//v\nvfdepk2bxpAhQ/j8889RSvH2229z8cUXM3DgQG6++WZ2797tPF5SUhK33norCQkJDB8+nKeeeoqq\nqqpznt/hcPDcc885X4+PPvoIAIvFwuDBg8/oKrrlllvO2lV09OhRNm7cyPTp052Be9LgwYP53//+\nx8CBA4FT3QsbN25k1qxZHD9+3Nkd0Lt3b7Zs2eJ8rFKKsWPHsnLlyjq+spCbm/u7x9u4cSPDhg1j\n6dKljB49miFDhvD0009jsVic+6empjJ9+nQGDBjA2LFjmTNnjktXiagfCd0GMhgMPPbYY9xxxx1M\nnDiRBx54gMjISObPn8+0adPw8/M77zGKi4u5+eabMRqNfPTRR8ydO5ft27fz5JNPArBhwwZCQ0N5\n8sknWbZsWb3qTE1N5bbbbqNXr14sW7aMZ599luXLl/Pvf/8bHx8flixZAsBHH33EHXfcwbZt25g1\naxZ333033377LfPmzWPv3r28/fbb9Tr/b61cuZI333yTmTNn8u233/Liiy/y3XffsXTpUuc+iYmJ\njBgxgsWLF3PhhRfy8ccf88knn/Dss8+yYsUKRo0axW233cbRo0cBeOSRR+jZsyerVq3izTffZMOG\nDbz77rvnrGHv3r0UFxezdOlSHn30UV5++WW+/vprzGYzl19+OV9++aVz35ycHHbs2MGkSZPOOM7B\ngwdRShEfH3/W8wwfPpyAgACXbUOGDGHGjBmEh4ezYcMGBgwYwAUXXOByzu3bt1NQUMC4ceNq96Ke\nJioq6rzHKy8v54MPPmDevHm88cYbbNiwgeeffx6A6upq7rrrLmJiYlixYgX//Oc/SUxM5J///Ged\naxG/4dHOjRakvLzc2XebmZmpLr30UmWxWNQbb7yhLrnkEjV16lR15MiRsz520aJFatiwYS59tTt3\n7lSxsbHq8OHDSimlhg4dqj777LPz1pGUlKRiY2NVVlaWy/YXXnhBXX311S7bPv/8c9W3b19VXV2t\n0tPTXfp09+zZo1asWOGy/9NPP63uvPNOpVTt+nT79eunEhISXL62bt2qlFLql19+Ud9//73LY6ZP\nn66eeuoppVRNn2tCQoLSNM35/dGjR6uvvvrK5TFTp05Vs2fPVkopNWDAAPWf//xHORwOpZRSBw4c\nUKmpqWet77XXXlNDhw51ec2fe+45dcsttyillNq4caPq06ePKigoUEop9fbbb6spU6ac9VgrVqxQ\nsbGxLrWey4033uis97ev4dKlS9WwYcOUzWZTSin1zDPPqIcffvi8x3zvvffUZZdddsb23zvezz//\nrGJjY9WOHTuc+69evVr17dtXlZeXqyVLlqgJEya4HG/Lli2qd+/eqqKi4rw1iXOTlm4jCQgIcPbd\nzps3j3vuuYekpCSWLFnCihUruPDCC52tiN9KTk6md+/e+Pr6OrfFx8djNBpJTU1tlPpSUlJISEhw\n2TZ48GBsNhsZGRln7N+vXz/i4+OZN28eDz/8MFdffTVLly7F4XDU+pz33XcfK1eudPnq168fUNP6\ni4yM5PXXX+cvf/kLEyZMYMOGDS7H79SpEzqdDoCysjLy8/N54oknGDhwoPNr+/btpKWlAfDoo48y\nf/58RowYwaOPPkp2djbdunU7Z31xcXFnvObJyckADBs2jLZt2/Ltt98C8OWXX561lQs1XUxQ0+/e\nEOPHj6eqqoqNGzdit9v55ptvznnOxjie0WhkwIABzn/379/f+X5ITk4mPT3d5bW+++67cTgcZGZm\nNuh5tnZyIa2RpaamsnPnTl588UU+/PBDBg4cSEhICGPHjuWdd94562NO/8H/LU3TGqUus9l8xjZ1\n4uLZ2c6xfv167r//fiZNmsTQoUOZNm0ay5cvJz09vdbnDA8Pp0uXLmf93tKlS3n++ee57rrrGDNm\nDA888ACvv/66yz6nvy42mw2A2bNnnzHs7OR+t956K5deeinff/8969ev56GHHuK6667j2WefPWsN\nBoPB5d+apmE0GgHQ6/VcddVVfP311wwdOpSUlBQmTJhw1uPEx8ej1+vZs2cPo0ePPuP7jzzyCBdf\nfDFXX331WR9/UmBgIJdccgmrV69GKYVS6qzHq63zHU+v17v0QZ98H+j1ehwOB4MHD+aFF14447hR\nUVH1rklIn26jmzdvHvfffz8+PjW/z06+kW022zkDtHv37hw8eJDq6mrntr1792Kz2X63pVYX3bt3\nZ+fOnS7bfv31V4xGI9HR0c4W5UmLFy9m0qRJvPTSS9x0003079+fzMzMRhvl8NFHH3HPPffwzDPP\ncP3119OrVy/S09PPefzw8HDCwsLIz8+nS5cuzq8PPviAjRs3UlpayrPPPouPjw+33XYb77zzDk88\n8QSrVq06Zw3Jycku/yc7d+6kR48ezn9fc8017Nixg88//5yRI0fSpk2bc9Z20UUXsXDhwjP+j3fs\n2MFXX31FSEhIrV6Xq6++msTERH788UcmTJjg/CVQX793PIvFQkpKivPfu3fvxtfXl65du9K9e3fS\n09Np376987UuLCzk1Vdfdf4CFPUjoduIkpKSSE5OdrZo+vfvz+bNm9m7dy/Lli1zXsH+rUmTJmE2\nm3nsscc4dOgQ27ZtY+bMmYwcOdIlBBpi6tSpZGRk8MILL5CamkpiYiKvvPIK1113HYGBgfj7+wM1\nF4XKysoIDQ1l165d7N+/n7S0NObMmcPPP//caFevQ0ND2bRpE6mpqRw6dIgnn3yS9PT03z3+XXfd\nxdy5c1m9ejVZWVnMmzePxYsXExMTQ3BwML/88gvPP/88qampJCcns2bNmnNe3IKayQyzZs0iJSWF\npUuXsnz5cu6++27n92NjY+nRowfvv//+eT/mz5gxgwMHDvDAAw+wbds2MjMzWblyJX/+858ZP348\nY8aMOeMxAQEBlJeXk5qa6hw1cOGFF6KUco4caajzHW/WrFns37+fX375hdmzZ3PDDTfg6+vLNddc\ng1KKJ554guTkZHbs2MGTTz6J1WptlCGQrZmEbiOaO3cuDz74oPMj26BBg7jhhhuYNm0aO3fuZNas\nWWd9nJ+fHwsWLKC8vJzrr7+eP/3pTwwaNKjWM8lqIyoqigULFrB7926uueYann76aa677jpnTW3b\ntuXaa6/l8ccfZ/78+fzf//0fHTp04JZbbuHmm28mLS2Nv/3tbyQnJzdK8D711FM4HA6uvfZa7rzz\nTjRN46677mLfvn3nfMydd97J7bffzssvv8zEiRP5/vvv+c9//uPsq37jjTcoLy9nypQp3HDDDQQE\nBPDKK6+c83gnA+m6665j/vz5PPPMM2fMsrvqqqvQ6/Vcdtllv/t8unbtyuLFiwkODuaRRx7hqquu\n4r///S+33347s2fPPuOTBMDIkSOJjY3lmmuuYf369UBNP+v48eNp27YtgwYN+t1z1sb5jjd+/Him\nTZvGww8/zIQJE3jssceAmq6Jd999l8LCQq6//noeeOABEhISmD17doNrau10qrE+LwrRAv3jH/+g\nqKjIrWHz4IMP0rNnTx566KEmO97GjRuZNm0au3fvPmt/v2g6ciFNiLPYtWsXhw4dYunSpb871rcx\n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\nQmCC\n",
      "text/plain": [
       "<matplotlib.figure.Figure at 0x20cf44bfac8>"
      ]
     },
     "metadata": {},
     "output_type": "display_data"
    }
   ],
   "source": [
    "plt.title(\"% of Total Fares by City Type\")\n",
    "plt.pie(fare, explode=explode, labels=types, colors=colors,\n",
    "        autopct=\"%1.1f%%\", shadow=True, startangle=90)\n",
    "plt.axis(\"equal\")\n",
    "\n",
    "plt.savefig('% of Total Fares by City Type')\n",
    "plt.show()"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 92,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "type\n",
       "Rural        5.193187\n",
       "Suburban    27.295388\n",
       "Urban       67.511425\n",
       "Name: date, dtype: float64"
      ]
     },
     "execution_count": 92,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "#% of Total Rides by City Type\n",
    "Total_Rides = combined_data['date'].count()\n",
    "\n",
    "Total_RidesType = combined_data.groupby(['type']).date.count()\n",
    "\n",
    "Rides = (Total_RidesType/Total_Rides)*100\n",
    "Rides"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 93,
   "metadata": {
    "collapsed": true
   },
   "outputs": [],
   "source": [
    " # Dataset Total Rides by City type\n",
    "types = [\"Rural\", \"Suburban\", \"Urban\",]\n",
    "rides = [5.2, 27.3, 67.5]\n",
    "colors = [\"yellowgreen\", \"red\", \"lightskyblue\"]\n",
    "explode = (0, 0, 0.05)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 94,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "image/png": "iVBORw0KGgoAAAANSUhEUgAAAV0AAAD4CAYAAABPLjVeAAAABHNCSVQICAgIfAhkiAAAAAlwSFlz\nAAALEgAACxIB0t1+/AAAADl0RVh0U29mdHdhcmUAbWF0cGxvdGxpYiB2ZXJzaW9uIDIuMS4wLCBo\ndHRwOi8vbWF0cGxvdGxpYi5vcmcvpW3flQAAIABJREFUeJzt3Xd8VGX69/HPmZbeQwgQCElI6BB6\nh1VBlKaoYMWCZdHd/a1lf4r1cXdZ91nbrg+Krn0Xy6qIrIoV6V1C7xBCOgmkT5Lp9/NHYCQQIHVm\nklzv1yuvwMyZM9e0b+65zjn30ZRSCiGEEB6h83YBQgjRnkjoCiGEB0noCiGEB0noCiGEB0noCiGE\nB0noCiGEB0noNoOffvqJCRMmMGbMGL744ota1/31r3/ltddea/J9fPfdd4wbN46BAweyevXqWtfN\nnz+fnj17XvBn4cKF9b6PgoKCei372WefMWbMmAteP378+PPqGDJkCHPmzGHPnj3u5f7whz/w0EMP\nXXA9DzzwAE8++WS9amqIjRs30rNnT6xWa7Ot026389ZbbzF9+nQGDhzIhAkTePrppyksLHQv8/e/\n/53Zs2e7/9+Q5/xsf/jDHy76mi9atKhZHpNoAUo0idPpVCNGjFBLly5V69atUwMGDFDFxcVKKaUK\nCgrU+PHjVUVFRZPvZ9KkSerxxx9XOTk5qrq6utZ15eXlqrCwUBUWFqotW7aolJQUtWvXLvdlZrP5\nkuvPzMxUKSkp6ujRo/Wq59NPP1WjR4++4PXjxo1Tb775pruGgoICtWvXLjVnzhw1atQoVVVV5a69\nvLz8guu5//771RNPPFGvmhpiw4YNKiUlRVkslmZZn81mU7feequaMmWK+uGHH1RWVpbaunWruvHG\nG9WkSZNUUVGRUkops9msSkpKlFINf87PdvZrvnHjRpWSkqL27dvnvqyysrJZHpdofgZvh35rV1xc\nTElJCVOnTsVkMhESEkJ2djYRERG88cYbzJkzh+Dg4CbfT3l5OUOGDKFLly7nXRcSEkJISAgAJSUl\nAERGRtKhQ4d6r1+1wDEywcHBtWqIiYnhueee44orrmDr1q1MmDDBXXdr984775CRkcHXX39NREQE\nAF27duWtt95i4sSJvP/++zz88MMEBQW5b9OU5/zs1/zUqVNAw19z4R3SXmiiiIgIAgMD2b17N5mZ\nmZSVlREbG0teXh6rV6/m1ltvrdd6jh8/zv3338+wYcMYMWIETz31FGazGYCePXtSUlLCE088weWX\nX97oWnft2sWcOXMYNGgQY8eO5aWXXsLhcOBwOLjyyisBmDJlivur6bJly5g+fTr9+vVj8ODBPPDA\nA+4PeGOZTCYAdLqat9657YUvvviCiRMnkpqayjPPPIPD4ah1+1WrVjFjxgwGDBjAtGnTWLZsmfu6\niooKHn74YUaMGMGgQYO49957ycrKumg9n332GWPHjmXw4ME8++yz7nbD3Llzefzxx2st+8orr3DH\nHXfUuZ4lS5Zwww03uAP3jJCQEN5++21uu+024Jf2Ql3P+eTJk3n11Vdr3f7RRx/liSeeuOhjuJCL\nrc/hcNCzZ0+WLFnClClTSE1N5e677yY3N9e9rNls5sknn2T48OGMGDGCBx98kJMnTzaqFvELCd0m\n0uv1PProo9x5551MmTKFBx54gJiYGBYtWsRdd91FQEDAJddRWlrKLbfcgtFo5MMPP2ThwoWkpaW5\nP2zr168nPDycJ554giVLljSqzvT0dG6//Xb3B+2Pf/wjS5cu5ZVXXsFgMPDJJ58A8OGHH3LnnXey\nbds2nnrqKe69916+//57Xn31Vfbu3cubb77ZqPuHmm8FzzzzDDExMQwePPi86zdu3MhTTz3F3Xff\nzeeff47JZGLNmjXu6w8ePMiDDz7Irbfeytdff828efNYsGAB3333HQAvv/wy+fn5LF68mCVLluBy\nuS7ZD/70009ZtGgRb7zxBuvWreO5554DYMaMGfz444/YbDb3ssuXL2f69OnnrcNsNpOdnU3//v3r\nvI/+/fsTExNT67K6nvPp06fz9ddfu5exWCysWLGizvusj/qs78UXX+R3v/sdn376KS6Xi3vvvdf9\nh+6JJ54gKyuLd955h3//+984nU7uuecenE5no+oRp3m7v9FWmM1md+82KytLXXHFFcpqtarXXntN\nXXbZZWrOnDkqNze3ztsuXrxYjRgxolavdufOnSolJUUdO3ZMKaXU8OHD1eeff37JOg4dOqRSUlJU\ndnZ2rcsXLFigZsyYUeuy//73v6pv377KYrGo48eP1+ov7tmzR33xxRe1ln/mmWfU3LlzlVL16+n2\n69dPpaamqtTUVDVgwADVt29fddddd9XqYT7yyCPqwQcfVEop9dvf/lY99NBD7uucTqe68sor3T3d\nhx9+WD3zzDO17mfhwoVq1qxZSiml7r33XnX33Xe7+5knTpxQ27dvr7O+Mz3dXbt2uS/77rvv3M+H\n2WxWAwcOVD/++KNSSqldu3apfv361dl/zs3NVSkpKWrz5s0XfD7OePnll931nvucZ2VlqZSUFLV/\n/36llFLLly9XY8eOVU6n86Lr3L9/v0pJSVH5+fm1Lr/Y+ux2u0pJSVFvvPGGe/mCggLVp08ftX79\nepWRkaFSUlLUyZMn3ddbLBY1cOBAtWbNmks+TnFh0tNtJmf36l599VXuu+8+Dh06xCeffMKXX37J\np59+yp///Gdef/3182575MgRevfujb+/v/uy/v37YzQaSU9PJyEhocn1HT16lNTU1FqXDRkyBLvd\nTmZmJn5+frWu69evHwEBAbz66qukp6eTnp7O0aNHGT58eL3vc968eUybNg2r1coHH3zAqlWr+N3v\nfkdSUlKdyx8+fJhZs2a5/6/T6ejXr1+tx5Cens6XX37pvszhcLift3nz5vHrX/+akSNHMnz4cCZO\nnMg111xzwfoMBkOt9ffv39/9fKSkpHDFFVewfPlyJk6cyFdffcVll11WZw/6TEuhvLy8ns9M3bp2\n7cqgQYNYvnw5vXv35uuvv2batGnuVkxzrs/lcgE174EzYmJiiI2N5ciRI1RXVwMwadKkWuu0WCxk\nZGQwfvz4Rj5KIe2FZpaens7OnTu57rrrSEtLY9CgQYSFhXH55ZeTlpZW523ODttznflwNNW5oQq/\nbMip6z7WrVvHNddcQ25uLsOHD2fBggW1dnWqj8jISOLj40lJSeFPf/oTqampzJs376K7SKlzNi4Z\njUb3v51OJ3fccQfLli1z/3z99dd8/vnnAAwePJhVq1axYMECwsPDeemll7j55ptrtQjOpmlarUA7\n8zycuc8ZM2awatUqKisr+fbbby/4NT8gIICUlJRau8Kd7Z///CfPP//8BR/z2WbMmME333xDRUUF\na9eubXRrob7rMxhqj7uUUuh0OhwOB35+frWe62XLlvH9999z7bXXNqmm9k5Ct5m9+uqr3H///e43\n85kPst1uv2CAJiUlcfDgQSwWi/uyvXv3YrfbSUxMbJa6kpKS2LlzZ63LduzYgdFoJC4uDk3Tal33\nn//8h+nTp/PXv/6Vm2++mQEDBpCVldWkLe7PPvssAH/84x/rvL5nz57s3r271mX79+93/zsxMZHs\n7Gzi4+PdP5s2beLjjz8G4PXXX2fv3r3MmDGDF198kY8//pgDBw5w5MiROu/PbreTnp7u/v+uXbvw\n9/d37yEyduxYgoKCePvtt7FarUyYMOGCj23mzJl89tlnlJaW1rq8tLSUxYsX13mbc59zqNmoVlhY\nyLvvvku3bt3o06fPBe+zPi61vn379rn/XVBQQEFBAb169SIpKQmr1YrVanU/11FRUTz//PNkZmY2\nqab2TkK3GR06dIgjR44wY8YMAAYMGMCWLVvYu3cvS5YsYdCgQXXebvr06fj5+fHoo49y+PBhtm3b\nxpNPPsno0aPp0aNHs9Q2Z84cMjMzWbBgAenp6axevZrnn3+e66+/nuDgYAIDA4GajVUVFRWEh4ez\na9cu9u/fT0ZGBi+++CIbNmy44KixPqKionjooYf46aefzjvAA+COO+5g5cqVvP/++2RkZPDSSy/V\nCsx77rmHH3/8kTfffJPMzEy+/fZb/va3v7l3k8rPz2fBggXs2LGD7OxsvvjiC0JDQ4mPj6+zHk3T\nmD9/Pnv27GHTpk288MIL3Hnnne49LPR6PVOmTOGdd95h8uTJ7svrcttttxEXF8ett97KihUryM7O\nZv369cydO5egoCDuu+++825z7nMOEB4ezvjx43nnnXeaPMqtz/oWLVrE2rVrOXToEI899hg9e/Zk\n6NChJCcnM2HCBB599FG2bdtGeno6jz32GLt37262gUB7JaHbjBYuXMhvfvMb91fWwYMHc+ONN3LX\nXXexc+dOnnrqqTpvFxAQwNtvv43ZbOaGG27gt7/9LYMHD673kWT1ERsby9tvv83u3bu55ppreOaZ\nZ7j++uvdNUVHR3Pdddfx2GOPsWjRIn7/+9/TuXNnbr31Vm655RYyMjL43//9X44cOdKk4L3xxhsZ\nOHAgCxYsOO9osCFDhvDyyy/z8ccfc80115CZmcnVV1/tvn7AgAG88sorfPXVV0ydOpXnn3+eefPm\nMXfuXAAee+wxBgwYwG9+8xumTJlCWloab7755gX3kw4ODmb69Once++9/M///A+TJk3it7/9ba1l\npk+fjtVqvWQAmkwm3nvvPa644gqef/55pk6dytNPP02/fv344IMPCA8PP+825z7nZ5zpg0+bNu3i\nT2Y9XWx9s2bN4i9/+Qs33XQTISEhvPnmm+737wsvvECvXr144IEHuOGGG6iurua9995rlv3O2zNN\nNeX7ohBt3IoVK/jLX/7CypUr62wHtIR//etffP/993z00Ucttj6Hw0Hfvn156623ZKOYh8neC0LU\nITs7m71797Jw4UJuuukmjwTuoUOHOHToEG+99Rbz58/3ufWJ5iHtBSHqkJOTw+OPP06XLl248847\nPXKf+/fv5+mnn2bcuHFMnTrV59Ynmoe0F0QtW7Zs4cEHH3RvwKusrCQuLo4XX3zxohuSLmb+/PlM\nmTJFvsYKgYx0RR1GjhzJ4sWLWbx4MUuXLsVoNLJy5UpvlyVEmyChKy7KZrNRWFhIWFhYrYlpzsyl\nO3/+fObNm8dNN91ESUkJTz75JHfffTfXXXcd//jHP7xVthA+SzakifNs3ryZOXPmUFRUhE6nY/bs\n2Rc9FHXkyJHceeed5OTkkJqayqxZs7BarYwfP54HH3zQg5UL4fskdMV5Ro4cyd///ndKSkqYO3cu\ncXFx5y1z9qaAM3NDhIeHs2fPHjZv3kxwcHCT9ucVoq2S9oK4oIiICF544QWeeuopTCaTey7V3Nxc\nysrK3Mud2Z1q6dKlhISE8NJLLzF37lwsFkuLTI4uRGsmI11xUT169GDOnDm8/fbbhISEMGvWLJKS\nkuoc/Y4aNYqHH36YtLQ0AgICiI+Pr3V+MCGE7DImhBAeJe0FIYTwIAldIYTwIAldIYTwIAldIYTw\nINl7QXiV02Wj2lFEtaMUi70Ei6OEakfN75qfUpzKjlJOXMpJXOgoUmPv9HbZQjSahK7wCJvTTHH1\nUYqrj1JqyaDMmkmpJZNK2wkU9T8PXIhf5xasUoiWJ6ErWkRxdTr55jTyK9I4WbUfsy0faP69E21O\nRZFFoWkaGmDUgb8B/PWg89Ck40I0hISuaBa/hOw2Tph3UO0o9sj9FlQrPjzirPM6k64mfP0NEKDX\nCDNBuJ9W83P634EGCWbhWRK6olGcLju5FVvIKF1Jdtk6j4XsGbknCti+5wAWYyiE9a9zGZur5qfc\nDr+MsmuPtv100CFAIzbwl58ov7rP1CtEc5DQFfXncMAPP5BbmcaK5BXYXGavlZJ+PIv045kQ2hHC\nGr8eqwtyKhU5lb+EsUkHHQM14oI0uofU/NbrJIRF85DQFZe2dSt88AHqk0/QCgvx69MN2+Job1cF\ntMyI1OaCbLMi26zYVFDTJ+4aXBPACSE6OgRIAIvGk9AVdbNaYfFi1Msvox04AMCZqIk6kE1gVgxV\n3eq/10FrZnfBsXLFsXIFuAg1Qq8IHX0idMQGSgCLhpHQFbWVlcEbb+D6+9/RFRRQV6RoSpH4tYO9\nD7TPY2vK7bC10MXWQhcRftA7vCaAo2UELOpBQlfUyM+Hf/wD16JF6MzmSx6qmLQqn70PdPFIab6s\nxAobC1xsLHAREwCDo/X0jdQwSg9YXICEbnt36BDq+edh8WI0u73ex4XHHCsg+FhXzInto8VQH4XV\n8F22k1V50D9Sx+BoHZH+Er6itvb5/VDA/v2oa69F9e6N9u67aHZ7g1eRuLzht2kPrE7YdtLFmwcc\nfHLUwbFy+cMkfiGh296YzTgfegjXgAFo//0vWhPmsE9cld+MhbVNGRWKT9Od/OuQg/QyCV8hoduu\nuD76CFv37uj/8Q90zrqP4mqIDpmFhB6Wt1B95FcpPjsm4SskdNuHAwewjByJ7tZbMRUVNeuqE76R\nM/42xNnhe7xCwrc9ktBty8xm7L//Pa7+/fHfsqVF7iJpdV6LrLety69S/OeokyXHHJRY5TSF7YmE\nbhvl/OQTbAkJGP/f/2uWVsKFRGWfIuyAvsXW39YdLVO8fcDBqlwnNqeEb3sgodvWVFZSOWMG+ptu\nwnTqlEfuMnG5xSP301Y5FWwpdPH2AQcHS6Xl0NZJ6LYh1p9/xtyjB0FffeXR+01aIy2G5lBuh2UZ\nTpZlOKhyyKi3rZLQbSNKXngB/ZgxBJ844fH7jsgrImKPtBiay8FSxTsHHByWUW+bJKHbyqmqKk5O\nnkzEo49iaMQBDs0l8Ztqr913W1TpgKUZTr7OdGCRXm+bIqHbitl276YiOZkOP/zg7VJIXJPr7RLa\npL3FNaPeLLOMetsKCd1WqnThQrRhwwjN841+anhBCZE7pMXQEirs8J8jTrYWttxeKMJzJHRbGeVy\nUXDjjYT/z/9gtPnWgQmJ30qLoaW4gJW5LpZlOGTXslZOQrcVsZnN5I4ZQ8dPP/V2KXVKWpPt7RLa\nvIOlin8fdlBkkeBtrSR0W4nKEyc4NWQIcZs3e7uUCwo9VUb0z/KWammnLPCvQw6OyhwOrZJ8QlqB\nssOHqRo2jM6HD3u7lEuSFoNn2Fzw+TEnu4okeFsbCV0fV7hjB47x4+mQk+PtUuolaV0WyiVffT1B\nAd9mOVmfLxvYWhMJXR+Ws24dhiuvJKqgwNul1FtwcQUdt8oJSTxp/QkX32Y5cDVhbmThORK6Pip7\n1SqCZ84k0kPzJzSnxG/N3i6h3dlVpFh6zIlDvmX4PAldH3R89WpCbriB8Gae+9ZTEtdno2S3Jo87\nWq5YmiHB6+skdH3M0Y0bCbjtNsKLi71dSqMFlZrptEkOlPCGY+WKLzKcOKXV4LMkdH3I8b170e65\nh465rf+Q2sTvpMXgLenliv9mOKXH66MkdH1EUV4epfPmkXTggLdLaRYJG7LB4e0q2q/DZYovj0vw\n+iIJXR9QbTZz8P77Sd2wwdulNJvA8ko6rZcWgzcdLFV8kyW7k/kaCV0vc9jtbHnkEUYuX+7tUppd\n4nfl3i6h3dtbrGQ/Xh8jO1R6kVKK9c89x8h//xt9C57HzFsSNmWxwd6bfz9dhSmw5rKwGB1Xz/N3\nL7PtGxsHN9b0IRJTDYy+wURFkYuvXrGg08PU3/kTEqlj/zo7Oj2kTPfGI2nd1p9wEeGn0TdSxli+\nQELXi7a89x6DXnkFf0vbPMdYgLmamJ80AG56JvC860sLXBxY7+DWBQFowMd/rCZ5mJ7MvU6GTTcB\ncGizg9SJRo6mOZn+ez9Plt+mfJPlJNQEXYMleL1NXgEv2bNqFV3/9CfCSkq8XUrL+qYCu03x2XPV\nfPLnavKO/DKiD4nSuH5+ADqdhqbTcDlBb9Iw+mvYrQq7RWH009j2jZ0hVxvRNM2LD6R1cypYeswp\np3v3ARK6XpC5bx+VCxbQJTPT26W0uMQ9+QybbOKGx/2ZdI8fy1+14Dp94ITeoBEYqqGUYvUHVmK6\n64jspKP3GANZe51kH3AS309P6QkXSsGPb1tY9+1RLz+i1qvaCUvSZT5eb5PQ9bCq8nK2v/IKQ9eu\n9XYpHtGzwsxEuwlN04jspCMgRMNc+suH3mFTLH/Vis2imDi3pn1g8te4ap4/k+/zJ+0bOyNnmti8\nzMYVc/3YsyWPqqoqbz2cVq/ICt9nt73tB62JhK4HKaVY8c47jFu+HIOjfezEuiQ0lFVf1OzFYC52\nYatWBIfXtAmUUix7yUKHeB1X3uOPTle7fXAy24nBBOEddThsCg1wuRQ2HztjRmuzr0TJlJBeJBvS\nPGjP6tXELV1KtI+c18wTbigrY+vJYD5+Rg86mPxrf7Z/Zye8ow6lIPuAE4ddkbGz5o/Q+Jv86JxS\ns3/vlmV2Jt5VM/rtO97Ih89U06tPZ8LDw732eNqKH7OddArUiAmQPrmnaUrJISueUF5UxOpHHmHq\n4sXoXe1vlPH9n4aSNbXpjzslagYT4v8Pazf/zPY9+9HCYqlOvrwZKmx/Iv3gzp4GTHoJXk+S9oIH\nuFwuVr75JuO/+aZdBi5A4g+l3i5BnKPYCitypL/raRK6HrD9++9JWraM8JMnvV2K13T/OQtdlYyo\nfM3uYkVGefscCHiLhG4LK8rLo2DxYvr+/LO3S/Eqo9VG1x+9XYWoy3fZTtmNzIMkdFuQ0+lk5Xvv\nMWrlSnTSOifpR2kx+KIyG6zJl9Gup0jotqCtX35J7ObNRLaic5y1pG5pWegrpMXgi7afdJFjluD1\nBAndFlJZVsaRDRsYtH69t0vxGUabnW4/eLsKUZczZxZ2yql+WpyEbgvZuGQJvffsIbhUvlKfLWlF\n6z0NUVtXZIWfT8pot6VJ6LaA4hMnKNi1i/4yyj1P1+3ZGMqkxeCrNp5wUWmX0W5LktBtARs/+4yB\nO3bgL3MEnMfgcBD/nXyofZXNBWtk0vMWJaHbzPKOHqVi/356bdni7VJ8VtKK1nlq+fZiT5HiZLX8\nYWwpXg/dN998kzvvvJO5c+dy9913s3fv3jqXy8nJYfbs2Y26j/nz57PWA7N6KaXYvHQpQ37+GaPd\n3uL311rF7c7BWCItBl+lgNV5MtptKV6d8Obo0aOsXLmSjz/+GE3TOHDgAI899hhffvmlN8tqtIyd\nO3EdPkyPHTu8XYpP0zucdP9WceQWb1ciLiS9XJFtdsmZJlqAV5/RyMhI8vLyWLJkCQUFBfTu3Zsl\nS5YwZ84c0tPTAfj4449ZuHAhAMXFxcybN4/Zs2fz2muvAbVHsWvXrmX+/PkAXHbZZdx999385S9/\nAeCjjz7ijjvu4LbbbiPz9OThL730EnfddRezZ8/m8ccfB2DhwoU89thj3HPPPUyZMoV169bV67G4\nXC5+Xr6cQWlp6Nrp/AoNkbjilLdLEJew6YS8j1uC10P39ddfZ/v27dx4441cddVVrFq16oLLV1VV\n8cILL/Dxxx+zbt06Dh48eMFl8/PzefHFF3nyyScBGDx4MP/617+49957eeGFFzCbzYSGhvLee+/x\nn//8h507d1Jw+iAGk8nE22+/zZNPPsn7779fr8eyf8MGnAUFxF+gPSJq67I3B1ORtBh82bEKxYkq\n6e02N6+2FzIzMwkODuavf/0rAHv27OG+++4jOjravczZM0/26tWLkJAQAPr3709GRkat9Z29bERE\nBBEREe7/Dx06FIBBgwbx/PPP4+fnR3FxMQ8//DCBgYFUVVVhP92H7d27NwCxsbH1mjBbKcW+NWvo\nc+BAu5mcvKn0Thfdv1EcnuPtSsTFbCpwMjNBpt1uTl4d6R46dIhnn30Wq9UKQEJCAiEhIYSHh3Py\n9Ixc+/fvdy+fnp5OZWUlDoeD3bt3k5ycjMlkqnNZna72Q9u9ezcA27ZtIzk5mbVr15Kfn8/LL7/M\nww8/jMVicYd2Q0+AmLV/P5XFxSRv29bAZ6B9S/qp/c661locLlUUWWS025y8+ifsyiuvJD09nVmz\nZhEYGIhSikcffRSj0cif/vQnOnXqRExMjHv5sLAwHnroIYqLi5kyZQo9evRg1qxZPPHEE3z11Vd0\n7979gve1a9cubr/9djRN47nnnsNkMrFo0SJmz56NyWSia9euFBYWNupx7Fqxgh45OQSVlTXq9u1V\n5325+BV0xNpReoe+SgGbC5xMjZfRbnORM0c0UdmpU3z+f/8vVy9bRqfTG/9E/a377SAO3lX/bxZy\n5gjP02nwm74GgozSg28Osj9IE23/7jvCbDY6Hjvm7VJapcSV0mLwdS4Fe4rl20hzkdBtAqfDQc7B\ngyTv3i3z5TZSpwO5+OfL29DX7SpyIV+Km4e825vgaFoaDouFxJ07vV1Kq6VTisSvZY8PX1dihUyz\nhG5zkNBtgoObNtGtsJBg2YDWJIkrG7cBU3jWrlPSYmgOErqNZC4poSg3l64XOUBD1E/skXwCc+St\n6OsOlymqHDLabSp5pzfS7pUrMZhMdDp61NultHqaUiRIi8HnORUcKJHRblNJ6DZSfno6EeXlhJSU\neLuUNiFp5QlvlyDq4VCpjHSbSkK3EarNZspPnqTzkSPeLqXN6Jh+gqDj8nb0ddlmRZWcWaJJ5F3e\nCBk7d4Km0VlaC80qcbnMQezrFHCkTEK3KSR0G+H4nj0EGo3EHD/u7VLalKRV0mJoDQ6VSV+3KeSA\n6gZyuVwU5+URl5GB3umZ2fXtwBOxseQaDNh0Ou4vKuLrkBBOGWpevlyjkYHV1fz9xC+hVaVpPNKp\nE2U6HQFK8cKJE0Q6nXwWGspnYWH0sVp59vRcE4/ExvLHwkKCvTwPcIeMAkLSu1GRJGct8GWZFQqL\nU+Gvl8OCG0NGug1UmJmJtarKo/3cL0NDCXc6+Sgnh7dycvhzTAx/P3GCxTk5vJqXR4jTyeMnax9O\n+2lYGH0tFj7KyWFqRQWLIiMB+G9oKP/JzqbAYKBMp2N1UBBDqqu9HrhnJC6/9FSawrucCjLKpcXQ\nWBK6DXRoyxb8AgM92s+9qqKC35/65UwL+rMOx1wYFcVtpaXEnDPqvrO0lPuLiwHIMxiIPn29v1JY\nNQ2HpqEDPg8NZbYPHdyRuCpANrc2AAAdXElEQVTP2yWIesiskNBtLAndBjqVmUlYaSnBpaUeu88g\npQhWCrOm8T+dO/NgUc3ZdIv0ejYFBnJdeXmdt9MDt8fF8UF4OBMqKwGYV1TEw506cWVFBV+GhHB9\neTlvR0byf2JiOGY0euohXVB01klCD+m9XYa4hCyzb3wzao0kdBugqqKC8qIionJzPX7f+QYDt3ft\nyjXl5UyvqADgu+BgplVUcLGI+ndODh9mZ/O7Tp0AGGqx8HpeHlebzaQFBNDNZqPQYOD3p07xWlSU\nBx7JpSUtt3i7BHEJxVYwy65jjSKh2wDHd+0CIKyRk5031im9nrlduvC/J09yw1mj2k2BgYw/PYI9\n1z8jIlh2+tRGgUqdF8z/jIzk3pISLDodOqXQgCqdb7wdElfne7sEUQ9ZMgFOo/jGp6yVyE9PxxQQ\nQLiHQ/eNyEjK9XoWRUUxJy6OOXFxWDSNDJOJrvba+7bO7dIFG3B9eTlfhYYyJy6OR2Jjee6sPRty\nDAbKdTp6W630slrJNxq5r0sXbvNgy+RiInNPEb5P3pq+Lkv6uo0iu4w1gLmkBE3TPB66T508yVMn\nz5/se/npU8mf7d3TrY9op5N3LtAGiXM4+OPpx6ADXsvzvY1XicutbO/r/R6zuLBsswsu2twSdZHh\nRAOYS0owWK1yLjQPSFrj+b65aJhiK9hdMtptKAndeqo2m7FVVXl8lNtehZ8oJnK3jKJ8mQJOVkvo\nNpSEbj0V5+fjcjo9vhGtPUtYXu3tEsQlFMpL1GASuvWUd+QIxoAAwgsKvF1Ku9FjTY63SxCXUCgj\n3QaT0K2nkrw8DEYj4XVs0BItI/RkKdFp0mLwZRK6DSehW0/m07tTSXvBsxK+rfJ2CeIiTlokdBtK\nQrcelFJUlZait9vxr5IQ8KSktdko2ULus6xOqJbzpjWIhG49VJaWYrNaMVXLVgNPCykqJ+ZnaTH4\nsnKZGK5BJHTrobKsDJfDgckicwJ4Q6K0GHxauczB0CASuvVQVV6OptPJSNdLEtdLi8GXldvktWkI\nCd16qCwrQ28wyEjXS4JLKui4SY5Y91UV0l5oEAndeqguL0dvNEroelHSd2ZvlyAuQNoLDSOhWw/V\nFRXo9HppL3hR4oYsNJeck8sXVcpJnBtEQrce7FYrmqbJSNeLAssq6bu/k7fLEHWwyUkkGkRCtx4c\ntpqmlVFC16t6/WT1dgmiDjbZyNkgErr1cCZ0ZaTrXeHfbEfnlBaDr7E5L72M+IWEbj3YrTUjLINN\nNtN6k3aqiKQdsheDr5H2QsNI6NbDmZGu8pFziLVb/v7EmDt6uwpxDruEboPIsKEenA4HAC69HI7q\nDU69nq09ujLqp/UYunTxdjniHC4FTpdCr5PWT31I6NaDptW8mVwy0vUop05HRmoq24cOxRwbxSgJ\nXJ8lm9LqT0K3HrTTYes0yNPlCS5NI2PgQLYPHYrq3p1BkyfTY8iQ85ZzhnfB2WWAFyoU55Ixbv1J\nitSD7nRbQdoLLculaWT268f2ESOwd+tG6qRJpAwfju6cbxhHy1zsMiRj7xHkpUrFuTRJ3XqT0K2H\nM6Fr9/PzciVtkwKy+vYlbcQIbPHxDLj8cnqNHn1e2GaUu1idY6fAqgO9BK6v0ACdpG69SejWw5kP\nv93f38uVtC0KyOnVi7SRI6k6Hba9x4xBf843isyKmrDNt+iQHW58j17ytkEkdOtBf7qXa5ORbrPJ\nTUkhbdQozPHx9Jswgb4TJpwXtjlmF6ty7ORWS9j6MoO8NA0ioVsPBpMJkJFuc8jr0YO0UaMo796d\nPuPGMeCyy9x/1NzLVNaMbLOqJGxbA5O8RA0ioVsPZ0LXJqHbaCcSEtg+ejQlCQn0Gj2aqydOxGA0\n1l6mSrE6x87xSg0J29Yj0CD9hYaQ0K0Hg8lUc3LKsDBvl9LqFMTHs330aIoSE+k5ahSTJk3CePqP\n2BmF1YrVuXaOVWjIzketT6Dx0suIX0jo1oN/cDAupxNzRAROnQ69S457vJSTcXHsGDuWE4mJpAwf\nzsSrrsJ4Tk/8VLViTa6dI+XIPketWKCkSIPI01UPUZ07s99qRR8UhDkigrCiIm+X5LOKOndmx9ix\n5CUl0WPoUG6aMgXTOW2ZYotiTZ6DQ6WqJmwlb1u1IGkvNIiEbj1Ed+2KctbMX1cRHS2hW4fi2Fh2\njhtHTlISiYMHc+O0afgFBNRapsSqWJfnYH/JmbCVD2tbICPdhpGnqx6CIyPRn97oUx4Z6eVqfEtp\nTAw7x47leI8eJA4ezOxp0/APqn3gQpmtJmz3FSuUhG2bE2SU17MhJHTrwWgy4R8UhMvloiI62tvl\n+ISy6Gh2jRtHRnIy3QYM4MZrriEgOLjWMuU2xYZ8B7uLXChNJ2HbRkXI7usNIqFbTwGhoVSWllIe\nFeXtUryqPDKS3WPHciQlhfj+/Zk1cyaBISG1ljHbFRvzHew4dSZsZfevtizKT/6YNoSEbj0FhYVR\nWVpKRTsNXXN4OLvHjuVwz5507deP2TNnEnTOLnSVdsWmEw62n3LhQsK2PQg0gL9sSGsQCd16Co+N\nJe/oUSzBwdj8/DBZ28dJEivDwtgzZgwHe/akS9++XD9zJiHn9LWrHYrNJ5xsO+nEiRxF1p5Eyii3\nwSR06yk2IYGdP/6IwWikIiqKqLw8b5fUoqpCQtg7ZgwHevcmtndvZs6cSdg5/WyLQ7GlwMnWQgnb\n9ipKDtJsMAndegrv2NE9mXlxp05tNnSrg4JqwrZPHzr07Mk1111HeExMrWWsTsXWQhdbTthxoEfC\ntv2SkW7DSejWU2BYmPvw1YKEBJLT0rxcUfOyBAayf/Ro9vTtS3RyMtOuv57I2Nhay9icim0nXWzK\nt2NHD8ik7u1dx0AJ3YaS0K0nnU5HUHg41qoqChISULSNA6msAQEcGDWK3X37EpmczNTrriP6nHOR\n2V2KtJMuNubbsSkJW1FDAzpL6DaYhG4DRHftSvaBA1gDAymJjSXyxAlvl9RoNj8/Dowcye7+/Qnr\n0YOrZ86kQ7dutZZxuBTbT7rYkG/HKmErzhHtDyaZwbzBJHQbIGnwYI5u20ZASAgFCQmtMnTtJhMH\nR4xg14ABhCQlMemaa4hNTKy1jNOl2FnkYn2unWoJW3EBXYKkl98YEroNEJuY6J5b90RCAr03bfJy\nRfVnNxo5PGwYOwcNIjAhgctmzKBLcnKtZZxKsadIsTbXRpVLwlZcXJcgGeU2hoRuAxiMRsI7dqSy\ntJTC+PhWMc2jw2DgyNCh7Bg0CP+EBCZMn06Xnj3Rzjok16UUe4oV63JtmJ0StqJ+JHQbR0K3gWLi\n4zl66hSYTBTFxRGTleXtkurk1Os5MmQIOwYPxti9O2OmTaNbnz61wlYpxb4SxZocGxUStqIBggwQ\n6S+h2xgSug2UNGQI+9evJyAkhBMJCT4Xuk69nmOpqaQNHYohPp6RU6fSvX//88L2YKlidY6NMoeE\nrWi4xFAJ3MaS0G2g6Lg4TKfniS1ITIQ1a7xcUQ2XTsexgQPZPnQoWvfuDJ08maTBg88L20NlNSPb\nEruErWi8pDDZiNZYEroNpNPpiIiNpfzUKU7FxWEJDMS/qspr9bg0jeMDBpA2fDiu+HgGXXklyUOH\n1gpbgCNlLlbn2CiySdh6wu5lb5GVthqXw06vSTeSt2cT1aWnADCfzKND8gB+9fsX3csrpfj0gSsI\nja3Zba9DykCG3vwQO5YsInfXBroOnsDAmffhcjpY/cr/8qsHX0Sn887rqNMgIURGuo0lodsInZOT\nKcrNxejnx/H+/em1ZYvHa3BpGln9+pE2fDj2+HhSJ04kZcQIdLraI5D0Mherc+2ctOqQsPWM/H1b\nKTy8k6l/XIzDZmHvV++5A9ZqLuO7P89l+O2P1bpNRUE2UQm9mfjoa7XXtWcz0/78Id88ewcDZ97H\noRWfkXLZdV4LXICuQRp+sn9uo0noNkLK8OHs/PFHjH5+pA8a5NHQVUBWnz6kjRyJNT6egZdfTq/R\no88L2+PlLlbl2CmwykQ0npa7ewMRXZP56aXfY682M+zWR9zX7VjyGr0n30JgRIdatzl1bB+VxYV8\n+6e70Jv8GXH7o4R1TkAzGHA67Gg6HbaqCgoP7aD35Js9/ZBqkX5u00joNkJwRAQRnTpRXVFBWceO\nFHXqRFR+fovfb3avXmwfOZKq7t3pN2ECfcaNQ6+vPeLJMrtYnWMnr1rC1lusFaWYT+Yx8bFFmAtz\nWPHC77ju5a+wlBeTv3fLeaNcgMCIDgy49h4SRk6m4OB21r46n+nPfUKfybew6u8P0XfK7ez+79v0\nm34XP3/4Mg5rNanX/ZqAcM+fySRZ+rlNIqHbSD1HjGDLf/+LX1AQx1JTWzR0c5OTSRs1CnP37vQZ\nN47+v/oVekPtly7HXNNGyKmSsPU2v+BwwjonoDcYa34bTVjKizm+5UcSx0ypszUQndgXTV/zmnbs\nNZjKkkKUUsQPn0j88IlUFOaQu3sDlvJi/EMj6NTnSvZ/9yFDbvq9Rx9bp0BNdhVrIvl0NlLy8OHu\no9OO9++PU9/8Pbb8pCSWz5nD6ptuouttt3Hj00+TOnFircDNr3Tx0SErHxxxng5c4W0dew4id9d6\nlFJUFRfisFbjFxJO3p5NdEkdV+dtdix5nf3fLAagOPMgwVGdam0M3bX0nwyc+Wsc1uqa0NY07BbP\nb8DtFymB21Qy0m0ko8lEx8RECjMzsQcEkNOrF/H79jXLuk90786OMWMoSkig9+jRTJ44EcPpsxG7\nl6lSrMm1k2HWkL+dvqXrkF9x4mAaXz95E0opRs19Cp1OT3n+cUJi4mot+/1f7mXiY4sYcM3drH1t\nPtk71qLT6Rl7/wL3MoWHdxLcoTOBER3oPGA0K174LRmbv2f0Pc949HHpUPSJkPdaU2lKKeXtIlqr\ngowMlr/6Kv4hIcSmp3P5Bx80aX2F3bqxfcwYTiYm0mvkSFKvvNI9h697meqasE0vR86uKzyqR5jG\nDYkyTmsqeQabIKZ7d4IjI3HY7ZxITKQyNJSg8vIGr+dUXBzbx47lRGIiKcOHc8VVV2H0q31e61MW\nxdpcO4fLqAlbyVvhYf0iZZTbHCR0m0DTNLr168ehLVswmkxkDBxIv3Xr6n37os6d2TlmDLk9etBj\nyBBumjoVk3/tk04VWxRr8xwcLFUStsJr/PXQQ3YVaxYSuk004PLLObBhA5hMHBk2jN4bN6J3Oi96\nm5KOHdk5bhxZSUkkDRnCjVOn4hcYWGuZUqtiXZ6DfSVnwlbe8MJ7BkfrMOjkPdgcJHSbKDAkhKi4\nOCqKiqgOCSF90CBStm2rc9nSDh3YNX48GUlJJKSmcuOMGfgHBdVapsymWJ/nYG+xC6XpJGyF1+lQ\nDO4grYXmIqHbDAZNnMiP776Lf3Aw+8eOJWn79lrz7JZFRbF73DjSk5OJHziQG6+5hoDg4FrrqLAp\nNuQ72FV0JmzlTS58Q58IHcFG+ePfXCR0m0Fc796EduiAtaqKqrAwMgYOpMeOHVRERLB73DiOpqQQ\n168fs2fOJDA0tNZtzXbFxnwHO0+5cEnYCh80LEbm7GhOsstYMzm2axerP/gA/6AggkpKiDl2jEM9\nexLXty8jZ84kODy81vJVdsXGEw62n3Lhkv1shY/qGgS3phgvvaCoNxnpNpOEAQNIi4zEWl1NsclE\n4LXXcv3MmYRERtZartqh2FzgZFuhEydyyK7wbSM7yii3uUnoNhNN0xg6ZQoHN21i9A03EBZdeyIS\ni1OxtcDJ1gIHDvRI2Apf1zlAyWTlLUDaCx6glOL93eUUuAIvvbAQPuLWZD1dgyV0m5uMdFvYgSPp\nrNuSRqnLH/pf7e1yhKiXboEuugZLL7clyJ+xFuRyufhu5TpsdjuBzgr0ZbneLkmIS1OKy7uaLr2c\naBQJ3Rak0+kYMXgAVqsNAL+83eC6+NFqQnhbj1CIDZT9cluKhG4LGz5oIH5+NaMGnbUC46kjXq5I\niAvTlIsrukpboSVJ6LYwg0HPuBFDqK62AmA6sR/N5r2zBwtxMcM76Ijwk1FuS5LQ9YABvXsSHRmO\nUgrN5cCUt9vbJQlxHj9lY2wX2bbe0iR0PUDTNKZOnODu7RpLs9CZC71clRC1TUv0xygzibU4CV0P\niYmOoldyIna7HQC/nO2yUU34jK4mK8nh9Tv6bMuWLTz00EO1LnvxxRdZunRprcsuv/xyrFZrs9XY\nVkjoetCkcaPdZ4LVW8oxFez3ckVCgM5l55qUoEsvKJqFNHA8yM/PxLgRQ1i5fjP+/n4YCw7iCO2E\nKyj60jcWooVM7qpvtqkbZ82ahdFoZPbs2QA888wz5ObmEhUVxd/+9jccDgdPPvkkFRUVlJSUMGvW\nLG655RbmzJlDr169OHLkCGazmVdeeYUuXbo0S02+Rka6HjaoX286deyA0+lEQ+GfuRWcdm+XJdqp\nzloFA2P8Lr1gPWiahtVq5aOPPuLaa68F4Oabb+aDDz6gS5cufPrpp2RmZjJ16lTeffdd3njjDd5/\n/3337QcMGMD777/PmDFjWL58ebPU5IskdD1M0zSuvWoiZ2a80NnMNQdNCOFhBkcVs/uFX3rBc/j7\n+2Oz2WpdVlVVhZ+fHwkJCe7LjEYjqampAAwePJiMjAyio6NZsWIFf/jDH3j99ddxOBzu5fv06QNA\nbGxsm+4FS+h6QVBgABPHjaK62gKAsSgdfXm+l6sS7YpycV0Pf/wNDY+ApKQkDhw4QGFhzR44VquV\nn3/+mcrKSnS6X9Znt9s5cOAAANu2bSM5OZl3332X1NRUXnzxRa666ira43xb0tP1kn69kjmUnkFW\nbj5GowG/rK1Up0xCmWQmMtHy+gRUkRgR0ajbBgcHM3/+fH7961/j7++P3W5nzpw5dOvWjY0bN7qX\nMxqNLF68mMzMTDp37swjjzxCWloazz77LF999RXh4eHo9frzRs1tnUzt6EVWq41/fvAJmqahaRrO\ngAiqky8HnUwcLVpOsL2UB4ZFo5OTnnqFtBe8yM/PxMyrJ7oPmtBXl9TsvytEC9FZK7hzYIQErhdJ\n6HpZ186dGDdiCBZLzYYDY3EGhlPpXq5KtElOOzckGgj2k66iN0no+oDhgwbQo3s3bGeOVsvdga7y\nlJerEm2KcjEqtJzEmNBLLytalISuD9A0jWmTLiMkKAiXy4WmXPhnbECzVni7NNFGdHMWMiEl1ttl\nCCR0fYbBoOfGGVfjdLpQSqFzWAlIX4tmr/Z2aaKVC63M5eahcd4uQ5wmoetDQkOCuX7qlVitNW0G\nna0S/2PrwNm+dqkRzcdUlsO9I+LQZMOZz5DQ9THdunRi6sQJ7g1r+upS/DM2yIxkosH0ZfncMywW\no1E2nPkSCV0f1Ds5kctGj3AHr8F8Ev/MLaBcXq5MtBZaxUnuSo0gNCjA26WIc0jo+qghA/sydGB/\nLKf34TWU5eB/fLMEr7gkrbKYW3v7Ex0e4u1SRB0kdH3YhFFD6ZOcVDt4MzZKq0FckFZRyKwEjbgO\nkd4uRVyAhK4P0zSNqy8fR58eiVgsp4O3PO90j9dxiVuL9kYrzeOark4Su8R4uxRxETL3QiuglOKH\nNRvYc+Aw/v41c586gmOwJIwBvZwuW4BWnMX1SX706C67hvk6Cd1WQinFT+s3s3PfQfz9TAA4AyOx\nJIxFGf29XJ3wJt2pDG7qG0a3zh29XYqoBwndVmb1xp/5eeduAgJqgtZlCsSSMA5XQJiXKxPeoM/b\ny+3Du9GxQ5S3SxH1JKHbCm1O28m6rdsJON1qUDoDlu6jcIZ28nJlwmNcDkzHt3DXFYOICJc/uK2J\nhG4rdTg9g69+XI3JZETTNBQati6p2Dske7s00dJslYRmb+H2q8cSHCRn8W1tJHRbscJTRfznv9+i\nlAu9vmbic3tUItYuqaCTo5DapIqTxFcc5IbJ4zEa5DVujSR0W7mqagsfffE15WYzJmPNngxO/zAs\n3Ueh/GUav7ZEyz/A0HALl48aJnMptGISum2Aw+Hky+9/Ij0rmwD/mg1sSqfHGjcYR2TCJW4tfJ7d\ngj59I1MGJ9G3Zw9vVyOaSEK3DUnbvY/VG7e6+7wA9oh4rHGDZX/eVkoryyM4N41ZkycQEy17KLQF\nErptTFFJKZ999T1Vlmp3u8FlCsbSbRiu4A5erk7Um8uJlrWD3kEWrr58nPRv2xAJ3TbI4XDy7cq1\nHDh6jMDT+/MqwB7dA1un/jLq9XG68hPoj//M1aMG0iclydvliGYmoduG7Tt0lBXrNqKUwnB6pOQy\nBmKNG4QzrIuXqxPncVjQZabR0VXKDdOuJCgw0NsViRYgodvGVVssfL1iDRlZOe5RL4AjrAvWLqko\nk+zn6XVKoS86hj5rB2MH92NYaj/ZO6ENk9BtJw4fy+CHNRux2e3uXq/SdNg7pGDr2Av0Ji9X2D7p\nKotQGT+TGG5gyhW/IihQJh1v6yR02xG7w8GKtZvYd+gIJpMRna5mZk+lN2GL7YM9Kgl0ei9X2T5o\nVjO67J0EVuYzecJYeiR083ZJwkMkdNuhkrJyvl25jtz8E/j7+7m/yrpMQdg69ccR3hXk622L0GxV\n6PP3QcFhUnv3ZMLoYbJnQjsjoduO5eSf4IfVGygqKXXPWgbg8gvBFtMLR0Q3Gfk2E81qxlB4CGfu\nAXrExzH5V2NkQ1k7JaHbziml2H84nbWbf6ayqto9STqAyxiAvUMK9qhE2c2skXSVRRgLD2I7cYxu\nnTsyafxooiMjvF2W8CIJXQGAy+Viz4HDbNmxm9LyCgLOajsovRF7VA/sUQkov2AvV9oKKBf68nz0\n+ftxluTTpVMsV4wdQccO0d6uTPgACV1Ri1KKoxlZrP85jcJTJQQGnBW+gDM4BkdUIo6wLtJ6OIdm\nrcBYfBxVeBSsVSTFd2XCqGFEhMnEQ+IXErrignLyC1i7eRt5BYXodRpG4y8tBqU3YY+IxxHVHVdA\nO/667LRhKM3BWHwc26lc/P1N9E5OYsywQe7Jh4Q4m4SuuKTKqmq27tzNoaMZlFWYCQzwr7XzvssU\njCOsC46wLriCIkFr4yeZdlgxlOdjKMvDVZyN02alY4doBvbpSd+eyRgM8g1AXJiErqg3pRQ5eQVs\n3r6TnPwCHA4n/v6m2gFs8MMZ2gVHWGecwR3azAY4zVKGoSwfQ3keVJzEarEQGhJMSmJ3hg8aQHCQ\n7Ikg6kdCVzSKzWbnUPpx9h0+QsHJIixW63kjYIWGKzACZ1AHnMHROIOiweB3kbX6COVCZylDby5C\nV3UKvfkUzupy7DY7oSHBdO4Yw5CBfencMUYO1xUNJqErmszpdHI8J5ed+w6RX1BIZVU1BoMeP1Pt\nQ4sV4PIPwxUYics/FFdAGC7/MJTRi4e+upzorGY0azn66jJ0VUXoK4vAacditaKhIzoyjPiuXUjt\n04vwsFAJWtEkErqiWSmlKC0r59Cx42Rm53GqpITKymp0Og0/P1OdgaX0JpwBYSi/UFzGAJQxAGUK\ncP+7SfNCuJxoDgua3eL+rbNVobOWobNUoFnNaCicTicWqw2DXk9YaAjREeEkdu9GckI32SAmmpWE\nrmhRSikqzJUcOZZJVl4+5RVmyivMWKxWnC4X/n4m97STF1yHzoDSG+H0b6XT12ys0/Q1hyu7nKBc\naMp11r+daA4bmtN2Xj1Wqw2H04lBrycwMIDQ4GA6REXQMzGBzp1i3BMCCdESJHSFxymlqKqupvBU\nMcdz8iguKaXaYsFisVFtsWCz23E6XThdTnQ6Db1Oj06vQ6/ToWma+0cphcvlqvmtFMpV89vhcKDT\n6dy39TOZ8PMzERgQQGhIEJ07xhDXqSPhYaESsMLjJHSFz7E7HFRWVVNZWYW5sooqi4Xq6mqsNjs2\nhwOn3YFTKQwGPUaD4ZcfowGT0UhYSDDBwUEEBgTg72dyz6YmhC+Q0BVCCA+SIYAQQniQhK4QQniQ\nhK4QQniQhK4QQniQhK4QQniQhK4QQniQhK4QQniQhK4QQniQhK4QQniQhK4QQniQhK4QQniQhK4Q\nQniQhK4QQniQhK4QQnjQ/wdiXWoVZsKpaQAAAABJRU5ErkJggg==\n",
      "text/plain": [
       "<matplotlib.figure.Figure at 0x20cf4087470>"
      ]
     },
     "metadata": {},
     "output_type": "display_data"
    }
   ],
   "source": [
    "plt.title(\"% of Total Rides by City Type\")\n",
    "plt.pie(rides, explode=explode, labels=types, colors=colors,\n",
    "        autopct=\"%1.1f%%\", shadow=True, startangle=90)\n",
    "plt.axis(\"equal\")\n",
    "\n",
    "plt.savefig('% of Total Rides by City Type')\n",
    "plt.show()"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 95,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "type\n",
       "Rural        3.105405\n",
       "Suburban    19.050463\n",
       "Urban       77.844133\n",
       "Name: driver_count, dtype: float64"
      ]
     },
     "execution_count": 95,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "#% of Total Drivers by City Type\n",
    "Total_Drivers = city_data_df['driver_count'].sum()\n",
    "\n",
    "Total_DriversType = city_data_df.groupby(['type']).driver_count.sum()\n",
    "\n",
    "Drives = (Total_DriversType/Total_Drivers)*100\n",
    "Drives"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 96,
   "metadata": {
    "collapsed": true
   },
   "outputs": [],
   "source": [
    " # Dataset Total Drivers by City type\n",
    "types = [\"Rural\", \"Suburban\", \"Urban\",]\n",
    "drivers = [3.1, 19.0, 77.8]\n",
    "colors = [\"yellowgreen\", \"red\", \"lightskyblue\"]\n",
    "explode = (0, 0, 0.05)"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 97,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "image/png": "iVBORw0KGgoAAAANSUhEUgAAAV0AAAD4CAYAAABPLjVeAAAABHNCSVQICAgIfAhkiAAAAAlwSFlz\nAAALEgAACxIB0t1+/AAAADl0RVh0U29mdHdhcmUAbWF0cGxvdGxpYiB2ZXJzaW9uIDIuMS4wLCBo\ndHRwOi8vbWF0cGxvdGxpYi5vcmcvpW3flQAAIABJREFUeJzt3Xd8VFX+//HXnT4ppBdI6B0lVAUp\nFmxIk10EbKhY1rL73a+yfhUV3bWsFfXrT8W6lrWh8MWCithgaYIC0lsSQgohCclMyiTT5/7+mDgS\nAUkmk8wk+Twfjzwgkzt3PjMZ3pw559xzFFVVVYQQQrQKTbgLEEKIjkRCVwghWpGErhBCtCIJXSGE\naEUSukII0YokdIUQohVJ6DbRd999xznnnMPYsWP5+OOPG/zsscce48UXX2z2Y3z11VeMHz+eIUOG\nsHr16gY/mz9/Pv379z/p1/PPP9/oxygtLW3UsUuWLGHs2LEn/fnZZ5/doIYhQ4Ywffp0li1bdspz\nn3322XzwwQeNqqMlPfvss8yaNSuk5ywvL+fhhx9mwoQJZGVlcfHFF/PSSy/hcrkCx1xxxRUsXLgQ\nAJfLxfvvvx/UY/32d/Dbr82bN4fkOYkQUEWjeb1eddSoUeqyZcvUtWvXqllZWarFYlFVVVVLS0vV\ns88+W62pqWn241x44YXqPffcoxYVFal2u73Bz6qrq9WysjK1rKxM3bRpk9qvXz91+/btgdtsNtsp\nz5+fn6/269dPzcnJaVQ9H330kTpmzJiT/nz8+PHqq6++qpaVlamlpaVqbm6u+uabb6qDBw9W33zz\nzd89d0VFxXHPMRyeeeYZdebMmSE7X0FBgTpu3Dj15ptvVn/88Ue1oKBAXbFihTpu3Dj1tttuCxxn\ntVoDv7NTvc6/p6KiIvAeeOGFF9Tzzjsv8H1ZWZnqcrlC8rxE8+nCHfpticViwWq1MnnyZAwGA7Gx\nsRQWFpKQkMDLL7/MnDlziImJafbjVFdXM2LECDIyMo77WWxsLLGxsQBYrVYAEhMTSUlJafT51Ra4\nHiYmJiZQQ2pqKr169UKj0fDMM88wbdo0EhMTT3i/k93e1v3973+nX79+LFq0CI3G/4Gya9eupKSk\ncOWVV7Ju3TrGjRtHfHx8SB7v2NcxOjoarVbbpPeEaD3SvdAECQkJREVFsWPHDvLz86mqqiI9PZ3i\n4mJWr17NVVdd1ajzHDp0iFtvvZUzzjiDUaNGsWDBAmw2GwD9+/fHarVy7733MmHChKBr3b59O3Pm\nzGHYsGGMGzeOp59+Go/Hg8fj4aKLLgJg0qRJLFq0CIBPPvmEqVOncvrppzN8+HBuu+02ysvLg358\ngBkzZuDz+VizZg3g/yj90EMPMXHiRM466yzy8vIC3Qtr167l9NNPp7q6OnD/8vJyBg0axI4dOwBY\ntWoV06ZNIysriylTpvDJJ58Ejn322We5+eabmTt3LiNHjuTTTz9l//79XH311QwdOpTRo0dz//33\nY7fbT1qv1+vloYceCrxm7733HgBOp5MRI0Yc15101VVXnbA7qbi4mA0bNnDDDTcEAvcXI0aM4O23\n32bYsGGB12ThwoVs2LCBBQsWUF5eHugOGDhwID/++GPgvqqqMmHChAbPu7FKSkp+93wbNmxg1KhR\nLFmyhHHjxjFy5EgeeOABnE5n4Pjc3FxuuOEGhgwZwoQJE1i4cGGDrhLROBK6TaDVarnrrru47rrr\nmDRpErfddhupqaksWrSIuXPnYjabT3mOyspKrrzySvR6Pe+99x7PP/88W7Zs4d577wVg3bp1xMfH\nc++997J06dKg6szNzeWaa66hf//+LF26lAcffJBly5bx3HPPodPp+PDDDwF47733uO6669i8eTML\nFizgpptuYuXKlbzwwgvs2rWLV199NajH/0V0dDRdunQhOzs7cNtHH33E/fffzyuvvELPnj0Dt48Z\nM4ZOnTrx7bffBm776quvyMzMJCsri3379nH77bdz1VVX8fnnn3PLLbfwyCOP8NVXXwWOX716NWed\ndRaLFy9m/PjxzJs3j759+7J8+XJeeukl1q1bx7/+9a+T1rtr1y4qKytZsmQJd955J0888QRffvkl\nRqORiy66iM8//zxw7JEjR9i6dStTp0497jz79u1DVVUGDx58wscZPXo00dHRDW4bOXIk8+fPJzEx\nkXXr1jFkyBDOOOOMBo+5ZcsWKioquPDCC0/6HE4mPT39lOez2Wz8+9//5oUXXuDFF19k3bp1PPzw\nwwA4HA5uvPFGevbsyccff8zjjz/O6tWrefzxx5tcS0cnodtEV1xxBZs2bWLTpk3ceuutFBYWsnHj\nRmbPns2iRYuYMGEC11xzDcXFxSe8/+eff47P5+PJJ5+kX79+nHnmmTz++OOsXLmSvLy8wEfC2NjY\noD96L168mB49erBgwQJ69+7N+eefz913382bb76J0+kkISEB+LXlbjKZeOSRR5g2bRoZGRmMGTOG\n8847j9zc3OBepGN06tQp0IoHGDt2LGPHjiUrK6vBcVqtlkmTJrFixYrAbV9++SVTpkwB4LXXXmP6\n9OnMnj2bbt26MWXKFK677jreeOONwPFRUVHcdNNN9OnTh8TERA4fPkxiYiIZGRkMGzaMl156iUmT\nJp201vj4eB599FH69OnD9OnTmTlzZmBga9q0aWzcuBGLxQL4f49ZWVl069btuPP80lpvSleTwWAg\nJiYGjUZDSkoKer2eadOm8fXXX+PxeAKPef755x8X2I11qvN5PB4eeughhg4dyqhRo7jrrrv45JNP\nqK2t5bPPPsNsNrNgwQJ69erFmWeeyd///ncWL15MXV1dUPV0VBK6QYiOjg78g3rhhRf405/+xP79\n+/nwww/5+OOPGT9+fKCF8FvZ2dkMHDgQk8kUuG3w4MHo9fqQhBxATk4OQ4cObXDbiBEjcLvd5Ofn\nH3f86aefzuDBg3nhhRe44447mDZtGkuWLMHr9Ta7FpvNFuiDBn+/5slMmTKFH374gaqqKkpKSti6\ndWsgdHNycvi///s/hg0bFvh65ZVXyMvLa3BuRVEC3995550sWrSIs846izvvvJOioiJ69ep10scf\nMGDAcb+XX1rpo0aNIjk5mZUrVwL+wDpRKxcI/Kd2bFdJMCZOnIjdbmfDhg14PB6++uqrkz5mKM6n\n1+sZMmRI4PusrKzAeyY7O5tDhw41eP1vuukmvF4vBQUFzXqeHY0MpDVDbm4u27Zt45///Cfvvvsu\nw4YNIy4ujgkTJvDaa6+d8D7H/qP+LZ/PF5K6jEbjcbf9Mnh2osdYu3Ytt956K1OnTuXMM89k7ty5\nLFu2jEOHDjWrjtraWvLz8xkwYEDgtt97/kOHDqVz585888031NTUMGjQoEBIer1err322uOmdR0b\nsr8999VXX83555/PN998w9q1a7n99tuZMWMGDz744AkfX6vVNvje5/Oh1+sB0Gg0TJkyhS+//JIz\nzzyTnJwcLrnkkhOeZ/DgwWg0Gnbu3Mm4ceOO+/m8efM499xzmTZt2klfC/C3lM877zxWrFiBqqqo\nqnrC8zXWqc6n0Wga9EH/8l7RaDR4vV5GjBjBI488ctx509PTg66pI5KWbjO88MIL3Hrrreh0/v+7\n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\nAElFTkSuQmCC\n",
      "text/plain": [
       "<matplotlib.figure.Figure at 0x20cf4372358>"
      ]
     },
     "metadata": {},
     "output_type": "display_data"
    }
   ],
   "source": [
    "plt.title(\"% of Total Drivers by City Type\")\n",
    "plt.pie(drivers, explode=explode, labels=types, colors=colors,\n",
    "        autopct=\"%1.1f%%\", shadow=True, startangle=90)\n",
    "plt.axis(\"equal\")\n",
    "\n",
    "plt.savefig('% of Total Drivers by City Type')\n",
    "plt.show()"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "metadata": {
    "collapsed": true
   },
   "outputs": [],
   "source": []
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "metadata": {
    "collapsed": true
   },
   "outputs": [],
   "source": []
  },
  {
   "cell_type": "code",
   "execution_count": null,
   "metadata": {
    "collapsed": true
   },
   "outputs": [],
   "source": []
  }
 ],
 "metadata": {
  "kernelspec": {
   "display_name": "Python 3",
   "language": "python",
   "name": "python3"
  },
  "language_info": {
   "codemirror_mode": {
    "name": "ipython",
    "version": 3
   },
   "file_extension": ".py",
   "mimetype": "text/x-python",
   "name": "python",
   "nbconvert_exporter": "python",
   "pygments_lexer": "ipython3",
   "version": "3.6.3"
  }
 },
 "nbformat": 4,
 "nbformat_minor": 2
}



```


![png](output_23_0.png)

