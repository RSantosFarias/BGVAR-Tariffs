# BGVAR-Tariffs
A Bayesian Global Vector Autoregression (BGVAR) framework implementing SSVS priors to quantify the financial and real transmission of US trade policy uncertainty (TPU) and tariff shocks on Brazil. Features sign-restricted identification and dominant unit specification for global financial cycles.

**Status:** Active [Research Phase]  
**Stack:** R (BGVAR), Bayesian Econometrics, Time-Series Analysis  
**Focus:** US-Brazil Macro-Financial Linkages

# Overview
This repository contains the replication code and data architecture for analyzing the transmission of US protectionist shocks to the Brazilian economy. 

Unlike standard trade models that focus on substitution elasticities, this project utilizes a **Bayesian Global Vector Autoregression (BGVAR)** with **Stochastic Search Variable Selection (SSVS)** priors to isolate the **Financial Channel** (Global Financial Cycle) from the **Trade Channel**.

# Methodologies
**Model:** High-dimensional GVAR (N ~ 10) with a Dominant Unit (US).
**Priors:** SSVS (Stochastic Search Variable Selection).
**Identification:** Sign Restrictions and Zero Restrictions to disentangle "Trade Policy Uncertainty" (TPU) shocks from "Supply Chain" (GSCPI) shocks.
**Transmission:** Analysis of the Dilemma hypothesis (Rey, 2015) via Impulse Response Functions (IRFs).

# Data Sources
**Financial:** FRED (VIX, Term Spreads), BIS (Banking Statistics - Pending).
**Uncertainty:** Caldara & Iacoviello TPU Index.

## GDP
To minimize measurement error and maximize structural representativeness, I am employing a heterogenous activity proxy strategy for GDP:
1. **Developed Economies:** Those are represented by their Industrial Production. Following standard GVAR literature (Pesaran et al., 2004; Chudik & Pesaran, 2016), IP serves as the high-frequency proxy for the business cycle in advanced economies, where manufacturing variance accounts for the majority of cyclical GDP volatility.
2. **Developing Economies (LatAm):** Those are represented by Monthly Economic Activity Indices. Unlike DMs, restricting the proxy to manufacturing (IP) in these markets would generate omitted variable bias. The IMAEs (e.g., IBC-Br, IMACEC) capture the service and agricultural sectors, which are critical transmission channels for terms-of-trade shocks in commodity-exporting nations.

**United States Industrial Production:** FRED - Industrial Production: Total Index | https://fred.stlouisfed.org/series/INDPRO
**Euro Area, United Kingdom, Japan, China Industrial Production:** Netherlands Bureau of Economic Policy Analysis - CPB World Trade Monitor | https://www.cpb.nl/en/wtm/cpb-world-trade-monitor-july-2025
**Brazil GDP (Proxy):** Banco Central do Brasil - Central Bank Economic Activity Index (IBC-Br) | https://dadosabertos.bcb.gov.br/dataset/24364-indice-de-atividade-economica-do-banco-central-ibc-br---com-ajuste-sazonal
**Mexico GDP (Proxy):** INEGI - Global Economic Activity Indicator (IGAE) | https://www.inegi.org.mx/temas/igae/#tabulados
**Chile GDP (Proxy):** Banco Central del Chile - Monthly Economic Activity Index (IMACEC) | https://si3.bcentral.cl/Siete/en/Siete/Cuadro/CAP_CCNN/MN_CCNN76/CCNN2018_IMACEC_03_A/638131831615238879
**Colombia GDP (Proxy):** DANE - INDICADOR DE SEGUIMIENTO A LA ECONOMÍA (ISE) | https://www.dane.gov.co/index.php/estadisticas-por-tema/cuentas-nacionales/indicador-de-seguimiento-a-la-economia-ise
**Argentina GDP (Proxy):** INDEC - Estimador mensual de actividad económica (EMAE) | https://www.indec.gob.ar/indec/web/Nivel4-Tema-3-9-48

## CPI

**Brazil, Chile, China, Colombia, UK, Japan, Mexico, US:** International Monetary Fund | https://data.imf.org/en/datasets/IMF.STA:CPI
**Euro Area:** EuroStat - Harmonised Indices of Consumer Prices (EA20 HICP) | https://ec.europa.eu/eurostat/web/hicp/database
**Argentina:**
The Argentine series is constructed via a regime-dependent splicing methodology to address the underreporting period (2007-2015).

**Jan 2010 – Dec 2010:** Billion Prices Project (Cavallo) | https://dataverse.harvard.edu/dataset.xhtml?persistentId=doi:10.7910/DVN/UYX11A
**Jan 2011 – Jul 2012:** IPC Congreso | https://docs.google.com/spreadsheets/d/1gUQEOnvv9WI3zB3S2AQaIkylsCqV5dYhMER4B0MGSys/edit?gid=0#gid=0
**Aug 2012 – Apr 2016:** IPC CABA (Buenos Aires City) | https://www.estadisticaciudad.gob.ar/eyc/banco-datos/ipcba-evolucion-del-nivel-general-de-los-bienes-y-de-los-servicios-indices-y-variaciones-porcentuales-respecto-del-mes-anterior-ciudad-de-buenos-aires-julio-2012-diciembre-2014/
**May 2016 – Present:** International Monetary Fund | https://data.imf.org/en/datasets/IMF.STA:CPI

**Note:** Obligatory citation of Cavallo, A., 2013. Online and official price indexes: Measuring Argentina's inflation. Journal of Monetary Economics, 60(2), pp.152-165. Check '00_Argentina_Cavallo_Agg.R' and '00_Argentina_CPI.R' on the repo.
