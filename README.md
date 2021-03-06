Package includes functions to manipulate sample patient data for demographic data, biopsy results, PSA results, and surgical results for patients with low grade prostate cancer. Includes functions to prepare these data for analysis in RJAGS, as well as sample results from the RJAGS model to show patients' risk of indolent cancer. Functions for model visualizations can be preformed on patients' predicted risk of indolent cancer, both at individual visit dates as well as through cumulitive prediction trajectories. 


1. Install package(s)

```r
# install.packages("devtools")
devtools::install_github("jbindman/prostate-project") 
```

2. Load in data from csv files for tx.data, demo.data, psa.data, bx.data, each of which must be saved locally. Combine these files into a more useful set of dataframes by calling fillPatientTables on the four files. The function will return three filled dataframes (pt.data, psa.data, bx.full) to the workflow in list called patientDataframes. 

```r
#demographic data. one record per patient
demo_data<-read.csv("julia-demo-data-IOP.csv")
names(demo_data)
#psa data. one record per PSA test per patient
psa_data<-read.csv("julia-psa-data-IOP.csv")
names(psa_data)
#bx.data. one record per biopsy per patient
bx_data<-read.csv("julia-bx-data-IOP.csv")
names(bx_data)
#surg.data. one record per treatment received per patient
surg_data<-read.csv("julia-surg-data-IOP.csv")
names(surg_data)
```

3. Organize data frames from clinical patient sources:

```r
ptDataframes <- ProstatePackage::fillPatientTables(demo_data, psa_data, bx_data, surg_data, IOP = TRUE)


inputPatient <- ProstatePackage::printIndividualData(198, ptDataframes)
```

4. Prepare data and arguments for RJAGS by calling RJAGS on a required text file required for RJAGS use, as well as the formatted list patient.Dataframes.

```r
jagsPrep <- RJAGSprep(ptDataframes, TRUE)
```

5. Execute RJAGS 

independently

6. Plot from predictions

```r
plotPtData(pt.id, what.data="both", log.scale=T, plot.psad=F)
plotBackgroundData(pt.id = 100, closest1000 = seq(1, 1000, by=1),  pt = ptDataframes, what.data="both", log.scale=TRUE, plot.psad=FALSE)
```


