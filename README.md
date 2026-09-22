# Telco Customer churn and retention strategy



## Project overview



&#x09;The project develops an end-to-end customer churn analysis and retention strategy using the Telco Customer churn dataset.



&#x09;The objective is not only to predict which customers are likely to churn, but also to translate model outputs into actionable customer segments, targeted retention interventions, and an illustrative business-impact framework.

&#x09;

&#x09;The project combines exploratory data analysis, classification modeling, cross-validation, hyperparameter tuning, threshold optimization, customer risk segmentation, retention strategy design, scenario-based campaign economics, and an interactive Power BI dashboard.



### Business problem



&#x09;Customer churn reduces recurring revenue and increases the pressure to acquire replacement customers. A useful churn analysis therefore needs to go beyond prediction and answer three business questions:



1. Which customers are most likely to churn?
2. What characteristics are associated with elevated churn risk?
3. Which customers should be prioritized for retention intervention given limited budget and operational capacity?



The project was designed around these questions, with emphasis on both predictive performance and practical business usability.



## Dataset



&#x09;The analysis uses the Telco Customer churn dataset containing 7,043 customers and information on:



* customer demographics
* tenure
* contract type
* internet and phone services
* support and security services
* billing and payment methods
* monthly and total charges
* churn status



The target variable is churn.



For model evaluation the data was split into training and test sets using stratifies sampling to preserve the churn distribution.



### Analytical workflow



1. Data cleaning

Prepared customer-level data, standardized column names, handles data types, preserved meaningful service categories, and encoded the churn target.



2\. Exploratory data analysis

Analyzed churn patterns across tenure, contract type, internet service, payment method, support services, customer characteristics, and selected interactions.



3\. Predictive modeling

Compared logistic regression, decision tree, and random forest classifiers.



4\. Model validation and tuning

Used stratified cross-validation and hyperparameter tuning to compare model performance.



5\. Threshold optimization

Evaluated alternative probability thresholds using out-of-fold prediction instead of relying on the default 0.50 threshold.



6\. Risk segmentation

Converted predicted churn probabilities to "Low", "Moderate", "High", and "Very high" risk segments.



7\. Retention strategy

Mapped risk segments and customer characteristics to differentiated retention actions



8\. Campaign economics 

Buid conservative, base and optimistic scenarios to estimate the potential economics of a targeted retention campaign.



9\. Power BI dashboard

Created a three-page dashboard covering executive churn trends, model performance and customer risk, and retention strategy and business impact.



### Key exploratory findings



Several customer characteristics showed strong differences in observed churn rates.



|**Segment**|**Approximate churn rate**|
|-|-|
|Overall customer base|26.5%|
|0-6 tenure|52.9%|
|Month-to-month contract|42.7%|
|Fiber optic internet|41.9%|
|Electronic check|45.3%|
|No tech support|41.6%|
|No online security|41.8%|
|Two-year contract|2.8%|





The analysis also identified several high-risk combinations, including newly acquired customers on month-to-month contracts and fiber customers without technical support.



### Model development



Three classification approaches were evaluated:



|**Model**|**CV ROC-AUC**|**General pattern**|
|-|-|-|
|Logistic regression|\~0.846|Strong discrimination and interpretability|
|Decision tree|\~0.827|More interpretable tree structure but weaker overall performance|
|Random forest|\~0.848|Similar ranking performance but more complex and less interpretable|



Logistic regression and random forest produced very similar ROC-AUC performance. The final model selected was tuned logistic regression because it provided strong predictive performance while maintaining substantially better interpretability for business stakeholders. Interpretability was particularly important because the project aims to support customer retention decisions, not only maximize predictive accuracy.



### Threshold selection



The default classification threshold of 0.50 was not automatically chosen. Instead, alternative thresholds were evaluated using out-of-fold training predictions. The selected operating threshold was: 35% predicted churn probability. At this threshold the model targets a larger population but captures substantially more actual churners. 



### Final model performance



The final tuned logistic regression model evaluated at the selected 35% threshold achieved:



|**Metric**|**Result**|
|-|-|
|ROC-AUC|0.841|
|Recall|71.1%|
|Precision|54.5%|
|F1 Score|0.617|
|Accuracy|76.6%|
|Target rate|34.6%|





The model identified **266** out of **374** actual churners in the evaluation sample. The selected threshold targets **488** of **1,409** customers or approximately **34.6%** of the evaluation population.



### Customer risk segmentation



Predicted probabilities were translated into four operational risk segments:





|**Risk segment**|**Probability range**|
|-|-|
|Low|<20%|
|Moderate|20-35%|
|High|35-60%|
|Very high|>=60%|





Observed churn increased strongly across these groups:



|**Risk segment**|**Observed churn rate**|**Average predicted risk**|
|-|-|-|
|Low|\~7.3%|\~6.3%|
|Moderate|\~27.5%|\~26.5%|
|High|\~41.6%|\~47.7%|
|Very high|\~71.8%|\~69.5%|





This increase in observed churn demonstrates that the segmentation successfully concentrates higher-risk customers into the upper risk groups.



### Very high-risk customer profile



Very high-risk customers displayed a particularly consistent profile:

* average tenure of approximately 8 months
* average monthly charges of approximately $82
* 100% on month-to-month contracts
* approximately 79% using electronic check
* approximately 97% without technical support
* approximately 98% without online security



### Retention strategy



Retention intensity is differentiated according to predicted customer risk:



|Risk segment|Recommended approach|
|-|-|
|Low|Standard engagement|
|Moderate|Preventative engagement|
|High|Targeted retention campaign|
|Very high|Priority outreach and personalized retention offer|



Potential interventions include:

* incentives to migrate from month-to-month to longer-term contracts
* promotion of automatic payment methods
* proactive onboarding for newer customers
* technical-support trials or service bundles
* online-security offers
* personalized retention outreach
* service-quality reviews for high-charge customers



These recommended interventions are hypotheses based on predictive associations. Their incremental effectiveness should be validated using controlled experiments or randomized A/B tests.



### Illustrative campaign economics



A simple scenario framework was created to estimate whether targeted retention could generate positive economic value.



|**Scenario**|**Campaign cost**|**Estimated customers retained**|**Preserved value**|**Net benefit**|**ROI**|
|-|-|-|-|-|-|
|Conservative|$14,640|26.6|$10,640|-$4,000|-27.3%|
|Base|$12,200|53.2|$26,600|$14,400|118.0%|
|Optimistic|$9,760|79.8|$47,880|$38,120|390.6%|



Under the base scenario, the campaign produces an estimated net benefit of approximately $14,400 and illustrative ROI of 118%. 

The conservative scenario produces a negative return, demonstrating the campaign economic are sensitive to retention effectiveness, intervention cost, and customer value.



### Power BI dashboard



A three-page interactive Power BI dashboard was developed to translate the analysis into a stakeholder-facing decision tool.



#### Executive overview





Provides a full-customer-base view of churn patterns across contract type, tenure, internet service and payment method.



#### Churn risk and model performance





Summarizes model performance, risk segmentation, observed versus predicted churn and priority customers.



#### Retention strategy and business impact





Connects churn risk to retention priorities, recommended customer actions, and illustrative campaign economics.



### Repository structure



customer-churn-retention-analysis/

|

|--- 1\_data/

&#x20;     |--- 1\_raw/

&#x20;           |---Telco\_Customer\_Churn.csv

&#x20;     |--- 2\_processed/

&#x20;           |--- dashboard\_customer\_data.csv

&#x20;           |--- dashboard\_overview.csv

&#x20;           |--- final\_churn\_predictions.csv

&#x20;           |--- retention\_roi-scenarios.csv

&#x20;           |--- telco\_churn\_clean.csv

|--- 2\_notebooks/

&#x20;     |--- 01\_data\_cleaning/

&#x20;           |--- data\_cleaning.ipynb

&#x20;     |--- 02\_exploratory\_analysis/

&#x20;           |--- exploratory\_analysis.ipynb

&#x20;     |--- 03\_churn\_modeling/

&#x20;           |--- best\_logistic\_model.pkl

&#x20;           |--- churn\_modeling.ipynb

&#x20;           |--- final\_threshold.joblib

&#x20;     |--- 04\_risk\_segmentation\_retention\_strategy/

&#x20;           |---risk\_segmentation\_retention\_strategy.ipynb

|--- 3\_dashboard/

&#x20;     |--- screenshots/

&#x20;           |--- executive\_overview.png

&#x20;           |--- churn\_risk\_model.png

&#x20;           |--- retention\_strategy.png

&#x20;     |--- telco\_churn\_prediction\_dashboard.pbix

|--- README.md

|--- requirements.txt

|--- .gitignore





### Tools and technologies



###### Python

* pandas
* NumPy
* Matplotlib
* Seaborn
* scikit-learn
* joblib



###### Analytics and modeling

* exploratory data analysis
* classification modeling
* stratified cross-validation
* hyperparameter tuning
* probability-threshold analysis
* customer segmentation
* scenario-based business-impact analysis



###### Visualization

* Power BI
* Matplotlib
* Seaborn



Development

* Jupyter Notebook
* Visual Studio Code
* Git
* Github



### How to run the project



Clone the repository:

git clone <https://github.com/mrsmv/Customer-churn-retention-analysis>

cd Customer-churn-retention-analysis



Create and activate a virtual environment, then install the required packages:

pip install -r requirement.txt



Run the notebooks in order:



01\_data\_cleaning.ipynb 

02\_exploratory\_data\_analysis.ipynb 

03\_churn\_modeling.ipynb 

04\_risk\_segmentation\_retention\_strategy.ipynb



The Power BI report can be opened using:

3\_dashboard/customer\_churn\_retention\_dashboard.pbix





### Limitations



This project has several important limitations. 

1. The Telco dataset is a historical analytical dataset and may not represent current behavior in a real telecommunications business.
2. The analysis identifies predictive associations but does not establish causal relationships between customer characteristic and churn.
3. Retention campaign economics are based on illustrative assumptions.
4. The final operating threshold reflects the current analytical objective and would need to be recalibrated using actual customer lifetime value, intervention costs, campaign capacity and retention-response data.

