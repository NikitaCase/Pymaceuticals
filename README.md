# Pymaceuticals

This project analyzes and visualizes results from a drug trial with four drug regimens for squamous cell carcinoma in mice. 


### Technology Used

- Python
- Jupyter notebooks
- Pandas
- Matplotlib
- NumPy 
- SciPy


### Process

- Data were loaded from csvs and converted to dataframes

```python
mouse_metadata_path = "data/Mouse_metadata.csv"
study_results_path = "data/Study_results.csv"

# Read the mouse data and the study results
mouse_metadata = pd.read_csv(mouse_metadata_path)
study_results = pd.read_csv(study_results_path)

# Merging the dataframes
combined_results = pd.merge(study_results, mouse_metadata, on='Mouse ID', how='left')
```

- Some summary statistics were performed 

```python 
# Using the aggregation method, produce the same summary statistics in a single line
reg2_df = combined_results.groupby(['Drug Regimen'])
tumor_vol_stats = reg2_df['Tumor Volume (mm3)'].agg(['mean','median','std','var','sem'])
```
![Tumor Volume Statistics](/images/tumor_vol_stats.png)

-  Tumor volumes were compared across regimens

```python 
# Group data
Capomulin = final_tvolume_df.loc[final_tvolume_df['Drug Regimen'] =='Capomulin', 'Tumor Volume (mm3)']
...

# Generate a box plot of the final tumor volume
plt.boxplot([Capomulin, Ramicane, Infubinol, Ceftamin], labels=drugs_to_analyse, showmeans=True, showfliers=True, sym="c+")
```
![Tumor Volume Comparison](/images/final_tumor_vol.png)

- Other correlations in the data were explored

```python

# Calculate the correlation coefficient and linear regression model 
# for mouse weight and average tumor volume for the Capomulin regimen
slope, intercept, rvalue, pvalue, stderr = sp.linregress(x_axis,y_axis)

#plot regression over existing scatter plot
x_reg = np.arange(min(x_axis)-1,max(x_axis)+2,1)
y_reg = slope * x_reg + intercept
eq = f'y= {str(round(slope))}x + {str(round(intercept))},   r={str(round(rvalue,1))}'

```

![Tumov Volume vs Weight](/images/tumorvol_vs_weight.png)

