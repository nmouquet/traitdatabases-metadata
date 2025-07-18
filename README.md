
# Trait databases: Metadata submission repo


<!-- badges: start -->
[![License CC BY 4.0](https://img.shields.io/badge/License-CC%20BY%204.0-green.svg)](https://creativecommons.org/licenses/by/4.0/)
![Lifecycle Experimental](https://img.shields.io/badge/Lifecycle-Experimental-339999)
<!-- badges: end -->


<p align="left">
• <a href="#overview">Overview</a><br> •
  <a href="#description">Description</a><br> • 
  <a href="#get-started">Get started</a><br> • 
  <a href="#contributing">Contributing</a><br> •
  <a href="#citation">Citation</a><br> •
  <a href="#acknowledgments">Acknowledgments</a><br> •
  <a href="#references">References</a>
</p>



## Overview

This repository is a bank centralizing metadata files describing various published trait databases.

Its content (folder `metadata/`) is used by the R package [`traitdatabases`](https://github.com/frbcesab/traitdatabases) to download, import, clean, and homogenize trait data.



## Description

The metadata file describes all information needed to document and process the trait database. It is structured in four sections:

- `status`: the status of the metadata file
- `dataset`: general metadata of the dataset
- `taxonomy`: information about taxonomic columns
- `traits`: description of the trait data



### Section `status`

| Tag name          | Description                                                                                                 | Example        |
| :---------------: | :---------------------------------------------------------------------------------------------------------- | :------------- |
| `status`          | The status of the metadata file. Should be one of:<br>- `draft`<br>- `incomplete` (some metadata need to be added)<br>-  `complete` (all metadata has been filled in) | `draft` |



### Section `dataset`

| Tag name          | Description                                                                                                 | Example        |
| :---------------: | :---------------------------------------------------------------------------------------------------------- | :------------- |
| `id`              | The dataset identifier[^1]. It's up to you to choose this identifier. Can be the name of the database, the first author and year, etc. | `hodgson_2023` |
| `title`           | The dataset title. Typically the title of the (data) paper. | "A functional trait database of arable weeds from Eurasia and North Africa" |
| `description`     | A short description of the dataset | "The functional traits of \[…\] for 928 arable weed species." |
| `license`         | The dataset license. | `CC BY-SA 4.0` |
| `bibtex`          | The name of the dataset citation file in a BibTex format (optional) | `hodgson_2023.bib` |
| `doi`             | The Digital Object Identifier (DOI) of the dataset description | `10.5287/ora-pp4y9nkoz` |
| `url`             | The URL of the dataset description (paper) | <https://ora.ox.ac.uk/objects/uuid:abafafd9-e8a2-4e84-a339-0a11bf2858ae> |
| `taxon`           | The taxonomic group (mammals, birds, etc.) | `plants` |
| `taxonomic_level` | The taxonomic resolution (individuals, species, genus, etc.) | `species` |
| `type`            | One of:<br>-  `static` (a file that can be downloaded)<br>- `api` (access data through a query) | `static` |
| `file_url`        | The full URL to download the static file.<br>**NB.** Equal to `.na` if `type: api` | <https://ora.ox.ac.uk/objects/uuid:abafafd9-e8a2-4e84-a339-0a11bf2858ae/files/s8p58pf68w> |
| `file_name`       | The name of the static file (with file extension).<br>**NB.** Equal to `.na` if `type: api` | `Functional+trait+database+of+arable+`<br>`weeds+from+Eurasia+and+`<br>`North+Africa.xlsx` |
| `file_extension`  | The file extension of the static file.<br>**NB.** Equal to `.na` if `type: api` | `.xlsx` |
| `manual_download` | Does the data file need to be manually downloaded? One of:<br>- `yes`: only for specific cases like data hosted by Wiley Online Library<br>- `no`: data file can be downloaded through command line (most cases)<br>- `.na`: if `type: api` | `no` |
| `sheet`           | The sheet number that contains data (only for `xslx` file)<br>**NB.** Equal to `.na` for non Excel file or if `type: api` | `1` |
| `long_format`     | Are the trait data in long format?. One of:<br>- `yes`: data are in long format<br>- `no`: data are in wide format (most cases)<br>- `.na`: if `type: api` | `no` |
| `skip_rows`       | The number of header rows to remove (if any) | `.na` |
| `col_separator`   | The character used to separate columns (for `txt` or `csv` files) | `.na` |
| `na_value`        | The characters used for missing values (if any) | `NA` |
| `comment`         | Any relevant comment (if any) | `.na` |

[^1]: The dataset identifier should be short and should only contain letters, numbers and the symbol `_`.



### Section `taxonomy`

| Tag name          | Description                                                                 | Example   |
| :---------------: | :-------------------------------------------------------------------------- | :-------- |
| `genus`           | The column name of the genus (when species and genus names are separated)   | `.na`     |
| `species`         | The column name of the species (when species and genus names are separated) | `.na`     |
| `binomial`        | The column name of the binomial name                                        | `Species` |




### Section `traits`

| Tag name   | Description                                                         | Example              |
| :--------: | :------------------------------------------------------------------ | :------------------- |
| `variable` | The column name of the trait (as in the data file)                  | `SLA`                |
| `name`     | The full name of the trait                                          | `Specific leaf area` |
| `category` | The category of the trait[^2]                                       | `Leaf morphology`    |
| `type`     | The type of the trait. One of:<br>- `quantitative`<br>- `categoric` | `quantitative`       |
| `units`    | The "original" unit of the trait (for quantitative trait only)      | `mm2.mg-1`           |

In the case of `categorical` traits, all categories should be listed with
two fileds: `value` and `description`. This information describes
each level of the categorical trait. For instance:

```yaml
- variable: VEGPROP      
  name: Vegetative propagation of perennials
  category: reproduction
  type: categorical      
  units: .na 
  levels: 
  - value: 1            
    description: yes
  - value: 0 
    description: no 
```



## Get started

> Follow this 6-step procedure to submit a metadata file for a new trait dataset.  

Before proceeding, make sure that the dataset you want to add is not
already in `traitdatabases-metadata`.

Also, have a look at the example from the [Hodgson et al. 2023](https://github.com/FRBCesab/traitdatabases-metadata/blob/main/metadata/hodgson_2023/hodgson_2023_metadata.yml) to understand which information is expected in each field.


#### 1. Fork this repository

Click on the Fork icon on the top right of this repository.

<figure>
<img src="doc/figures/fork-1.png" style="width:50.0%"
alt="click on ‘Create fork’" />
<figcaption aria-hidden="true">click on ‘Create fork’</figcaption>
</figure>


#### 2. Install the traitdatabases package

```r
## Install < remotes > package (if not already installed) ----
if (!requireNamespace(c("remotes", "here"), quietly = TRUE)) {
  install.packages(c("remotes", "here"))
}

## Install < traitdatabases > from GitHub ----
remotes::install_github("frbcesab/traitdatabases")
```

#### 3. Create a new metadata file

Choose the name of your dataset. Then, use the function
[`td_create_metadata_file`](https://frbcesab.github.io/traitdatabases/reference/td_create_metadata_file.html) as follow:

```r
traitdatabases::td_create_metadata_file(
  name = "hodgson_2023", # name of your dataset
  path = here::here("metadata")
)
```


#### 4. Complete the metadata

Depending on the format, open a text editor or excel to fill in the
metadata.

It is recommended to add a bibtex file with the citation information of
the trait database in the same folder as the metadata file.



#### 5. Check and commit changes

Double check that everything is complete, without errors. Finally,
update the status of the metadata file (‘complete’, or ‘incomplete’),
stage the new files and commit the changes.


#### 6. Make a pull request

This will contribute directly to the growth of the metadata on trait
databases. Your pull request will be reviewed in the shortest delay.  
Thank you for your contribution :)

## Contributing

All types of contributions are encouraged and valued. For more
information, check out our [Contributor
Guidelines](https://github.com/frbcesab/traitdatabases/blob/main/CONTRIBUTING.md).

Please note that the `traitdatabases-metadata` project is released with
a [Contributor Code of
Conduct](https://contributor-covenant.org/version/2/1/CODE_OF_CONDUCT.html).
By contributing to this project, you agree to abide by its terms.

## Citation

Please cite `traitdatabases` as:

> Casajus N, Coux C & Frelat R (2025) traitdatabases: An R package to
> compile trait databases. R package version 0.0.0.9000.
> <https://github.com/frbcesab/traitdatabases/>

## Acknowledgments

Coming soon…

<!-- Should we have automatic list of contributors that participated in one or more metadata? (e.g. Github bot?)-->

## References

Coming soon…

<!-- Should we have automatic list of metadata covered in the package?-->
