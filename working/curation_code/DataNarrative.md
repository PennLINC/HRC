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
