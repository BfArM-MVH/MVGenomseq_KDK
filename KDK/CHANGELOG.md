# Changelog
## [1.6.6] - 2025-07-14
### Added
- Added `test` to `submissionType` in `Submission` and `Modellvorhaben_SubmissionSchema`.
# Changelog
## [1.6.5] - 2025-07-07
### Changed
- **OncologyCase**
  - Changed `priorDiagnostics` to array
- **RareDiseasesCase** 
  - Changed `PriorRds` to array
- **RareDiseasesPlan**
  - Renamed `variantReferences` to `variants` according to the documentation
### Fixed
- **RareDiseases**
  - Fixed bad links
- **Submission**
  - Fixed syntax error
- **Substance**
  - Fixed bad links
### Removed
- **OncologyMolecular**
  - Removed `transcriptId` from `SmallVariant` required properties
# Changelog
## [1.6.4] - 2025-06-06
### Added
- **Oncology**
  - Added `case` to required properties.
- **OncologyCase**
  - Added `libraryType` to `diagnosisOd`.
- **OncologyFollowUp**
  - Added `reference` to `Therapy` required properties.
  - Added `phenotypes` to `FollowUpOd`.
- **OncologyMolecular**
  - Added `chromosome`, `startPosition`, `endPosition`, `ref` and `alt` to `SmallVariant` properties and added it to its required properties.
- **OncologyPlan**
  - Added `Z(FDA)` to `RecommendedSystemicTherapy.evidenceLevelDetails` enum.
  - Added `CarePlanOd` to required properties.
  - Added `evidenceLevel`,`evidenceLevelDetails` and `priority` to `RecommendedStudy` and added `evidenceLevel` and `priority` to its required properties.
  - Added `CI`,`CZ`,`CIZ` and `IZ` to enum of `RecommendedSystemicTherapy.therapeuticStrategy`.
- **RareDiseases**
  - Added `case` to required properties.
- **RareDiseasesCase** 
  - Added `diagnosticAssessment` to `DiagnosisRd` required properties.
  - Added `libraryType` to `diagnosisRd`.
  - Added `version` to `DiagnosisRd.phenotypes` required properties.
  - Added `genomicStudyType` and `diagnosticResult` to `PriorRd` required properties.
- **RareDiseasesFollowUp**
  - Added `phenotypes` to `followUpRds` required properties.
- **RareDiseasesPlan**
  - Added `strategyCombination` to `RecommendedTherapy`.
  - Added `yesButStudyIsUnknown` to enum of `RecommendedStudy.register`.
- **Submission**
  - Added `localCaseId`.
### Changed
- **OncologyCase**
  - Changed the `type` of `additionalClassification` from `object` to `array`. An example of a valid `additionalClassification` array:
    - ```json
      {
        "additionalClassification": [
           {
            "system": "TNM",
            "key": "T2N1M0"
           }
        ]
      }
      ```
  - Changed logic of `prioProcedures.substances`, so that `name` is only required when ATC code in `code.code` does not describe the acitve substance (ATC level 5). An example of a valid `substances` object:
    - ```json
      {
        "substances": [
          {
            "code": {
              "system": "ATC-Code",
              "code": "A01AB02",
              "version": "04/2025"
            }
          },
          {
            "code": {
              "system": "ATC-Code",
              "code": "A01",
              "version": "04/2025"
            },
            "name": "Stomatologika"
          }
        ]
      }
      ```
- **OncologyFollowUp**
  - Change description of `therapy.refernce` to `Identifier of the recommended systemic therapies or, if not available, new identifier for future reference.`.
  - Changed logic of `therapies.substances`, so that `name` is only required when ATC code in `code.code` does not describe the acitve substance (ATC level 5). An example of a valid `substances` object:
    - ```json
      {
        "substances": [
          {
            "code": {
              "system": "ATC-Code",
              "code": "A01AB02",
              "version": "04/2025"
            }
          },
          {
            "code": {
              "system": "ATC-Code",
              "code": "A01",
              "version": "04/2025"
            },
            "name": "Stomatologika"
          }
        ]
      }
      ```
- **OncologyMolecular**
  - Changed the `type` of `transcriptId` from `string` to `object`. An example of a valid `transcriptId` object:
    - ```json
      {
        "transcriptId": [
          {
            "code": "ENST00000644379",
            "system": "Ensembl"
          }
        ]
      }
      ```
  - Changed `sbsSignatures` to array with an `sbsSignature` object containing `identifier`, `version` and an array `name`. An example of a valid `sbsSignature` object:
    - ```json
      {
        "SbsSignature": [
          {
            "identifier": "sig-001",
            "version": "v3.2",
            "name": ["SBS6", "SBS15"]
          }
        ]
      }
      ```
- **OncologyPlan**
  - Moved `recommendedStudies` from properties of `RecommendedSystemicTherapy` to properties of `OncologyPlan`.
  - Changed logic of `recommendedStudies.substances` and `recommendedSystemicTherapies.substances`, so that `name` is only required when ATC code in `code.code` does not describe the acitve substance (ATC level 5). An example of a valid `substances` object:
    - ```json
      {
        "substances": [
          {
            "code": {
              "system": "ATC-Code",
              "code": "A01AB02",
              "version": "04/2025"
            }
          },
          {
            "code": {
              "system": "ATC-Code",
              "code": "A01",
              "version": "04/2025"
            },
            "name": "Stomatologika"
          }
        ]
      }
      ```
- **RareDiseasesMolecular**
  - Changed required properties `position` of `SmallVariant` to `startPosition` and `endPosition`.
  - Changed `items` of `genes` from `string` to `object`. An example of a valid `genes` array:
    - ```json
      {
        "genes": [
          {
            "code": "HGNC:1100"
          },
          {
            "code": "HGNC:5173"
          }
        ]
      }
      ```
  - Moved `localization` property from inside each `genes` item to the `Variant` object.
  - Changed `intronicIntergenic` in enum of `Variant.localization` to `intronic` and `intergenic`.
- **RareDiseasesPlan**
  - Change `RecommendedStudy.variants` to only include `identifier`.
- **Submission**
  - Renamed `inclusionBoardDecisionDate` to `molecularBoardDecisionDate`.
  - Add `Not required in cases where diagnosisOd.libraryType = "none".` to `description` of `diagnosisOd.genomicCentreId` and removed it from required properties.
### Fixed
- **OncologyCase** 
  - Renamed enum value of `diagnosticAssessment` from `furtherGeneticDiagnosisRecommended` to `furtherGeneticDiagnosticRecommended`.
- **RareDiseasesCase**
  - Renamed enum value of `diagnosticAssessment` from `furtherGeneticDiagnosisRecommended` to `furtherGeneticDiagnosticRecommended`.
- **RareDiseasesPlan** 
  - Renamed enum value of `register` from `EudraCT` to `Eudra-CT/CTIS`.
- **Submission**
  - Fixed `GDCXXXnnn` to `GRZXXXnnn` in description of `submission.genomicDataCenterId`.
### Removed
- **OncologyCase**
  - Removed `transcript` from `PriorVariants` required properties.
- **OncologyFollowUp**
  - Removed `therapyResponseDate` from `Therapy` required properties.
- **OncologyMolecular**
  - Removed version from description of `transcriptId`.
- **OncologyPlan**
  - Removed `evidenceLevel`, `evidenceLevelDetails` and `priority` from `CarePlanOd.RecommendedSystemicTherapy` and its required properties.
- **RareDiseasesCase** 
  - Removed `diagnosticAssessment` from `PriorRd` required properties.
  - Removed `hpoVersion` from `DiagnosisRd` and its required properties.
- **RareDiseasesMolecular**
  - Removed `variants` array from top level; `Variant` now is an abstract base definition that serves purely as a base class for every other variant type. 
- **RareDiseasesPlan** 
  - Removed `description` from `CarePlanRd.clinicalManagementDescriptions`.
## [1.6.3] - 2025-03-24
### Changed
- **OncologyMolecular:**
  - Updated `StructuralVariant` description by removing the sentence: '_(except in-frame fusions of two coding genes)_'
- **OncologyCase:**
  - Changed the required properties in `hpoTerms` to be only `code`. An example of a valid `hpoTerms` array: 
    - ```json
      {
        "hpoTerms": [
           {
            "code": "HP:0001250",
            "text": "Patient experiences frequent nocturnal seizures.",
            "system": "http://purl.obolibrary.org/obo/hp.owl",
            "display": "Seizure"
          },
          {
            "code": "HP:0001249"
          }
        ]
      }
      ```
- **RareDiseasesFollowUp:**
  - Changed the required properties in `phenotypes` to be only `code`. An example of a valid `phenotypes` array:
    - ```json
        {
          "phenotypes": [
            {
                "code": "HP:0001250",
                "text": "Patient experiences frequent nocturnal seizures.",
                "system": "http://purl.obolibrary.org/obo/hp.owl",
                "display": "Seizure",
                "change": "newlyAdded"
            },
            {
                "code": "HP:0001249"
            }
          ]
        }
        ```
- **RareDiseasesCase:**
  - Changed the required properties in `phenotypes` to be only `code`. An example of a valid `phenotypes` array:
    - ```json
        {
          "phenotypes": [
            {
                "code": "HP:0001250",
                "text": "Patient experiences frequent nocturnal seizures.",
                "system": "http://purl.obolibrary.org/obo/hp.owl",
                "display": "Seizure"
            },
            {
                "code": "HP:0001249"
            }
          ]
        }
        ```
## [1.6.2] - 2025-03-24
### Changed
- **OncologyPlan, OncologyFollowUp, and OncologyCase:**
  - Updated the logic of `substances` array to accept either `code` or `name`, but not both.
    - Valid `substance` object: 
      - ```json
        {
          "code": {
            "system": "http://example.com/system",
            "code": "ABC123",
            "version": "1.0"
          }
        }
        ```
      - ```json
        {
          "name": "Example"
        }
        ```
    - Invalid `substance` object: 
      - ```json
        {
          "code": {
            "system": "http://example.com/system",
            "code": "ABC123",
            "version": "1.0"
          },
          "name": "Example"
        }
        ```
      - ```json
        {
          "code": {
            "system": "http://example.com/system",
            "code": "ABC123"
          }
        }
        ```
- **OncologyCase:**
  - Updated `PriorDiagnostic.type` enums to include `none`.
  - Changed cardinality of `PriorDiagnostic.date` from 1 to 0.
  - Updated the `hpoTerms` to require `code` and `text` only. Example of valid `hpoTerms` array: 
    - ```json
      {
        "hpoTerms": [
          {
            "code": "HP:0001250",
            "text": "Patient experiences frequent nocturnal seizures.",
            "system": "http://purl.obolibrary.org/obo/hp.owl",
            "display": "Seizure"
          },
          {
            "code": "HP:0001249",
            "text": "Evidence of intellectual disability observed during assessment."
          }
        ]
      }
      ```

- **RareDiseasesCase:**
  - Updated `PriorRd.genomicTestType` enums to include `none`.
  - Changed cardinality of `PriorRd.diagnosticDate` from 1 to 0.
  - Updated the required array of `phenotypes` to have both `code` and `text`.
  - Updated the required array of `PriorRd` to include `diagnosticResult` and exclude `diagnosticAssessment`.
  - Renamed `PriorRd.genomicStudyType` enums to become 
    - `single`
    - `duo`
    - `trio`
  - Updated the `phenotypes` to require `code` and `text` only. Example of valid `phenotypes` array:
    - ```json
      {
        "phenotypes": [
          {
              "code": "HP:0001250",
              "text": "Patient experiences frequent nocturnal seizures.",
              "system": "http://purl.obolibrary.org/obo/hp.owl",
              "display": "Seizure"
          },
          {
              "code": "HP:0001249",
              "text": "Evidence of intellectual disability observed during assessment."
          }
        ]
      }
      ```
- **RareDiseasesFollowUp:**
  - Updated the `phenotypes` to require `code` and `text` only. Example of valid `phenotypes` array:
    - ```json
      {
        "phenotypes": [
          {
              "code": "HP:0001250",
              "text": "Patient experiences frequent nocturnal seizures.",
              "system": "http://purl.obolibrary.org/obo/hp.owl",
              "display": "Seizure",
              "change": "newlyAdded"
          },
          {
              "code": "HP:0001249",
              "text": "Evidence of intellectual disability observed during assessment."
          }
        ]
      }
      ```
- **OncologyPlan:**
  - Changed the type of `otherRecommendation` from _string_ to _array_.
  - Renamed `otherRecommendation` to `otherRecommendations`.
  - Relocated the `otherRecommendations` array to be directly inside the `CarePlanOd`. 
  - Changed the type of `priorities` from _array_ to _integer_.
  - Renamed `priorities` to `priority`.
  - Renamed `variantReferences` to `variants`.
  - Renamed `systemicTherapies` to `therapeuticStrategy`. 
  - Changed the type of `therapeuticStrategy` from _array_ to _string_.
  - Updated required array of `RecommendedSystemicTherapy` to include `therapeuticStrategy`.
- **RareDiseasesPlan:**
  - Changed the type of `registers` from _array_ to _string_.
  - Renamed `registers` to `register`.
  - Renamed the enum value `Eudra-CT/CTIS` in `register` to `EudraCT`. 
  - Changed the type of `names` from _array_ to _string_, and renamed it to `name`.
  - Changed the type of `ids` from _array_ to _string_, and renamed it to `id`.
  - Updated the required array of `RecommendedStudy` to include `identifier`, `register`, `name`, and `id`.
  - Changed the type of `types` from _array_ to _string_, and renamed it to `type`.
  - Changed the type of `strategies` from _array_ to _string_, and renamed it to `strategy`.
  - Updated `strategy` enums to include `genetic` instead of `geneTherapy`.
  - Updated `RecommendedTherapy` required array to include `identifier`, `type` and `strategy`.
- **RareDiseasesMolecular:**
  - Updated `chromosome` enums by removing the `chr` prefix.
### Removed
- **RareDiseasesCase:**
  - Removed `phenotypes.identifier`.






## [1.6.1] - 2025-03-20
### Fixed
- **Submission:**
  - Relocating the required array in the `researchConsents` attribute.

## [1.6.0] - 2025-03-19
### Added
- **RareDiseasesFollowUp:**
  - Added `text`property to `phenotypes` attribute.
- **RareDiseasesCase:**
  - Added `text`property to `phenotypes` attribute.
  - Added new boolean attribute `noMatchingCodeExists` after `diagnoses` array to indicate whether a matching code exists.
  - Introduced new attribute `genomicStudyType` to `PriorRd` with enum values in camel case to follow the typographical convention of the schema, and to match the enums of `DiagnosisRd.diagnosticExtent` as follows:
    - `singleGenome`
    - `duoGenome`
    - `trioGenome`
  - Added the following enum values to `hospitalizationPeriods`: 
    - `none`
    - `upToFive`
    - `upToTen`
    - `upToFifteen`
    - `moreThanFifteen`
    - `unknown`
  - Added the following enum values to `hospitalizationDuration`: 
    - `none`
    - `upToFive`
    - `upToFifteen`
    - `upToFifty`
    - `moreThanFifty`
    - `unknown`
- **OncologyPlan:**
  - Added `KW` to the enums of `otherRecommendation`.
- **OncologyMolecular:**
  - Added `translocation` to `structureType` enum values.
### Changed
- **RareDiseasesFollowUp:**
  - Rolled back the change in the format of `deathDate` to be _YYYY-MM_.
- **OncologyFollowUp:**
  - Rolled back the change in the description of `deathDate` to include full accurate death date in the format _YYYY-MM-DD_.
  - Renamed attribute `terminationReason` to `terminationReasonOBDS`.
  - Changed the enum values of `terminationReasonOBDS` to match the enums in **OncologyCase** as follows:
    ```json
    {
      "enum": [
         "E",
         "R",
         "W",
         "A",
         "P",
         "S",
         "V",
         "T",
         "U"
      ]
    }
    ```
  - 
- **RareDiseasesMolecular:**
  - Renamed `positionFrom` and `positionTo` to `startPosition` and `endPosition` as used in **OncologyMolecular**.
- **OncologyMolecular:**
  - Renamed `variantType` to `variantTypes` to match the naming convention.
  - Changed `variantTypes` from an array of _strings_ to an array of _objects_ with the following properties:
    - `code`
    - `system`
    - `version`
  - Changed `variantTypes` cardinality from 1...N to 0...N.
- **OncologyCase:**
  - Changed `PriorVariant.variantTypes` cardinality from 1...N to 0...N.
  - Changed `PriorVariant.variantTypes` from an array of _strings_ to an array of _objects_ with the following properties:
    - `code`
    - `system`
    - `version`
- **RareDiseasesPlan:**
  - Renamed enum values of `clinicalManagementDescriptions` to the following:
    ```json
    {
      "enum": [
        "diseaseSpecificAmbulatoryCare",
        "universityAmbulatoryCare",
        "localCrd",
        "otherCrd",
        "otherAmbulatoryCare",
        "gp",
        "specialist"
      ]
    }
    ```
- **RareDiseasesCase:**
  - Changed the type of `hospitalizationPeriods` & `hospitalizationDuration` from _integer_ to _string_.
### Removed
- **RareDiseasesCase:**
  - Removed `trioExomeAnalysis` from the enums of `genomicTestType`.
### Fixed
- **OncologyPlan:**
  - Fixed attribute name `systematicTherapies` to `systemicTherapies`.

## [1.5.0] - 2025-03-18
### Added
- **Submission:**
  - Added new properties to the `submission` object with cardinality 1:  
    - `submitterId`, `genomicDataCenterId`, ``clinicalDataNodeId``, and `diseaseType`.
- **OncologyCase:**
  - Added a new optional property `text` to the hpoTerms.
- **OncologyMolecular:**
  - Added new properties `geneA` and `geneB` to `StructuralVariant`.
  - Introduced new attribute `ComplexBiomarker` with the following properties: 
    - `identifier`
    - `ploidy`
    - `tmb`
    - `hrdHigh`
    - `lstHigh`
    - `taiHigh`
  -  Introduced new attribute `SbsSignature` with the following properties:
      - `identifier`
      - `sbsVersion`
      - `sbsSignatures` with cardinality 1...N
      - `sbsSignaturePresent`
- **OncologyPlan:**
  - Introduced `systematicTherapies` & `otherRecommendation` to replace the removed property `therapeuticStrategy`. 
  - `systematicTherapies` is an array of strings with cardinality 0...N, and the enums are: 
    - `CH`
    - `HO`
    - `IM`
    - `ZS`
    - `SZ`
  - `otherRecommendation` is a string with cardinality 0...1, and the enums are: 
    - `WW`
    - `AS`
    - `WS`
    - `OP`
    - `ST`
    - `SO`
### Changed
- **Submission:**
  - Updated `researchConsents` to become an array of objects without further specification to contain a FHIR object.
- **OncologyCase:**
  - Changed the cardinality of `hpoTerms.version` from 1 to 0.
  - Updated the enums of `diagnosticAssessment` to the following: 
    ```json 
      {
        "enum": [
          "noGeneticDiagnosis",
          "suspectedGeneticDiagnosis",
          "furtherGeneticDiagnosisRecommended",
          "confirmedGeneticDiagnosis",
          "partialGeneticDiagnosis"
        ]
      }
      ```
- **RareDiseasesCase:**
  - Updated the enums of `PriorRd.genomicTestType` by adding `trioExomeAnalysis` and `none` as follows:
    ```json 
        {
          "enum": [
            "exome",
            "trioExomeAnalysis",
            "genomeLongRead",
            "genomeShortRead",
            "panel",
            "single",
            "array",
            "karyotyping",
            "other",
            "none"
          ]
        }
    ```
- **OncologyFollowUp:**
  - Updated the `deathDate` attribute to accept a date in the format `YYYY-MM-DD`, with updated description: _Date of death. If the day is unknown, use the 15th of the month._
- **RareDiseasesFollowUp:**
  - Updated the `deathDate` attribute to accept a date in the format `YYYY-MM-DD`, with updated description: _Date of death. If the day is unknown, use the 15th of the month._
  - Updated the `change` enums to the following:
  ```json
    {
      "change": {
        "type": "string",
        "enum": [
          "newlyAdded",
          "improved",
          "degraded",
          "noLongerObserved",
          "unchanged"
        ]
      }
    }
  ```
  - Updated _description_ for `diseaseProgression` attribute to become: _Case-relevant supplementary data on the progression of the disease._
- **RareDiseasesPlan:**
  - Updated the attribute `clinicalManagementDescriptions` with enum list as follows:
    ```json
    {
      "clinicalManagementDescriptions": {
        "type": "array",
        "items": {
            "type": "string",
            "enum": [
              "disease-specific-ambulatory-care",
              "university-ambulatory-care",
              "local-crd",
              "other-crd",
              "other-ambulatory-care",
              "gp",
              "specialist"
            ],
            "description": "Description of clinical management, e.g., hearing test, ultrasound."
          }
      }
    }
    ```
### Removed
- **OncologyMolecular:**
  - Removed `gene` and `geneC` from `StructuralVariant`.
  - Removed the following properties from `ExpressionVariant`: 
    - `tmb`
    - `hrdHigh`
    - `lstHigh`
    - `taiHigh`
    - `sbsVersion`
    - `sbsSignatures`
    - `sbsSignaturePresent`
  - Removed the `localization` from the required array of `ExpressionVariant` as the property is not part of it.
- **OncologyFollowUp:**
  - Removed `unknown` from the enum list of `vitalStatus`.
- **OncologyPlan:**
  - Removed `therapeuticStrategy` property as it is now replaced by `systematicTherapies` & `otherRecommendation`.

## [1.4.0] - 2025-02-20
### _This release includes changes in some attribute names, refactoring of some objects, updating some enum values, and cardinality change for some attributes._

### Added
- **Submission:** 
  - Added new properties to `mvConsent.scope`: 
    - `type`, `date`, and `domain`.
  - Added new property `scope` of type _string_ to the `researchConsents` array
- **OncologyCase:**
  - Added a `date` attribute to both `mainDiagnosis`  and each item in `additionalDiagnoses` to record the date of each diagnosis. The `date` fields follow the `YYYY-MM-DD` format as specified by the _JSON Schema_ date format.
  - Introduced a description to the ``additionalClassification`` attribute to handle cases where the _TNM classification system (AJCC or UICC)_ is unknown. This provides a string alternative to the _SNOMED CT_ coding of TNM, using a system 'TNM'.
  - Introduced new attribute `priorDiagnostics` that merges both ``priorOd`` and ``priorVariants``.
- **OncologyMolecular:**
  - Added `translocationWithCodingRegion` to `structureType` enum values.
- **OncologyFollowup:**
  - Added `date` to `additionalDiagnoses`.
  - Added `description` field to `substances`. 
- **RareDiseasesMolecular:**
  - Introduced two new attributes; `positionFrom` & `positionTo` as replacements for the removed attribute `position`.
   ```json 
  {
    "positionFrom": {
      "type": "integer",
      "description": "Start coordinate in GRCh38 VCF-style."
    },
    "positionTo": {
      "type": "integer",
      "description": "End coordinate in GRCh38 VCF-style."
    }
  }
  ```
### Changed
  - **Submission:**
    - Renamed the following enum values of the attribute `rejectionJustification`: 
      - `targetDiagnosisRecommended` &rarr; `targetedDiagnosticRecommended`.
      - `probablyNotGeneticCause` &rarr; `probablyNoGeneticCause`.
    - Changed the enum values of ``coverageType`` to the following: 
      ```json  
          {
            "enum": [
              "GKV",
              "PKV",
              "BG",
              "SEL",
              "SOZ",
              "GPV",
              "PPV",
              "BEI",
              "SKT",
              "UNK"
            ]
          }
         ```
      | Code | Display                          |
      |------|----------------------------------|
      | GKV  | gesetzliche Krankenversicherung  |
      | PKV  | private Krankenversicherung      |
      | BG   | Berufsgenossenschaft             |
      | SEL  | Selbstzahler                     |
      | SOZ  | Sozialamt                        |
      | GPV  | gesetzliche Pflegeversicherung   |
      | PPV  | private Pflegeversicherung       |
      | BEI  | Beihilfe                         |
      | SKT  | Sonstige Kostenträger            |
      | UNK  | unknown                          |
    - Changed cardinality of `presentationDate` from 1 to 0.
    - Changed an enum value of `gender` from `diverse` to `other`.
    - Updated description of `mvConsent.presentationDate` and `mvConsent.version`
    - Changed type of `scope` from _object_ to _array_
  - **OncologyCase:**
    - Changed cardinality of `priorOd` from 1 to 0
    - Changed cardinality of `tnmSystem` and `tnmVersion` from 1 to 0.
    - Renamed:
      - `genomicTestType` &rarr; `type`.
      - `genomicTestDate` &rarr; `date`.
      - `presentedDate` &rarr; `presentationDate`.
      - `complexAlterations` &rarr; `complexVariants`.
    - Introduced new attribute `simpleVariants` references `PriorVariant`. 
    - Moved `complexVariants` outside the `PriorVariant` object as a second array of variants.
  - **OncologyMolecular:** 
    - Changed ``chromosome`` enum values to numbers without `chr`.
    - Updated `cnvType` enums to the following array: 
      ```json  
         {
            "enum": [
              "completeLoss",
              "heterozygousLoss",
              "loss",
              "lowLevelGain",
              "highLevelGain",
              "gain"
            ]
         }
      ```
  - **OncologyPlan:**
    - Moved `recommendedStudies` to be part of `RecommendedSystemicTherapy`.
    - Renamed: 
      - `evidenceLevels` &rarr; `evidenceLevel`.
      - `evidenceGradings` &rarr; `evidenceLevelDetails`.
    - Changed type of `evidenceLevel` from _array_ to _string_.
    - Changed type of `evidenceLevelDetails` from _string_ to _array_.
    - Changed cardinality of `evidenceLevel` from 0 to 1.
  - **OncologyFollowup:**
    - Changed cardinality of `therapy.reference` from 1 to 0. 
    - Renamed: 
      - `metachroneTumorObserved` &rarr; `metachroneDiagnoses`.
      - `metachroneTumorDiagnoses` &rarr; `additionalDiagnoses`.
      - `substance` &rarr; `substances`.
    - Changed cardinality of `additionalDiagnoses` from 1 to 0.
  - **RareDiseasesCase:**
    - Renamed `heterozygousVariantInGeneticDisease` &rarr; `unclearVariantInGeneticDisease`.
  - **RareDiseasesMolecular:**
    - Updated the enum values of `chromosome` to show only the numbers without `chr`. 
### Removed
- **Coding:**
  - Removed the option `userSelected`.
- **Submission:**
  - Removed `date` from ``mvConsent`` object.
  - Removed `date` from ``researchConsents`` array.
  - Removed the following properties from the `mvConsent.scope`: 
    - `consentMvSequencing`, `consentCaseIdentification`, and `consentReIdentification`.
  - Removed the following properties from `mvConsent`:
    -  `terminationDate`, `terminationScope`
  - Removed the following properties from `researchConsents`: 
    - `date`, `version`, `revocationDate`, and `revocationScope`. 
- **OncologyCase:**
  - Removed ``diagnosisDate`` as it is superfluous after introducing the ``date`` attribute for both ``mainDiagnosis`` and ``additionalDiagnoses``
- **OncologyMolecular:**
  - Removed `localization` from `ExpressionVariant`.
  - Removed `copyNumber` attribute.
-  **OncologyFollowup:**
  - Removed `code` from required array within `substances`. 
- **RareDiseasesMolecular:**
  - Removed attribute `position`.
- **RareDiseasesFollowup:**
  - Removed attribute `lastContactDate` as this will be given by the date of the last followup.
  - Removed enum value `unknwon` from the attribute `vitalStatus` as the followup either contacts the person, or it is deceased. 
### Fixed
- **RareDiseasesMolecular:**
  - Fixed typo in enum value of `localization`. Instead of `intromicIntergenic` &rarr; `intronicIntergenic`.

## [1.3.0] - 2025-02-06
### _This release includes changes in some attribute names, refactoring of some objects and cardinality change for some attributes._

### Added
- **OncologyCase**:
  - Introduced `diagnosticAssessment` attribute with cardinality 1.
- **OncologyPlan**:
  - Introduced two new required attributes; `suitableInterventions.interventionsIsRiskReducing` and `suitableInterventions.interventionIsTherapeutic` to replace the removed `suitableInterventions.purpose` attribute.
- **OncologyFollowUp**:
  - Added new enum value `notApplicable` to `therapies` attribute.
  - Added `system` to the required attributes in `substance`.
### Changed
- **OncologyCase**:
  -  Renamed `terminationReason` to be `terminationReasonOBDS`.
  - Changed the cardinality of `ecogPerformanceStatusScore` to be 1.
  - Adding two new values to the enum list for `ecogPerformanceStatusScore`: `unknown` and `notApplicable`.
  - Changed `additionalClassificationSystems` to be `additionalClassification`.
  - Changed the type of `additionalClassification` from array to object.
  - Changed properties of `additionalClassification` to be `system` and `key`.
- **OncologyMolecular**:
  - Changed `loh` cardinality to 0.
- **OncologyFollowUp**:
  - Changed the cardinality of `therapies` to 0.
- **OncologyPlan**:
  - Changed the $ref in `suitableInterventions` from `https://www.bfarm.de/schemas/genomde/data-types/Substance#` to `https://www.bfarm.de/schemas/genomde/data-types/Coding#` to accept OPS codes, and adding `name` attribute to it.
- **RareDiseasesFollowUp**:
  - Changed the cardinality of `phenotypes.code` and `phenotypes.change`to 1.
### Removed
- **OncologyPlan**:
  - Removed `diagnosticAssessment` attribute as it is now part of `OncologyCase`.
  - Removed `suitableInterventions.purpose` attribute.

## [1.2.1] - 2025-01-27

### _This patch release continues with resolving attribute naming inconsistencies._

### Changed
- **Oncology**:
  - Renamed properties to: 
    - `OncologyCase` &rarr; `case`.
    - `OncologyMolecular` &rarr; `molecular`.
    - `OncologyPlan` &rarr; `plan`.
    - `OncologyFollowUp` &rarr; `followUp`.
- **RareDiseases**:
  - Renamed properties to:
    - `RareDiseasesCase` &rarr; `case`.
    - `RareDiseasesMolecular` &rarr; `molecular`.
    - `RareDiseasesPlan` &rarr; `plan`.
    - `RareDiseasesFollowUp` &rarr; `followUp`.
- **OncologyCase**:
  -  Renamed `ECOGPerformanceStatusScore` to be `ecogPerformanceStatusScore`.
  -  Renamed `HPOTerms` to be `hpoTerms`.
- **OncologyPlan**:
  - Renamed `MolecularBoardDecisionDate` to be `molecularBoardDecisionDate`.
  - Renamed `StudyRecommended` to be `studyRecommended`.
  - Renamed `StudyRecommended` to be `studyRecommended`.

## [1.2.0] - 2025-01-23

### _This release resolves attribute naming inconsistencies and standardizes the distinction between singular and plural terms for arrays and objects/strings. Using camelCase for all attribute names, while using PascalCase for object definitions._

### Added
- **Submission**:
  - Introduced new `submission` object with required array includes:
    - `date`, and `type`.
  - Introduced new `mvConsent` object with required array includes: 
    - `date`, `presentedDate`, `version`, and `scope`.
<div style="height:20px;"></div>

### Changed
- **Submission**:
  - Encapsulating the following attributes in the new `submission` object:
    - `date` (previously `submissionDate`).
    - `type` (previously `submissionType`).
  - Encapsulating the following attributes in the new `mvConsent` object: 
    - `date` (previously `mvConsentDate`).
    - `presentedDate` (previously `mvConsentPresentedDate`).
    - `version` (previously `mvConsentVersion`).
    - `scope` (previously `mvConsentScope`).
    - `terminationDate` (previously `mvConsentTerminationDate`).
    - `terminationScope` (previously `mvConsentTerminationScope`).
    - Updated the required array to include `submission` instead of `submissionDate` and `submissionType`.
    - Updated the required array to include `mvConsent` instead of `mvConsentDate`, `mvConsentPresentedDate`, `mvConsentVersion`, and `mvConsentScope`.
  - Renamed `researchConsent` to `researchConsents` to reflect that multiple entries are permitted.
  - Within each item of `researchConsents`, the following property name changes were made:
    - `date` (previously `researchConsentDate`).
    - `presentationDate` (previously `researchConsentPresentationDate`).
    - `version` (previously `researchConsentVersion`).
    - `scope` (previously `researchConsentScope`).
    - `revocationDate` (previously `researchConsentRevocationDate`).
    - `revocationScope` (previously `researchConsentRevocationScope`).
- **OncologyCase**:
  - Schema Naming Conventions:
    - Renamed `diagnosisOD` to be `diagnosisOd`.
    - Renamed `priorOD` to be `priorOd`.
    - Renamed `PriorVariants` definition to be `PriorVariant` as it is a singular object.
    - Renamed `PriorProcedures` definition to be `PriorProcedure` as it is a singular object.
    - Renamed `germlineDiagnosis` array to be `germlineDiagnoses`.
    - Renamed `tnmClassification` array to `tnmClassifications`.
    - Renamed `additionalClassificationSystem` array to `additionalClassificationSystems`.
    - Renamed `variantType` array to `variantTypes`.
    - Renamed `complexAlteration` array to `complexAlterations`.
    - Renamed `substance` array to `substances`.
    - Definitions: Updated all object definitions in the schema to use **PascalCase**. 
      - Changed attributes: `diagnosisOD` &rarr; `DiagnosisOd`, `priorOD` &rarr; `PriorOd`, `priorVariants` &rarr; `PriorVariant`, and `priorProcedures` &rarr; `PriorProcedure`.
    - Updated the required array to include `diagnosisOd` instead of `diagnosisOD` and `priorOd` instead of `priorOD`.
- **OncologyFollowUp**:  
  - Renamed `followUpOD` to be `followUpOds`.
  - Renamed `metachroneTumorDiagnosis` to be `metachroneTumorDiagnoses`.
  - Renamed `ECOGPerformanceStatusScore` to be `ecogPerformanceStatusScore`.
  - Definitions: Updated all object definitions in the schema to use **PascalCase**.
    - Changed attributes: `followUpOD` &rarr; `FollowUpOd`, `therapy` &rarr; `Therapy`, and `preventiveMeasures` &rarr; `PreventiveMeasure`.
- **OncologyMolecular**:
  - Renamed `SmallVariant` array to be `smallVariants`.
  - Renamed `CopyNumberVariant` array to be `copyNumberVariants`.
  - Renamed `StructuralVariant` array to be `structuralVariants`.
  - Renamed `ExpressionVariant` array to be `expressionVariants`.
  - Renamed `LOH` to be `loh`.
  - Renamed `TMB` to be `tmb`.
  - Renamed `HRDhigh` to be `hrdHigh`.
  - Renamed `LSThigh` to be `lstHigh`.
  - Renamed `TAIhigh` to be `taiHigh`.
  - Renamed `SBSversion` to be `sbsVersion`.
  - Renamed `SBSsignatures` to be `sbsSignatures`.
  - Renamed `SBSsignaturePresent` to be `sbsSignatures`.
- **OncologyPlan**:
    - Changed the type of `substance` in `RecommendedSystemicTherapy` from object to array, thus renaming the attribute to `substances`.
    - Renamed `carePlanOD` to be `carePlanOd`.
    - Renamed `substance` array to be `substances`.
    - Renamed `evidenceLevel` array to be `evidenceLevels`.
    - Renamed `evidenceGrading` array to be `evidenceGradings`.
    - Renamed `priority` array to be `priorities`.
    - Definitions: Updated all object definitions in the schema to use **PascalCase**.
      - Changed attributes: `recommendedStudies` &rarr; `RecommendedStudy`, `carePlanOD` &rarr; `CarePlanOd`, `recommendedSystemicTherapies` &rarr; `RecommendedSystemicTherapy`, and `preventiveMeasures` &rarr; `PreventiveMeasure`.
- **RareDiseasesCase**:
  - Renamed `diagnosisRD` to be `diagnosisRd`.
  - Renamed `priorRD` to be `priorRd`.
  - Renamed `HPOVersion` to be `hpoVersion`.
  - Renamed `diagnosis` array to be `diagnoses`.
  - Renamed `diagnosisGMFCS` array to be `diagnosisGmfcs`.
  - Renamed `ZSEcontactDate` array to be `zseContactDate`.
  - Definitions: Updated all object definitions in the schema to use **PascalCase**.
    - Changed attributes: `diagnosisRD` &rarr; `DiagnosisRd`, and `priorRD` &rarr; `PriorRd`.
- **RareDiseasesFollowUp**:
  - Renamed `followUpRD` to be `followUpRds`.
  - Renamed `gMFCS` to be `gmfcs`.
- **RareDiseasesMolecular**:
  - Renamed `StructuralVariant` array to be `structuralVariants`.
  - Renamed `SmallVariant` array to be `smallVariants`.
  - Renamed `CopyNumberVariant` array to be `copyNumberVariants`.
  - Renamed `gDNAChange` to be `gdnaChange`.
  - Renamed `cDNAChange` to be `cdnaChange`.
  - Definitions: Updated all object definitions in the schema to use **PascalCase**.
    - Changed attributes: `variants` &rarr; `Variant`.
- **RareDiseasesPlan**:
  - Renamed `carePlanRD` to be `carePlanRd`.
  - Renamed `clinicalManagementDescription` to be `clinicalManagementDescriptions`.
  - Renamed `register` array in `RecommendedStudy` to be `registers`.
  - Renamed `name` array in `RecommendedStudy` to be `names`.
  - Renamed `id` array in `RecommendedStudy` to be `ids`.
  - Renamed `type` array in `RecommendedTherapy` to be `types`.
  - Renamed `strategy` array in `RecommendedTherapy` to be `strategies`.
  - Definitions: Updated all object definitions in the schema to use **PascalCase**.
    - Changed attributes: `carePlanRD` &rarr; `CarePlanRd`, `recommendedStudies` &rarr; `RecommendedStudy`, and `recommendedTherapies` &rarr; `RecommendedTherapy`.
<div style="height:20px;"></div>

## [1.1.0] - 2025-01-17

### Added
- **data-types**:
  - Introduced two new `data-types`; `Identifier` and `Substance`.

- **Submission**:
    - Added `birthDate` to required list.

- **OncologyCase**:
    - Introduced `tnmClassification` array to consolidate T, N, and M classifications. This change removes the three attributes ``tClassification``, ``nClassification`` and ``mClassification``. Each object in the array has:
      - ``code`` (SNOMED code)
      - ``system``
      - ``version``
      - ``display`` (Should have display values matching the ones in SNOMED; such as American Joint Committee on Cancer cT1a, American Joint Committee on Cancer pM1a, etc.). 
      - Added optional `text` property to include shorthand notations like `cT1a`.
      - SNOMED codes for both AJCC and UICC can be found here: [ American Joint Committee on Cancer allowable value - AJCC](https://browser.ihtsdotools.org/?perspective=full&conceptId1=1222584008&edition=MAIN/2025-01-01&release=&languages=en), [ Union for International Cancer Control allowable value - UICC ](https://browser.ihtsdotools.org/?perspective=full&conceptId1=1352503003&edition=MAIN/2025-01-01&release=&languages=en)
      ```json 
        {
           "tnmClassification": [
              {
                  "code": "1228889001",
                  "system": "http://snomed.info/sct",
                  "version": "20210131",
                  "display": "American Joint Committee on Cancer cT1 (qualifier value)",
                  "text": "cT1"
              },
              {
                  "code": "1229973008",
                  "system": "http://snomed.info/sct",
                  "version": "20210131",
                  "display": "American Joint Committee on Cancer cN1 (qualifier value)",
                  "text": "cN1"
              },
              {
                  "code": "1229903009",
                  "system": "http://snomed.info/sct",
                  "version": "20210131",
                  "display": "American Joint Committee on Cancer cM1 (qualifier value)",
                  "text": "cM1"
              }
          ],
          "tnmSystem": "AJCC",
          "tnmVersion": "8"
        }
      ```
    - Enhanced descriptions for schema properties `tnmClassification`, `text`, `tnmSystem`, `tnmVersion`, `variantType`, `germlineDiagnosis`, and `therapyStartDate` to improve clarity and understanding.

- **OncologyPlan**:
    - Enhanced description for `evidenceLevel`.
    - Introduced `suitableInterventions` array to include both ``purpose`` and ``type``.

- **OncologyFollowUp**:
    - Adding `unknown` to enum list for `ECOGPerformanceStatusScore`.

- **OncologyMolecular**:
    - Adding `cnvType` to required properties.

- **RareDiseasesPlan**:
    - Introduced new property `variantReferences` in `recommendedTherapies`.
  
<div style="height:20px;"></div>

### Changed
- **Submission**:
    - Updated description of `mvConsentVersion`.

- **OncologyCase**:
    - Renamed `germlineDiagnosisCode` to be `germlineDiagnosis`
    - Cardinality changed for `diagnosisDate` (cardinality = 1).  
    - tnmSystem and tnmVersion are required (cardinality = 1).  
    - Renamed `diagnosisDate` to `genomicTestDate`.
    - Cardinality change for `germlineDiagnosis` (cardinality = 0...N).
    - Cardinality change for `diagnosisDate` (cardinality = 1).
    - Cardinality change for `ECOGPerformanceStatusScore` (cardinality = 0...1).

- **OncologyPlan**:
    - Updating the enum value text for `register` to be `Eudra-CT/CTIS`.

- **OncologyFollowUp**:
    - Changing the enum values for `vitalStatus` to be `["living", "deceased", "unknown"]`.
    - Changing cardinality for `preventiveMeasures` (cardinality = 0...N).
    - Changing cardinality for `therapyResponseDate` (cardinality = 1).
    - Nesting all attributes under `followUpOD`. 
    - Changing cardinality for `followUpOD` (cardinality = 1...N).
    - Changing enum value for `preventiveMeasureResult` from `o.B. to noFindings`.
- **OncologyMolecular**:
    - Modified `identfier` attribute using `$ref` definition.
    - Changing `SBSsignatures` type from `string` to `array`.
    - Update of `SBSsignaturePresent` description.
- **RareDiseasesPlan**:
  - Modified `identfier` attribute using `$ref` definition.
  - Modified enum values in `register` property in `recommendedStudies` to include full name `Eudra-CT/CTIS`. 
  - Updated Enum value in `strategy` Property of `recommendedTherapies`. Old value `genetic` updated to `geneTherapy`. 
  
<div style="height:20px;"></div>

### Deprecated
- **OncologyCase**:
    - Deprecated `tnmSystem` and `tnmVersion` properties, which are marked for potential removal in future versions.
    - Deprecated `germlineDiagnosisConfirmed` due to redundancy with `germlineDiagnosis`.
- **OncologyMolecular**:
    - Deprecated `SBSsignaturePresent` boolean and marked for potential removal in future versions.

<div style="height:20px;"></div>

### Fixed
- **OncologyCase**:
    - Fixed typo in genomicTestType emum value `karyotyping`.

- **RareDiseasesPlan**:
    - Fixed reference of variants in `recommendedTherapies` to be an array of references under the property `variantReferences`.
- **OncologyFollowUp**:
  - Fixed the object name `therapies` (plural) to become `therapy`.
<div style="height:20px;"></div>

### Removed
- **OncologyCase**:
    - Removed the `tClassification`, `nClassification`, and `mClassification` attributes in favor of the new `tnmClassification` array.

- **RareDiseasesPlan**:
  - Removal of `variants` property from `recommendedTherapies` and replaced with `variantReferences`.

- **OncologyPlan**:
    - Removed `interventionType` and `interventionPurpose`.
    - Removed `interventionPurpose` from required array, and required only if there were suitableIntervention.
