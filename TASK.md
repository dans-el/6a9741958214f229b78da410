# Live coding exercise: PDF in, JSON out

## Situation

A pilot receives clinical PDFs and needs a structured list of patient measurement results. Your task is to turn a supplied PDF into JSON and link its measurements to the supplied LOINC vocabulary. All PDFs are synthetic. You do not need prior healthcare or OMOP knowledge; the [appendix](#appendix-glossary) explains the terms needed for extraction.

## Your task

Build a small program that accepts a local PDF path, a synthetic `documentId`, and an integer `personId`, and returns the JSON described below.

Choose your language and extraction approach. We provide optional TypeScript and Python starters in `starter-ts/` and `starter-py/`. You may use Gemini; the interviewer can provide an interview-only API key privately if you want one. You may also use an AI coding assistant.

We use the exercise to discuss how you investigate, make decisions, test assumptions, and respond to uncertainty. Finishing the program or every case is not a requirement. Make your priorities and reasoning visible, including what you would investigate next.

## Supplied data

The SQLite file `vocabulary/loinc.sqlite` has one table:

```sql
measurement_concept(concept_id, loinc_code, name)
```

Every row is an eligible current standard LOINC Measurement concept. `concept_id` is the integer to return. Use the full supplied vocabulary for matching; do not hardcode IDs from examples. Any concept ID returned must be checked against SQLite, including IDs suggested by a model. Explain why the chosen concept fits the measurement.

The visible PDFs and their `documentId`/`personId` inputs are listed in `pdfs/manifest.json`. The visible set includes a simple English result, a two-page German report with current and previous results, and an Italian note stored as a page image without an embedded text layer. One extra PDF may be used in the walkthrough with a different layout and mixed languages. You may use translation tools or ask the interviewer about unfamiliar terms; language fluency and clinical knowledge are not being assessed. All inputs are synthetic.

## Output contract

Return one JSON object per PDF with these fields:

| Field | Type | Meaning |
| --- | --- | --- |
| `documentId` | string | The supplied document identifier. |
| `personId` | integer | The supplied person identifier. |
| `results` | array of objects | Measurement results that can be dated and matched confidently. |
| `unresolved` | array of objects | Plausible measurements that cannot be dated or matched safely. |

Each object in `results` has:

| Field | Type | Meaning |
| --- | --- | --- |
| `conceptId` | integer | A verified `measurement_concept.concept_id`. |
| `date` | string | Collection or result date in `YYYY-MM-DD` format. |
| `value` | string | The decimal result as printed, including a decimal comma or point, without the unit. |
| `unit` | string or null | The unit as printed, or null if absent; do not convert. |
| `sourceTerm` | string | The short printed test name or code, at most 50 characters. |
| `evidence` | object | Contains `page` (1-based integer) and `quote` (short verbatim phrase from the PDF). |

Each object in `unresolved` has `page` (1-based integer), `quote` (short verbatim phrase), and `reason` (string explaining the uncertainty).

Attempt every patient measurement result, including repeated results, and keep results in document order. Only patient measurements with numeric results belong in `results`. Reference ranges, orders without a result, medication doses, and demographic numbers are not patient measurements. A result needs an explicitly associated collection or result date; a report issue date alone is insufficient. If the date or concept match is uncertain, use `unresolved`. An irrelevant document can return empty arrays.

Quotes may join text across layout whitespace; preserve the printed words and values. Explain any assumptions you make about ambiguous layout, reading order, or wording.

## Demonstration and tests

Walk us through your approach, the parts you can run, and a decision or problem you investigated. For results you produce, show the source evidence and how you checked the selected SQLite row. Discuss exclusions, uncertainty, and checks that would reveal a wrong result. Use offline tests where they help demonstrate your decisions; they must run without a live model call. If a chosen model is unavailable, the interviewer can supply sample extracted observations so you can continue investigating matching and validation. These are authored fixtures, not captured model responses.

Use only the provided synthetic PDFs with the interview credentials. Keep API keys out of code, commits, logs, and submitted artifacts. Do not include full PDF contents, prompts, model responses, or source excerpts in diagnostic logs. The required JSON evidence is part of the output.

## Interview format

The session lasts 90-120 minutes. Roughly 8-10 minutes are for briefing, 48-65 minutes for coding and testing, 12-15 minutes for a walkthrough, and 18-25 minutes for a system design discussion extending your approach to a reliable service. You may explain what you would do next if you do not finish every fixture.

## Appendix: glossary

These definitions are here so the exercise does not depend on clinical training. The vocabulary database remains the source for concept IDs.

| Term | Plain-language meaning |
| --- | --- |
| Measurement result | A value actually measured for this patient, usually with a date and unit. |
| Specimen | The material tested, such as blood or serum. |
| Serum / plasma | Liquid components of blood used for many laboratory tests. |
| Whole blood | Blood tested without separating out its cells. |
| Reference interval | A comparison range printed by the lab; it is not this patient's result. |
| Result pending | A test was ordered, but this document has no measured value for it. |

Preserve printed units as text. For this exercise, no unit conversion or clinical interpretation is required.
