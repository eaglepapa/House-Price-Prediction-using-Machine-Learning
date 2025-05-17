# House Price Prediction using Machine Learning

## Table of Contents
- [Project Overview](#project-overview)
- [Data Sources](#data-sources)
- [Tools](#tools)
- [Data Cleaning/Preparation](#data-cleaningpreparation)
- [Exploratory Data Analysis](#exploratory-data-analysis)
- [Data Analysis](#data-analysis)
- [Results/Findings](#resultsfindings)
- [Recommendations](#recommendations)
- [Limitations](#limitations)
- [References](#references)
- [Contact](#contact)
  
### Project Overview
---
This report applies the Cross-Industry Standard Process for Data Mining (CRISP-DM) methodology to analyze the Miami housing dataset. CRISP-DM offers a structured approach to data mining, guiding the project through six key phases: Business Understanding, Data Understanding, Data Preparation, Modeling, Evaluation, and Deployment. By following this framework, the goal is to uncover meaningful patterns, extract valuable insights, and provide actionable recommendations for Real Estate Agencies. Random Forest Regression using number of trees of 200 was the best model with a RMSE of $105061.10

![modell errors](https://github.com/user-attachments/assets/aefaea74-14fc-49b9-902d-2ad02c0302b1)

### Data Sources
Housing Data: The dataset used in this analysis was sourced from Kaggle and contains detailed information about housing with variables such as Avg. Area Income, House Age, Number of Rooms, Number of Bedrooms, SquareFeet, Price, Neighborhood, Country, and capital. 
[miami-housing-dataset](https://www.kaggle.com/datasets/deepcontractor/miami-housing-dataset)

### Tools
- RStudio – Data cleaning and analysis  
  [Download here](https://posit.co/products/open-source/rstudio/)

- Power BI – Report creation and data visualization  
  [Download here](https://www.microsoft.com/en-us/download/details.aspx?id=58494)

- Excel – Data cleaning, transformation, and visualization  
  [Download here](https://www.microsoft.com/en-us/microsoft-365/excel)

#### Data Cleaning/Preparation
In the initial data preparation please, I performed the following tasks:
1.	Data loading and inspection.
2.	Handling missing values.
3.	Data cleaning and formatting.
4. 	Building the model
5.	Predicting values

   
### Exploratory Data Analysis
EDA involved exploring the housing data to answer key questions, such as: 
-	What machine learning models can be performed using the provided dataset?
-	What is the correlation between X and Y variables in the dataset? 
-	What is the best model among the other machine learning models?
-	What will be the predicted house price after inputting the values; LND_SQFOOT: 11247, TOTLVGAREA: 4552, SPECFEATVAL: 2105, RAIL_DIST: 4871.9, OCEAN_DIST: 18507.2, WATER_DIST: 375.8, CNTR_DIST: 43897.9, SUBCNTR_DI: 40115.7, HWY_DIST: 41917.1, age: 42, avno60plus: 0, structure_quality: 5, month_sold: 8, into the best model?
  
  ![corr](https://github.com/user-attachments/assets/4c50f732-4ea4-489a-8f0c-d9aae7d53005)

  
### Data Analysis 
```r 
# Dataframe of Error Metrics - RMSE of all the models created
model_rmse_df <- data.frame(
  model = c("LR", "SVR LINEAR","SVR RBF","SVR POLY", "DT", "RF N=100", "RF N=200", "RF N=500"),
  rmse = c(1.841267e+05, 2.092939e+05, 1.145848e+05, 1.298094e+05, 1.785767e+05, 1.055497e+05, 1.050611e+05, 1.053093e+05)
)

# Bar chart of Error Metrics - RMSE of all the models created
ggplot(data = model_rmse_df, aes(x = model, y = rmse)) +
  geom_bar(stat = "identity", fill = "skyblue") +
  labs(title = "Bar chart of models RMSE", x = "Model", y = "RMSE")

# Save the trained model object to a file
saveRDS(rf_model_n200, "rf_model_n200.rds")

# Load the Random Forest Regression model
rf_model_n200 <- readRDS("rf_model_n200.rds")

# Prepare the input data
input_data <- data.frame(
  PARCELNO = 728980145245,
  LND_SQFOOT = 11247,
  TOT_LVG_AREA = 4552,
  SPEC_FEAT_VAL = 2105,
  RAIL_DIST = 4871.9,
  OCEAN_DIST = 18507.2,
  WATER_DIST = 375.8,
  CNTR_DIST = 43897.9,
  SUBCNTR_DI = 40115.7,
  HWY_DIST = 41917.1,
  age = 42,
  avno60plus = 0,
  month_sold = 8,
  structure_quality = 5
)

# Make predictions
predictions <- predict(rf_model_n200, input_data)
```

### Results/Findings
The analysis results are summarized as follows:
1.	Machine learning models such as Multiple Linear Regression, Support Vector Regression using kernels like Linear, Polynomial, and Radial Basis Functions (RBF), Decision Tree Regression, Random Forest Regression using number of trees of 100, 200 and 500 were performed.
2.	
|X vrs. Y variables|Correlation coefficient|Strength|Direction|
|------------------|-----------------------|--------|---------|
|SALE_PRC and TOT_LVG_AREA|+0.67|Strong|As floor area increases, sale price also increases|
|CNTR_DIST and  SUBCNTR_DI|+0.77|Strong|As distance to the Miami central business district increases,  distance to the nearest sub center also increases|
|CNTR_DIST and age|-0.55|Moderate|As age of the structure increases, distance to the Miami central business district decrease|
4.	The Random Forest Regression using number of trees of 200 was the best model with a Root Mean Squared Error (RMSE) of $105,061.10.
5.	After inputting the values; LND_SQFOOT: 11247, TOTLVGAREA: 4552, SPECFEATVAL: 2105, RAIL_DIST: 4871.9, OCEAN_DIST: 18507.2, WATER_DIST: 375.8, CNTR_DIST: 43897.9, SUBCNTR_DI: 40115.7, HWY_DIST: 41917.1, age: 42, avno60plus: 0, structure_quality: 5, month_sold: 8, into the best model, the predicted house price was $1,227,864.

### Recommendations
I recommend adopting Random Forest Regression with 200 trees as the predictive model for housing prices, based on the performance illustrated in the bar chart below.

![rmse1](https://github.com/user-attachments/assets/8e03c3d3-5c7e-4409-83fe-cda328dd19ca)

### Limitations
The dataset was sourced from Kaggle, and as such, the authenticity and reliability of the data cannot be fully guaranteed. Additionally, Random Forest is considered a black-box model, offering limited interpretability compared to more transparent models like linear regression. This lack of explainability can pose challenges when communicating insights and justifying predictions to stakeholders.

### References
1.	Bevans, R. (2020) Linear Regression in R | A Step-by-Step Guide & Examples, [Online]. Available from: https://www.scribbr.com/statistics/linear-regression-in-r/. [Accessed 24 April 2024].
2.	Essense. (2023) Turning Data Into Actionable Insights: A Step-By-Step Guide. [Online] Available from: https://www.essense.io/blog/turning-data-into-actionable-insights-a-step-by-step-guide. [Accessed 24 April 2024].
3.	Hotz, N. (2018) What is CRISP DM? Data Science Process Alliance. [Online] Available from: https://www.datascience-pm.com/crisp-dm-2/. [Accessed 2 March 2024].
4.	Talaviya, A. (2023). CRISP-DM framework: A foundational data mining process model. [Online] Available from: https://medium.com/@avikumart_/crisp-dm-framework-a-foundational-data-mining-process-model-86fe642da18c. [Accessed 22 April 2024].
5.	Zach. (2021) How to Interpret Root Mean Square Error (RMSE). [Online]. Available from: https://www.statology.org/how-to-interpret-rmse/. [Accessed 22 April 2024].
6.	HAYES, A. (2023). Multiple Linear Regression (MLR) Definition, Formula, and Example. [Online] Available from: https://www.investopedia.com/terms/m/mlr.asp. [Accessed 24 Apr 2024].
7.	Prasad, A. (2024) Regression Trees | Decision Tree for Regression | Machine Learning. [Online]. Available from: https://medium.com/analytics-vidhya/regression-trees-decision-tree-for-regression-machine-learning-e4d7525d8047. [Accessed 24 April 2024].

## Contact
Feel free to reach out!  
📧 Email: [oduroprince08@gmail.com](mailto:oduroprince08@gmail.com) &nbsp;|&nbsp; 🔗 LinkedIn: [linkedin.com/in/oduroprince24](https://linkedin.com/in/oduroprince24)


🚀
📊
📈
🧠

Thanks for visiting! 😄
