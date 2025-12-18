# COVID-19 Vaccine Allocation Optimisation (England)

This repository contains a linear programming model for designing a Phase-1 COVID-19 vaccine delivery strategy for the UK Vaccine Taskforce.

The goal is to maximise protection of high-risk population groups across 9 English regions under constraints on vaccine supply, regional capacity, and logistics.

---

## Problem Overview

In December 2020, the UK secured limited early doses of two vaccines (Pfizer/BioNTech and Oxford/AstraZeneca). For Phase-1, the government must decide:

- how many doses of each vaccine to allocate to each **region** and **age group**  
- while respecting:
  - limited national supply of each vaccine,
  - **regional boxing capacity** (cold-chain and transport constraints),
  - age-based **prioritisation scores**,
  - minimum coverage of frontline health and social care workers.

The objective is to maximise a **benefit score**, representing the mortality-reduction impact of vaccinating a given age group with a given vaccine.

---

## Model

We formulate this as a **linear programming (LP)** problem.

### **Decision variables**
- Number of Pfizer/BioNTech doses allocated per region × age group  
- Number of Oxford/AstraZeneca doses allocated per region × age group  

The variables are treated as continuous because we are dealing with very large population counts, making the linear relaxation a suitable approximation.

### **Objective**
Maximise total benefit score (criticality score × number of vaccinated individuals).

### **Key constraints**
- National dose limits for Pfizer/BioNTech and Oxford/AstraZeneca  
- Regional boxing capacity  
  - Pfizer/BioNTech requires **2** boxing units per dose  
  - Oxford/AstraZeneca requires **1** boxing unit per dose  
- Population availability per region & age group  
- Minimum vaccination of frontline health and social care workers  
- Feasible distribution across a limited number of daily delivery sites

The model is implemented in R using a standard LP solver.

---

## Repository Structure

```text
data/           # Population, capacity and parameter data (CSV)
code/           # RMarkdown optimisation model (vaccine_optimisation.Rmd)
results/        # Model outputs, summary tables, visualisations
presentation/   # Project proposal and pitch slides (PDF)
