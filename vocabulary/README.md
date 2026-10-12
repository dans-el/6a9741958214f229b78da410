# Measurement vocabulary for the interview

Open `loinc.sqlite` with SQLite. It contains one table:

```sql
measurement_concept(concept_id, loinc_code, name)
```

`concept_id` is the identifier to return for a matched measurement. `loinc_code` is the standard measurement code. `name` is the measurement name. Every concept in this file is eligible for matching; you do not need to filter by status.

This file contains all 68,106 current standard LOINC Measurement concepts from the pinned Athena export (OMOP vocabulary release `v5.0 27-FEB-26`, LOINC `2.80`). It contains no patient data.

For example:

```sql
SELECT concept_id, loinc_code, name
FROM measurement_concept
WHERE loinc_code = '8480-6';
```

This material contains content from LOINC (http://loinc.org). LOINC is copyright © Regenstrief Institute, Inc. and the Logical Observation Identifiers Names and Codes (LOINC) Committee and is available at no cost under the license at http://loinc.org/license. LOINC® is a registered United States trademark of Regenstrief Institute, Inc.
