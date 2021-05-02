# Notes Based on Gitbook

The setup of gitbook on github is based on [link](https://medium.com/@richdayandnight/simple-tutorial-on-hosting-your-gitbook-documentation-on-github-pages-bonus-with-gitbook-editor-f27f60d5d408)  
**Note 1:** need to change all "master" on  this webpage to "main" due to BLM  
**Note 2:** I stopped at Step 9 on this webpage. Instead, I did the following:

> Step 1: create a repository at GitHub  
> Step 2: clone the GitHub repository to a local directory.  
>   run some code in the Shell:  
>   git clone https://github.com/QingLu-USF/myrepo.git  
>   cd myrepo  

> Step 3: install NPM at [link](https://www.npmjs.com/get-npm) (**Note:** see note below on what to install and how to resolve some issues.)     
> Step 4: Install gitbook-cli by running "npm install -g gitbook-cli"   
>
> gitbook init   
> npm init  
> gitbook install  
> gitbook build  
> git add .  
> git commit -m 'some message'  
> git pull  
> git push -u origin main  
> git subtree push --prefix=\_book origin gh-pages  

The online book can be viewed at https:\/\/*Github-Usnername*.github.io\/*Repo-Name*  

For example, The online book for this repo can be viewed at [link](https://qinglu-usf.github.io/ITDSCE/) 


If the files in the local directory are updated, run the following to update the contents on GitHub (and therefore the webpage):  
> gitbook build  
> git add .   
> git commit -m 'some message'  
> git pull  
> git push -u origin main  
> git subtree push --prefix=\_book origin gh-pages  

## **Note on installing NPM**  
After I installed gitbook-cli using "npm install -g gitbook-cli" and ran "gitbook help", I got an error message. I did the following  
> In the shell, go to "C:\Users\qlu\AppData\Roaming\npm\node_modules\gitbook-cli\node_modules\npm\node_modules" and run  
> $ npm install graceful-fs@latest --save

based on the information at this [link](https://stackoverflow.com/questions/64211386/gitbook-cli-install-error-typeerror-cb-apply-is-not-a-function-inside-graceful)  
and it works. But then when I ran *"gitbook init"*, I got another error message:  
> "TypeError [ERR_INVALID_ARG_TYPE]: The "data" argument must be of type string or an instance of Buffer, TypedArray, or DataView. Received an instance of Promise".   
>

Based on the info at [link](https://stackoverflow.com/questions/61538769/gitbook-init-error-typeerror-err-invalid-arg-type-the-data-argument-must-b), I need to install an older version of node 12.18.1 LTS.  

I uninstalled the Node Version 14.16.1 and downloaded the installer for node version 12 at [Node Version 12](https://nodejs.org/download/release/latest-v12.x/) or [here](https://nodejs.org/en/download/releases/) and installed it. Then the "gitbook init" worked!  

However, next when I run "gitbook serve" I got another error message:  
> TypeError: cb.apply is not a function
>    at C:\Users\qlu\AppData\Roaming\npm\node_modules\gitbook-cli\node_modules\npm\node_modules\graceful-fs\polyfills.js:287:18
>    at FSReqCallback.oncomplete (fs.js:169:5)  


I did the following:  
> In the shell, go to "C:\Users\qlu\AppData\Roaming\npm\node_modules\gitbook-cli\node_modules\npm\node_modules" and run 
> $ npm install graceful-fs@4.2.0 --save

and the "gitbook serve" worked.





