### This is the online repository of smart contract vulnerability detection and localization.
## Task Definition

Detect and Localize reentrancy vulnerabilities in smart contract.

## Dataset

The dataset we use is [SmartBugs Wild Dataset](https://github.com/smartbugs/smartbugs-wild/tree/master/contracts) and filtered following the paper [Empirical Review of Automated Analysis Tools on 47,587 Ethereum Smart Contracts](https://arxiv.org/abs/1910.10601).

The tools analysis results we use is [Vulnerability Analysis of Smart Contracts using SmartBugs](https://github.com/smartbugs/smartbugs-results) and filtered following the paper [Empirical Review of Automated Analysis Tools on 47,587 Ethereum Smart Contracts](https://arxiv.org/abs/1910.10601).

### Data Format

1. dataset/data.jsonl is stored in jsonlines format. Each line in the uncompressed file represents one contract.  One row is illustrated below.

   - **contract:** the smart contract

   - **idx:** index of the contract
  
   - **address:** the smart contract's address

2. train.txt/valid.txt/test.txt provide examples, stored in the following format:    **idx	label**

## Example
We provide an example,line 40 is the vulneralbility statement and ranked 1st in the ranking list
```shell
cd demo
cd dataset
unzip data.zip
cd ..
python detect.py dev
cd saved_models
vim predictions.txt
vim programs.txt
```

## Dependency

- python version: python3.7.6
- pip install torch
- pip install transformers
- sudo apt install build-essential
- pip install tree_sitter
- pip install sklearn


## Vulnerability localization

```shell
cd contract_all
cd dataset
unzip dataset.zip
cd ..
python detect.py dev
```
### Get the result
We provide the result ranking list in txt form
```shell
cd contract_all
cd saved_models
vim predictions.txt
```

### Docker implementation
We also provide docker implementation
```shell
docker pull zz8477/ubuntu18.04:IA_contract
docker run -it --gpus all zz8477/ubuntu18.04:IA_contract /bin/bash

#run demo
cd /home/IA_contract_github/demo/
python detect.py dev
cd saved_models/
vim predictions.txt
vim programs.txt

#run whole project
cd /home/IA_contract_github/contract_all/
python detect.py dev
cd saved_models/
vim predictions.txt
```

## Result

Recall,Precision and F1 on the test set are shown as below:

| Method      |  Recall   | Precision |    F1     |
| ----------- | :-------: | :-------: | :-------: |
| Honeybadger |   50.55%  |   87.21%  |   50.85%  |
| Manticore   |   49.99%  |   49.72%  |   49.86%  |
| Mythril     |   51.78%  |   50.25%  |   49.75%  |
| osiris      |   53.91%  |   59.02%  |   55.42%  |
| Oyente      |   54.20%  |   65.64%  |   56.56%  |
| securify    |   54.92%  |   52.64%  |   53.40%  |
| Slither     |   65.79%  |   51.98%  |   52.62%  |
| smartcheck  |   70.88%  |   79.35%  |   74.39%  |
| DR-GCN      |   80.89%  |   72.36%  |   76.39%  |
| TMP         |   82.63%  |   74.06%  |   78.11%  |
| Vanilla-RNN |   58.78%  |   49.82%  |   50.71%  |
| LSTM        |   67.82%  |   51.65%  |   58.64%  |
| GRU         |   71.30%  |   53.10%  |   60.87%  |
| GCN         |   78.79%  |   70.72%  |   74.15%  |
| CGE         |   87.62%  |   85.24%  |   86.41%  |
| ReVulDL     | **93.29%**| **91.81%**| **92.54%**|

Ranking list on the test set are shown as below:
| Method      |   top-1   |   top-3   |   top-5   |   top_10  |   top_20  |    MFR    |    MAR    |
| ----------- | :-------: | :-------: | :-------: | :-------: | :-------: | :-------: | :-------: |
| ReVulDL     |   20.40%  |   44.05%  |   58.99%  |   70.38%  |   84.05%  |   4.87    |   5.70    |
