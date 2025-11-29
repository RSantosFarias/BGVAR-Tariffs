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

## Financial & Uncertainty
* **Financial:** FRED (VIX, Term Spreads), BIS (Banking Statistics - Pending).
* **Uncertainty:** Caldara & Iacoviello TPU Index.

## GDP Proxies

To minimize measurement error and maximize structural representativeness, I am employing a heterogenous activity proxy strategy for GDP:

1.  **Developed Economies:** These are represented by their **Industrial Production**. Following standard GVAR literature (Pesaran et al., 2004; Chudik & Pesaran, 2016), IP serves as the high-frequency proxy for the business cycle in advanced economies, where manufacturing variance accounts for the majority of cyclical GDP volatility.
2.  **Developing Economies (LatAm):** These are represented by **Monthly Economic Activity Indices**. Unlike Developed Markets (DMs), restricting the proxy to manufacturing (IP) in these markets would generate omitted variable bias. The IMAEs (e.g., IBC-Br, IMACEC) capture the service and agricultural sectors, which are critical transmission channels for terms-of-trade shocks in commodity-exporting nations.

| Country | Variable (Proxy) | Source/Series | Link |
| :--- | :--- | :--- | :--- |
| **United States** | Industrial Production | FRED - Total Index | https://fred.stlouisfed.org/series/INDPRO |
| **Euro Area, UK, Japan, China** | Industrial Production | CPB World Trade Monitor | https://www.cpb.nl/en/wtm/cpb-world-trade-monitor-july-2025 |
| **Brazil** | IBC-Br | Central Bank Economic Activity Index | https://dadosabertos.bcb.gov.br/dataset/24364-indice-de-atividade-economica-do-banco-central-ibc-br---com-ajuste-sazonal |
| **Mexico** | IGAE | Global Economic Activity Indicator | https://www.inegi.org.mx/temas/igae/#tabulados |
| **Chile** | IMACEC | Monthly Economic Activity Index | https://si3.bcentral.cl/Siete/en/Siete/Cuadro/CAP_CCNN/MN_CCNN76/CCNN2018_IMACEC_03_A/638131831615238879 |
| **Colombia** | ISE | Indicador de Seguimiento a la Economía | https://www.dane.gov.co/index.php/estadisticas-por-tema/cuentas-nacionales/indicador-de-seguimiento-a-la-economia-ise |
| **Argentina** | EMAE | Estimador mensual de actividad económica | https://www.indec.gob.ar/indec/web/Nivel4-Tema-3-9-48 |

## CPI (Index)

* **Brazil, Chile, China, Colombia, UK, Japan, Mexico, US:** International Monetary Fund | https://data.imf.org/en/datasets/IMF.STA:CPI
* **Euro Area:** EuroStat - Harmonised Indices of Consumer Prices (EA20 HICP) | https://ec.europa.eu/eurostat/web/hicp/database
* **Argentina (Spliced Series):**
    * The Argentine series is constructed via a regime-dependent splicing methodology to address the underreporting period (2007-2015).
    * **Jan 2010 – Dec 2010:** Billion Prices Project (Cavallo) | https://dataverse.harvard.edu/dataset.xhtml?persistentId=doi:10.7910/DVN/UYX11A
    * **Jan 2011 – Jun 2012:** IPC Congreso | https://docs.google.com/spreadsheets/d/1gUQEOnvv9WI3zB3S2AQaIkylsCqV5dYhMER4B0MGSys/edit?gid=0#gid=0
    * **Jul 2012 – Nov 2016:** IPC CABA (Buenos Aires City) | https://www.estadisticaciudad.gob.ar/eyc/banco-datos/ipcba-evolucion-del-nivel-general-de-los-bienes-y-de-los-servicios-indices-y-variaciones-porcentuales-respecto-del-mes-anterior-ciudad-de-buenos-aires-julio-2012-diciembre-2014/
    * **Dec 2016 – Present:** International Monetary Fund | https://data.imf.org/en/datasets/IMF.STA:CPI

> **Note:** Obligatory citation of Cavallo, A., 2013. Online and official price indexes: Measuring Argentina's inflation. Journal of Monetary Economics, 60(2), pp.152-165. Check '00_Argentina_Cavallo_Agg.R' and '00_Argentina_CPI.R' on the repo.

## Short-Term Interest Rates

* **United States:** FRED - Federal Funds Effective Rate | https://fred.stlouisfed.org/series/FEDFUNDS
* **Euro Area:** European Central Bank - Euribor 3-month | https://data.ecb.europa.eu/data/datasets/FM/FM.M.U2.EUR.RT.MM.EURIBOR3MD_.HSTA (Searching for an overnight alternative!)
* **United Kingdom:** Bank of England - Sterling Overnight Index Average (SONIA) | https://www.bankofengland.co.uk/boeapps/database/fromshowcolumns.asp?Travel=NIxSUx&FromSeries=1&ToSeries=50&DAT=ALL&FNY=&CSVF=TT&html.x=199&html.y=48&C=5JK&Filter=N
* **Japan:** FRED -  Immediate Rates (< 24 Hours) | https://fred.stlouisfed.org/series/IRSTCI01JPM156N
* **China:** China Foreign Exchange Trade - Shanghai Interbank Offered Rate (SHIBOR Overnight) | https://www.shibor.org/shibor/dataservicesen/
* **Brasil:** Banco Central do Brasil - CDI in annual terms | https://www3.bcb.gov.br/sgspub/consultarmetadados/consultarMetadadosSeries.do?method=consultarMetadadosSeriesInternet&hdOidSerieSelecionada=4389
* **Mexico:** FRED - Immediate Rates (< 24 Hours) | https://fred.stlouisfed.org/series/IRSTCI01MXM156N
* **Chile:** Banco Central - 1-day interbank interest rate | https://si3.bcentral.cl/Siete/en/Siete/Cuadro/CAP_TASA_INTERES/MN_TASA_INTERES_09/TSF_23/T51
* **Colombia:** Banco de la Republica - Indicador Bancario de Referencia (IBR) overnight | https://suameca.banrep.gov.co/estadisticas-economicas/informacionSerie/241/tasas_interes_indicador_bancario_referencia_ibr
 
