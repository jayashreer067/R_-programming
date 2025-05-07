# README

## Title: **Data Analysis of the Rare Soay Sheep**

### Date: January 10, 2024

---

### **Project Overview**

This study investigates how the **North Atlantic Oscillation (NAO)** affects the survival of the rare Soay sheep population. The primary focus is on how changes in **mean NAO values**, along with **age** and **sex**, influence **sheep weight**, which is considered the response variable in this analysis.

---

### **Objectives**

- Assess the relationship between sheep weight and environmental (NAO) and biological (age, sex) factors.
- Build and interpret a predictive model to understand the impact of these variables on sheep weight.
- Visualize and interpret interaction effects.

---

### **Methods**

- **Data Preprocessing**:
  - Two TSV files were loaded using the `readr` package.
  - `year` was used as a common column to merge datasets.
  - Missing values were dropped; `sex` was recoded (`female = 0`, `male = 1`).

- **Feature Engineering**:
  - New columns were created for `mean summer NAO` and `mean annual NAO`.
  - Aggregated by year and merged with the sheep data to form `merged_sheep_data`.

- **Modeling**:
  - A Generalized Linear Model (GLM) with a log link and Gaussian family was used:
    ```r
    glm(weight ~ mean_NAO + age + sex + 
               mean_NAO:age + age:sex + 
               sex:mean_NAO + mean_NAO:age:sex, 
        data = merged_sheep_data)
    ```

---

### **Results Summary**

- Significant variables:
  - **Intercept**, `mean_NAO`, `age`, and `sex` were significant predictors of weight.
- Interaction terms were generally not significant but helped explain trends.
- **Model Output**:
  - The model showed a residual deviance of 1687.5 on 2777 degrees of freedom.
  - AIC: 6526, suggesting decent model fit.
- **Predictions**:
  - At age 15 and mean NAO = 1.02:
    - Female predicted weight ≈ 12.37
    - Male predicted weight ≈ 12.87

---

### **Visualization**

Plots generated using `ggeffects::ggpredict()` showed:
- Clear distinctions in weight predictions based on **age**, **sex**, and **NAO**.
- Males generally weighed more than females under similar conditions.

---

### **Conclusion**

The analysis concludes that **sheep weight is influenced by mean summer NAO, age, and sex. The plot predicts that the weight of the sheep is affected by summer NAO and its internal factors such as age, sex and individuality**. Males are predicted to weigh more than females given the same environmental conditions, highlighting the compound impact of environmental and biological factors on the health and survival of the rare Soay sheep.
