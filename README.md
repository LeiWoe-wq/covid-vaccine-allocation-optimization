# COVID-19 Vaccine Allocation Optimisation (England)

This repository contains a linear programming model for designing a Phase-1 COVID-19 vaccine delivery strategy for the UK Vaccine Taskforce.

The goal is to maximise protection of high-risk population groups across nine English regions under strict constraints on vaccine supply, regional distribution capacity, and age-based prioritisation rules.

---

## Problem Overview

In December 2020, the UK secured limited early doses of two vaccines (Pfizer/BioNTech and Oxford/AstraZeneca). For Phase-1, the government must decide:

- how many doses of each vaccine to allocate to each **region** and **age group**,  
- while respecting:
  - national dose availability constraints,  
  - **regional cold-chain boxing capacity**,  
  - age-based **criticality scores** reflecting mortality-reduction impact,  
  - minimum coverage for frontline health and social care workers,  
  - practical limitations on the number of distribution sites.

The objective is to maximise a **benefit score**, representing the expected reduction in mortality risk based on vaccine type and age group.

---

## Model

We formulate this as a **linear programming (LP)** problem.

### **Decision variables**
- Number of Pfizer/BioNTech doses allocated per region × age group  
- Number of Oxford/AstraZeneca doses allocated per region × age group  

These variables are treated as continuous due to the large population counts involved, making the LP relaxation a good approximation to the underlying integer allocation task.

### **Objective**
Maximise the total benefit score across all region × age-group combinations.

### **Constraints**
- National supply caps for Pfizer/BioNTech and Oxford/AstraZeneca doses  
- Regional boxing capacity constraints  
  - Pfizer/BioNTech requires **2** boxing units per dose  
  - Oxford/AstraZeneca requires **1** boxing unit per dose  
- Population availability by region and age group  
- Required minimum vaccination of health and social care workers  
- Operational feasibility of daily delivery limits per region  

The model is implemented in R in `vaccine_optimisation.Rmd`.

---

## Repository Structure

```text
data/           
    population_by_region_agegroup.csv      # Population counts by region and age group
    regional_boxing_capacity.csv           # Regional packaging/boxing capacity
    criticality_scores.csv                 # Mortality-reduction benefit scores by vaccine & age group

code/
    vaccine_optimisation.Rmd               # LP model definition, constraints, and optimisation logic

results/
    optimal_phase1_allocation_ordered.csv  # Model output: ordered vaccine allocation by region & age group

presentation/
    Phase1_Proposal.pdf                    # Formal proposal prepared for the simulated UK Vaccine Taskforce
    Pitch_Slides.pdf                       # Presentation deck for client briefing
