# Data Narrative

This file describes how the data was curated into BIDS after it was de-identified.
For more details, see the commit history of this repository.

Note: In this special case, original data is stored in 
`/cbica/projects/RBC/RBC_RAWDATA/bidsdatasets/HRC`

# Transfer Process

The data were acquired at [SITE] as part of [STUDY] study [CITATION]. Access was given
to PennLINC as part of the Reproducible Brain Chart project [CITATION]. The data was
transferred from [SITE] to PMACs using [Globus](https://www.globus.org/). After
this, the data was transferred from PMACs to CUBIC. The approximate date of 
transfer was late January 2021. In sum, PennLINC received approximately 108 GB 
comprising of 608 subjects and 905 individual sessions (with session labels 
ranging from `ses-1` to `ses-2`). The imaging data consisted of anatomical
(`T1w`), functional (`BOLD`), and diffusion (`dwi`, `bval`, `bvec`). Task
data consisted of `rest` scans.

No additional cohort data was provided at this time of transfer. The imaging data was
organized in BIDS and anonymized at the time of transfer. The raw data was copied to `/cbica/projects/RBC/HRC/working/BIDS`
for BIDS curation and acquisition group testing, where it was checked into `datalad`. See [this notebook](SubjectsSessionsModalities.ipynb)
for a code walkthrough of this investigation.

# BIDS Curation

The data was partially curated before the beginning of this git history. Using the titles of the outputs of the validate tool, the change history of BIDS can still be pieced together.

---

On 01/27/2021, the following errors were found:

Code 55 — JSON_SCHEMA_VALIDATION_ERROR: One subject (sub-20765 ses-2)
Code 1 — NOT_INCLUDED: Multiple cases
Code 50 — TASK_NAME_MUST_DEFINE: Multiple cases
Code 67 — NO_VALID_DATA_FOUND_FOR_SUBJECT: Multiple cases

Code 55 was a case where the Slice Timing had negative values in run 1 of the resting state scan; we removed this scan from the session.

Code 1 was resolved by reordering the entities in the BIDS filenames.

Code 50 was resolved by adding the task `Rest` to each corresponding JSON file.

Code 67 was resolved by removing sessions which were clearly incomplete/unusable data.

---

On 02/11/2021, the final remaining BIDS validation issue was: 

Code 39 — INCONSISTENT_PARAMETERS: Multiple cases

We tolerate this error as it is expected to appear as there may be multiple scanning parameters available across similar runs.

In [this notebook](UnderstandingRunNaming.ipynb) we found that there were multiple images per session with incremental runs. We learned from the study coordinators that this was due to motion, and that some scans had to subsequently be re-run. We decided to keep functional data where this may have happened, but to only maintian one single T1w image. Samples of these were inspected by hand, and it was decided the best strategy would be to remove the old T1w images and keep only 1 T1w (the most recent) per session. See [this notebook](RemovingExtraT1ws.ipynb) for code.

The final validation run is from [03/03/2021](hrc_validation_03-03-21_validation.csv).