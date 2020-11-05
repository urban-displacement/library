# Data Directory

In general, you should not store data on github except when the repo will be made public and certain files are necessary to execute the code. You should use Google Drive to store data in a `data` folder in the respective project folder. Then, use code to pull the data from Google Drive using their API. There's an R package [`googledrive`](https://github.com/tidyverse/googledrive) and a python package [`tbd`]() to do so.  

The reason is that Github allows only 2gb of storage on each repo and you can't upload a file larger than 100mb through `git push`. Because of these limitations, you should zip all your files and unzip them in the code.  
  
If you do store data on github, make sure to store it in a parent folder like the structure listed above. 

* The `raw` directory is where you store untouched data (e.g. imported or downloaded raw data). These files are usually used to create files that will go into your `output` folder. You never want to manipulate these so that you can revert back to the original file structure in case you need to start over. 
* The `output` directory is where you put data outputs that are created in the `data.r` or `data.py` scripts. These files will likely be used in the `analysis.r` or `analysis.py` scripts. 