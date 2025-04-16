# Sanction-List-Data-Processing

This project processes the UK Consolidated Financial Sanctions List to create a deduplicated dataset for financial crime screening, reducing ~18,798 records to 4,673 unique entities and individuals. It generates an `Aliases` column to capture name variants in order to enhance matching accuracy for Anti-Money Laudering (AML) compliance.

## Overview
The project has transformed raw sanctions data into a clean format for screening and better visualisation:
1. **Load**: Imported the UK Sanctions List (~18,798 rows, 36 columns).
2. **Explore**: Analysed columns (`Name 1-6`, `DOB`, etc.), noting sparsity (e.g., 34.12% missing `DOB`).
3. **Filter**: Reduced to 18,717 relevant records.
4. **Transform**: Created 11 columns (e.g., `PrimaryName` from `Name 1` + `Name 6`, `Nationality`).
5. **Deduplicate**: Consolidated to 4,673 records, adding `Aliases` for variants (e.g., `['Mian Mithoo', 'Mian Mithu']`).

## Files
- `sanctions_processing.ipynb`: Jupyter Notebook with the full pipeline (load, explore, filter, transform, deduplicate).
- `ConList.csv`: Original UK Consolidated Financial Sanctions List (~18,798 rows).
- `ConList_Processed.csv`: Processed dataset (4,673 rows, 12 columns: `UniqueID`, `EntityType`, `PrimaryName`, `Aliases`, `DOB`, `Nationality`, `Country of Birth`, `Current Country`, `SanctionType`, `PassportNumber`, `NationalID`, `AliasQuality`).

## Purpose
Supports financial crime screening:
- **Matching**: `PrimaryName` and `Aliases` ensure accurate identification (e.g., `Mian Abdul Haq` with `['Mian Mithoo', 'Mian Mithu']`).
- **Risk Assessment**: `DOB`, `Nationality` (e.g., `Pakistan`, `Indonesia`), `Country of Birth`, `Current Country` align with global jurisdictions (e.g., `Canada`, `U.K.`, `U.S.`).
- **Compliance**: `SanctionType` (e.g., `Global Human Rights`, `Russia`) meets OFSI requirements.

## Key Results
- Reduced dataset from 18,717 to 4,673 records (~75% reduction).
- Created `Aliases` for variant matching (e.g., `['Tharwat Shihata', 'Tharwat Ali']`).
- Cleaned country fields (e.g., `Indonesia`, `Afghanistan`) for clarity.
- Handled sparsity (34.12% missing `DOB`, 44.15% missing `Nationality`).

## Insights
- **Dataset Size**: Deduplicated to 4,673 unique entities and individuals, with 13,692 individuals and 5,025 entities pre-deduplication, streamlining screening.
- **Name Variants**: `Aliases` captures diverse spellings (e.g., `['Fikiruddin Muqti', 'Mohamad Abdurrahman']` for `UniqueID` 6894), critical for matching names like `Muhammad bin Salman Al Saud`.
- **Sparsity**: 34.12% missing `DOB`, 44.15% missing `Nationality`, and 85.24% missing `PassportNumber`, requiring robust handling for KYC.
- **Sanction Types**: Dominated by regimes like `ISIL (Da'esh) and Al-Qaida`, `Russia`, and `Global Human Rights`, indicating high-risk jurisdictions.
- **Countries**: Frequent `Nationality` and `Current Country` values include `Pakistan`, `Afghanistan`, `Russia`, highlighting geopolitical risk areas, with alignment to global contexts (e.g., `Canada`, `U.K.`, `U.S.`).

## Execution
To run the pipeline:
1. Ensure `ConList.csv` and `ConList_Processed.csv` are in the same directory as `sanctions_processing.ipynb`.
2. Open `sanctions_processing.ipynb` in Jupyter Notebook.
3. Run all cells in the kernel (e.g., click **Kernel > Restart & Run All** or **Run > Run All Cells**).
4. The notebook processes `ConList.csv` to generate `ConList_Processed.csv` (4,673 records).

## Requirements
- Python 3.x
- Required libraries:
  ```bash
  pip install pandas numpy unidecode fuzzywuzzy matplotlib
