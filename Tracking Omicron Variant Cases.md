                                                                                                 18-01-2022

## Tracking the current progression of the new omicron COVID-19 variant
    
The dataset used is sourced from the **Daily Updated Omicron (COVID-19 Variant) cases** as recorded in the **Kaggle** platform, and saved as **covid-variants.csv**.

**The data**

**location**- this is the country for which the variants information is provided;
**date** - date for the data entry;
**variant** - this is the variant corresponding to this data entry;
**num_sequences** - the number of sequences processed (for the country, variant and date);
**perc_sequences** - percentage of sequences from the total number of sequences (for the country, variant and date);
**numsequencestotal** - total number of sequences (for the country, variant and date);

### Reading and Exploring the Data


```python
# Importing libraries
# Reading in the csv datafile into a pandas dataframe

import pandas as pd
import numpy as np
from matplotlib import pyplot as plt
covid_variants = pd.read_csv('covid-variants.csv')
covid_variants
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
      <th>location</th>
      <th>date</th>
      <th>variant</th>
      <th>num_sequences</th>
      <th>perc_sequences</th>
      <th>num_sequences_total</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Angola</td>
      <td>2020-07-06</td>
      <td>Alpha</td>
      <td>0</td>
      <td>0.0</td>
      <td>3</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Angola</td>
      <td>2020-07-06</td>
      <td>B.1.1.277</td>
      <td>0</td>
      <td>0.0</td>
      <td>3</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Angola</td>
      <td>2020-07-06</td>
      <td>B.1.1.302</td>
      <td>0</td>
      <td>0.0</td>
      <td>3</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Angola</td>
      <td>2020-07-06</td>
      <td>B.1.1.519</td>
      <td>0</td>
      <td>0.0</td>
      <td>3</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Angola</td>
      <td>2020-07-06</td>
      <td>B.1.160</td>
      <td>0</td>
      <td>0.0</td>
      <td>3</td>
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
      <th>100411</th>
      <td>Zimbabwe</td>
      <td>2021-11-01</td>
      <td>Omicron</td>
      <td>0</td>
      <td>0.0</td>
      <td>6</td>
    </tr>
    <tr>
      <th>100412</th>
      <td>Zimbabwe</td>
      <td>2021-11-01</td>
      <td>S:677H.Robin1</td>
      <td>0</td>
      <td>0.0</td>
      <td>6</td>
    </tr>
    <tr>
      <th>100413</th>
      <td>Zimbabwe</td>
      <td>2021-11-01</td>
      <td>S:677P.Pelican</td>
      <td>0</td>
      <td>0.0</td>
      <td>6</td>
    </tr>
    <tr>
      <th>100414</th>
      <td>Zimbabwe</td>
      <td>2021-11-01</td>
      <td>others</td>
      <td>0</td>
      <td>0.0</td>
      <td>6</td>
    </tr>
    <tr>
      <th>100415</th>
      <td>Zimbabwe</td>
      <td>2021-11-01</td>
      <td>non_who</td>
      <td>0</td>
      <td>0.0</td>
      <td>6</td>
    </tr>
  </tbody>
</table>
<p>100416 rows × 6 columns</p>
</div>



### Selecting only the locations with Omicron cases


```python
omicron_variant = covid_variants.loc[covid_variants['variant'] == 'Omicron']
omicron_variant
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
      <th>location</th>
      <th>date</th>
      <th>variant</th>
      <th>num_sequences</th>
      <th>perc_sequences</th>
      <th>num_sequences_total</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>19</th>
      <td>Angola</td>
      <td>2020-07-06</td>
      <td>Omicron</td>
      <td>0</td>
      <td>0.0</td>
      <td>3</td>
    </tr>
    <tr>
      <th>43</th>
      <td>Angola</td>
      <td>2020-08-31</td>
      <td>Omicron</td>
      <td>0</td>
      <td>0.0</td>
      <td>1</td>
    </tr>
    <tr>
      <th>67</th>
      <td>Angola</td>
      <td>2020-09-28</td>
      <td>Omicron</td>
      <td>0</td>
      <td>0.0</td>
      <td>10</td>
    </tr>
    <tr>
      <th>91</th>
      <td>Angola</td>
      <td>2020-10-12</td>
      <td>Omicron</td>
      <td>0</td>
      <td>0.0</td>
      <td>29</td>
    </tr>
    <tr>
      <th>115</th>
      <td>Angola</td>
      <td>2020-10-26</td>
      <td>Omicron</td>
      <td>0</td>
      <td>0.0</td>
      <td>7</td>
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
      <th>100315</th>
      <td>Zimbabwe</td>
      <td>2021-09-06</td>
      <td>Omicron</td>
      <td>0</td>
      <td>0.0</td>
      <td>14</td>
    </tr>
    <tr>
      <th>100339</th>
      <td>Zimbabwe</td>
      <td>2021-09-20</td>
      <td>Omicron</td>
      <td>0</td>
      <td>0.0</td>
      <td>6</td>
    </tr>
    <tr>
      <th>100363</th>
      <td>Zimbabwe</td>
      <td>2021-10-04</td>
      <td>Omicron</td>
      <td>0</td>
      <td>0.0</td>
      <td>2</td>
    </tr>
    <tr>
      <th>100387</th>
      <td>Zimbabwe</td>
      <td>2021-10-18</td>
      <td>Omicron</td>
      <td>0</td>
      <td>0.0</td>
      <td>5</td>
    </tr>
    <tr>
      <th>100411</th>
      <td>Zimbabwe</td>
      <td>2021-11-01</td>
      <td>Omicron</td>
      <td>0</td>
      <td>0.0</td>
      <td>6</td>
    </tr>
  </tbody>
</table>
<p>4184 rows × 6 columns</p>
</div>



Grouping up the **omicron_variant** DataFrame by location, and summing up the total cases per location.


```python
omicron_per_country = omicron_variant.groupby('location').sum()
omicron_per_country
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
      <th>num_sequences</th>
      <th>perc_sequences</th>
      <th>num_sequences_total</th>
    </tr>
    <tr>
      <th>location</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Angola</th>
      <td>0</td>
      <td>0.00</td>
      <td>1055</td>
    </tr>
    <tr>
      <th>Argentina</th>
      <td>93</td>
      <td>100.05</td>
      <td>8411</td>
    </tr>
    <tr>
      <th>Aruba</th>
      <td>0</td>
      <td>0.00</td>
      <td>3000</td>
    </tr>
    <tr>
      <th>Australia</th>
      <td>1693</td>
      <td>89.89</td>
      <td>47199</td>
    </tr>
    <tr>
      <th>Austria</th>
      <td>34</td>
      <td>18.99</td>
      <td>12580</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>United States</th>
      <td>28536</td>
      <td>133.87</td>
      <td>2081677</td>
    </tr>
    <tr>
      <th>Uruguay</th>
      <td>0</td>
      <td>0.00</td>
      <td>682</td>
    </tr>
    <tr>
      <th>Vietnam</th>
      <td>1</td>
      <td>2.00</td>
      <td>1805</td>
    </tr>
    <tr>
      <th>Zambia</th>
      <td>46</td>
      <td>200.00</td>
      <td>1117</td>
    </tr>
    <tr>
      <th>Zimbabwe</th>
      <td>0</td>
      <td>0.00</td>
      <td>686</td>
    </tr>
  </tbody>
</table>
<p>121 rows × 3 columns</p>
</div>



### Top 10 Countries with Omicron Cases


```python
# Sorting by column "num_sequences_total"
top_10_countries = omicron_per_country.sort_values(by=['num_sequences_total'], ascending=False).head(10)
top_10_countries
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
      <th>num_sequences</th>
      <th>perc_sequences</th>
      <th>num_sequences_total</th>
    </tr>
    <tr>
      <th>location</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>United States</th>
      <td>28536</td>
      <td>133.87</td>
      <td>2081677</td>
    </tr>
    <tr>
      <th>United Kingdom</th>
      <td>65137</td>
      <td>171.03</td>
      <td>1559482</td>
    </tr>
    <tr>
      <th>Germany</th>
      <td>2270</td>
      <td>16.01</td>
      <td>327143</td>
    </tr>
    <tr>
      <th>Denmark</th>
      <td>4823</td>
      <td>53.80</td>
      <td>280370</td>
    </tr>
    <tr>
      <th>Canada</th>
      <td>612</td>
      <td>50.94</td>
      <td>181885</td>
    </tr>
    <tr>
      <th>Japan</th>
      <td>150</td>
      <td>90.89</td>
      <td>177839</td>
    </tr>
    <tr>
      <th>France</th>
      <td>843</td>
      <td>105.61</td>
      <td>150116</td>
    </tr>
    <tr>
      <th>Sweden</th>
      <td>634</td>
      <td>40.61</td>
      <td>137854</td>
    </tr>
    <tr>
      <th>Switzerland</th>
      <td>782</td>
      <td>44.09</td>
      <td>99667</td>
    </tr>
    <tr>
      <th>India</th>
      <td>215</td>
      <td>38.54</td>
      <td>91028</td>
    </tr>
  </tbody>
</table>
</div>




```python
top_10_countries = top_10_countries.reset_index()
top_10_countries
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
      <th>location</th>
      <th>num_sequences</th>
      <th>perc_sequences</th>
      <th>num_sequences_total</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>United States</td>
      <td>28536</td>
      <td>133.87</td>
      <td>2081677</td>
    </tr>
    <tr>
      <th>1</th>
      <td>United Kingdom</td>
      <td>65137</td>
      <td>171.03</td>
      <td>1559482</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Germany</td>
      <td>2270</td>
      <td>16.01</td>
      <td>327143</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Denmark</td>
      <td>4823</td>
      <td>53.80</td>
      <td>280370</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Canada</td>
      <td>612</td>
      <td>50.94</td>
      <td>181885</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Japan</td>
      <td>150</td>
      <td>90.89</td>
      <td>177839</td>
    </tr>
    <tr>
      <th>6</th>
      <td>France</td>
      <td>843</td>
      <td>105.61</td>
      <td>150116</td>
    </tr>
    <tr>
      <th>7</th>
      <td>Sweden</td>
      <td>634</td>
      <td>40.61</td>
      <td>137854</td>
    </tr>
    <tr>
      <th>8</th>
      <td>Switzerland</td>
      <td>782</td>
      <td>44.09</td>
      <td>99667</td>
    </tr>
    <tr>
      <th>9</th>
      <td>India</td>
      <td>215</td>
      <td>38.54</td>
      <td>91028</td>
    </tr>
  </tbody>
</table>
</div>



### Bottom 10 Countries with Omicron cases


```python
bottom_10_countries = omicron_per_country.sort_values(by=['num_sequences_total'], ascending=False).tail(10)
bottom_10_countries
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
      <th>num_sequences</th>
      <th>perc_sequences</th>
      <th>num_sequences_total</th>
    </tr>
    <tr>
      <th>location</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Jamaica</th>
      <td>0</td>
      <td>0.00</td>
      <td>366</td>
    </tr>
    <tr>
      <th>Togo</th>
      <td>0</td>
      <td>0.00</td>
      <td>338</td>
    </tr>
    <tr>
      <th>Brunei</th>
      <td>8</td>
      <td>72.73</td>
      <td>331</td>
    </tr>
    <tr>
      <th>Kuwait</th>
      <td>1</td>
      <td>33.33</td>
      <td>328</td>
    </tr>
    <tr>
      <th>Hungary</th>
      <td>0</td>
      <td>0.00</td>
      <td>326</td>
    </tr>
    <tr>
      <th>Belize</th>
      <td>0</td>
      <td>0.00</td>
      <td>314</td>
    </tr>
    <tr>
      <th>Iraq</th>
      <td>0</td>
      <td>0.00</td>
      <td>167</td>
    </tr>
    <tr>
      <th>Moldova</th>
      <td>0</td>
      <td>0.00</td>
      <td>152</td>
    </tr>
    <tr>
      <th>Mongolia</th>
      <td>0</td>
      <td>0.00</td>
      <td>150</td>
    </tr>
    <tr>
      <th>Monaco</th>
      <td>0</td>
      <td>0.00</td>
      <td>84</td>
    </tr>
  </tbody>
</table>
</div>



### Data Visualization

Visualizing the top 10 leading countries on Omicron cases using horizontal bar plot.


```python
Country = top_10_countries['location']
Number_of_cases = top_10_countries['num_sequences_total']
 
# Figure Size
fig, ax = plt.subplots(figsize =(12, 5))
 
# Horizontal Bar Plot
ax.barh(Country, Number_of_cases)
 
# Remove axes splines
for s in ['top', 'bottom', 'left', 'right']:
    ax.spines[s].set_visible(False)
 
# Remove x, y Ticks
ax.xaxis.set_ticks_position('none')
ax.yaxis.set_ticks_position('none')
 
# Add padding between axes and labels
ax.xaxis.set_tick_params(pad = 5)
ax.yaxis.set_tick_params(pad = 10)
 
# Add x, y gridlines
ax.grid(b = True, color ='black',
        linestyle ='-.', linewidth = 0.5,
        alpha = 0.2)
 
# Show top values
ax.invert_yaxis()
 
# Add annotation to bars
for i in ax.patches:
    plt.text(i.get_width()+0.2, i.get_y()+0.5,
             str(round((i.get_width()), 2)),
             fontsize = 12, fontweight ='bold',
             color ='green')
 
# Add Plot Title
ax.set_title('Top 10 Countries Leading in Omicron Variant Cases - Jan 2022',
             loc ='left',fontweight='bold',size = 16 )
 
# Add Text watermark
fig.text(0.9, 0.15, 'Jeeteshgavande30', fontsize = 12,
         color ='black', ha ='right', va ='bottom',
         alpha = 0.7)
 
# Show Plot
plt.show()
```


    
![png](output_14_0.png)
    


### Summary

The highly transmissible Omicron variant of COVID-19 is driving an unprecedented surge of infections globally.
The Omicron variant of COVID-19 has been called a variant of concern by WHO based on the evidence that it has several mutations that may have an impact on how it behaves. There is consistent evidence that Omicron is spreading significantly faster than the Delta variant in countries with documented community transmission, with a doubling time of 2-3 days. The overall risk related to this new variant remains very high.

Omicron has now been detected in over 121 countries across the world, after the variant was first detected in November 2021. 

An analysis of the Daily Updated Omicron (COVID-19 Variant) cases, as recorded on the **Kaggle** platform, shows that United States is the worst hit, already recording over 2 miilion cases of Omicron variant, which is closely followed by United Kingdom, recording slightly over 1.5 million cases.

The rest of the 8 remaining countries in the top 10, including Germany,Denmark, Canada, Japan, France, Sweden, Switzerland, and India in that order  have recorded less than 500k cases each.

Data Source: https://www.kaggle.com/yamqwe/omicron-covid19-variant-daily-cases



```python

```
