

```python
# Import Numpy for calculations, matplotlib for charting, & Pandas because everyone loves Pandas
import os
import numpy as np
import matplotlib.pyplot as plt
import pandas as pd
```


```python
# Load in clinical trial data csv
clinical_trial_df = pd.read_csv("/Users/rohanmohindroo/Documents/NUCHI201804DATA2-Class-Repository-DATA/05-Matplotlib/Homework/Instructions/Pymaceuticals/raw_data/clinicaltrial_data.csv")
clinical_trial_df.head()
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
      <th>Mouse ID</th>
      <th>Timepoint</th>
      <th>Tumor Volume (mm3)</th>
      <th>Metastatic Sites</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>b128</td>
      <td>0</td>
      <td>45.0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>f932</td>
      <td>0</td>
      <td>45.0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>g107</td>
      <td>0</td>
      <td>45.0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>a457</td>
      <td>0</td>
      <td>45.0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>c819</td>
      <td>0</td>
      <td>45.0</td>
      <td>0</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Load in mouse drug data csv
mouse_drug_df = pd.read_csv("/Users/rohanmohindroo/Documents/NUCHI201804DATA2-Class-Repository-DATA/05-Matplotlib/Homework/Instructions/Pymaceuticals/raw_data/mouse_drug_data.csv")
mouse_drug_df.head()
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
      <th>Mouse ID</th>
      <th>Drug</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>f234</td>
      <td>Stelasyn</td>
    </tr>
    <tr>
      <th>1</th>
      <td>x402</td>
      <td>Stelasyn</td>
    </tr>
    <tr>
      <th>2</th>
      <td>a492</td>
      <td>Stelasyn</td>
    </tr>
    <tr>
      <th>3</th>
      <td>w540</td>
      <td>Stelasyn</td>
    </tr>
    <tr>
      <th>4</th>
      <td>v764</td>
      <td>Stelasyn</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Merge the two dataframes using an outer join
merge_drug_data = pd.merge(clinical_trial_df, mouse_drug_df, on="Mouse ID", how="outer")
merge_drug_data.head()
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
      <th>Mouse ID</th>
      <th>Timepoint</th>
      <th>Tumor Volume (mm3)</th>
      <th>Metastatic Sites</th>
      <th>Drug</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>b128</td>
      <td>0</td>
      <td>45.000000</td>
      <td>0</td>
      <td>Capomulin</td>
    </tr>
    <tr>
      <th>1</th>
      <td>b128</td>
      <td>5</td>
      <td>45.651331</td>
      <td>0</td>
      <td>Capomulin</td>
    </tr>
    <tr>
      <th>2</th>
      <td>b128</td>
      <td>10</td>
      <td>43.270852</td>
      <td>0</td>
      <td>Capomulin</td>
    </tr>
    <tr>
      <th>3</th>
      <td>b128</td>
      <td>15</td>
      <td>43.784893</td>
      <td>0</td>
      <td>Capomulin</td>
    </tr>
    <tr>
      <th>4</th>
      <td>b128</td>
      <td>20</td>
      <td>42.731552</td>
      <td>0</td>
      <td>Capomulin</td>
    </tr>
  </tbody>
</table>
</div>




```python
reduced_clinical_df = merge_drug_data.loc[:, ["Drug", "Timepoint", "Tumor Volume (mm3)"]]
reduced_clinical_df.head()

drug_totals = reduced_clinical_df.set_index('Drug', 'Timepoint')
drug_totals.head()
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
      <th>Timepoint</th>
      <th>Tumor Volume (mm3)</th>
    </tr>
    <tr>
      <th>Drug</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Capomulin</th>
      <td>0</td>
      <td>45.000000</td>
    </tr>
    <tr>
      <th>Capomulin</th>
      <td>5</td>
      <td>45.651331</td>
    </tr>
    <tr>
      <th>Capomulin</th>
      <td>10</td>
      <td>43.270852</td>
    </tr>
    <tr>
      <th>Capomulin</th>
      <td>15</td>
      <td>43.784893</td>
    </tr>
    <tr>
      <th>Capomulin</th>
      <td>20</td>
      <td>42.731552</td>
    </tr>
  </tbody>
</table>
</div>




```python
drug_totals_pivot = pd.pivot_table(drug_totals, values='Tumor Volume (mm3)', index=['Timepoint'], columns=['Drug'])
drug_totals_pivot
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
      <th>Drug</th>
      <th>Capomulin</th>
      <th>Ceftamin</th>
      <th>Infubinol</th>
      <th>Ketapril</th>
      <th>Naftisol</th>
      <th>Placebo</th>
      <th>Propriva</th>
      <th>Ramicane</th>
      <th>Stelasyn</th>
      <th>Zoniferol</th>
    </tr>
    <tr>
      <th>Timepoint</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>45.000000</td>
      <td>45.000000</td>
      <td>45.000000</td>
      <td>45.000000</td>
      <td>45.000000</td>
      <td>45.000000</td>
      <td>45.000000</td>
      <td>45.000000</td>
      <td>45.000000</td>
      <td>45.000000</td>
    </tr>
    <tr>
      <th>5</th>
      <td>44.266086</td>
      <td>46.503051</td>
      <td>47.062001</td>
      <td>47.389175</td>
      <td>46.796098</td>
      <td>47.125589</td>
      <td>47.248967</td>
      <td>43.944859</td>
      <td>47.527452</td>
      <td>46.851818</td>
    </tr>
    <tr>
      <th>10</th>
      <td>43.084291</td>
      <td>48.285125</td>
      <td>49.403909</td>
      <td>49.582269</td>
      <td>48.694210</td>
      <td>49.423329</td>
      <td>49.101541</td>
      <td>42.531957</td>
      <td>49.463844</td>
      <td>48.689881</td>
    </tr>
    <tr>
      <th>15</th>
      <td>42.064317</td>
      <td>50.094055</td>
      <td>51.296397</td>
      <td>52.399974</td>
      <td>50.933018</td>
      <td>51.359742</td>
      <td>51.067318</td>
      <td>41.495061</td>
      <td>51.529409</td>
      <td>50.779059</td>
    </tr>
    <tr>
      <th>20</th>
      <td>40.716325</td>
      <td>52.157049</td>
      <td>53.197691</td>
      <td>54.920935</td>
      <td>53.644087</td>
      <td>54.364417</td>
      <td>53.346737</td>
      <td>40.238325</td>
      <td>54.067395</td>
      <td>53.170334</td>
    </tr>
    <tr>
      <th>25</th>
      <td>39.939528</td>
      <td>54.287674</td>
      <td>55.715252</td>
      <td>57.678982</td>
      <td>56.731968</td>
      <td>57.482574</td>
      <td>55.504138</td>
      <td>38.974300</td>
      <td>56.166123</td>
      <td>55.432935</td>
    </tr>
    <tr>
      <th>30</th>
      <td>38.769339</td>
      <td>56.769517</td>
      <td>58.299397</td>
      <td>60.994507</td>
      <td>59.559509</td>
      <td>59.809063</td>
      <td>58.196374</td>
      <td>38.703137</td>
      <td>59.826738</td>
      <td>57.713531</td>
    </tr>
    <tr>
      <th>35</th>
      <td>37.816839</td>
      <td>58.827548</td>
      <td>60.742461</td>
      <td>63.371686</td>
      <td>62.685087</td>
      <td>62.420615</td>
      <td>60.350199</td>
      <td>37.451996</td>
      <td>62.440699</td>
      <td>60.089372</td>
    </tr>
    <tr>
      <th>40</th>
      <td>36.958001</td>
      <td>61.467895</td>
      <td>63.162824</td>
      <td>66.068580</td>
      <td>65.600754</td>
      <td>65.052675</td>
      <td>63.045537</td>
      <td>36.574081</td>
      <td>65.356386</td>
      <td>62.916692</td>
    </tr>
    <tr>
      <th>45</th>
      <td>36.236114</td>
      <td>64.132421</td>
      <td>65.755562</td>
      <td>70.662958</td>
      <td>69.265506</td>
      <td>68.084082</td>
      <td>66.258529</td>
      <td>34.955595</td>
      <td>68.438310</td>
      <td>65.960888</td>
    </tr>
  </tbody>
</table>
</div>




```python
Capomulin = [45.00, 44.27, 43.08, 42.06, 40.72, 39.94, 38.77, 37.85, 36.96, 36.24]
Ceftamin = [45.00, 46.50, 48.29, 50.09, 52.16, 54.29, 56.77, 58.83, 61.47, 64.13]
Infubinol = [45.00, 47.06, 49.40, 51.30, 53.20, 55.72, 58.30, 60.74, 63.16, 65.76]
Ketapril = [45.00, 47.40, 49.58, 52.40, 54.92, 57.68, 60.99, 63.37, 66.07, 70.66]
Naftisol = [45.00, 46.80, 48.69, 50.93, 53.64, 56.73, 59.56, 62.69, 65.60, 69.27]
Placebo = [45.00, 47.13, 49.42, 51.34, 54.36, 57.48, 59.81, 62.42, 65.05, 68.08]
Popriva = [45.00, 47.25, 49.10, 51.07, 53.35, 55.50, 58.20, 60.35, 63.05, 66.26]
Ramicane = [45.00, 43.94, 42.53, 41.50, 40.24, 38.97, 38.70, 37.45, 36.57, 34.96]
Stelasyn = [45.00, 47.53, 49.46, 51.53, 54.07, 56.17, 59.83, 62.44, 65.36, 68.44]
Zoniferol = [45.00, 46.85, 48.69, 50.78, 53.17, 55.43, 57.71, 60.09, 62.92, 65.96]
Timepoint = [0, 5, 10, 15, 20, 25, 30, 35, 40, 45]

plt.scatter(Timepoint, Capomulin, marker="o", facecolors="red", edgecolors="black", label="Capomulin")
plt.scatter(Timepoint, Ceftamin, marker="o", facecolors="blue", edgecolors="black", label="Ceftamin")
plt.scatter(Timepoint, Infubinol, marker="o", facecolors="green", edgecolors="black", label="Infubinol")
plt.scatter(Timepoint, Ketapril, marker="o", facecolors="orange", edgecolors="black", label="Ketapril")
plt.scatter(Timepoint, Naftisol, marker="o", facecolors="pink", edgecolors="black", label="Naftisol")
plt.scatter(Timepoint, Placebo, marker="o", facecolors="purple", edgecolors="black", label="Placebo")
plt.scatter(Timepoint, Popriva, marker="o", facecolors="black", edgecolors="black", label="Popriva")
plt.scatter(Timepoint, Ramicane, marker="o", facecolors="yellow", edgecolors="black", label="Ramicane")
plt.scatter(Timepoint, Stelasyn, marker="o", facecolors="DarkBlue", edgecolors="black", label="Stelasyn")
plt.scatter(Timepoint, Zoniferol, marker="o", facecolors="DarkGreen", edgecolors="black", label="Zoniferol")

# Give the chart a title, x label, and y label
plt.title("Tumor Response to Treatment")
plt.xlabel("Time (Days)")
plt.ylabel("Tumor Volume (mm3)")
```




    Text(0,0.5,'Tumor Volume (mm3)')




![png](output_6_1.png)



```python
met_merge = merge_drug_data.dropna(how='any')
met_merge

reduced_met = merge_drug_data.loc[:, ["Drug", "Timepoint", "Metastatic Sites"]]
reduced_met.head()

met_totals = reduced_met.set_index('Drug', 'Timepoint')
met_totals.head()
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
      <th>Timepoint</th>
      <th>Metastatic Sites</th>
    </tr>
    <tr>
      <th>Drug</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Capomulin</th>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>Capomulin</th>
      <td>5</td>
      <td>0</td>
    </tr>
    <tr>
      <th>Capomulin</th>
      <td>10</td>
      <td>0</td>
    </tr>
    <tr>
      <th>Capomulin</th>
      <td>15</td>
      <td>0</td>
    </tr>
    <tr>
      <th>Capomulin</th>
      <td>20</td>
      <td>0</td>
    </tr>
  </tbody>
</table>
</div>




```python
met_pivot = pd.pivot_table(met_totals, values='Metastatic Sites', index=['Timepoint'], columns=['Drug'])
met_pivot
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
      <th>Drug</th>
      <th>Capomulin</th>
      <th>Ceftamin</th>
      <th>Infubinol</th>
      <th>Ketapril</th>
      <th>Naftisol</th>
      <th>Placebo</th>
      <th>Propriva</th>
      <th>Ramicane</th>
      <th>Stelasyn</th>
      <th>Zoniferol</th>
    </tr>
    <tr>
      <th>Timepoint</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
    </tr>
    <tr>
      <th>5</th>
      <td>0.160000</td>
      <td>0.380952</td>
      <td>0.280000</td>
      <td>0.304348</td>
      <td>0.260870</td>
      <td>0.375000</td>
      <td>0.320000</td>
      <td>0.120000</td>
      <td>0.240000</td>
      <td>0.166667</td>
    </tr>
    <tr>
      <th>10</th>
      <td>0.320000</td>
      <td>0.600000</td>
      <td>0.666667</td>
      <td>0.590909</td>
      <td>0.523810</td>
      <td>0.833333</td>
      <td>0.565217</td>
      <td>0.250000</td>
      <td>0.478261</td>
      <td>0.500000</td>
    </tr>
    <tr>
      <th>15</th>
      <td>0.375000</td>
      <td>0.789474</td>
      <td>0.904762</td>
      <td>0.842105</td>
      <td>0.857143</td>
      <td>1.250000</td>
      <td>0.764706</td>
      <td>0.333333</td>
      <td>0.782609</td>
      <td>0.809524</td>
    </tr>
    <tr>
      <th>20</th>
      <td>0.652174</td>
      <td>1.111111</td>
      <td>1.050000</td>
      <td>1.210526</td>
      <td>1.150000</td>
      <td>1.526316</td>
      <td>1.000000</td>
      <td>0.347826</td>
      <td>0.952381</td>
      <td>1.294118</td>
    </tr>
    <tr>
      <th>25</th>
      <td>0.818182</td>
      <td>1.500000</td>
      <td>1.277778</td>
      <td>1.631579</td>
      <td>1.500000</td>
      <td>1.941176</td>
      <td>1.357143</td>
      <td>0.652174</td>
      <td>1.157895</td>
      <td>1.687500</td>
    </tr>
    <tr>
      <th>30</th>
      <td>1.090909</td>
      <td>1.937500</td>
      <td>1.588235</td>
      <td>2.055556</td>
      <td>2.066667</td>
      <td>2.266667</td>
      <td>1.615385</td>
      <td>0.782609</td>
      <td>1.388889</td>
      <td>1.933333</td>
    </tr>
    <tr>
      <th>35</th>
      <td>1.181818</td>
      <td>2.071429</td>
      <td>1.666667</td>
      <td>2.294118</td>
      <td>2.266667</td>
      <td>2.642857</td>
      <td>2.300000</td>
      <td>0.952381</td>
      <td>1.562500</td>
      <td>2.285714</td>
    </tr>
    <tr>
      <th>40</th>
      <td>1.380952</td>
      <td>2.357143</td>
      <td>2.100000</td>
      <td>2.733333</td>
      <td>2.466667</td>
      <td>3.166667</td>
      <td>2.777778</td>
      <td>1.100000</td>
      <td>1.583333</td>
      <td>2.785714</td>
    </tr>
    <tr>
      <th>45</th>
      <td>1.476190</td>
      <td>2.692308</td>
      <td>2.111111</td>
      <td>3.363636</td>
      <td>2.538462</td>
      <td>3.272727</td>
      <td>2.571429</td>
      <td>1.250000</td>
      <td>1.727273</td>
      <td>3.071429</td>
    </tr>
  </tbody>
</table>
</div>




```python
Capomulin = [0.00, 0.16, 0.32, 0.375, 0.652, 0.818, 1.091, 1.182, 1.381, 1.476]
Ceftamin = [0.00, 0.381, 0.600, 0.789, 1.111, 1.500, 1.937, 2.071, 2.357, 2.692]
Infubinol = [0.00, 0.280, 0.667, 0.905, 1.050, 1.278, 1.589, 1.667, 2.100, 2.111]
Ketapril = [0.00, 0.304, 0.591, 0.842, 1.211, 1.632, 2.056, 2.294, 2.733, 3.364]
Naftisol = [0.00, 0.261, 0.524, 0.857, 1.150, 1.500, 2.067, 2.267, 2.467, 2.538]
Placebo = [0.00, 0.375, 0.833, 1.250, 1.526, 1.941, 2.267, 2.643, 3.167, 3.273]
Popriva = [0.00, 0.320, 0.565, 0.765, 1.000, 1.357, 1.615, 2.300, 2.778, 2.571]
Ramicane = [0.00, 0.120, 0.250, 0.333, 0.348, 0.652, 0.783, 0.953, 1.100, 1.250]
Stelasyn = [0.00, 0.240, 0.478, 0.783, 0.952, 1.158, 1.389, 1.563, 1.583, 1.727]
Zoniferol = [0.00, 0.167, 0.500, 0.810, 1.294, 1.688, 1.933, 2.286, 2.786, 3.071]
Timepoint = [0, 5, 10, 15, 20, 25, 30, 35, 40, 45]

plt.scatter(Timepoint, Capomulin, marker="o", facecolors="red", edgecolors="black", label="Capomulin")
plt.scatter(Timepoint, Ceftamin, marker="o", facecolors="blue", edgecolors="black", label="Ceftamin")
plt.scatter(Timepoint, Infubinol, marker="o", facecolors="green", edgecolors="black", label="Infubinol")
plt.scatter(Timepoint, Ketapril, marker="o", facecolors="orange", edgecolors="black", label="Ketapril")
plt.scatter(Timepoint, Naftisol, marker="o", facecolors="pink", edgecolors="black", label="Naftisol")
plt.scatter(Timepoint, Placebo, marker="o", facecolors="purple", edgecolors="black", label="Placebo")
plt.scatter(Timepoint, Popriva, marker="o", facecolors="black", edgecolors="black", label="Popriva")
plt.scatter(Timepoint, Ramicane, marker="o", facecolors="yellow", edgecolors="black", label="Ramicane")
plt.scatter(Timepoint, Stelasyn, marker="o", facecolors="DarkBlue", edgecolors="black", label="Stelasyn")
plt.scatter(Timepoint, Zoniferol, marker="o", facecolors="DarkGreen", edgecolors="black", label="Zoniferol")

# Give the chart a title, x label, and y label
plt.title("Metastatic Spread During Treatment")
plt.xlabel("Time (Days)")
plt.ylabel("Metastatic Sites")
```




    Text(0,0.5,'Metastatic Sites')




![png](output_9_1.png)



```python
merge_drug_data['Mouse ID'] = pd.to_numeric(merge_drug_data['Mouse ID'], errors='raise')
merge_drug_data
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
      <th>Mouse ID</th>
      <th>Timepoint</th>
      <th>Tumor Volume (mm3)</th>
      <th>Metastatic Sites</th>
      <th>Drug</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>NaN</td>
      <td>0</td>
      <td>45.000000</td>
      <td>0</td>
      <td>Capomulin</td>
    </tr>
    <tr>
      <th>1</th>
      <td>NaN</td>
      <td>5</td>
      <td>45.651331</td>
      <td>0</td>
      <td>Capomulin</td>
    </tr>
    <tr>
      <th>2</th>
      <td>NaN</td>
      <td>10</td>
      <td>43.270852</td>
      <td>0</td>
      <td>Capomulin</td>
    </tr>
    <tr>
      <th>3</th>
      <td>NaN</td>
      <td>15</td>
      <td>43.784893</td>
      <td>0</td>
      <td>Capomulin</td>
    </tr>
    <tr>
      <th>4</th>
      <td>NaN</td>
      <td>20</td>
      <td>42.731552</td>
      <td>0</td>
      <td>Capomulin</td>
    </tr>
    <tr>
      <th>5</th>
      <td>NaN</td>
      <td>25</td>
      <td>43.262145</td>
      <td>1</td>
      <td>Capomulin</td>
    </tr>
    <tr>
      <th>6</th>
      <td>NaN</td>
      <td>30</td>
      <td>40.605335</td>
      <td>1</td>
      <td>Capomulin</td>
    </tr>
    <tr>
      <th>7</th>
      <td>NaN</td>
      <td>35</td>
      <td>37.967644</td>
      <td>1</td>
      <td>Capomulin</td>
    </tr>
    <tr>
      <th>8</th>
      <td>NaN</td>
      <td>40</td>
      <td>38.379726</td>
      <td>2</td>
      <td>Capomulin</td>
    </tr>
    <tr>
      <th>9</th>
      <td>NaN</td>
      <td>45</td>
      <td>38.982878</td>
      <td>2</td>
      <td>Capomulin</td>
    </tr>
    <tr>
      <th>10</th>
      <td>NaN</td>
      <td>0</td>
      <td>45.000000</td>
      <td>0</td>
      <td>Ketapril</td>
    </tr>
    <tr>
      <th>11</th>
      <td>NaN</td>
      <td>0</td>
      <td>45.000000</td>
      <td>0</td>
      <td>Ketapril</td>
    </tr>
    <tr>
      <th>12</th>
      <td>NaN</td>
      <td>5</td>
      <td>48.791665</td>
      <td>0</td>
      <td>Ketapril</td>
    </tr>
    <tr>
      <th>13</th>
      <td>NaN</td>
      <td>10</td>
      <td>53.435987</td>
      <td>0</td>
      <td>Ketapril</td>
    </tr>
    <tr>
      <th>14</th>
      <td>NaN</td>
      <td>15</td>
      <td>58.135545</td>
      <td>0</td>
      <td>Ketapril</td>
    </tr>
    <tr>
      <th>15</th>
      <td>NaN</td>
      <td>20</td>
      <td>62.706031</td>
      <td>0</td>
      <td>Ketapril</td>
    </tr>
    <tr>
      <th>16</th>
      <td>NaN</td>
      <td>25</td>
      <td>64.663626</td>
      <td>0</td>
      <td>Ketapril</td>
    </tr>
    <tr>
      <th>17</th>
      <td>NaN</td>
      <td>30</td>
      <td>69.160520</td>
      <td>0</td>
      <td>Ketapril</td>
    </tr>
    <tr>
      <th>18</th>
      <td>NaN</td>
      <td>35</td>
      <td>71.905117</td>
      <td>0</td>
      <td>Ketapril</td>
    </tr>
    <tr>
      <th>19</th>
      <td>NaN</td>
      <td>0</td>
      <td>45.000000</td>
      <td>0</td>
      <td>Ketapril</td>
    </tr>
    <tr>
      <th>20</th>
      <td>NaN</td>
      <td>5</td>
      <td>47.462891</td>
      <td>0</td>
      <td>Ketapril</td>
    </tr>
    <tr>
      <th>21</th>
      <td>NaN</td>
      <td>10</td>
      <td>49.783419</td>
      <td>0</td>
      <td>Ketapril</td>
    </tr>
    <tr>
      <th>22</th>
      <td>NaN</td>
      <td>0</td>
      <td>45.000000</td>
      <td>0</td>
      <td>Ketapril</td>
    </tr>
    <tr>
      <th>23</th>
      <td>NaN</td>
      <td>5</td>
      <td>45.769249</td>
      <td>1</td>
      <td>Ketapril</td>
    </tr>
    <tr>
      <th>24</th>
      <td>NaN</td>
      <td>10</td>
      <td>46.658395</td>
      <td>1</td>
      <td>Ketapril</td>
    </tr>
    <tr>
      <th>25</th>
      <td>NaN</td>
      <td>15</td>
      <td>48.370999</td>
      <td>1</td>
      <td>Ketapril</td>
    </tr>
    <tr>
      <th>26</th>
      <td>NaN</td>
      <td>20</td>
      <td>49.762415</td>
      <td>1</td>
      <td>Ketapril</td>
    </tr>
    <tr>
      <th>27</th>
      <td>NaN</td>
      <td>25</td>
      <td>51.828357</td>
      <td>1</td>
      <td>Ketapril</td>
    </tr>
    <tr>
      <th>28</th>
      <td>NaN</td>
      <td>30</td>
      <td>56.098998</td>
      <td>1</td>
      <td>Ketapril</td>
    </tr>
    <tr>
      <th>29</th>
      <td>NaN</td>
      <td>35</td>
      <td>57.729535</td>
      <td>1</td>
      <td>Ketapril</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>1876</th>
      <td>NaN</td>
      <td>25</td>
      <td>44.596219</td>
      <td>0</td>
      <td>Capomulin</td>
    </tr>
    <tr>
      <th>1877</th>
      <td>NaN</td>
      <td>30</td>
      <td>45.261384</td>
      <td>0</td>
      <td>Capomulin</td>
    </tr>
    <tr>
      <th>1878</th>
      <td>NaN</td>
      <td>35</td>
      <td>45.941949</td>
      <td>0</td>
      <td>Capomulin</td>
    </tr>
    <tr>
      <th>1879</th>
      <td>NaN</td>
      <td>40</td>
      <td>46.821070</td>
      <td>1</td>
      <td>Capomulin</td>
    </tr>
    <tr>
      <th>1880</th>
      <td>NaN</td>
      <td>45</td>
      <td>47.685963</td>
      <td>1</td>
      <td>Capomulin</td>
    </tr>
    <tr>
      <th>1881</th>
      <td>NaN</td>
      <td>0</td>
      <td>45.000000</td>
      <td>0</td>
      <td>Capomulin</td>
    </tr>
    <tr>
      <th>1882</th>
      <td>NaN</td>
      <td>5</td>
      <td>45.622381</td>
      <td>1</td>
      <td>Capomulin</td>
    </tr>
    <tr>
      <th>1883</th>
      <td>NaN</td>
      <td>10</td>
      <td>46.414518</td>
      <td>1</td>
      <td>Capomulin</td>
    </tr>
    <tr>
      <th>1884</th>
      <td>NaN</td>
      <td>15</td>
      <td>39.804453</td>
      <td>1</td>
      <td>Capomulin</td>
    </tr>
    <tr>
      <th>1885</th>
      <td>NaN</td>
      <td>20</td>
      <td>38.909349</td>
      <td>1</td>
      <td>Capomulin</td>
    </tr>
    <tr>
      <th>1886</th>
      <td>NaN</td>
      <td>25</td>
      <td>37.695432</td>
      <td>1</td>
      <td>Capomulin</td>
    </tr>
    <tr>
      <th>1887</th>
      <td>NaN</td>
      <td>30</td>
      <td>38.212479</td>
      <td>1</td>
      <td>Capomulin</td>
    </tr>
    <tr>
      <th>1888</th>
      <td>NaN</td>
      <td>35</td>
      <td>32.562839</td>
      <td>1</td>
      <td>Capomulin</td>
    </tr>
    <tr>
      <th>1889</th>
      <td>NaN</td>
      <td>40</td>
      <td>32.947615</td>
      <td>1</td>
      <td>Capomulin</td>
    </tr>
    <tr>
      <th>1890</th>
      <td>NaN</td>
      <td>45</td>
      <td>33.329098</td>
      <td>1</td>
      <td>Capomulin</td>
    </tr>
    <tr>
      <th>1891</th>
      <td>NaN</td>
      <td>0</td>
      <td>45.000000</td>
      <td>0</td>
      <td>Capomulin</td>
    </tr>
    <tr>
      <th>1892</th>
      <td>NaN</td>
      <td>5</td>
      <td>38.796474</td>
      <td>0</td>
      <td>Capomulin</td>
    </tr>
    <tr>
      <th>1893</th>
      <td>NaN</td>
      <td>10</td>
      <td>35.624403</td>
      <td>0</td>
      <td>Capomulin</td>
    </tr>
    <tr>
      <th>1894</th>
      <td>NaN</td>
      <td>15</td>
      <td>32.623003</td>
      <td>0</td>
      <td>Capomulin</td>
    </tr>
    <tr>
      <th>1895</th>
      <td>NaN</td>
      <td>20</td>
      <td>30.485985</td>
      <td>0</td>
      <td>Capomulin</td>
    </tr>
    <tr>
      <th>1896</th>
      <td>NaN</td>
      <td>0</td>
      <td>45.000000</td>
      <td>0</td>
      <td>Capomulin</td>
    </tr>
    <tr>
      <th>1897</th>
      <td>NaN</td>
      <td>5</td>
      <td>41.408591</td>
      <td>1</td>
      <td>Capomulin</td>
    </tr>
    <tr>
      <th>1898</th>
      <td>NaN</td>
      <td>10</td>
      <td>36.825367</td>
      <td>1</td>
      <td>Capomulin</td>
    </tr>
    <tr>
      <th>1899</th>
      <td>NaN</td>
      <td>15</td>
      <td>35.464612</td>
      <td>1</td>
      <td>Capomulin</td>
    </tr>
    <tr>
      <th>1900</th>
      <td>NaN</td>
      <td>20</td>
      <td>34.255732</td>
      <td>1</td>
      <td>Capomulin</td>
    </tr>
    <tr>
      <th>1901</th>
      <td>NaN</td>
      <td>25</td>
      <td>33.118756</td>
      <td>1</td>
      <td>Capomulin</td>
    </tr>
    <tr>
      <th>1902</th>
      <td>NaN</td>
      <td>30</td>
      <td>31.758275</td>
      <td>1</td>
      <td>Capomulin</td>
    </tr>
    <tr>
      <th>1903</th>
      <td>NaN</td>
      <td>35</td>
      <td>30.834357</td>
      <td>1</td>
      <td>Capomulin</td>
    </tr>
    <tr>
      <th>1904</th>
      <td>NaN</td>
      <td>40</td>
      <td>31.378045</td>
      <td>1</td>
      <td>Capomulin</td>
    </tr>
    <tr>
      <th>1905</th>
      <td>NaN</td>
      <td>45</td>
      <td>28.430964</td>
      <td>1</td>
      <td>Capomulin</td>
    </tr>
  </tbody>
</table>
<p>1906 rows × 5 columns</p>
</div>




```python
reduced_mouse = merge_drug_data.loc[:, ["Drug", "Timepoint", "Mouse ID"]]
reduced_mouse.head()

mouse_totals = reduced_mouse.set_index('Drug', 'Timepoint')
mouse_totals.head()
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
      <th>Timepoint</th>
      <th>Mouse ID</th>
    </tr>
    <tr>
      <th>Drug</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Capomulin</th>
      <td>0</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>Capomulin</th>
      <td>5</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>Capomulin</th>
      <td>10</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>Capomulin</th>
      <td>15</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>Capomulin</th>
      <td>20</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
</div>



Three Takeaways:
1) Capomulin and Ramicane were the most effective treatments in regard to reducing the size/volume of tumors over the period of 45 days.
2) Ketapril proved to be the least effective treatment, as it displayed the greatest increase in tumor volume and the greatest degree of metastatic site spread.  Towards the end of the treatment period, Ketapril showed to be even slightly worse than the placebo.
3) Between the two best treatments, Ramicane showed a slightly better percentage decrease in tumor volume, as well as more favorably limiting the spread of metastases.
