# Project Faunheal

A project to track animal health and its consequences

## What

The goal of this project is to create a **grid locator for animal illnesses**, coupled with a **predictive model** for the spread, containment, and propagation of these illnesses.

## How

The project requires the integration of several key datasets:
1. **Animal illnesses** - database of recorded cases and symptoms.
2. **Veterinary treatments** - database of animals treated by veterinarians.
3. **Drug stocks** - database of available and needed veterinary medicines.
4. **Bioenvironmental surveys** - data on wildlife, species, and habitat.
5. **Households with animals** - demographic and geographical data.

The aim is to:
- **Link** the veterinary treatment data to illness cases to track contagion, propagation chances, and treatment required.
- **Create two predictive models**:
    1. One to determine which illness an animal may have based on symptoms.
    2. A second to predict new illnesses entering specific zones.
- Additionally, a **model to track the natural movement of fauna over time** will be integrated.

## Why

- **Illness diagnosis**: A model to determine illness from symptoms can assist in faster diagnosis, decongesting veterinary clinics. The system could be linked to a website form for quicker diagnosis.
- **Illness prediction**: A model to predict illnesses in a given region can save time for both veterinarians and the general public.
- **Stock renewal optimization**: By predicting illnesses, the model can help in optimizing drug stock levels, ensuring that the right medicines are available in the required quantities and at the right time.
- **Cross-species contagion**: Linking animal illness data to human health symptoms can potentially predict cross-species disease transmission (e.g., diseases carried by mosquitoes or animals like dogs).
- **Impact on industries**: The project can identify the economic and health risks, e.g., a farm reporting avian flu after receiving contaminated hay. Early warnings allow other farms to prevent further spread.
- **Human impact**: Understanding the movement of fauna and the potential spread of zoonotic diseases (like monkeypox or chikungunya) can help mitigate human health risks.

## Data Sources

- [**WAHIS**](https://wahis.woah.org/) - World Organisation for Animal Health (WOAH)  
  Daily dataset of reported animal cases by veterinarians.
  
- [**EMPRES-i**](https://empres-i.apps.fao.org/) - Global Animal Disease Information System (FAO)  
  Continuously updated dataset of global animal disease cases.

- [**EMA**](https://www.ema.europa.eu/) - European Medicines Agency  
  Historical database of veterinary medicines for treating specific diseases.

- [**ANSES**](https://www.anses.fr/) - French Agency for Food, Environmental and Occupational Health & Safety  
  Regularly updated database of animal health situations in France.

- [**GBIF**](https://www.gbif.org/) - Global Biodiversity Information Facility  
  Regularly updated datasets on animal presence across different regions.

- [**INSEE**](https://www.insee.fr/) - National Institute of Statistics and Economic Studies (France)  
  Historical datasets on companion animal demographics.

- [**FACCO**](https://www.facco.fr/) - French Federation of Manufacturers of Dog, Cat, and Bird Food  
  Updated data on companion animals in France.

## Tech Stack

### Data Ingestion
- **Apache Airflow** for periodic data retrieval of cases (ETL).
- **Apache Airflow** for one-time data retrieval of illness records (ELT).

### Data Storage
- **Google Cloud Storage (GCS)** to store parquet data (cases).
- **Google Cloud Storage (GCS)** to store CSV data (definitions).

### Data Processing
- **Spark** to process parquet data (large datasets).
- **Pandas** for processing CSV data (smaller datasets).

### Visualization
- **Flask** for web interface to visualize the data and sort cases.
- **Streamlit** to present raw data and insights.

### Modelling
- **Scikit-Learn** for modeling the probability of an illness based on symptoms.
- **Scikit-Learn** for predicting the number of cases in a region at a given time.
- TBD (Model to predict disease spread to new geographical zones).

### Deployment
- **Apache Airflow** to deploy on Google Cloud Storage (GCS).

## Dataflow
```plaintext
[Data Sources]
 ↓ 
[ETL/ELT Pipeline] → Airflow
 ↓ 
[Data Lake] → GCS
 ↓ 
[Data Processing] → Spark/Pandas
 ↓ 
[ML Modeling] → SKLearn/???
 ↓ 
[Prediction APIs / User Interface] → Flask
 ↓ 
[Deployment] → Airflow/GCS
```

## POC (Proof of Concept)
For the POC, we will focus on avian influenza, a disease carried by both wild and domesticated birds. It has distinct symptoms, seasonal recurrence, migratory patterns, and impact on both health and the economy. It serves as an excellent case study for this project.

### Stages of the POC:
- **Data Collection:** Document past and present cases of avian influenza in Europe, specifically in birds. Data on human deaths and economic impact on farmers will be considered but will not be advanced in this phase.

- **Symptom Prediction:** Develop a model that can predict whether symptoms align with avian influenza and determine if the zone and/or period pose a risk.

- **Geographical Prediction:** Create a map showing the probable spread of avian influenza in Europe over time, based on factors like migratory patterns and seasonality.

- **Economic and Health Impact:** Analyze the influence of the disease spread on human health and economy, with and without countermeasures in place.

## Timeline
**First 2 weeks:** Implement the first and second stages of the POC (data collection and symptom prediction).
