# INDIA STARTUP ECOSYSTEM: DATA ANALYST'S VIEW

![india_head_image](https://github.com/snyamson/LPI---Indian-Startup-Ecosystem-Analysis/assets/58486437/3c417701-f967-436a-912d-6e120f07086f)

In recent years, India has witnessed a remarkable surge in entrepreneurial activities, propelling the growth of its startup ecosystem. With a burgeoning population, a thriving digital landscape, and a supportive environment for innovation and entrepreneurship, India has become a hotbed for startups across various industries. 

This data analysis task aims to provide a comprehensive overview of the Indian startup ecosystem, focusing on the period from 2018 to 2021. By examining a rich dataset encompassing this timeframe, we aim to uncover key trends, patterns, and insights that shed light on the dynamic nature of India's startup landscape.


# Project Structure

To analyze the funding received by startups in India from 2018 to 2021, separate data for each year of funding will be provided, where you will find the startups' details.

The steps involved in the project are:

# Importation

Import necessary libraries
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import plotly.express as px
import missingno as msno

# Data Loading

•The dataset for 2020 and 2021 is stored in a database that is accessed using credentials stored in a .env file in the folder. A gitignore file is created to prevent git from tracking the .env file.
•Create a connection string to access the defined environment variables and set up a query to access the data. I used the open Database Connectivity standard library pyodbc.
•The 2018 dataset is hosted on the Azubi Africa GitHub repo.
•The 2019 dataset is downloaded from the Azubi Africa OneDrive.

# Exploratory Data Analysis (EDA)

I used various pandas functions and methods to gain an initial understanding of the data, such as `.head()` to view rows in the dataset, `.shape()` to get the total rows and columns in the dataset, `.info()` to get information on the columns, `.describe()` to get descriptive statistics about the DataFrame, `.unique()` and `.value_counts()` to count the number of occurrences of a value, `.isnull()` to check for missing values, and `.duplicated()` to check for duplicate values.

After looking at the datasets, I have identified several data quality issues while exploring the datasets:

•	Inconsistent and missing columns: Some datasets have inconsistent column structures, with missing columns in certain cases.
•	Missing columns and duplicates in the datasets: Specifically, the 2018 dataset is missing additional columns that are present in other datasets.
•	Inconsistent values and currencies in the Amount column: The Amount column contains inconsistent values and different currencies.
•	Inconsistent values in the Stage column: The Stage column exhibits inconsistent values across all datasets, which hampers uniform analysis.
•	Missing values: Some datasets contain missing values, which need to be addressed for a complete and reliable analysis.

I came up with a hypothesis that is to be proved by the data.

`Null Hypothesis (H0):` The round of funding (Stage_of_funding) does not have a significant impact on the amount of funds raised (Amount) by Indian startups.

`Alternate Hypothesis (H1):` The round of funding (Stage_of_funding) has a significant impact on the amount of funds raised (Amount) by Indian startups.

Questions that guided the test and the analysis are:

1.	How does the distribution of funding amounts vary across different stages of funding? Are there any outliers in the funding amount within each stage?
2.	What has been the trend of investment amount over the years (2018–2021)?
3.	What has accounted for the distribution of stages of funding in a year-by-year case?
4.	What stage of startups received the highest funding investment and why?
5.	Does the sector of startups have an influence on the stage of funding they receive and why?

# Feature Processing

After conducting the hypothesis test, it was found that there is a significant difference in the funding amount received by startups at different stages of funding.

To handle the missing values in the Amount column, It was decided to replace them with the median funding amount for each respective stage. This approach addresses outliers and provides a more accurate estimate of the funding amount a startup is likely to receive at a specific stage of funding.

By using the median, we ensure that the replaced values align with the overall funding trends observed in each funding stage.

# Data Merging

As the data is from different sources, merging is done with a few considerations and cleaned.
•	The  `Location` column in the 2018 dataset will be dropped since it does not impact our analysis.
•	The `index` column in the 2019 dataset will also be dropped.
•	The `HeadQuarter, Founders, and Investors` columns will be dropped as our analysis or hypothesis does not involve analyzing those columns.

![missing values percentage per column](https://github.com/snyamson/LPI---Indian-Startup-Ecosystem-Analysis/assets/58486437/3185dbb0-d4c6-4565-91a9-6cf59d476454)
![total rows of missing data](https://github.com/snyamson/LPI---Indian-Startup-Ecosystem-Analysis/assets/58486437/c767df0c-00ec-4f0f-b17e-a5fc01b647db)
![total percentage of missing data](https://github.com/snyamson/LPI---Indian-Startup-Ecosystem-Analysis/assets/58486437/7e8b5dc5-20b0-416d-ab12-8aecb14e9988)

After merging and cleaning, it was revealed that the merged dataset contains 9 duplicated data points. These rows will be examined further and dropped. The code above reveals that there are a total of 257 rows that contain at least one missing value in one of its feature fields. 
The total percentage of missing values will be computed and examined and dropped where necessary.

- The Sector is missing about 0.63% of data points.
- Founded (Year) is missing about 8.45% of data points.
- The Whole dataset is missing about 9.01% observations.
  
Since the whole dataset is missing only 9% of observations and will not have an impact on the analysis, they will be dropped.


Applying the `.info()` function on the master dataset

![dataset overview](https://github.com/snyamson/LPI---Indian-Startup-Ecosystem-Analysis/assets/58486437/a7933a9b-5554-4cad-82c6-df4ed52c96fa)


To enable deep-level analysis, the data will be further processed by categorizing the `Stage` column into high-level funding stages based on the stages listed on the Indian Startup Ecosystem website. A new column, `Stage_of_funding`, will be created to facilitate the groupings.

![high level stage of funding groupings](https://github.com/snyamson/LPI---Indian-Startup-Ecosystem-Analysis/assets/58486437/41afa0b1-ab43-4f57-b7af-0f26ecbd8388)


A high-level function was written to facilitate these groupings, and the results are shown below.

![grouping result](https://github.com/snyamson/LPI---Indian-Startup-Ecosystem-Analysis/assets/58486437/2d408af9-ee97-42f4-8941-8ece402d6355)

 
From statistics done, the numbers indicate the distribution of companies across different stages of funding:

•	Early Traction: 1398 companies are in this stage.
•	Validation: 689 companies are in this stage.
•	Scaling: 347 companies are in this stage.
•	Ideation: 76 companies are in this stage.
•	Other: 76 companies are in this stage.
•	Exit Option: 8 companies are in this stage.

# Hypothesis Testing

The ANOVA test was used to test the hypothesis defined earlier, either to reject or not to reject the null hypothesis. The result of the test is displayed below.

![anova result](https://github.com/snyamson/LPI---Indian-Startup-Ecosystem-Analysis/assets/58486437/a8f0c0ee-c48a-4ca5-ab30-7e84727e8fbb)

Based on the given table, since the p-value is less than the significance level `(0.05)`, we can conclude that the stage of funding has a statistically significant impact on the amount of funding received by startups. Therefore, we can reject the null hypothesis that the round of funding `(Stage_of_funding)` does have a significant impact on the amount of funds raised `(Amount)` by Indian startups.

This implies that the amount of funding received by startups at one stage of funding is statistically different from the amount received in a different stage of funding.

# Investigating the questions

Investigating the questions, we can draw the following insights:

### 1. Distribution of Funding Amounts Across Different Stages of Funding. Are there any outliers in the funding amount within each stage?
![box plot](https://github.com/snyamson/LPI---Indian-Startup-Ecosystem-Analysis/assets/58486437/e8dfd307-9219-411f-90be-9f9139342eb9)

![voilin plot](https://github.com/snyamson/LPI---Indian-Startup-Ecosystem-Analysis/assets/58486437/fa8548a0-7a34-42c7-b35e-13d6f776e8e6)

The box plot and violin plot depict the funding amount distribution across different stages of funding based on the data. 

For each stage below is the observation:

1. Early Traction has a median funding amount of $3,450,000, ranging from $877 to $70,000,000.
2. Exit Option shows a concentrated distribution around $71,629,435, with values ranging from $16,517,739 to $224,992,100.
3. Ideation exhibits a narrow distribution, with most data points below $500,000, and a median funding amount of $325,000.
4. Other displays a wide funding range, with a median funding amount of $5,020,000 and values from $1,461 to $150,000,000,000.
5. Scaling demonstrates a moderate concentration around $30,000,000, ranging from $410,000 to $1,000,000,000.
6. Validation shows a narrow distribution with a significant concentration around $730,873, and values ranging from $1,461 to $140,000,000.
Both plots reveal variations in funding amounts among different stages and potential outliers. The violin plot highlights the density of funding amounts at various points, providing a comprehensive view of funding distribution across stages.


### 2. Funding Trends Over the Years (2018-2021)
![average investment trend plot](https://github.com/snyamson/LPI---Indian-Startup-Ecosystem-Analysis/assets/58486437/ab03c6a0-3c52-4c94-ba17-3d982d686426)
![total investment plot](https://github.com/snyamson/LPI---Indian-Startup-Ecosystem-Analysis/assets/58486437/2b092112-5997-4fe6-8c3a-fbe8c16445ec)

From the Line Chart and the Bar Graph above, these points demonstrate the contrasting trends in average investment amounts and total investment amounts across all startups over the years. 
The line graph reflects the fluctuations in average investments, showcasing a significant increase in 2018, followed by a decline in 2019 and 2020, and an increase in 2021. 


### 3. Factors Accounting for the Distribution of Stages of Funding Year-by-Year
![distribution of stage of funding across years](https://github.com/snyamson/LPI---Indian-Startup-Ecosystem-Analysis/assets/58486437/9fb6651a-003c-4781-876d-f89f8fdd0c68)

The funding trend depicted in the graph reveals interesting insights. In 2018, a noticeable decrease in funding amounts can be attributed to many startups in the Exit Option and Other stages not receiving further funding, as they were already at an advanced stage of development. These stages generally require substantial funding.

Additionally, the declining funding in 2019 can be linked to a decrease in the number of Early Traction and Validation startups receiving funding.
 In 2020, there was a shift in investor focus, leading to increased funding for startups in the Ideation and Validation stages.
 
However, funding for startups in the Early Traction and Scaling stages reduced, possibly as investors sought to support fresh and innovative ideas in the economy.


### 4. Stage of Startups Receiving the Highest Funding Investment
![stages of startups with highest funding amount](https://github.com/snyamson/LPI---Indian-Startup-Ecosystem-Analysis/assets/58486437/cc86e8d6-e307-4c52-8972-9f4a49ed6f9b)

From the Graph above, Over the years, a majority of the startups that have received funding fall under the "Other" category, which includes Private Equity, Corporate Round, Undisclosed, Non-equity Assistance, Debt, Bridge, and Edge. These types of funding are often associated with more mature startups. As the startup ecosystem has matured, investors have become more comfortable investing in later-stage startups that are closer to profitability.


On the other hand, early-stage startups categorized as "Ideation" have received less attention and funding. This could be attributed to the global economic slowdown during the period from 2018 to 2021. Economic downturns can make it more challenging for early-stage startups to raise capital. These startups are typically considered riskier, and investors tend to be more risk-averse in a recessionary environment.


These observations suggest that the funding landscape has favored more mature startups in recent years, while early-stage startups face additional challenges due to the economic conditions. It highlights the importance for early-stage startups to navigate the funding landscape effectively and demonstrate their potential for growth and profitability to attract investors even during challenging times.


### 5. Influence of the Sector on the Stage of Funding Received
![sector and funding](https://github.com/snyamson/LPI---Indian-Startup-Ecosystem-Analysis/assets/58486437/bbb586c7-871f-453e-ac86-beddd1017b25)


Based on the above graph, it is evident that the hospitality sector has the highest count in the stages of funding, namely early traction, validation, and scaling, within the Indian startup ecosystem. This pattern can be explained by several factors, including:

•	**Market Demand:** The hospitality sector, encompassing industries such as hotels, restaurants, and travel, experiences significant demand due to India's growing population, rising disposable incomes, and increasing tourism. The demand for hospitality services creates a favorable environment for startups in this sector, leading to a higher count of funding in early traction, validation, and scaling stages.

•	**Potential Growth:** The hospitality sector in India offers substantial growth potential, driven by factors such as an expanding tourism industry and the government's focus on promoting travel and hospitality. Investors recognize the growth opportunities in this sector and are more inclined to fund startups operating in hospitality, thereby contributing to the higher count of funding in the early stages.

•	**Innovation and Disruption:** Startups in the hospitality sector often introduce innovative solutions and disruptive business models to address emerging market needs. These innovations can range from online booking platforms, sharing economy concepts, technology-driven solutions for customer experience, and sustainable practices. The ability of hospitality startups to innovate and disrupt traditional industry practices attracts attention from investors, leading to increased funding in the early traction, validation, and scaling stages.


# Recommendations

Based on the comprehensive deep-level analysis conducted above, the following recommendations are proposed.

1. Investors should consider allocating funds to startups in different stages of funding, as the analysis reveals variations in the median funding amounts across stages. For instance, startups in the "Exit Option" stage have a median funding of $71,629,435, while startups in the "Ideation" stage have a median funding of $325,000. This diversification can help balance potential risks and returns.
2. Startups in the "Other" category, which includes mature stages like Private Equity and Corporate rounds, received the highest count of funding over the years (781 startups). Investing in this category may offer stable investment opportunities, considering its wide distribution of funding amounts ranging from $1,461 to $150,000,000,000.
3. Despite the relatively high count of startups in the "Early Traction" stage (1398 startups), its median funding amount is $3,450,000, with potential outliers reaching as high as $70,000,000. Investors should carefully assess these outliers to understand their potential for high returns or the risks associated with large funding requirements.
4. The "Ideation" stage has the lowest median funding amount of $325,000, indicating a potential investment opportunity for venture capitalists seeking to support early-stage innovative ideas. Investing in this stage could lead to significant returns if promising startups scale successfully.
5. The analysis also reveals a decline in average investment amounts from 2018 to 2019 and a subsequent increase in 2021. Investors should be cautious of economic trends and consider the fluctuating investment climate when making funding decisions. Thorough due diligence and an assessment of startups' growth potential are essential to making well-informed investment choices.

   
# References

 https://www.startupindia.gov.in/
 
# Appreciation

I highly recommend Azubi Africa for their comprehensive and effective programs. Read More articles about Azubi Africa here and take a few minutes to visit this link to learn more about Azubi Africa life-changing programs.
