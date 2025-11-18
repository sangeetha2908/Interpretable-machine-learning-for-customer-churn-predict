#  Local SHAP Force Plot Analysis: Deep Dive into Individual Predictions

This section presents a nuanced interpretation of SHAP force plots for three customers, revealing how specific feature interactions shape the model’s decision boundary. Each profile is grounded in actual model outputs and visualized using SHAP to highlight directional feature impacts.

---

##  Customer 1 — High-Risk Churn Profile  
- **Prediction**: Churn  
- **SHAP Value**: +1.37  
- **Base Value**: ~ -2.0  
- **Final Output**: f(x) = 1.37  

###  Positive Contributors (Push Toward Churn)
- `Contract_One year = 1.0`: Indicates lack of long-term commitment, increasing churn likelihood.  
- `PaperlessBilling_No = 1.0`: Suggests digital disengagement, often correlated with higher churn.  
- `InternetService_Fiber optic = 1.0`: While high-speed, this service is often bundled with fewer add-ons, paradoxically increasing churn risk.  
- `OnlineSecurity_No = 1.0`: Absence of security services is a strong churn driver.  
- `TotalCharges = 74.3` and `tenure = 1.0`: Low financial and temporal investment signal a new, uncommitted customer.

###  Negative Contributor (Push Against Churn)
- `OnlineBackup_No = 0.0`: Presence of backup service slightly offsets churn risk.

###  Interpretation
This customer exhibits a classic early-stage churn profile: minimal tenure, low spending, and absence of retention-oriented services. The SHAP force plot shows a strong cumulative push from red features, overwhelming the minor blue resistance.

---

##  Customer 2 — Amplified Churn Risk  
- **Prediction**: Churn  
- **SHAP Value**: +2.64  
- **Base Value**: ~ -2.0  
- **Final Output**: f(x) = 2.64  

###  Dominant Risk Factors
- `TechSupport_No`, `OnlineSecurity_No`, `OnlineBackup_No`: Triple absence of support services creates a vulnerability cluster.  
- `Contract_One year`, `Contract_Two year = 0.0`: No long-term contract commitment.  
- `InternetService_Fiber optic`: High-speed but often unbundled, reinforcing churn risk.  
- `MonthlyCharges ≈ 73.9`, `TotalCharges = 195.05`: Moderate financial engagement with minimal tenure (`tenure = 2.0`) suggests early dissatisfaction.  
- `SeniorCitizen_0`: Younger customers may exhibit lower inertia and switch more easily.

###  Interpretation
This profile intensifies the churn signal seen in Customer 1. The SHAP force plot reveals a dense concentration of red arrows, each representing a missing retention lever. The prediction is not only positive but sharply elevated, indicating high confidence in churn classification.

---

##  Customer 3 — Ambiguous Retention Case  
- **Prediction**: No Churn  
- **SHAP Value**: +0.70  
- **Base Value**: ~ -2.0  
- **Final Output**: f(x) = 0.70  

###  Risk Indicators
- `OnlineBackup_No = 1.0`, `OnlineSecurity_No = 1.0`: Absence of protective services.  
- `InternetService_Fiber optic = 1.0`: Again, a churn-prone service when not bundled.  
- `MonthlyCharges = 88.75`: High monthly cost may indicate dissatisfaction.  
- `SeniorCitizen_1 = 1.0`: Older customers may churn due to usability or cost concerns.

###  Protective Anchors
- `Tenure = 16.0`: Strong loyalty signal.  
- `TotalCharges = 1587.55`: High cumulative spending suggests long-term engagement.

###  Interpretation
This customer sits near the decision boundary. Despite several churn indicators, the model leans toward retention due to tenure and financial investment. The SHAP force plot shows a tug-of-war between red and blue forces, with blue features narrowly winning.

---

##  Feature Interaction Summary

| Feature               | Churn Risk ↑ | Retention Signal ↓ | Notes |
|----------------------|--------------|---------------------|-------|
| Tenure < 3 months    | ✅            | ❌                  | Strong churn predictor |
| No security/backup   | ✅            | ❌                  | Consistent across churn cases |
| Fiber optic internet | ✅            | ❌ (contextual)     | Risky when unbundled |
| Month-to-month       | ✅            | ❌                  | Lack of commitment |
| High charges         | ❌            | ✅                  | Indicates engagement |
| Long tenure          | ❌            | ✅                  | Loyalty buffer |

---



#  Task 4: Counter-Intuitive Feature Interactions via SHAP Dependence Plots

This section explores three unexpected feature interactions discovered using SHAP dependence plots. These findings challenge initial assumptions and offer deeper insights into churn behavior.

---

##  Interaction 1: Tenure × MonthlyCharges

###  Observation
- SHAP dependence plot shows that **customers with low tenure and high monthly charges** have sharply elevated SHAP values for churn.
- The churn risk **spikes disproportionately** when tenure is below 6 months and monthly charges exceed ₹80.

###  Initial Hypothesis
- High-paying customers are more engaged and less likely to churn, regardless of tenure.

###  Counter-Intuitive Insight
- New customers with high bills may feel overwhelmed or dissatisfied early, leading to rapid churn.
- High charges without bundled services or long-term contracts may signal poor value perception.

---

##  Interaction 2: InternetService_Fiber optic × OnlineSecurity_No

### Observation
- Fiber optic users **without online security** show significantly higher SHAP values for churn.
- The absence of security services **amplifies churn risk** more for fiber users than DSL users.

###  Initial Hypothesis
- Fiber optic customers are tech-savvy and less reliant on bundled security features.

###  Counter-Intuitive Insight
- Fiber optic users may expect premium service bundles. Missing security features create dissatisfaction.
- DSL users may be more tolerant of limited service offerings, reducing churn sensitivity.

---

##  Interaction 3: SeniorCitizen × Contract Type

###  Observation
- Senior citizens on **month-to-month contracts** have higher churn SHAP values than expected.
- Long-term contracts (1–2 years) **significantly reduce churn risk** for this group.

###  Initial Hypothesis
- Senior citizens are less likely to churn due to inertia or loyalty, regardless of contract type.

###  Counter-Intuitive Insight
- Flexibility may backfire: month-to-month contracts offer easy exit, increasing churn.
- Structured contracts provide stability and reduce decision fatigue, especially for older customers.

---

##  Summary Table

| Interaction                          | Initial Assumption                          | SHAP-Based Insight                            |
|--------------------------------------|---------------------------------------------|------------------------------------------------|
| Tenure × MonthlyCharges              | High spenders are loyal                     | New high spenders churn faster                |
| Fiber optic × No Security            | Tech-savvy users need fewer add-ons         | Missing bundles increase churn risk           |
| SeniorCitizen × Contract Type        | Older users are loyal regardless of terms   | Contract structure crucial for retention      |

---

>  *These findings highlight the value of SHAP dependence plots in surfacing nuanced, non-obvious relationships that traditional feature importance metrics may overlook.*


>  *SHAP force plots reveal not just feature importance, but directional influence — showing how each feature pushes the prediction toward or away from churn. This interpretability is critical for actionable retention strategies.*
