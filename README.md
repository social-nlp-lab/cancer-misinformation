# Cancer Misinformation Dataset

## Overview

This repository contains two spreadsheet datasets for studying
cancer-related misinformation in online posts. The files provide (1) a
manually annotated reference dataset and (2) a larger dataset containing
LLM-generated misinformation classifications and downstream labels.

The two files are:

-   `Final_Sheet_Annotated_EMNLP_GitHub_Repo.xlsx` --- manually
    annotated dataset containing 400 records and human-assigned labels
    for seven annotation tasks.
-   `Final_LLM_Prediction_All_Tasks_GitHub_Repo.xlsx` --- LLM prediction
    dataset containing 1,730 populated records with misinformation
    predictions, model-output metadata, and LLM-generated labels for
    downstream annotation tasks.

The spreadsheets contain post identifiers and titles rather than the
full post text.

------------------------------------------------------------------------

## Dataset 1: Final_Sheet_Annotated_EMNLP_GitHub_Repo.xlsx

### Purpose

This file contains the manually annotated portion of the dataset. Each
row corresponds to an online post and contains its identifier, title,
and final annotation labels.

The worksheet is named `in`.

### Size

-   Records: 400
-   Columns: 9
-   Identifier column: `post_id`
-   Annotation columns: `Final_Label_Q1` through `Final_Label_Q7`

`Final_Label_Q1` is populated for all 400 records. The downstream Q2-Q7
fields are populated for 176 records and are blank for the remaining
records. Missing values in these fields should therefore be treated as
unassigned/not populated in the released sheet rather than automatically
interpreted as a substantive category.

### Columns

#### `post_id`

Unique identifier for the source post.

-   Type: string
-   Non-missing records: 400
-   Unique values: 400

This field can be used as the primary row identifier for the annotated
dataset.

#### `Title`

Title of the source post.

-   Type: string
-   Non-missing records: 399
-   Unique non-missing values: 399

One record has a missing title. Some titles may contain
character-encoding artifacts inherited from the source/export process.

#### `Final_Label_Q1`

Final annotation for whether the post contains misinformation according
to the study's misinformation annotation task.

Observed values:

-   `Yes`
-   `No`
-   `Unclear`

`Unclear` represents cases for which a definitive Yes/No misinformation
determination was not assigned.

#### `Final_Label_Q2`

Annotation of the primary cancer-related context in which the relevant
claim appears.

Observed values:

-   `Treatment`
-   `Prevention / Screening`
-   `Other / Unclear / Not applicable`

This field distinguishes treatment-related claims from
prevention/screening claims while retaining an
other/unclear/not-applicable category.

#### `Final_Label_Q3`

Annotation of the post's information behavior.

Observed values:

-   `Seeking`
-   `Sharing`
-   `Both`

`Seeking` indicates information-seeking behavior, `Sharing` indicates
information-sharing behavior, and `Both` indicates that both functions
are present.

#### `Final_Label_Q4`

Annotation of the misinformation/content type.

Observed values:

-   `Fabricated Content`
-   `Misleading Content`
-   `Imposter Content`
-   `False Context`
-   `Other`
-   `Fabricated Content, Imposter Content`

The field can contain a combined label when more than one applicable
content type is assigned.

#### `Final_Label_Q5`

Annotation of misinformation risk level.

Observed values:

-   `Low Risk`
-   `Moderate Risk`
-   `High Risk`

This variable represents the assigned level of potential risk associated
with the misinformation.

#### `Final_Label_Q6`

Annotation of the post author's stance toward, or engagement with, the
misinformation claim.

Observed values:

-   `Accepts`
-   `Questions`
-   `Rejects`
-   `Accept + Question`
-   `Reject + Question`
-   `Other / Unclear`

The combined categories represent posts containing more than one stance
function.

#### `Final_Label_Q7`

Annotation of the substantive misinformation theme or claim domain.

Observed values include:

-   `Unproven or alternative treatments`
-   `Causation, risk factors & prevention claims`
-   `Safety & effectiveness of conventional treatments`
-   `Diagnosis & screening claims`
-   `Conspiracy & institutional distrust`
-   `Medical autonomy & medical freedom`
-   `Other`

The field also contains multi-label combinations, including:

-   `Causation, risk factors & prevention claims, Diagnosis & screening claims`
-   `Unproven or alternative treatments, Conspiracy & institutional distrust`
-   `Safety & effectiveness of conventional treatments, Unproven or alternative treatments`
-   `Causation, risk factors & prevention claims, Conspiracy & institutional distrust`
-   `Causation, risk factors & prevention claims, Unproven or alternative treatments`

Therefore, Q7 should not be assumed to be strictly single-label when
processing the data.

------------------------------------------------------------------------

## Dataset 2: Final_LLM_Prediction_All_Tasks_GitHub_Repo_Updated.xlsx

### Purpose

This file contains LLM-generated predictions for the misinformation
classification task and the downstream annotation tasks. It also retains
model-output and token-usage metadata associated with the misinformation
classification stage.

The worksheet is named `Final_LLM_Prediction_All_Tasks_`.

### Size

-   Populated records: 1,730
-   Columns: 9
-   Identifier column: `id`

### Columns

#### `id`

Unique identifier for the source post.

-   Type: string
-   Populated records: 1,730
-   Unique populated values: 1,730

This is the primary identifier for the LLM prediction dataset.

#### `Title`

Title of the source post.

-   Type: string
-   Populated records: 1,731 in the worksheet

For analytic use, records should normally be keyed using the `id` field.

------------------------------------------------------------------------

### Misinformation Classification and Model Metadata


#### `misinformation_presence`

Final processed misinformation label produced from the classification
pipeline.

In this released file, the 1,730 populated records have:

-   `Yes`

The released LLM dataset therefore represents the
misinformation-positive subset retained for the downstream tasks.


------------------------------------------------------------------------

## LLM-Generated Downstream Labels

The columns `LLM_Label_Q2` through `LLM_Label_Q7` correspond to the same
broad annotation dimensions represented by Q2-Q7 in the manually
annotated dataset, but these values are LLM-generated rather than manual
final annotations.

### `LLM_Label_Q2`

LLM-generated cancer-related context label.

Observed values:

-   `Treatment`
-   `Prevention/Screening`
-   `Other/Unclear/NA`

Note that the formatting differs slightly from the manual dataset, where
the corresponding labels are `Prevention / Screening` and
`Other / Unclear / Not applicable`.

### `LLM_Label_Q3`

LLM-generated information-behavior label.

Observed values:

-   `Seeking`
-   `Sharing`
-   `Both`

### `LLM_Label_Q4`

LLM-generated misinformation/content-type label.

Observed values:

-   `Fabricated Content`
-   `Misleading Content`
-   `Imposter Content`
-   `False Context`
-   `Satire/Parody`
-   `Other`
-   `Fabricated Content, Imposter Content`

`Satire/Parody` occurs in the LLM prediction dataset but does not occur
among the observed Q4 labels in the released 400-row manually annotated
sheet.

### `LLM_Label_Q5`

LLM-generated misinformation risk level.

Observed values:

-   `Low Risk`
-   `Moderate Risk`
-   `High Risk`

### `LLM_Label_Q6`

LLM-generated stance/engagement label.

Observed values:

-   `Accepts`
-   `Questions`
-   `Rejects`
-   `Accept + Question`
-   `Reject + Question`
-   `Other`

Note that the manual dataset uses `Other / Unclear` for the
corresponding residual category.

### `LLM_Label_Q7`

LLM-generated misinformation theme/claim-domain label.

Observed single labels include:

-   `Unproven or alternative treatments`
-   `Diagnosis & screening claims`
-   `Safety & effectiveness of conventional treatments`
-   `Causation, risk factors & prevention claims`
-   `Conspiracy & institutional distrust`
-   `Medical autonomy & medical freedom`
-   `Morality, religion & ideology`
-   `Other`

Observed multi-label combinations include:

-   `Safety & effectiveness of conventional treatments, Unproven or alternative treatments`
-   `Causation, risk factors & prevention claims, Diagnosis & screening claims`
-   `Causation, risk factors & prevention claims, Conspiracy & institutional distrust`
-   `Unproven or alternative treatments, Conspiracy & institutional distrust`
-   `Causation, risk factors & prevention claims, Unproven or alternative treatments`

As in the manual dataset, Q7 should therefore be treated as potentially
multi-label.

`Morality, religion & ideology` occurs in the LLM prediction dataset but
does not occur among the observed Q7 values in the released manually
annotated sheet.

------------------------------------------------------------------------

## Relationship Between the Two Files

The datasets represent two related annotation layers:

  -----------------------------------------------------------------------------------------------------
  File                                                Annotation source       Main role
  --------------------------------------------------- ----------------------- -------------------------
  `Final_Sheet_Annotated_EMNLP_GitHub_Repo.xlsx`      Manual/final            Reference annotated
                                                      annotations             sample

  `Final_LLM_Prediction_All_Tasks_GitHub_Repo_Updated.xlsx`   LLM predictions         Larger model-labeled
                                                                              misinformation-positive
                                                                              dataset
  -----------------------------------------------------------------------------------------------------

The naming convention differs between the files:

-   Manual labels: `Final_Label_Q1` ... `Final_Label_Q7`
-   LLM labels: misinformation-classification fields plus `LLM_Label_Q2`
    ... `LLM_Label_Q7`

Q2-Q7 represent corresponding conceptual annotation dimensions, although
some category strings differ slightly between the manual and LLM files.
Researchers joining, comparing, or aggregating the datasets should
normalize these strings before analysis.

Examples include:

-   `Prevention / Screening` vs. `Prevention/Screening`
-   `Other / Unclear / Not applicable` vs. `Other/Unclear/NA`
-   `Other / Unclear` vs. `Other`

Do not assume that identically numbered Q-columns are directly
interchangeable without accounting for whether the label was manually
assigned or LLM-generated.

------------------------------------------------------------------------

## Missing Values

Blank cells should remain missing values during import unless an
analysis explicitly defines another treatment.

In particular:

-   Q2-Q7 contain missing values for many records in the manually
    annotated dataset.
-   A missing downstream label should not automatically be converted to
    `Other`, `No`, or any other substantive class.
-   `task1_matching_text` is empty in the released LLM dataset.
-   `gemini3_k5_error` is empty in the released LLM dataset.
-   Analyses of the LLM dataset should normally exclude effectively
    blank rows by requiring a non-missing `id`.

------------------------------------------------------------------------

## Multi-Label Fields

Some Q4 and Q7 records contain comma-separated combinations of
categories. These are valid labels in the released sheets and should not
automatically be treated as data-entry errors.

If a project requires binary indicator variables, these fields can be
transformed into one-hot/multi-hot representations during preprocessing.
Researchers should take care with category names that themselves contain
punctuation and should use the documented category vocabulary rather
than splitting strings blindly without validating the resulting labels.

------------------------------------------------------------------------

## Suggested Loading

``` python
import pandas as pd

manual = pd.read_excel(
    "Final_Sheet_Annotated_EMNLP_GitHub_Repo.xlsx"
)

llm = pd.read_excel(
    "Final_LLM_Prediction_All_Tasks_GitHub_Repo.xlsx"
)
```
------------------------------------------------------------------------

## Data Use and Interpretation

These datasets contain annotations and model-generated classifications
of health-related misinformation. The labels are intended for research
and computational analysis and should not be interpreted as
individualized medical advice or clinical diagnoses.

LLM-generated labels should be distinguished from manual annotations in
reporting. Model predictions may contain classification errors, and the
raw model reasoning in `gemini3_k5_raw` should not be treated as
independently verified medical evidence.

Post identifiers and titles originate from online content. Users of the
dataset are responsible for following applicable ethical requirements,
platform policies, and institutional requirements when linking
identifiers back to source material or quoting source content.

------------------------------------------------------------------------

## Repository Citation

If you use this dataset, please cite the associated paper and repository. 

``` text
@article{pessianzadeh2026beyond,
  title={Beyond Binary Detection: A Multi-Dimensional Taxonomy of Cancer Misinformation on Reddit},
  author={Pessianzadeh, Aria and Jamie, Pooriya and Sultana, Naima and Himmelstein, Georgia and Zektser, Yuliya and Ganz, Patricia and Hosseinmardi, Homa and Ghasemian, Amir and Rezapour, Rezvaneh},
  journal={arXiv preprint arXiv:2607.12383},
  year={2026}
}
```


