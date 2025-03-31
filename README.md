# STPComplEx 
## Installation
Create a conda environment with pytorch and scikit-learn :
```
conda create --name tkbc_env python=3.7
source activate tkbc_env
conda install --file requirements.txt -c pytorch
```

Then install the kbc package to this environment
```
python setup.py install
```

## Datasets

To download the datasets, go to the ./tkbc/scripts folder and run:
```
chmod +x download_data.sh
./download_data.sh
```

GDELT dataset can be download [here](https://github.com/BorealisAI/de-simple/tree/master/datasets/gdelt) and rename the files without ".txt" suffix.

Once the datasets are downloaded, add them to the package data folder by running :
```
python tkbc/process_icews.py
python tkbc/process_yago.py
python tkbc/process_gdelt.py
```

This will create the files required to compute the filtered metrics.
After that, you can run `data_view.py` to check the current data structure.

## Reproducing results

Run the following commands to reproduce the results

```
CUDA_VISIBLE_DEVICES=0 python tkbc/learner.py --dataset ICEWS14 --model STPComplEx --rank 1594 --emb_reg 1e-1 --time_reg 1e-4 --x 0.1 --y 22977 

CUDA_VISIBLE_DEVICES=0 python tkbc/learner.py --dataset ICEWS05-15 --model STPComplEx --rank 886 --emb_reg 1e-1 --time_reg 1e-1  --x 0.1 --y 54117  

CUDA_VISIBLE_DEVICES=0 python tkbc/learner.py --dataset yago15k --model STPComplEx --rank 364 --no_time_emb --emb_reg 1e-1 --time_reg 1e-4
 --x 0.1 --y 42099
CUDA_VISIBLE_DEVICES=0 python tkbc/learner.py --dataset gdelt --model STPComplEx --rank 1256 --emb_reg 1e-5 --time_reg 1e-2  --x 0.005 --y 9754

```

## Acknowledgement
We refer to the code of [TPComplEx](https://github.com/Jinfa/TPComplEx) and [FTPComplEx](https://github.com/trungnnhcmue/FTPComplEx). Thanks for their contributions.
