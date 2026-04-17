# 🌍 CO₂ Emissions and Deforestation Analysis in the Amazon

<p align="center">
  🇺🇸 English •
  <a href="README.pt-br.md">🇧🇷 Português</a>
</p>

---

## 📌 Overview
This project analyzes how deforestation in the Amazon directly influences CO₂ emissions over the decades, highlighting how traditional models underestimate environmental impact by ignoring forest degradation.

The analysis uses preprocessed data that considers two scenarios:
- First-order model (without degradation)
- Second-order model (with degradation)

The objective is to understand how environmental degradation intensifies emissions.

---

## 📂 Data

The data used in this project comes from the National Institute for Space Research (INPE), through the Amazon gross emissions estimation system:

🔗 https://inpe-em.ccst.inpe.br/emissoes-brutas-amz/

### 📊 Included information:
- CO₂ emissions associated with deforestation
- Estimates considering forest degradation
- Historical time series of the Brazilian Amazon

### 🧭 Notes:
- The data represents **gross emissions**, meaning it does not consider carbon removal by vegetation
- The methodology is based on scientific modeling developed by INPE
- There may be differences compared to other databases (e.g., SEEG)

---

## ⚙️ How the analysis was built

- Separation of data into scenarios with and without degradation  
- Aggregation by year  
- Comparison between different emission models  
- Identification of extreme values  
- Visualization of results  

---

## 📊 Results and Visualizations

---

### 🔹 Deforestation over time

This graph shows the evolution of deforestation in the Amazon over the years, considering only areas without degradation.

<details>
  <summary>💻 Code (click to expand)</summary>

```python
# Filter data (without degradation)
df_without_degradation = filter_without_degradation(df)

# Aggregate deforestation by year
df_grouped_deforestation_without_degradation = aggregation_deforestation(df_without_degradation)

# Find max and min values
max_year_deforestation_without_degradation, max_value_deforestation_without_degradation, min_year_deforestation_without_degradation, min_value_deforestation_without_degradation = extremes_deforestation_without_degradation(df_grouped_deforestation_without_degradation)

# Generate graph
plot_graphic_deforestation_without_degradation(
    df_grouped_deforestation_without_degradation,
    max_year_deforestation_without_degradation,
    max_value_deforestation_without_degradation,
    min_year_deforestation_without_degradation,
    min_value_deforestation_without_degradation
)
```
</details>

---

🖼️ Graph:

![Deforestation](images/deforestation_without_degradation.png)

---

📊 Analysis:

The graph shows that deforestation increases consistently until the 1990s, reaching its peak during this period. This behavior suggests a phase of intense economic expansion in the region, with strong pressure on the forest.

From the 2000s onward, a downward trend is observed, becoming more evident after 2010. This decline may be associated with the implementation of stricter environmental policies, satellite monitoring, and more effective enforcement.

Additionally, the presence of sharp peaks and drops throughout the series suggests that deforestation does not occur in a stable way, but responds to external factors such as economic changes, government policies, and international pressure.

Overall, the graph highlights not only the magnitude of deforestation over time but also the direct influence of human and institutional actions on the environmental dynamics of the Amazon.

---

### 🔹 CO₂ emissions with degradation (second-order)

This graph presents CO₂ emissions over time considering environmental degradation, using the second-order model.

<details>
  <summary>💻 Code (click to expand)</summary>

```python
# Filter data (with degradation)
df_with_degradation = filter_with_degradation(df)

# Aggregate emissions by year
df_grouped_carbon_emission_with_degradation = aggregation_carbon_emission_with_degradation(df_with_degradation)

# Find max and min values
max_year_carbon_emission_with_degradation, max_value_carbon_emission_with_degradation, min_year_carbon_emission_with_degradation, min_value_carbon_emission_with_degradation = extremes_carbon_emission_with_degradation(df_grouped_carbon_emission_with_degradation)

# Generate graph
plot_graphic_carbon_emission_with_degradation(
    df_grouped_carbon_emission_with_degradation,
    max_year_carbon_emission_with_degradation,
    max_value_carbon_emission_with_degradation,
    min_year_carbon_emission_with_degradation,
    min_value_carbon_emission_with_degradation
)
```
</details>

---

🖼️ Graph:

![Second Order CO₂](images/second_order_carbon_emission.png)

---

📊 Analysis:

CO₂ emissions show a growth pattern over time, with peaks associated with periods of higher deforestation activity.

By considering environmental degradation, this model captures broader impacts beyond direct vegetation removal, resulting in more realistic emission values.

The variation over the years indicates that emissions depend not only on deforested area but also on degradation intensity and environmental conditions. This behavior reinforces the importance of more complete models for climate analysis.

---

### 🔹 Emissions comparison (with vs without degradation)

This graph compares CO₂ emissions under two scenarios: with and without environmental degradation, allowing visualization of the additional impact of degradation.

<details>
  <summary>💻 Code (click to expand)</summary>

```python
# Aggregate emissions without degradation
df_grouped_carbon_emission_without_degradation = aggregation_carbon_emission_without_degradation(df_without_degradation)

# Aggregate emissions with degradation
df_grouped_carbon_emission_with_degradation = aggregation_carbon_emission_with_degradation(df_with_degradation)

# Find extremes (without degradation)
max_year_carbon_emission_without_degradation, max_value_carbon_emission_without_degradation, min_year_carbon_emission_without_degradation, min_value_carbon_emission_without_degradation = extremes_carbon_emission_without_degradation(df_grouped_carbon_emission_without_degradation)

# Find extremes (with degradation)
max_year_carbon_emission_with_degradation, max_value_carbon_emission_with_degradation, min_year_carbon_emission_with_degradation, min_value_carbon_emission_with_degradation = extremes_carbon_emission_with_degradation(df_grouped_carbon_emission_with_degradation)

# Generate comparison graph
plot_graphic_comparison_carbon_emission(
    df_grouped_carbon_emission_without_degradation,
    max_year_carbon_emission_without_degradation,
    max_value_carbon_emission_without_degradation,
    min_year_carbon_emission_without_degradation,
    min_value_carbon_emission_without_degradation,
    df_grouped_carbon_emission_with_degradation,
    max_year_carbon_emission_with_degradation,
    max_value_carbon_emission_with_degradation,
    min_year_carbon_emission_with_degradation,
    min_value_carbon_emission_with_degradation
)
```
</details>

---

🖼️ Graph:

![Comparison](images/comparison_carbon_emission.png)

---

📊 Analysis:

The comparison between the two scenarios clearly highlights the impact of environmental degradation on CO₂ emissions. In all periods, the model with degradation shows higher values than the model without degradation.

The area between the curves represents additional emissions that would not be captured by a simplified model. This shows that considering only direct deforestation leads to a significant underestimation of environmental impact.

This difference becomes more relevant during periods of higher activity, indicating that degradation further intensifies the effects of land-use changes.

---

### 🔹 Deforestation vs emissions

This graph presents, in subplots, the relationship between deforestation and CO₂ emissions over time, allowing a visual comparison of both variables.

<details>
  <summary>💻 Code (click to expand)</summary>

```python
# Aggregate deforestation
df_grouped_deforestation_without_degradation = aggregation_deforestation(df_without_degradation)

# Aggregate emissions with degradation
df_grouped_carbon_emission_with_degradation = aggregation_carbon_emission_with_degradation(df_with_degradation)

# Find deforestation extremes
max_year_deforestation_without_degradation, max_value_deforestation_without_degradation, min_year_deforestation_without_degradation, min_value_deforestation_without_degradation = extremes_deforestation_without_degradation(df_grouped_deforestation_without_degradation)

# Find emission extremes
max_year_carbon_emission_with_degradation, max_value_carbon_emission_with_degradation, min_year_carbon_emission_with_degradation, min_value_carbon_emission_with_degradation = extremes_carbon_emission_with_degradation(df_grouped_carbon_emission_with_degradation)

# Generate combined graph
plot_graphic_deforestation_carbon_emission(
    df_grouped_deforestation_without_degradation,
    max_year_deforestation_without_degradation,
    max_value_deforestation_without_degradation,
    min_year_deforestation_without_degradation,
    min_value_deforestation_without_degradation,
    df_grouped_carbon_emission_with_degradation,
    max_year_carbon_emission_with_degradation,
    max_value_carbon_emission_with_degradation,
    min_year_carbon_emission_with_degradation,
    min_value_carbon_emission_with_degradation
)
```
</details>

---

🖼️ Graph:

![Deforestation vs CO₂](images/deforestation_carbon_emission.png)

---

📊 Analysis:

The comparison between deforestation and CO₂ emissions reveals a consistent relationship between the two variables over time. Periods of increased deforestation tend to coincide with higher emissions.

However, the relationship is not perfectly linear, indicating the presence of other factors influencing emissions, such as degradation, vegetation type, and fire intensity.

This analysis reinforces that deforestation is one of the main drivers of emissions in the Amazon, but not the only one, highlighting the complexity of the environmental system.

---

## 🚀 How to run

Clone the repository, navigate to the folder, and run:

    git clone https://github.com/RuyMachado/amazon-deforestation-carbon-emissions.git
    cd amazon-deforestation-carbon-emissions
    pip install -r requirements.txt
    python main.py

---

## 🛠️ Technologies used

- Python  
- Pandas  
- Matplotlib 

---

## 📌 Conclusion

The results demonstrate that forest degradation has a significant impact on CO₂ emissions and is often underestimated by simplified models.

The comparison between scenarios shows that:

- Models without degradation underestimate real emissions
- The relationship between deforestation and CO₂ is strong, but not linear
- Public policies and external factors directly influence observed patterns

These findings reinforce the need for more complete approaches in climate modeling and environmental strategy development.

Additionally, the results highlight the critical role of the Amazon in global climate balance and the importance of effective environmental policies.

---