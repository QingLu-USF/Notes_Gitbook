# Writing R Packages  

## Writing R Packages in RStudio  

**Step 1:** Install two packages for package development tools (*devtools*) and writing documentation (*roxygen2*). 

> install.packages("devtools")  
> install.packages("roxygen2")  

**Step 2:** Create an R Project in a directory on your computer  
In the R project folder, create some .R script files that contain the functions you want to have in your package, along with comments that will be used to create the help files. Below is one example of a customized .R script file that contains two function definitions.

> #' Stress Unit Conversion from psi to MPa
> #' 
> #' Convert stress in PSI to stress in MPa
> #' @param PSI The stress in psi
> #' @return The stress in MPa
> #' @examples 
> #' stress1 <- PSI_to_MPa(100);
> #' stress2 <- PSI_to_MPa(c(40,60,800));
> #' @export
> PSI_to_MPa <- function(PSI){
>   MPa <- PSI*0.00689476;
>   return(MPa);
> }
> 
> #' Stress Unit Conversion from MPa to psi
> #' 
> #' Convert stress in MPa to stress in psi
> #' @param MPa The stress in MPa
> #' @return The stress in psi
> #' @examples 
> #' stress1 <- MPa_to_PSI(0.7);
> #' stress2 <- MPa_to_PSI(c(0.4, 0.6, 0.8));
> #' @export
> MPa_to_PSI <- function(MPa){
>   PSI <- MPa*145.038;
>   return(PSI);
> }
> 

**Step 3:** Run the following codes in the Console while the working directory is where the R project is.

> library(roxygen2); # Read in the roxygen2 R package  
> roxygenise();      # Builds the help files  
> 
