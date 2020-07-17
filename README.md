# Mapping old swiss communes to 2020 territorial boundaries

## "cw_commune2020.csv" 

This is a crosswalk file that can be used to map old, disappeared Swiss communes to their 2020 territorial equivalents. In this file the column "commune_ID" is the original OFS commune id number associated with the old, disappeared communes, while "commune2020_ID" represents the actual commune number of where the old commune has been merged or changed to. The old commune names "commune" is provided for reference only and should not be used as a unique key to map old to new communes.

## "crosswalk_commune.xlsx"

This is a slightly modified version of the ["Réperatoire official des communes Suisse"](https://www.bfs.admin.ch/bfs/fr/home/bases-statistiques/repertoire-officiel-communes-suisse.html), where I have renamed the columns and sheets into english and removed white spaces from column and sheet names. Up to date as of 13 January 2020.

Note that the crosswalk file is not exhaustive, and that mappings were added as cases were discovered during the course of my own research.

### Using the file

To harmonize any given commune-level dataset to their 2020 names and ID numbers the following steps can be used:
Please note that these steps are written according to how the crosswalk file is currently constructed, with my own naming conventions. If you prefer to use the original column names from the Swiss Federal Statistics office, please rename the columns in the crosswalk file so that they match accordingly.

1. In the unharmonized dataset, rename the column with the official commune ID number (often listed as "GDENR") to "commune_ID".
2. Merge the crosswalk file to this unharmonized dataset (e.g. left join) by "commune_ID".
3. Looking at the new merged dataset, check to see if any of the original commune numbers do not have a modern match by looking for missing values in the "commune2020_ID" column. If all old communes are correctly matched to 2020 communes, there should be no missing values in "commune2020_ID"
4. If there are missing values, find the original commune names that do not have a match ("commune") and find their current name and ID number using the "communes_disappeared" and the "communes2020" tables in the "crosswalk_commune.xlsx" file. Update the mapping file accordingly, and repeat steps 1-3.
5. When all old communes in the dataset have a corresponding match, aggregate (or "collapse") the variables of interest in the dataset on the commune2020_ID number to get the final harmonized dataset.

Please note that the old commune names ("commune") in the crosswalk file is listed purely as a reference and should not be used as a unique key to match 
old to new communes, as there can be discrepencies in how commune names are spelled or listed at different years 
in the past.  Only the old and new commune ID numbers should be used to map ("commune_ID --> commune2020_ID")

In exceptional cases, there are sometimes communes with no matches where you only have the old commune number, but you do not have the old commune name. When this is the case, the old commune name can be found by using the ["liste historisée des communes"](https://www.bfs.admin.ch/bfs/fr/home/bases-statistiques/repertoire-officiel-communes-suisse/liste-historisee-communes.html).  

As mentioned the crosswalk file only captures the cases in all the data that I've worked with, but it is not exhaustive. If anyone finds this file useful and finds new mappings to add to the crosswalk file, pull requests are welcome!

