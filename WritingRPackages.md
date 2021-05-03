# Writing R Packages  

## Writing R Packages in RStudio  

**Step 1:**  Create a new package in RStudio by clicking " **File -> New Project -> New Directory -> R Package** ", check "Create a git repository". The "Open in a new session" may also be checked.  

Create some R script files in the folder "R". The format of the comment for functions defined in the files should follow the examples later on this page.  


### To create data set files:  

**Approach 1:**  
  1. First create a folder "Data" in the package directory;   
  2. Save data variable into the "Data" folder with the following R code:  
  ```r
  save(DataSetName,file="DataSetName.RData")  
  ``` 

Note: after the package is loaded by library(package name), the data set can be accessed via the name DataSetName. One file contains a single object with the same name as the file.  

**Approach 2:**  
In the R project directory, run the following codes:
```r
install.packages("devtools")  
library(devtools)  
use_data(DataSetName)
```

See more details on including data sets in the R package at https://r-pkgs.org/data.html   

### To create documentation for a data set file:  

1. In RStudio, select "**File -> New File -> R Documentation...**"  
2. In the popup windown, enter the data set file name in the "Topic name" textbox, and select "Dataset" as Rd template.  

See more details on dataset documentation at https://r-pkgs.org/data.html and https://cran.r-project.org/doc/manuals/R-exts.html#Documenting-data-sets  
<br/><br/>

After the data files and R script files are created, to create the R package, in the Console, run:  
> library(roxygen2)  
> roxygenise()  
> 

**Step 2:**  Stage and commit  
* Click the “Git” tab in upper right pane
* Check “Staged” box for all files you want to commit.
    - Default: stage everything
    - When to do otherwise: this will all go to GitHub. So consider if that is appropriate for each file. You can absolutely keep a file locally, without committing it to the Git repo and sending to GitHub. Just let it sit there in your Git pane, without being staged. No harm will be done. If this is a long-term situation, list the file in .gitignore.
* If you’re not already in the Git pop-up, click “Commit”
* Type a message in “Commit message”.
* Click “Commit”  

**Step 3:**  Make and connect a GitHub repo  

*Make a new repo on GitHub*  
1. Go to https://github.com and make sure you are logged in.  
2. Click the green “New repository” button. Or, if you are on your own profile page, click on “Repositories”, then click the green “New” button.  
3. Pick a repository name – it should probably match the name of your local Project and directory.    
   * Public or private, as appropriate  
   * DO NOT initialize this repository with a README.  
4. Click the big green button “Create repository.”  
5. Copy the HTTPS clone URL to your clipboard via the green “Clone or Download” button.   

*Connect local repo to GitHub repo*  
Click on the “two purple boxes and a white square” in the Git pane. Click “Add remote”. Paste the URL here and pick a remote name, almost certainly origin. Now “Add”.  

We should be back in the “New Branch” dialog (if not, click on the “two purple boxes and a white square” in the Git pane again). I assume you’re on the master branch want it to track master on GitHub. Enter master as the branch name and make sure “Sync branch with remote” is checked. Click “Create” (yes, even though the branch already exists). In the next dialog, choose “overwrite”.  

# To install a package from Github: #  
Run the following codes:  
> install.packages("devtools")  
> library(devtools)  
> install_github("username/packagename")  [e.g.,  install_github("QingLu-USF/FirstTry")]   
> library(packagename)  
> 

# To install an updated package from Github: #
1. First uninstall and detach the installed package by running:  
> remove.packages("packagename")  
> detach("package:packagename", unload = TRUE)    
>

  - The R session may be re-started by running:  
    > .rs.restartR()  
    > 

2. repeat the above codes:  
> install_github("username/packagename")  [e.g.,  install_github("QingLu-USF/FirstTry")]   
> library(packagename)  
> 


# Useful links that were referred to:  
1. https://happygitwithr.com/existing-github-last.html  
2. https://kbroman.org/pkg_primer/pages/github.html  
3. https://r-pkgs.org/index.html  
4. https://ourcodingclub.github.io/tutorials/writing-r-package/  

# Below procedures were followed previously but seemed to be unnecessary. However, the format of the comments for the R script file is useful.  


Note:  the following notes are based on the content at [link](https://ourcodingclub.github.io/tutorials/writing-r-package/).

**Step 1:** Install two packages for package development tools (*devtools*) and writing documentation (*roxygen2*). 

> install.packages("devtools")  
> install.packages("roxygen2")  

**Step 2:** Create an R Project in a directory on your computer  
In the R project folder, create a folder named "R". **In this "R" folder**, you may create some .R script files that contain the functions you want to have in your package, along with comments that will be used to create the help files. Below is one example of a customized .R script file that contains two function definitions.

``` 
  #' Stress Unit Conversion from psi to MPa  
  #'   
  #' Convert stress in psi to stress in MPa  
  #' @param PSI The stress in psi  
  #' @return The stress in MPa  
  #' @examples   
  #' stress1 <- PSI_to_MPa(100);  
  #' stress2 <- PSI_to_MPa(c(40,60,800));  
  #' @export  
      PSI_to_MPa <- function(PSI){  
        MPa <- PSI*0.00689476;  
        return(MPa);  
        }  
  
  #' Stress Unit Conversion from MPa to psi  
  #'   
  #' Convert stress in MPa to stress in psi  
  #' @param MPa The stress in MPa  
  #' @return The stress in psi  
  #' @examples   
  #' stress1 <- MPa_to_PSI(0.7);  
  #' stress2 <- MPa_to_PSI(c(0.4, 0.6, 0.8));  
  #' @export  
      MPa_to_PSI <- function(MPa){  
        PSI <- MPa*145.038;  
        return(PSI);  
        }
```  

**Step 3:** Create a DESCRIPTION file in the R project directory (**Note:** not the "R" folder), which is a plain text file without extension.  This file will hold some of the meta-data on the R package.  
For example, something like the following:  

> Package: FirstTry  
> Type: Package  
> Title: Some function definitions and data sets for Demonstration  
> Version: 0.0.1.0  
> Encoding: UTF-8  
> 

**Step 4:** Run the following codes in the Console while the working directory is where the R project is.

> library(roxygen2); # Read in the roxygen2 R package  
> roxygenise();      # Builds the help files  
> 
