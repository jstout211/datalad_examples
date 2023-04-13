# datalad_examples

## Create an environment and install datalad
mamba create -n dataladENV datalad -y <br>
conda activate dataladENV <br>


## Pulling data
datalad install https://github.com/OpenNeuroDatasets/ds004215.git <br>
cd ds004215 <br>
find ./ -name '*T1w.nii.gz'    #Pull all the T1s <br>
datalad get $(find ./ -name '*T1w.nii.gz') <br>

## Look at different versions of the data
git tag   # List the different versions <br>
git checkout 1.0.2 <br>

## Datalad storage for new data
mkdir TESTdatalad  <br>
cd TESTdatalad <br>
mkdir code <br>
mkdir data <br>
cp $(locate *.nii | head -2) ./data  <br>
ls ./data <br><br>
datalad create #This won't work as is <br>
datalad create --force  <br>
datalad status <br>
datalad save <br>

## Combining Code with datalad
echo '#!/bin/bash' > ./code/testcode.sh <br>
echo 'for i in ../data/*; do cp ../data/${i} ../data/NEW_${i} ; done' >> ./code/testcode.sh <br>
chmod +x ./code/testcode.sh <br>

## Upload to a git server (NOT GITHUB)
datalad siblings-create

## Datalad Unlock
cd data <br>
ls -a <br>
datalad unlock * <br>
ls -a <br>

## Python interface
These can be embedded into your code, so that the outputs can be saved at runtime

## Remove datalad tracking 
ls -a <br>

datalad unlock   ## This has to be done or you will remove all of your data  <br>
rm -rf .git*  .datalad* <br><br>

Now you are back to just a regular dataset (no datalad tracking) <br>

# Reproducible usage for other purposes --- automated test data
https://github.com/nih-megcore/TEST_ctf_data



