# Sasha Main
# 06-Feb-2023 
# Purpose: To explore the curatedMetagenomicsData package in R.

## Load libraries
library(BiocManager)
library(dplyr)
library(DT)
library(ggplot2)

# Install the new package
#BiocManager::install("curatedMetagenomicData")
library(curatedMetagenomicData)

sampleMetadata |>
  filter(study_name == "AsnicarF_2017") |>
  select(where(~ !any(is.na(.x)))) |>
  dplyr::slice(1:10) |>
  dplyr::select(1:10) |>
  datatable(options = list(dom = "t"), extensions = "Responsive")

View(sampleMetadata)
dim(sampleMetadata) #20533   136
str(sampleMetadata)
unique(sampleMetadata$disease) #132 different diseases...

hmp_ibd_meta <- sampleMetadata[sampleMetadata$study_name == "HMP_2019_ibdmdb", ]

get_abun_data <- function(meta_df, data_type) {
  
  abun_data_df <- returnSamples(sampleMetadata[sampleMetadata$sample_id %in% meta_df$sample_id, ],
                                data_type)
  
  as.data.frame(t(as.matrix(abun_data_df@assays@data@listData[[data_type]])))
  
}

genus_abun_df <- get_abun_data(hmp_ibd_meta, "relative_abundance")
pwy_abun_df <- get_abun_data(hmp_ibd_meta, "pathway_abundance")
