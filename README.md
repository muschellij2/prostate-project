# prostate-project
A single package synthesizing the work of Yates Coley

1. Install packages

install.packages("devtools")
devtools::install_github("jbindman/prostate-project") 

2. Load in data from csv files for tx.data, demo.data, psa.data, bx.data.To combine these files into a more useful set of dataframes, call fillPatientTables on the four files. The function will return three filled dataframes (pt.data, psa.data, bx.full) to the workflow in list called patientDataframes. 
   
3. Prepare data and arguments for RJAGS by calling RJAGS on the formatted list patientDataframes and the specific file name for the required accompanying RJAGS txt file.

4. Execute RJAGS 
