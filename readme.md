

<h1 style="text-align: center; color: Purple;">What drives a used car price?</h1>
<p>This Python application using Jupyter Notebook explores a dataset containing information of 430,000 people in order to determine which factors make them accept a driving coupon.</p>
<p><a href="https://github.com/Balu-A/UsedCarPriceDrivers/blob/main/Used%20Car%20Price%20Drivers.ipynb" target="_blank">Jupiter Notebook used</a></p>
<p> The current CRISP-DM Process Model for Data Mining (see Figure 1) was followed.</p>
<p align="center">
<img src="images/CRISP.jpg" width="300px" height="300px">
<h4 align="center"> Figure 1</h4>
</p>

<h2>Business Understanding</h2>
From a business perspective, we are tasked with identifying key drivers for used car prices.  In the CRISP-DM overview, we are asked to convert this business framing to a data problem definition.  Using a few sentences, reframe the task as a data task with the appropriate technical vocabulary. 

<hr style="border: solid 1px #000;">
<ol style="font-family: Arial;font-size: 16px;">
    <li style="color:Blue"> <span style="color:Blue; font-size:15px;font-weight: bold;">Tasks Involved:</li>
    <ul>
        <li style="color:Blue"> <span style="color:Blue; font-size:15px;">Develop a predictive modeling framework to estimate used car prices based on a variety of features.</span></li>
        <li style="color:Blue"> <span style="color:Blue; font-size:15px;">Perform exploratory data analysis to identify potential predictors of car prices, such as make, model, year, mileage, and condition.</span></li>
        <li style="color:Blue"> <span style="color:Blue; font-size:15px;">Construct a regression model that can quantify the impact of these features on the car's price. Key tasks include feature selection, model training, and validation to ensure the model accurately captures the relationship between car attributes and their market values.</span></li>
        <li style="color:Blue"> <span style="color:Blue; font-size:15px;">Pinpoint the most influential factors affecting used car prices and provide actionable insights for pricing strategies.</span></li>
    </ul>
</ol>

<h2>Data Understanding</h2>
After considering the business understanding, we want to get familiar with our data.  Write down some steps that you would take to get to know the dataset and identify any quality issues within.  Take time to get to know the dataset and explore what information it contains and how this could be used to inform your business understanding.

<hr style="border: solid 1px #000;">
 
<ol style="font-family: Arial;font-size: 16px;">
    <li style="color:Blue"> <span style="color:Blue; font-size:15px;font-weight: bold;"> Data Exploration: </span></li>
    <ul>
        <li style="color:Blue"> <span style="color:Blue; font-size:15px;">Begin by examining the structure of the dataset. How many columns and rows does it contain?</span></li>
        <li style="color:Blue"> <span style="color:Blue; font-size:15px;">Print out the first few rows of the dataset to get a sense of what the data looks like.</span></li>
        <li style="color:Blue"> <span style="color:Blue; font-size:15px;">Check the data types of each column. Are they numerical, categorical, or date-time?</span></li>
        <li style="color:Blue"> <span style="color:Blue; font-size:15px;">Look for any missing values in the dataset. How prevalent are they, and how might they affect your analysis?</span></li>
    </ul>
    <li style="color:Blue"> <span style="color:Blue; font-size:15px;font-weight: bold;"> Column Analysis: </span></li>
    <ul>
        <li style="color:Blue"> <span style="color:Blue; font-size:15px;">Examine the unique values in categorical columns. Are there any unexpected or invalid values?</span></li>
        <li style="color:Blue"> <span style="color:Blue; font-size:15px;">For numerical columns, check for outliers. Are there any values that seem unreasonable or far from the central tendency of the data?</span></li>
        <li style="color:Blue"> <span style="color:Blue; font-size:15px;">Check for consistency in date-time columns. Are all dates formatted correctly, and do they fall within expected ranges?</span></li>
    </ul>
    <li style="color:Blue"> <span style="color:Blue; font-size:15px;font-weight: bold;"> Data Quality Assessment: </span></li>
    <ul>
        <li style="color:Blue"> <span style="color:Blue; font-size:15px;">Assess the completeness of the dataset. Are there any columns with a high proportion of missing values?</span></li>
        <li style="color:Blue"> <span style="color:Blue; font-size:15px;">Look for duplicates in the dataset. Are there any rows that are exact duplicates or nearly identical duplicates?</span></li>
    </ul>
    <li style="color:Blue"> <span style="color:Blue; font-size:15px;font-weight: bold;"> Visualization: </span></li>
    <ul>
        <li style="color:Blue"> <span style="color:Blue; font-size:15px;">Create visualizations such as histograms, box plots, or scatter plots to explore the relationships between variables and identify any patterns or trends.</span></li>
        <li style="color:Blue"> <span style="color:Blue; font-size:15px;">Visualize missing data patterns to understand if there are any systematic issues with missing values.</span></li> 
    </ul> 

<h2>Data Preparation</h2>
<hr style="border: solid 1px #000;">
<span style="font-family: Arial;font-size: 16px;">1. A quick examination using DF.INFO yielded 
results that show **null data** across some features. 
</span> 
<p align="center">
<img src="images/Info.png" width="344px" height="436px">
<h4 align="center"> Figure 2</h4>
</p>

<span style="font-family: Arial;font-size: 16px;">Nulls per column:</span>

<p align="center">
<img src="images/Nulls_Pct.png" width="835px" height="451px">
<h4 align="center"> Figure 3</h4>
</p>

<span style="font-family: Arial;font-size: 16px;">2. Also, there is "**other**" value across multiple categorical features. This could potentially
create an issue when the categorical features are encoded. So, it makes sense to rename these
values according to feature. The list below shows the columns that have "other" values.</span>

<p align="center">
<img src="images/Other_Cleanup.png" width="391px" height="487px">
<h4 align="center"> Figure 4</h4>
</p>

<span style="font-family: Arial;font-size: 16px;">3. Upon inspection, there are **no duplicate rows** in the 
dataframe.</span>

<span style="font-family: Arial;font-size: 16px;">4. Next up, all the **categorical** features were encoded using 'Target encoding' technique.
A correlation heatmap was developed to understand the strength between dependent
and independent variables.
</span>

<p align="center">
<img src="images/Correlation.png" width="977px" height="902px">
<h4 align="center"> Figure 5</h4>
</p>

<span style="font-family: Arial;font-size: 16px;">5. In order to build effective models, some of the 
low-importance features were **dropped** from the dataframe.</span>

<span style="font-family: Arial;font-size: 16px;color: blue;"><strong>['id','region','title_status','VIN','paint_color','state','model']</strong></span>

<span style="font-family: Arial;font-size: 16px;">6. A close examination of the dataset reveals that
there are a lot of **outliers**. The below bar plot shows that Year and Price have huge outliers. 
These need to treated using **Interquartile Range [IQR]** technique.</span>

<p align="center">
<img src="images/Outliers Histogram.png" width="1494px" height="478px">
<h4 align="center"> Figure 6</h4>
</p>

<span style="font-family: Arial;font-size: 16px;"> After removing the outliers, 
this is the range of the numerical features:
<br>
(a) Lower limit for price is 0 and the upper limit is 45259
<br>
(b) Lower limit for odometer is 0 and the upper limit is 255000
<br>
(c) Lower limit for year is 1998 and the upper limit is 2026</span>


<h2>Data Modeling </h2>
<hr style="border: solid 1px #000;">
<span style="font-family: Arial;font-size: 16px;">The prediction of output was made using various
set of independent variables/input variables using three linear regression models. The models were: </span>
<span style="font-family: Arial;font-size: 16px;color: red;">
<br><br> 
<strong>(a) Linear Regression [w/ Permutation Importance]</strong> <br> 
<strong>(b) Ridge Regression [w/ GridSearch CV & Permutation Importance]</strong> <br> 
<strong>(c)Lasso Regression [w/ GridSearchCV & SequentialForwardSelection]</strong>
</span>
<br><br> 
<span style="font-family: Arial;font-size: 16px;">Out of the 3 models, the Lasso regression model performed relatively better with 70% of R-Squared error. 
This means that <strong> 70% of the variance in the dependent variable (the variable being predicted) is explained by 
the independent variables (the predictors) used in the model</strong>. This suggests that the model has a good level of 
fit and is able to explain a substantial portion of the observed variability in the outcome. </span>

<p align="center">
<img src="images/R2.png" width="579px" height="472px">
<h4 align="center"> Figure 7</h4>
</p>

<h2>Findings</h2>
<hr style="border: solid 1px #000;">
<span style="font-family: Arial;font-size: 16px;">(a) The<strong> most important drivers</strong> depicted by the Lasso 
regression are: </span>
<span style="font-family: Arial;font-size: 16px;color: blue;">
<div style="margin-left: 40px;">
1. Year  <br> 2. Odometer  <br> 3. Cylinders <br> 4. Transmission <br> 5. Drivetrain <br> 6. Trim Type
<br> 7. Fuel Injection </div></span>
<br><br>


<p align="center">
<img src="images/Price_Year_Cyl_Hist.png" width="1213px" height="342px">
<h4 align="center"> Figure 8</h4>
</p>
<span style="font-family: Arial; font-size: 16px;">
(b) Most used cars cost between $8000 and $10000. <br>
(c) The years that dominate:
<div style="margin-left: 40px;">
- Low price group are 2006, 2007, and 2008; <br>
- Medium price group are 2015, 2016, and 2017; <br>
- High price group are 2017, 2018, and 2019; <br>
</div>
(d) In regard to the engine configuration:
<div style="margin-left: 40px;">
- High price group are <strong>not</strong> 4-cylinder <br>
- Medium price group are either 6-cylinder or 8-cylinder <br>
- Low price group are 4-cylinder or 6-cylinder <br>
</div>
</span>


<p align="center">
<img src="images/Odo_Trans_Type_Hist.png" width="1167px" height="348px">
<h4 align="center"> Figure 9</h4>
</p>
<span style="font-family: Arial; font-size: 16px;">
(e) Cars under 50000 miles sell at a high price, decreasing exponentially thereafter. Cars with odometer between 
50000 and 10000 are popular among the low price group.<br>
(f) Automatic transmission is the most popular among the three price categories.<br>
(g) Pick-up trucks sell at a high price, while sedans and SUVs are popular in the low price tag. <br>
</span><nobr>

<h2>Next Steps and Recommendations</h2>
<hr style="border: solid 1px #000;">
<span style="font-family: Arial; font-size: 16px;">
- Consumers value recent models, so it is recommended that acquiring recent cars (2017 and beyond) is prioritised. Acquiring cars 
made in 2008 and prior should not be a priority <br>
- Cars made in 2017 and beyond can be listed at higher prices, while cars older than 2008 should be more affordably priced.<br>
- If the target market for the dealership is high price group, then they should prioritize selling 6-cylinder engine 
configuration cars. For the coupon-clippers, the 4- and 6-cylinder cars are recommended.<br>
- Lower odometer readings are valued, and efforts to list cars with odometer readings below 50000 miles are recommended. 
Cars with odometer readings above 100000 should not be prioritised, and when listed, they should be more affordably 
priced. <br>
- Automatic transmission cars are the most popular breed. Avoid listing manual transmission cars at all costs.<br>
- Consumers in the high price group value pick-up models. So, they can be priced higher. However, SUVs and sedans
are mostly preferred by price-conscious and savvy consumers.
</span>
