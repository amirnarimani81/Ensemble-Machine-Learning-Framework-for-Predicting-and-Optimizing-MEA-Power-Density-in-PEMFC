<div style="border-radius: 5px;
           -webkit-border-radius: 5px;
           -moz-border-radius: 5px;
           font-family: cursive;
           border: 3px solid #008000;
           text-align: justify;
           color: black;
           font-size: 14px;
           padding: 5px;
           background:#F2FFFF">

  <p style="text-align: justify; font-family: cursive; font-size: 14px; color : green ; font-weight : bold">Objective</p>
  <p style="text-align: justify;">Development of high-performance MEAs for PEMFCs by identifying critical features, predicting power density, and optimizing design without trial-and-error.</p>

  <p style="text-align: justify; font-family: cursive; font-size: 14px; color : green ; font-weight : bold">Issues in the Dataset</p>
  <ul>
    <li><b>Missing Values:</b> Present across various columns, requiring imputation.</li>
    <li><b>High Dimensionality:</b> Over 100 features, some irrelevant/redundant.</li>
    <li><b>Mixed Data Types:</b> Numerical and categorical variables need preprocessing.</li>
    <li><b>Imbalanced Data:</b> Skewed target or feature distributions may bias models.</li>
    <li><b>Correlated Features:</b> Multicollinearity can affect linear models.</li>
    <li><b>Outliers:</b> Can skew predictions (e.g., high specific activity).</li>
    <li><b>Complex Relationships:</b> Non-linear physics demands advanced models.</li>
  </ul>

  <p style="text-align: justify; font-family: cursive; font-size: 14px; color : green ; font-weight : bold">Why Stacking & Voting Regressors?</p>
  <ul>
    <li><b>Stacking:</b> Trains diverse base models and a meta-model to learn from them for better generalization.</li>
    <li><b>Voting:</b> Aggregates base model predictions to reduce overfitting and variance.</li>
    <li>Suitable for capturing non-linear, high-dimensional relationships while boosting robustness.</li>
  </ul>

  <p style="text-align: justify; font-family: cursive; font-size: 14px; color : green ; font-weight : bold">ML Pipeline Solution</p>
  <ul>
    <li><b>Data Preprocessing:</b>
      <ul>
        <li>Impute missing values (mean/median for numeric, mode for categorical).</li>
        <li>Encode categorical variables (e.g., One-Hot or Target Encoding).</li>
        <li>Normalize numeric values (e.g., StandardScaler).</li>
      </ul>
    </li>
    <li><b>Feature Engineering:</b>
      <ul>
        <li>Drop irrelevant features (e.g., Title, Authors).</li>
        <li>Use PCA/Kernel PCA for dimensionality reduction.</li>
        <li>Log-transform skewed features (e.g., current density).</li>
      </ul>
    </li>
    <li><b>Outlier/Imbalance Handling:</b>
      <ul>
        <li>Use transformations or capping for outliers.</li>
        <li>Apply weighting or SMOTE for imbalanced targets.</li>
      </ul>
    </li>
    <li><b>Base Models:</b>  Random Forest, Gradient Boosting (XGBoost/LightGBM).</li>
    <li><b>Meta-Model (for stacking):</b> XGBoost for blending predictions.</li>
    <li><b>Voting Regressor:</b> Combine predictions via (weighted) averaging from top base models.</li>
  </ul>

  <p style="text-align: justify; font-family: cursive; font-size: 14px; color : green ; font-weight : bold">Model Pipeline Summary- Regression</p>
  <table style="width:100%; border-collapse: collapse; font-size: 13px;">
    <tr style="background-color: #d0f0c0;">
      <th style="border: 1px solid green;">Model</th>
      <th style="border: 1px solid green;">Hyperparameters</th>
      <th style="border: 1px solid green;">Goal</th>
    </tr>
    <tr>
      <td style="border: 1px solid green;">Decision Tree</td>
      <td style="border: 1px solid green;">max_depth, min_samples_split</td>
      <td style="border: 1px solid green;">Avoid overfitting</td>
    </tr>
    <tr>
      <td style="border: 1px solid green;">Random Forest</td>
      <td style="border: 1px solid green;">n_estimators, max_features</td>
      <td style="border: 1px solid green;">Balance bias-variance</td>
    </tr>
    <tr>
     <td style="border: 1px solid green;">Gradient Boost</td>
      <td style="border: 1px solid green;">n_estimators, max_features</td>
      <td style="border: 1px solid green;">Balance bias-variance</td>
    </tr>
    <tr>
      <td style="border: 1px solid green;">XGBoost</td>
      <td style="border: 1px solid green;">learning_rate, gamma, lambda</td>
      <td style="border: 1px solid green;">Handle imbalanced data</td>
    </tr>
    <tr>
      <td style="border: 1px solid green;">LightGBM</td>
      <td style="border: 1px solid green;">num_leaves, feature_fraction</td>
      <td style="border: 1px solid green;">Speed + accuracy</td>
    </tr>
    <tr>
      <td style="border: 1px solid green;">CatBoost</td>
      <td style="border: 1px solid green;">depth, l2_leaf_reg</td>
      <td style="border: 1px solid green;">Categorical feature robustness</td>
    </tr>
  </table>

  <p style="text-align: justify; font-family: cursive; font-size: 14px; color : green ; font-weight : bold">Hyperparameter Tuning</p>
  <ul>
    <li>GridSearchCV to the  Optimization with cross-validation ( 5-fold).</li>
  </ul>

  <p style="text-align: justify; font-family: cursive; font-size: 14px; color : green ; font-weight : bold">Expected Outcomes</p>
  <ul>
    <li><b>Performance Prediction:</b> Stacked/Voting models aim to outperform Linera Regression baseline (RMSE < 148.3 mW/cm²).</li>
    <li><b>Parameter Optimization:</b> Leverage PSO/GA to approach literature target (~1545.9 mW/cm²).</li>
  </ul>

  <p style="text-align: justify; font-family: cursive; font-size: 14px; color : green ; font-weight : bold">Why This Works</p>
  <ul>
    <li><b>PCA:</b> Reduces dimensionality while preserving key patterns.</li>
    <li><b>Ensemble Models:</b> Capture non-linear interactions and reduce overfitting.</li>
    <li><b>Pipeline Approach:</b> Ensures scalable, interpretable, and reproducible workflow.</li>
  </ul>

  <p style="text-align: justify; font-family: cursive; font-size: 14px; color : green ; font-weight : bold">Model Evaluation</p>
  <ul>
    <li><b>Regression:</b> RMSE, R² – Target RMSE &lt; 150 mW/cm².</li>
    <li><b>Interpretability:</b> Tree-based rules, feature analysis to highlight feature impact.</li>
  </ul>
 
</div>
