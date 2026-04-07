# Model Card — [SafeScreen]

**Scenario:** [AI-Driven Content Access Gating System]
**Authors:** [Maisun Ansary]
**Date:** [4/1/2026]

---

## 1. Model Details

> What model or API is being used? Who built it? What version? What type of
> model — classification, prediction, generation, optimization? When was it
> developed?

Model/API: SafeScreen.

Builder/Version/Date: SaferSystems Inc.(v1.3), July 2024

Model Type: A hybrid system using a decision-tree model (for profile classification) and a text classifier (for real-time browsing analysis).

---

## 2. Intended Use

> What is the primary task? Who are the intended users? What decisions does
> the system inform? In what context is it deployed?

Primary Task: Dynamically gating and restricting website access based on inferred user risk profiles.

Users: IT departments, librarians, and school administrators in public libraries and K-12 schools.

Decisions: Assigning different levels of content restrictions, and triggering mid-session access changes as needed.

Context: Public library and K-12 computer networks in urban regions across four states (RI, DE, CT, NJ).

---

## 3. Out-of-Scope Uses

> What should this system NOT be used for? What populations, settings, or
> decisions are outside its design? What misuses are foreseeable?

_Not suitable for:_

Parents: The system should not be used to notify parents unless valid, written justification is provided.

Law Enforcement: The system should not be used to report users to the police or immigration authorities based on "risk profiles."

Medical/Legal Advice: The system should not be used to diagnose mental health issues or provide legal counsel, even if it "infers" a vulnerability.

Employee Monitoring: It should not be used to track the productivity or political leanings of library/school staff.


_Excluded Contexts by Design:_

Journalists & Researchers: Professionals requiring unfettered access to "political content" or "high-risk" materials for legitimate work are outside the model's design scope.

Critical Emergency Settings: The system is not designed for environments where a 24-48 hour override delay could result in physical or psychological harm (e.g., emergency shelters).


_Possible misuses:_ 

Ideological Censorship: IT administrators might use the "political content" filter to suppress specific viewpoints or marginalized perspectives under the guise of "safety."

Data Monetization: Using the intake survey or behavioral profiles to sell data to third-party advertisers or data brokers.

Circumvention/Adversarial Use: Students or users may intentionally "game" the survey or browsing behavior to trigger profile errors, potentially crashing the filter or gaining unauthorized access.

---

## 4. Training Data

> What data was used to build or train this model? How was it collected? What
> populations, geographies, languages, and time periods does it cover? What
> is missing?

Data Source: 180,000 browsing sessions from a 14-month pilot (two school districts, one library system).

Labels: Content accessed, flags triggered, override requests, and 15,000 manually labeled edge-case URLs.

Populations/Geography: Pilot users in the specific districts/library system.

Demographics: 71% White, 24% African American, 4% Hispanic/Latinx, 1% American Indian; all English speakers; East Coast cities.

---

## 5. Evaluation Data & Metrics

> How was performance measured? What metrics were used — accuracy, sensitivity,
> specificity, F1, AUC, RMSE? On what test set? Is it independent from the
> training data?

Performance was primarily evaluated using a multi-class F1-score to balance the precision and recall of risk classifications across imbalanced datasets (where "high-risk" sessions are rare compared to "normal" ones). The pilot data (180,000 sessions) was split using a 70/30 independent holdout method, ensuring the model was tested on 54,000 sessions it had never seen during training. Key metrics included a False Positive Rate (FPR) target of <2% to minimize the "censorship" of legitimate educational resources.

---

## 6. Quantitative Analysis

> Performance broken down by relevant subgroups — age, sex, race/ethnicity,
> geography, income, language. Does the model perform differently across
> these groups? Where are the gaps?

Subgroup Breakdown: The model uses age and literacy as factors.

Analysis of the pilot data revealed a "Literacy Bias" where users with lower literacy scores or non-native English browsing patterns experienced a 15% higher rate of mid-session escalation. Performance was consistent across geographic locations (the four pilot states), but age-based gaps were identified - over-filtering teens: the model was significantly more restrictive for the "13-17" age bracket than the "18+" bracket when searching for identical health-related terms (e.g., "reproductive health").

---

## 7. Ethical Considerations

> Bias risks, informed consent, privacy, potential harms, equity implications.
> Does this system reproduce or amplify existing disparities? Who bears the
> consequences when it fails?

Bias Risks & Equity: The use of "literacy level" and "vulnerability indicators" as classification features poses a significant risk of socioeconomic and racial profiling. Users from under-resourced educational backgrounds or non-native English speakers may be funnelled into more restrictive tiers, limiting their access to information compared to peers.

Informed Consent & Privacy: While users complete a survey, the "real-time behavior classifier" constitutes persistent surveillance. In a public library setting—often the only source of internet for low-income individuals—consent is arguably coercive, as users must submit to profiling to exercise their right to information.

Potential Harms: The "mid-session escalation" and filtering of "political content" create a chilling effect on free inquiry. False positives in categories like "substance use" or "self-harm" can block domestic violence survivors or individuals in crisis from reaching life-saving resources.

Consequences of Failure: When the model fails (false blocks), the marginalized user bears the total cost. Because the override process takes 24–48 hours, users with time-sensitive needs (job applications, legal deadlines, health crises) are effectively denied service without immediate recourse.

---

## 8. Limitations & Caveats

> Known failure modes, edge cases, what the model does not capture. Conditions
> where it performs poorly. Assumptions baked into the design that may not
> hold in all deployment contexts.

Contextual Blindness: Legitimate research into LGBTQ+ support, domestic violence resources, or harm reduction can be misclassified as "high-risk" due to keyword overlap with restricted categories.

Geographic & Cultural Homogenization: 

- Because the model was trained on data from only four states, it assumes that the definitions of "political content" and "appropriate material" are universal. It may perform poorly in communities with different cultural standards or legal definitions of protected speech.

- The system was deployed in urban areas with relatively higher education rates, and may not be suitable for use in lower-income and/or rural areas of the country.


No reporting of specific systems: The school districts and public library used for training are unspecified to protect their privacy.

Geographic Bias: Since it was trained in only four states, it may fail to understand regional slang or local political content in the other 46.

---

## 9. Human Oversight

> Who reviews outputs before action is taken? Human in the loop, on the loop,
> or out of the loop? What is the escalation path when the model is wrong?
> Can it act autonomously — and should it?

Oversight Type: Human-in-the-loop. The system operates autonomously to categorize users and block content in real-time, but human administrators (librarians and IT staff) monitor the system via aggregate logs and individual override requests.

Review Process: There is no "pre-action" human review; the AI makes the immediate decision to grant or revoke access. Post-action review occurs only when a user initiates a formal written justification for an override.

Escalation Path: Requests are routed to institutional IT departments or school administrators. The current path involves a 24–48 hour latency period, meaning the system does not support real-time human intervention for false positives.

Autonomy Limits: The model currently lacks an automated threshold that would trigger a human review before a block occurs. It is fully autonomous in its enforcement of tiered restrictions and mid-session escalations.

---

## 10. Temporal Validity

> When does this model need retraining or re-evaluation? What triggers a
> review — new data, policy change, population shift, outbreak? How does
> performance degrade over time?

This model requires a full re-evaluation every 6 months or upon any major state policy change regarding library content. A retraining trigger is also set for any 10% drift in the "Override Request Rate," as a spike in overrides indicates the model’s classification of "risk" is no longer aligned with human judgment or current language trends (e.g., new social media platforms or slang).
