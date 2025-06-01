# Ethnoracial Disparities in Breast Cancer Treatment Time and Survival: A Systematic Review With a DAG-based Causal Model

This repository contains the R code used for the paper [here] (https://scholar.google.ca/scholar?hl=en&as_sdt=0%2C5&q=Causal+Mediation+Analysis+of+Time-to-Event+Data+in+the+Context+of+Causal+Mediation+Analysis+of+Time-to-Event+Data+in+the+Context+of+Intersectionality+in+Breast+Cancer+Intersectionality+in+Breast+Cancer+&btnG=) [Mokhtari Hesari, P. (2025). Causal Mediation Analysis of Time-to-Event Data in the Context of Intersectionality in Breast Cancer. ]:  
"Ethnoracial Disparities in Breast Cancer Treatment Time and Survival: A Systematic Review With a DAG-based Causal Model."

## Abstract 
For interventions aimed at redressing health disparities in breast cancer to be effective, a clear understanding of the nature and causes of these disparities is required. Our question is: what is the current evidence for ethnoracial disparities in time-to-treatment initiation and survival in breast cancer, and how are the causal mechanisms of these disparities conceptualized in the literature? A comprehensive systematic search of studies on cohorts of female breast cancer patients diagnosed with stage I-III was performed. Directed acyclic graphs were used to describe implicit causal relationships between racial/ethnic group membership and time-to-treatment initiation and survival outcomes. This review revealed strong evidence for ethnoracial disparities in both time to treatment and survival among breast cancer patients. Unmeasured factors identified by the authors highlighted gaps in data sources and opportunities for causal reasoning. While the existing literature describes ethnoracial disparities, there is very limited discussion of causal mechanisms, and no discussion of system-level rather than individual-level effects. Addressing established ethnoracial disparities in breast cancer requires new research that explicitly considers the causal mechanisms of potential interventions, incorporating unmeasured factors contributing to these disparities.

## Contents
- `data_preparation.R`: Code for loading and cleaning data
- `dag_construction.R`: Code for building and visualizing DAGs (using `dagitty`bfor each study included in the systematic review and the final summary DAG)
- `mediation_analysis.R`: Code for causal mediation analysis
- `sensitivity_analysis.R`: Code for assessing robustness of findings
- `utils/`: Helper functions

## Dependencies
The analysis was performed in R using the following packages:
- `dagitty`
- `tidyverse`
- `survival`
- `mediation`  
(see `requirements.txt` or install manually)

## Usage
Clone the repo and run each script in order. You can also open the project in RStudio and use the R scripts interactively.

## Notes
- DAGs were created based on literature and expert knowledge.
- The analysis focuses on observational data; assumptions are discussed in the manuscript.



---
title: "Summary_DAG_No40"
author: "Parisa Hesari"
date: "2024-09-19"
output: word_document
---


```{r}
#Load required Packages
library(dagitty)
library(ggdag)
library(ggplot2)

```

```{r}

#summary of of all included studies: A composit DAG
set.seed(12143)
#summary of of all included studies: A composit DAG
dagRace <- dagify(O1 ~ RE + HRF + GS + A + C+ O2,
                  O2 ~ RE + MD + DOT + Y + AI + PS + TPH + TD + SO + MS + SCH + IS + TCH + FCH + S + SBA + HD + ST + SFT + ES + PC + R + CP + CS + FI,
                  PC ~ RE,
                  R ~ RE,
                  CP ~ RE,
                  CS ~ RE,
                  FI ~ RE,
                  HD ~ RE,
                  ST ~ RE,
                  SFT ~ RE,
                  ES ~ RE,
                  IS ~ RE,
                  TCH ~ RE,
                  FCH ~ RE,
                  S ~ RE,
                  SBA ~ RE,
                  TT ~ RE,
                  exposure = "RE",
                  outcome = c("O1", "O2"),
                  labels = c(O1 = "Survival", O2 = "Time To Treatment",
                             RE = "Racial/ethnic groups",
                             HRF = "Health Risk Factors",
                             GS = "Gender/Sex",
                             MD = "Method of Diagnosis",
                             DOT = "Delay in other Treatments",
                             Y = "Year of Diagnosis",
                             AI = "Access to Information",
                             PS = "Performance Status",
                             TPH = "Trust in Physician",
                             TD = "Treatment Duration",
                             SO = "Surgical Outcomes",
                             MS = "Marital Status",
                             SCH = "Surgeon Characteristics",
                             IS = "Insurance Status",
                             TCH = "Tumor Characteristics",
                             FCH = "Facility Characteristics",
                             SBA = "Structural Barrier/Access",
                             HD = "HealthCare Discrimination",
                             ST = "Surgery Type",
                             SFT = "Surgery as first Treatment",
                             ES = "English Speaking",
                             PC = "Pretreatment Care",
                             R = "Recurrence",
                             CP = "Clinical Presentation",
                             CS = "Cancer Stage",
                             FI = "Financial Issues",
                             A = "Age",
                             C = "Comorbidities",
                             S = "SES",
                             TT = "Therapy Type"))

dag_plot <- ggdag_status(dagRace,var=c("O1","O2"),text_size = 2, text_col = "black",node_size=6, use_labels = "label") +
  theme_void()


print(dag_plot)



```

