# BGVAR-Tariffs
A Bayesian Global Vector Autoregression (BGVAR) framework implementing SSVS priors to quantify the financial and real transmission of US trade policy uncertainty (TPU) and tariff shocks on Brazil. Features sign-restricted identification and dominant unit specification for global financial cycles.

**Status:** Active [Research Phase]  
**Stack:** R (BGVAR), Bayesian Econometrics, Time-Series Analysis  
**Focus:** US-Brazil Macro-Financial Linkages

# Overview
This repository contains the replication code and data architecture for analyzing the transmission of US protectionist shocks to the Brazilian economy. 

Unlike standard trade models that focus on substitution elasticities, this project utilizes a **Bayesian Global Vector Autoregression (BGVAR)** with **Stochastic Search Variable Selection (SSVS)** priors to isolate the **Financial Channel** (Global Financial Cycle) from the **Trade Channel**.

# Methodologies
**Model:** High-dimensional GVAR (N ~ 20) with a Dominant Unit (US).
**Priors:** SSVS (Stochastic Search Variable Selection).
**Identification:** Sign Restrictions and Zero Restrictions to disentangle "Trade Policy Uncertainty" (TPU) shocks from "Supply Chain" (GSCPI) shocks.
**Transmission:** Analysis of the Dilemma hypothesis (Rey, 2015) via Impulse Response Functions (IRFs).

# Data Sources
**Real Economy:** CPB World Trade Monitor, IBGE (PIM-PF).
**Financial:** FRED (VIX, Term Spreads), BIS (Banking Statistics - Pending).
**Uncertainty:** Caldara & Iacoviello TPU Index.
