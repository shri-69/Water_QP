# Water_QP
## Water Quality Prediction 

This project aims to predict multiple water quality parameters using machine learning techniques, specifically MultiOutputRegressor wrapped around a RandomForestRegressor. It was developed as part of a one-month AICTE Virtual Internship sponsored by Shell in June 2025.

Overview
Access to clean water is a critical global concern. Accurate prediction of various water quality metrics can help in early detection of pollution and ensure timely intervention.

In this project, we:

Collected and preprocessed real-world water quality datasets
Used supervised machine learning for multi-target regression
Built a pipeline using MultiOutputRegressor with RandomForestRegressor
Evaluated the model using appropriate regression metrics
Technologies Used
Python 3.12
Pandas, NumPy – Data handling
Scikit-learn – Machine learning model and evaluation
Matplotlib, Seaborn – Data visualization
Jupyter Notebook – Interactive experimentation
Predicted Water Quality Parameters
The model predicts multiple water quality parameters such as:

NH4
BOD5 (BSK5)
Colloids
O2, NO3, NO2, SO4, PO4 and
CL
Model Performance
The model was evaluated using:

R² Score
Mean Squared Error (MSE)

## Motivation for Improvisations:
While the initial model provides a baseline, real-world environmental data often benefits significantly from deeper understanding and transformation. The improvisations were driven by the need to:

1.Enhance Predictive Accuracy: By providing the model with more informative features that capture complex relationships.
2.Incorporate Domain Knowledge: Leveraging insights from water chemistry and environmental science to create meaningful variables.
3.Improve Model Interpretability: Making the model's decisions more understandable by encoding explicit relationships.
4.Handle Data Nuances: Addressing temporal, spatial, and outlier characteristics inherent in environmental datasets.

Detailed Improvisations
The enhancements primarily fall under Feature Engineering and Exploratory Data Analysis (EDA).

1. Feature Engineering: Creating New Informative Variables
This involves transforming raw data into features that provide richer context and stronger predictive signals for the machine learning model.

  Interaction Terms between Pollutants:

      Manual Creation: New features like NH4_BOD5 (product of Ammonia and Biological Oxygen Demand) and NO3_SO4 (product of Nitrate and Sulfate) were created. These terms         capture synergistic effects where the combined presence or concentration of two pollutants might have a more significant impact than their individual levels.                For example, high NH4 coupled with high BOD5 can be a strong indicator of severe organic pollution.


      Automated Generation with PolynomialFeatures: For a selected subset of features (NH4, BSK5, SO4), PolynomialFeatures (with degree=2 and interaction_only=True) was           used. This systematically generates all pairwise interaction terms, helping to uncover hidden relationships that might not be immediately apparent. A crucial                preprocessing step involved using SimpleImputer to fill any missing values (with the mean) before generating these polynomial features, ensuring data completeness and       preventing errors.

Temporal Features (Seasonal Information):

      Month and Season Extraction: The month was extracted from the date column, and then categorized into seasons (summer, monsoon, winter, spring).

      One-Hot Encoding: These seasonal categories were converted into numerical binary features using one-hot encoding. This allows the model to effectively learn from the        strong seasonal variations in water quality, which are often influenced by factors like rainfall, temperature, and agricultural runoff.

      High-Risk Period Flag: The monsoon season was explicitly designated as a high_risk_period feature, directly encoding a known environmental factor that often                 correlates with changes in water quality.

Geographical Features (Location/Region Specifics):

      Location One-Hot Encoding: Synthetic location zones were created and then transformed into one-hot encoded features. This enables the model to account for spatial           differences in water quality, as pollution sources and environmental conditions can vary significantly across regions.

      Industrial Region Flag: An is_industrial flag was introduced, marking specific regions (e.g., ZoneA) as industrial. This is a highly valuable feature, as industrial         activities are a primary determinant of water quality, allowing the model to specifically learn the impact of such zones.

Domain-Specific Composite and Alert Features:

      NH4_monsoon Interaction: An interaction term combining NH4 levels with the monsoon season was created. This helps the model understand if ammonia levels behave              differently or have a more pronounced impact during the monsoon period.
      
      NH4_alert Flag: A binary feature NH4_alert was generated, set to 1 if NH4 levels exceeded the 95th percentile. This serves as an "anomaly" or "warning" indicator,           allowing the model to learn from unusually high pollutant concentrations.

      total_nitrogen Composite: A total_nitrogen feature was calculated by summing NH4, NO3, and NO2. This creates a comprehensive measure of nitrogenous compounds, which         is a key aggregate parameter in water quality assessment and directly reflects scientific understanding.
      
      NH4_risk Categorization: NH4 levels were categorized into NH4_risk ('High' or 'Normal') based on a predefined threshold. This provides a more interpretable,                 qualitative risk assessment that can be directly utilized by the model.

2. Exploratory Data Analysis (EDA) and Visualization: Gaining Insights
Beyond just creating features, visualizations and aggregations were used to understand their implications and validate feature engineering choices.

  Regional Pollutant Level Summaries: Average levels of key pollutants (NH4, O2, NO3) were calculated and printed for each synthetic region. This provides a quick overview    of how pollutant concentrations vary geographically.

  Visualizing Regional Differences: Bar plots were generated to visually compare average NH4 levels across different regions. These visualizations effectively highlight       patterns and confirm if certain regions consistently exhibit higher or lower pollutant concentrations, supporting the inclusion of geographical features.

  Visualizing Risk Distribution: A count plot was used to show the distribution of NH4_risk ('High' vs. 'Normal') specifically within the monsoon season. This helps in        understanding if the monsoon period indeed correlates with a higher occurrence of "High" NH4 risk, thereby reinforcing the validity of monsoon-related feature               engineering.

Impact and Benefits of Improvisations
These comprehensive improvisations significantly enhance the Water Quality Prediction project by:

Improving Predictive Performance: Providing the RandomForestRegressor with richer, more contextual features enables it to learn complex relationships more effectively, leading to more accurate predictions.

Increasing Model Interpretability: By explicitly encoding domain knowledge into features (e.g., is_industrial, total_nitrogen), the model's outputs become more explainable and actionable for environmental agencies.

Robustness to Data Characteristics: Addressing missing values and capturing temporal and spatial variations makes the model more robust and reliable across diverse real-world scenarios.

Actionable Insights: The engineered features and accompanying visualizations provide deeper insights into the factors influencing water quality, which can inform policy decisions and intervention strategies.

In summary, these improvisations demonstrate a strong, data-driven approach to solving a critical environmental problem, moving beyond basic model application to a more sophisticated and effective predictive system.
Performance was acceptable across all parameters

Internship Details
Internship Type: AICTE Virtual Internship - Edunet Foundation
Sponsor: Shell
Duration: June 2025 (1 month)
Focus Area: Machine Learning in Environmental Monitoring
