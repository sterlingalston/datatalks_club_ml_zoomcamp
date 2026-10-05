![image](.attachments/4fd18fb220a414c180773baf8847fd257d284ef4.png) 
![image](.attachments/1ee2e7b191a7719b07794aea8c75e0c4811ae555.png) 
![image](.attachments/770024cb521590921d40f752ebfd9bfcd53c8bea.png) 
![image](.attachments/d9d569a127bc347007f223c48d6e93ec927eb4dd.png) 
![image](.attachments/f6b42a57580666997b05bdb8c710f901abe97c10.png) 
![image](.attachments/1e7802235ee96bbcb7be4734b2ccd2f28c7cfb39.png) 
- fill missing values with 0 to make model ignore features
- ![image](.attachments/08a0ab1119bd0f096f688f81c61c830bc842c69d.png)
- zero not always best way to deal with missing variables
- ![image](.attachments/dc2cc020bf2c46f26f1c99d11b5711a7556017ab.png)
- maybe replacing hp with '0', doesn't make sense, but for machine learning it can sometimes be practical
- ![image](.attachments/e1c54a1d25ce9cf14ea5c07cd5f0151e58f67a91.png)
- `y_train `in lesson 2.2

```
import numpy as np

# 1. Split the dataset (60% train, 20% val, 20% test)
n = len(df)
n_val = int(0.2 * n)
n_test = int(0.2 * n)
n_train = n - (n_val + n_test)

# Shuffle indices
idx = np.arange(n)
np.random.seed(2)
np.random.shuffle(idx)

# Create split DataFrames
df_train = df.iloc[idx[:n_train]].copy()
df_val = df.iloc[idx[n_train:n_train+n_val]].copy()
df_test = df.iloc[idx[n_train+n_val:]].copy()

# Reset indices
df_train = df_train.reset_index(drop=True)
df_val = df_val.reset_index(drop=True)
df_test = df_test.reset_index(drop=True)

# 2. Extract and transform the target variable (MSRP/Price)
y_train = np.log1p(df_train.msrp.values)
y_val = np.log1p(df_val.msrp.values)
y_test = np.log1p(df_test.msrp.values)

# 3. Remove target column from features so the model doesn't leak target data
del df_train['msrp']
del df_val['msrp']
del df_test['msrp']
```
- ![image](.attachments/72bf6c3bbb2f79abfaa4745398d55fbd10e32853.png)
- see if the predictions are similar
- ![image](.attachments/0a786006216c6708a7b821ea4ab64e0d5d95211e.png)
- model not ideal, but need to have objective way to see if model is good
