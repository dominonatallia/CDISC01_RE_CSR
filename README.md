# Template Reporting Effort repository

This repo contains the folder structure to template a reporting effort making ADaM and TFL code for the Domino clinical trial demo

# Directory structure

The programming is created in a typical clinical trial folder structure, where the production (prod) and qc programs have independent directory trees.

Reporting effort level standard code (e.g. SAS macros) should be stored in the `share/macros` folder.

The global `domino.sas` autoexec progam is also included in the repository to appropriately set up the SAS environment. 

```
repo
│   domino.sas
|   init_datasets.py
├───prod
│   ├───adam
│   └───tfl
├───qc
│   ├───adam
│   │       compare.sas
│   └───tfl
└───share
    └───macros
```

# Setup

1. Create a new project, named `CDISC01_RE_YOURNAME`.
1. Run `dataset_init.py` as a job to create the appropriate analysis domino datasets (ADAM, TFL, ADAMQC and TFLQC). As well as import SDTM datasets from an existing project following the same naming convention (`CDISC01_SDTM` for `CDISC01_RE_XXXXX`).
1. Add the external volume `pvc-rev4-nfs` to your project.
1. Import the `CDISC01_SDTM` within artifacts to get the DCUTDTC environment variable.
1. Run `import_metadata.sas` as a job (on the SAS environment!). 
1. Run `snakemake.sh` as a job (on the 'w/ Snakemake' environment) to kick off the pipeline. 
1. Within the project start the app to see the visual dependency graph.

# Naming convention

The programs follow a typical clinical trial naming convention, where the ADaM programs are named using the dataset name (e.g. ADSL.sas, etc.) and the TFL programs have a `t_` prefix to indicate tables, etc.

# QC programming and reporting

The QC programming is all in SAS, and there is a `compare.sas` program which uses SAS PROC COMPARE to create a summary report of all differences between the prod and qc datasets. This program also generates the `dominostats.json` files which Domino uses to display a dashboard in the jobs screen.

# Support

Programming was created by Veramed Ltd. on behalf of Domino Data Lab, Inc.
