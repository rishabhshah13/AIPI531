# AIPI 531 F23 - Homework 3 Build a product recommender


## Objectives:

1. Train different session (contextual, sequential) based product recommendation recommenders for E-commerce use cases and compare the performances of the recommenders.
2. Include item and/or user features as side information for cold items/users.

## Requirements:
- Include item features as side information for cold items with the DRL recommenders mentioned in https://arxiv.org/abs/2111.03474 [DRL2]
- Include a performance comparison between the recommenders with and without item features.

## Datasets:
- Retailrocket, https://www.kaggle.com/datasets/retailrocket/ecommerce-dataset

## Pre-process

- Remove the 'timestamp' column from the item_properties dataframe and drop any duplicate rows
- Get a list of unique item IDs from the sorted_events dataframe
- Filter the item_prop dataframe to only include items that are in the item_list and drop any duplicate rows
- Select only static properties which is not affected by time
- droppig rows from item_prop where the 'property' is 'available' and the 'value' is '0'. This effectively removes any items that are not available.
- Create a new column in item_prop called 'prop_val' that is a combination of the 'property' and 'value' columns. 
- Made changes in code to use GPU instead of CPU which increases the speed of training

## Important Files
- SNQN Jupyter Notebook - SNQN.ipynb - https://github.com/rishabhshah13/AIPI531/blob/main/Homework/HW3/SNQN.ipynb 
- Preprocessing Notebook - https://github.com/rishabhshah13/AIPI531/blob/main/Homework/HW3/preprocessing_data.ipynb
- SNQN without features file SNQN_new.py - https://github.com/rishabhshah13/AIPI531/blob/main/Homework/HW3/kaggle/SNQN_new.py
- SNQN with features file SNQN_new_with_features.py - https://github.com/rishabhshah13/AIPI531/blob/main/Homework/HW3/kaggle/SNQN_new_with_features.py


## Results
Performance of Recommender with features and without features for clicks and puchases
### Without Features 
| Models      | HR@5      | NDCG@5    | HR@10     | NDCG@10   | HR@15     | NDCG@15   | HR@20     | NDCG@20   |
|-------------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|
| [CLICKS]    | 0.263258  | 0.203387  | 0.314447  | 0.219983  | 0.341673  | 0.227198  | 0.361114  | 0.231791  |
| [PURCHASE]  | 0.519751  | 0.437260  | 0.568324  | 0.453015  | 0.594406  | 0.459933  | 0.614251  | 0.464617  |


### With Features
|  lambda_value          | HR@5      | NDCG@5    | HR@10     | NDCG@10   | HR@15     | NDCG@15   | HR@20     | NDCG@20   |
|------------------------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|-----------|
| (lambda=0.1) [PURCHASE] | 0.255717  | 0.220330  | 0.285390  | 0.229856  | 0.301266  | 0.234081  | 0.311283  | 0.236437  |
| (lambda=0.1) [CLICKS]   | 0.107273  | 0.090943  | 0.120493  | 0.095217  | 0.128768  | 0.097402  | 0.133814  | 0.098596  |
| (lambda=0.2) [CLICKS]   | 0.109741  | 0.093468  | 0.122471  | 0.097577  | 0.130129  | 0.099607  | 0.135885  | 0.100969  |
| (lambda=0.2) [PURCHASE] | 0.258363  | 0.227042  | 0.278208  | 0.233413  | 0.290493  | 0.236654  | 0.302211  | 0.239430  |
| (lambda=0.5) [CLICKS]   | 0.102767  | 0.087199  | 0.115599  | 0.091354  | 0.123705  | 0.093495  | 0.129148  | 0.094784  |
| (lambda=0.5) [PURCHASE] | 0.241542  | 0.210101  | 0.270837  | 0.219610  | 0.283878  | 0.223066  | 0.294084  | 0.225473  |
