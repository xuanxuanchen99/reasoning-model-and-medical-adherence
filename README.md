# Personalized Medical Adherence Reasoning with ChatGPT

An AI system that personalizes outreach strategies by reasoning model and simulation grounded in real-world situations

working with AdhereHealth, a medical adherence company, supported by Professor Kempton Presley and Jake Woods

supported by Professor Jesse Spencer-Smith and Dr. Abbie Petulante from Vanderbilt Data Science 

## Summary

This project examines whether ChatGPT o1, a reasoning model, can improve decision-making in the medical adherence context, where the objective is to increase patient medication pickup and continuity.

### Can a generative AI model generate outreach recommendations that account for both individual behavior and social context compared to the industry-standard threshold-based rules?

The objective is to balance:

-Patient health outcomes — improving medication adherence,

-Cost to the outreach company,

-Social equity — by accounting for patient vulnerability,

## Problem & Context

Current industry standard practice:

If PDC (proportion of days covered) ≥ 80% -> the patient is considered adherent -> use low-cost methods: text to patient or fax to doctor
If PDC < 80% -> the patient is non-adherent -> use high-touch, high-cost method: call to patient

This rule may

-Ignores context such as patient vulnerability

-Fails to optimize cost-effectiveness across patients

-Does not offer an explanation for the outreach decision

This project asks whether LLMs can learn the decision logic and add explainability, or even improve on outreach targeting.

## Dataset & Simulation Grounding

The dataset is synthetic, but grounded in real-world logic. It is created and revised with feedback from a data scientist at AdhereHealth.

### It includes 150 Medicare Advantage patients with:
Demographics: sex, DOB, ZIP code

Disease states: diabetes, hypertension, cholesterol (1–3 per patient)

Pre- and post-PDC scores (2024)

Outreach channel: call (high-touch), text, fax to doctor (low-touch)

Adherence outreach attempt (0 = no attempt, 1 = attempted but failed, 2 = attempted and succeeded)

Days supply: 30 or 90 (35% of records are 90-day fills, assigned per disease rules)

Outreach date calculated as last pickup date + days supply

Low-Income Subsidy flag (LIS: Yes or No)

### Social Context Columns

ZIP → FIPS mapping using HUD ZIP-TRACT crosswalks

Merged CDC Social Vulnerability Index (SVI) data for 2018, 2020, 2022

Computed:

SVI_Change_2018_2022

SVI_Change_Category:

Improved (declining vulnerability)

Stable

Declined (rising vulnerability)

## Codes & Data Engineering

-Define categorization function

-Compute SVI changes

as shown in the code file

Other engineered features:

Outreach date: last_pickup_date + days_supply

Disease-specific duplication to assign multiple rows per patient

Patient disease ID as primary key

These steps enabled ChatGPT to reason about each patient's medical behavior and living environment.

## Methodology

I tested ChatGPT o1 using two setups:

### Attempt 1: In-context learning only — 140 patient examples with outreach channels

### Attempt 2: In-context learning plus chain-of-thought reasoning — model explains each decision

Procedure:
Held out 10 patients with different numbers of diseases (1, 2, or 3)

Removed these columns: adherence_outreach_attempt, outreach_channel, outreach_channel_detail, and post_pdc_2024

Prompted the model to recommend a outreach method based on patient data

Both attempts followed the same instructions, but Attempt 2 required chain of thought for each prediction.

## Evaluation

I compared each model’s predictions to the ground truth outreach method, which was generated using the industry-standard PDC logic.

Metric table 

A contingency plot was created to visualize

-Agreement between the two attempts

-Deviations from the PDC-based ground truth

Although both approaches recommended the same channels, Attempt 2 added explanation and interpretability for why each decision was made.

## Insights

ChatGPT o1 accurately learned industry outreach logic from the 140 examples.

Chain-of-thought prompting led to explanations based on refill timing, LIS status, and SVI context.

The model's ability to reason about outreach strategies is valuable for explainability in healthcare.

## Critical Analysis

### Strengths:

Use of LLMs with CDC social vulnerability data for outreach simulation

Pipeline can ingest real simulation data once available

Demonstrates how reasoning can coexist with cost and policy constraints

### Limitations:

Dataset is synthetic — no real adherence outcome labels

All patients follow 1 outreach — no multi-stage outreach simulation yet

### Future Work:

Expand dataset to thousands of patients

Compare performance against non-LLM baselines

### Ethics & Fairness

No real patient data used

ZIP → FIPS → SVI mapping used public sources

SVI and LIS were used to increase outreach support, not deny care

Outreach strategies reflect real-world policy shared by the data scientist, but not proprietary algorithms

## Resources and Links

-CDC Social Vulnerability Index (SVI)

https://www.atsdr.cdc.gov/placeandhealth/svi/index.html

Where I downloaded the CSVs for 2018, 2020, and 2022

-HUD ZIP Code to Census Tract Crosswalk

Used to match ZIP codes to FIPS for SVI merge

https://www.huduser.gov/portal/datasets/usps_crosswalk.html

## Thank You

Presented by Xuanxuan Chen




