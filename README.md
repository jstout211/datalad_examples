# Quick datalad_examples
Full website for much better examples and documentation <br>
https://www.datalad.org/

# What is Datalad
Datalad is a mix of git and git-annex <br>
Git has trouble with large datasets.  A hash is performed on each file, and results in a unique result <br>
This hashing is slow on larger files, so git-annex was created.  This creates symlinks to the data, which can be locked/unlocked for changes. <br>
Datalad is an easy wrapper around this, with upload/download features to major storage companies AWS/OpenNeuro/...

## Create an environment and install datalad
```
# If mamba is not installed::  conda install -n base mamba -y 
mamba create -n dataladENV conda-forge::datalad -y 
conda activate dataladENV 
```

# check out openneuro
https://openneuro.org/

# Pulling some example data with Datalad
```
datalad install https://github.com/OpenNeuroDatasets/ds004215.git
cd ds004215 
find ./ -name '*T1w.nii.gz'    #Pull all the T1s 
datalad get $(find ./ -name '*T1w.nii.gz') 

## Look at different versions of the data
git tag   # List the different versions 
git checkout 1.0.2 
```

# Datalad storage for new data
```
mkdir TESTdatalad  
cd TESTdatalad 
mkdir data 
cp $(locate *.nii | head -2) ./data  
ls ./data
```
```
datalad create #This won't work as is, unless empty

datalad create --force  
datalad status 
datalad save 
```
## Combining Code with datalad
```
git submodule add https://github.com/jstout211/datalad_examples.git code 
datalad status 
datalad save 
```
```
echo '#!/bin/bash' > ./code/testcode.sh 
echo 'for i in ./data/*; do fname=$(basename ${i}); cp ${i} ./data/NEW_${fname} ; done' >> ./code/testcode.sh 
chmod +x ./code/testcode.sh 

#New code -- check this into git and datalad <br>
datalad status 
cd code 
git add testcode.sh 
git commit -m 'New' 
cd .. 
datalad status 
datalad save 
```

## Run your code 
```
./code/testcode.sh 

#The datalad repository has now changed 
datalad status 

#Now the code and new data will be saved together
datalad save 

## What if I want to go back to a previous version of the data
git log 
git checkout <<PUT the hash ID>> 
```


## Datalad Unlock
```
cd data 
ls -a 
datalad unlock * 
ls -a 
```

## Python interface
These can be embedded into your code, so that the outputs can be saved at runtime <br>
```
#%% Test data setup
data_server = os.environ['MEG_DATA_SERVER']  #Get the server name or network address from a bash environmental variable
testdata = f'{data_server}:/home/git/testdata'

import datalad.api as dl
dl.clone(testdata, './TEST_DATA')
dl.get('./TEST_DATA')

```

## Upload to a git server (NOT GITHUB)
#datalad create --force
#datalad save
datalad siblings-create -s <NAME>  <USERNAME@MEG_SERVER:Folder> 
datalad push --to <NAME>

## Remove datalad tracking
```
ls -a 

datalad unlock   ## This has to be done or you will remove all of your data  <br>
rm -rf .git*  .datalad* 

Now you are back to just a regular dataset (no datalad tracking)
```

# Example of reproducible usage for other purposes --- automated test data
https://github.com/nih-megcore/TEST_ctf_data



