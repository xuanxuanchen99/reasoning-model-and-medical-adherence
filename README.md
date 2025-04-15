# Personalized Medical Adherence Reasoning with ChatGPT

A hybrid AI system that personalizes outreach strategies by analyzing each patient's behavior and environment

working with AdhereHealth, a medical adherence company, supported by Professor Kempton Presley and Jake Woods

project supported by Professor Jesse Spencer-Smith and Dr. Abbie Petulante from Vanderbilt Data Science 

## Summary

This project explores how generative AI, specifically ChatGPT, can be applied to improve decision-making in the medical adherence industry. Industry-standard adherence classification relies heavily on a single cutoff (80% proportion of days covered, or PDC), often resulting in group-level outreach strategies that may overlook individual patient circumstances.

To challenge this, I built a hybrid framework which:

-generates a realistic synthetic dataset of 150 Medicare Advantage patients using ChatGPT-4o,

-applies ChatGPT o1 to individually analyze patients, considering both medical history and social determinants of health,

-compares industry-standard vs. individualized AI recommendations for improving patient adherence,

-compares the two approaches using contingency plots to visualize how their recommendations vary across patients

This pipeline demonstrates how reasoning-capable LLMs can support healthcare AI systems that are cost-aware, outcome-driven, and equity-conscious.

## Key Features

Synthetic data based on real-world Medicare adherence insights

Integrated 2018–2022 CDC SVI indicators (tract-level FIPS mapping)

Reasoning model generates explanations, adherence class, predictions, and outreach suggestions

Comparison of group-based and personalized recommendations via contingency visualization

Claude model serves as the judge to evaluate which recommendation style better suits each case

## What I Learned

Designing reasoning workflows for LLMs requires structured outputs, data validation, and domain grounding

Simple adherence thresholds overlook regional decline, vulnerability persistence, and outreach costs

Reasoning models such as ChatGPT o1 can suggest context-aware strategies which improve both adherence and program ROI

AI tools can complement human judgment in domains with sensitive information such as healthcare

## Technologies Used

Python

OpenAI API (ChatGPT-4o, ChatGPT o1)

Claude (Anthropic) as evaluator

CDC SVI data (2018, 2020, 2022) matched via HUD ZIP-TRACT crosswalk

GitHub and Jupyter Notebooks
