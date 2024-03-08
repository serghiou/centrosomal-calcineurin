# README

## Authors

Stylianos (Stelios) Serghiou, Eirini Tsekitsidou

## Publication

When we have the preprint or publication, we will post the link here.

## File structure

Combining resources across OSF and GitHub should yield the following structure.

```         
├── .gitignore          <- Lists files to be ignored in syncing between local and remote.
├── LICENSE             <- Describes license to the contents of this repo.
├── README.md           <- Describes the project and orchestration (how to run)
│
├── data
│   ├── 0_external        <- Data from third party sources (e.g., US Census).
│   │   └── <source>
│   │       └── <date as YYYY-MM-DD>
│   ├── 1_raw             <- The original, immutable data dump.
│   │   └── <experiment>
│   │       └── <conditions/replicate>
│   │           └── <date as YYYY-MM-DD>
│   ├── 2_processed       <- Intermediate data that has been standardized, formatted, deduped, etc.
│   │   └── <experiment>
│   │       └── <conditions/replicate>
│   │           └── <date as YYYY-MM-DD>
│   │
│   └── 3_tidy            <- The final, canonical datasets for analysis. Includes engineered features.
│       └── <experiment>
│
├── code
│   ├── data_processing  <- Code to process data from raw all the way to tidy.
│   │   └── <experiment>
│   │
│   ├── draft_analyses   <- Code that operates on tidy data for draft data analytics and visualizations.
│   └── final_analyses   <- Code that operates on tidy data to produce text, figures and tables as they appear in pubilcations.
│
├── output
│   ├── draft_analyses  <- Tables and figures from the draft analytics
│   │   └── <experiment>
│   │
│   └── final_analyses  <- Tables and figures from the final analytics
│
├── docs                <- Data dictionaries, manuals, and all other explanatory materials.
│
├── Dockerfile          <- Use docker build to build Docker container based on this file
├── deps.R              <- Import packages not used elsewhere to help renv
├── renv.lock           <- Lockfile with all dependencies managed by renv
├── renv                <- Package dependency management directory with renv
│
└── publication                      
    └── journal                      <- Journal that this was submitted to
        └── submission-1_YYYY-MM-DD  <- All materials of submission 1
            ├── docs                 <- All documents for submission
            ├── figures              <- All figures for submission
            └── tables               <- All tables for submission


```

## Code structure

All code follows the following structure.

```         
├── Title
│   ├── Inputs          <- Define the input sources.
│   └── Outputs         <- Define the outputs.
│
├── Setup
│   ├── Import          <- Import modules.
│   ├── Parameters      <- Input parameters (e.g., data definitions)
│   ├── Configs         <- Input any configurations (e.g., source data, % sampled).
│   └── Functions       <- Define all functions.
│
├── Read
│   ├── Import          <- Import data.
│   └── Conform         <- Conform data to a format appropriate for analysis.
│
├── Compute
│   └── Compute - <Analysis type>   <- Compute descriptive statistics, visualize, analyze.
│       └── <Analysis subtype>      <- Analysis subtype (if applicable; e.g., histograms).
│
└── Write
    ├── Conform         <- Conform data to a format appropriate for storage.
    └── Export          <- Write/push/sink data to a storage service.
```

## How to get the data

As of the time of writing, these are on a Share Drive on Google Drive [here](https://drive.google.com/drive/u/1/folders/0AHwZeCcC1chbUk9PVA).

## How to run

### From source

1.  Fork this repo to your GitHub profile.
2.  Clone the forked repo locally (e.g., your own laptop).
3.  Click on the .Rproj file (make sure you've already installed R and RStudio).
4.  In the Console, run the following code to install all dependencies: `renv::restore()`.
5.  Get all published figures and tables by executing `code/final_analytics/paper-from-code.Rmd`.

For all other code, use the following diagrammatic acyclic graph (DAG). Note that this applies to each experiment. Note that you need to combine all resources first into one repository to run this.

![](https://github.com/serghiou/centrosomal-calcineurin/blob/main/how-to-run.jpg?raw=true)

### From the Dockerfile

To build and run the Docker container, use the following commands in your terminal, executed in the directory containing your Dockerfile (note that Docker needs to be installed and running before you run these commands in your terminal - also, you need to make sure that you have the image by running the following in your terminal: `docker pull rocker/r-ver:4.2.3`):

``` sh
docker build -t calcineurin_image .
docker run calcineurin_image
```

Then, get the container ID by looking underneath the container name or running

``` sh
docker ps -a
```

Finally, retrieve the output:

``` sh
docker cp -a 355b7a4764f6:/project/code/final_analytics/ code/final_analytics/docker
```

or

``` sh
docker cp 355b7a4764f6:/project/code/final_analytics/paper-from-code.html code/final_analytics/paper-from-code_docker.html
```

## How to get help

If you encounter a bug, please file an issue with a minimal reproducible example [here](https://github.com/serghiou/centrosomal-calcineurin/issues) and please Label it as a "bug" (option on the right of your window). For help on how to use the package, please file an issue with a clearly actionable question [here](https://github.com/serghiou/centrosomal-calcineurin/issues) and label it as "help wanted." For all other questions and discussion, please email the first author.

## How to contribute

1.  Create an issue as described above.
2.  Create a branch from the issue as described [here](https://docs.github.com/en/issues/tracking-your-work-with-issues/creating-a-branch-for-an-issue).
3.  Branch names should use the format and voice of this example: "152-bugfix-fix-broken-links".
4.  Issue a pull request to initiate a review.
5.  Merge using "Rebase and merge" after you've squashed all non-critical commits.

## Be a good citizen

If you like or are reusing elements of this repo, please give a star!
