# KDK – Data Specification for the German Model Project Genome Sequencing

This repository contains the **data specification** for the **German Model Project Genome Sequencing (Modellvorhaben Genomsequenzierung)**, coordinated by the **Federal Institute for Drugs and Medical Devices (BfArM)**.

The schema defines the structure and validation rules for data submitted in the context of the project. It uses the [JSON Schema Draft 2020-12](https://json-schema.org/draft/2020-12/schema) standard to ensure syntactic and semantic validation of the **clinical data**.

Further information and documentation can be found on the [website](https://www.bfarm.de/DE/Das-BfArM/Aufgaben/Modellvorhaben-Genomsequenzierung/Informationen-und-downloads/_node.html) of the **Federal Institute** in the downloads section under **'Datensatzspezifikationen'**.


## Repository Structure

### `/KDK`

This folder contains the core JSON Schemas for the **data types** used in the model project. These schemas are grouped by indication area and submission component:

#### Common
- `Submission.json`: Submission metadata including technical info and consent status

#### Oncology Schemas
- `Oncology.json`: Entry point schema for oncology submissions
- `OncologyCase.json`: Clinical case data
- `OncologyPlan.json`: Tumor board recommendations
- `OncologyMolecular.json`: Molecular findings (e.g., variants, fusions)
- `OncologyFollowUp.json`: Follow-up data

#### Rare Diseases Schemas
- `RareDiseases.json`: Entry point schema for rare diseases submissions
- `RareDiseasesCase.json`: Clinical case data
- `RareDiseasesPlan.json`: Tumor board recommendations
- `RareDiseasesMolecular.json`: Molecular findings
- `RareDiseasesFollowUp.json`: Follow-up data


#### Changelog
- `CHANGELOG.md`: Tracks changes and version history of the data specification


### `/Prüfbericht`

This folder contains the schema and example data for **Prüfberichte** (data review reports).

- `Modellvorhaben_SubmissionSchema`: Schema definition for a review report
- `submission_example`: Example file conforming to the schema
