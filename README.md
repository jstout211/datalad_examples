# Quick datalad_examples
Full website for much better examples and documentation <br>
https://www.datalad.org/


## Create an environment and install datalad
mamba create -n dataladENV datalad -y <br>
conda activate dataladENV <br>

# THIS IS NOT SARCASM - check out openneuro
https://openneuro.org/

# Pulling data with Datalad
datalad install https://github.com/OpenNeuroDatasets/ds004215.git <br>
cd ds004215 <br>
find ./ -name '*T1w.nii.gz'    #Pull all the T1s <br>
datalad get $(find ./ -name '*T1w.nii.gz') <br>

## Look at different versions of the data
git tag   # List the different versions <br>
git checkout 1.0.2 <br>

# Datalad storage for new data
mkdir TESTdatalad  <br>
cd TESTdatalad <br>
mkdir data <br>
cp $(locate *.nii | head -2) ./data  <br>
ls ./data <br><br>
datalad create #This won't work as is <br>
datalad create --force  <br>
datalad status <br>
datalad save <br>

## Combining Code with datalad  -- this is a suboptimal test (code would typically be a git repo already and can be synced independently)
git submodule add https://github.com/jstout211/datalad_examples.git code <br>
datalad status <br>
datalad save <br>

echo '#!/bin/bash' > ./code/testcode.sh <br>
echo 'for i in ./data/*; do fname=$(basename ${i}); cp ${i} ./data/NEW_${fname} ; done' >> ./code/testcode.sh <br>
chmod +x ./code/testcode.sh <br>
<br>
#New code -- check this into git and datalad <br>
datalad status <br>
cd code <br>
git add testcode.sh <br>
git commit -m 'New' <br>
cd .. <br>
datalad status <br>
datalad save <br>

## Run your code 
./code/testcode.sh <br>
<br>
#The datalad repository has now changed <br>
datalad status <br>
#Now the code and new data will be saved together
datalad save <br><br>

## What if I want to go back to a previous version of the data
git log <br>
git checkout ----- <br>


## Datalad Unlock
cd data <br>
ls -a <br>
datalad unlock * <br>
ls -a <br>

## Python interface
These can be embedded into your code, so that the outputs can be saved at runtime <br>
https://github.com/nih-megcore/enigma_anonymization/blob/main/enigma_preupload/tests/OLD_test_enigma_anonymization.py <br>

## Upload to a git server (NOT GITHUB)
datalad siblings-create

## Remove datalad tracking 
ls -a <br>

datalad unlock   ## This has to be done or you will remove all of your data  <br>
rm -rf .git*  .datalad* <br><br>

Now you are back to just a regular dataset (no datalad tracking) <br>

# Reproducible usage for other purposes --- automated test data
https://github.com/nih-megcore/TEST_ctf_data



