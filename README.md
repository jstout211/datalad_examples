# datalad_examples

## Create an environment and install datalad
mamba create -n dataladENV datalad -y
conda activate dataladENV


## Pulling data
datalad install https://github.com/OpenNeuroDatasets/ds004215.git <br>
cd ds004215 <br>
find ./ -name '*T1w.nii.gz'    #Pull all the T1s <br>
datalad get $(find ./ -name '*T1w.nii.gz') <br>

## Look at different versions of the data
git 


## Datalad storage
https://github.com/nih-megcore/TEST_ctf_data

mkdir TESTdatalad
cd TESTdatalad
cp $(locate *.nii | head -2) ./
datalad create 
datalad create --force
datalad status
datalad save
#


## Datalad Unlock
ln -s 


# Python interface
These can be embedded into your code


# Remove datalad tracking 
ls -a

datalad unlock   ## This has to be done or you will remove all of your data
rm -rf .git*  .datalad*


# Reproducible usage for other purposes --- automated test data
https://github.com/nih-megcore/TEST_ctf_data
