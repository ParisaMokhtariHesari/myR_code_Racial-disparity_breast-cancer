---
title: "Summary_DAG_No40"
author: "Parisa"
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

