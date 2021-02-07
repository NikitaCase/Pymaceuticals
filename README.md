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

- Some summary statistcis were performed 

```python 
# Using the aggregation method, produce the same summary statistics in a single line
reg2_df = combined_results.groupby(['Drug Regimen'])
tumor_vol_stats = reg2_df['Tumor Volume (mm3)'].agg(['mean','median','std','var','sem'])
```

