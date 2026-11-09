![image](.attachments/ed96b8198a5ff5bd92a72d1d404bf78cc7c4b73b.png) 
![image](.attachments/2eca15373c3a1a9e24ac9ee65e3487a3b7c141f9.png) 
![image](.attachments/0642e2ef304ee589335ed205b6bc54eef571d39f.png) 
![image](.attachments/10db18ea391544bb12604bd133737974353c4d69.png) 
![image](.attachments/b7896916ea04c4fd0a982a56337bc8f5874277c7.png) 
- these are the weights for logistic regression
- ![image](.attachments/8b4649bfb4a4251982fda67ca1d78b162d1e7fe3.png)
- ![image](.attachments/7a462815ea342b928f39ee36ee4c277c63c8c590.png)
- bias and intercept
- ![image](.attachments/9c63e43ebcc9496c1089304c1ef3c86ea7c11c8d.png)
- ![image](.attachments/ff2d4f8428eb3ec27097bfac13680d166e8711ad.png)
- using the model
- ![image](.attachments/574987acc1e0db3a443da0429e490e553053aa64.png)
- 1 = churn
- ![image](.attachments/b76f2b63fa6feca5356d8465cae3609269b080bf.png)
- not just number (0 or 1), but a score
- ![image](.attachments/d32fa46ac642a64a86a18404a2b22df1da40318c.png)
- ![image](.attachments/b0fd78b447bf46d8dff930d3db8bff16fea6c8cb.png)
- ![image](.attachments/9b02b2c08a992ddf38f23e64b41dad191a6cda2a.png)
- ![image](.attachments/f455e09333094b3bb79a2d4a533bbdc475d643f3.png)
- ![image](.attachments/f455ade504d01f63ccc1648b6209200e5080b99d.png)
- ![image](.attachments/18a80ab7fa33d148ace874978a0316240f951250.png)
- ![image](.attachments/07a21877207cd007a54979ebcecf612fecf148a2.png)
- ![image](.attachments/c90b5ea82c10e2029c792f1fe31d557ba1503ae0.png)
- ![image](.attachments/6bef8b65c5fa180c7f143381e0bc58cef92a4d6d.png)
- It works because of **boolean masking**, which has three parts.

**1. `churn_decision` is a boolean array.**  
`model.predict_proba(X_val)[:, 1]` returns a NumPy array of churn probabilities, one per validation row. `y_pred >= 0.5` compares each value to the threshold and gives an array of `True`/`False` of the same length, for example `[False, False, False, True, ...]`.

**2. `df_val[churn_decision]` filters rows.**  
When you pass a boolean array the same length as the DataFrame into `[]`, pandas treats it as a row filter. It keeps the rows where the value is `True` and drops the rest. If you pass a string or list of strings instead, `[]` selects columns, so the type of what you pass decides which behaviour you get.

**3. `.customerid` pulls out one column.**  
Attribute access is shorthand for `["customerid"]`. It returns a Series of the customer IDs for the rows that survived the filter.

**Why the index reads 3, 8, 11, 12, 19 … 1408 and not 0, 1, 2 …:**  
Pandas keeps the original row labels when it filters. Row 3 of `df_val` was predicted to churn, so it appears with label 3. The `Length: 311` is the number of `True` values, which is about 22% of the ~1,409 validation rows. That is roughly the "25%" in the drawing: the customers who would get the promo email.

**Why the row positions line up:**  
The mask comes from `X_val`, which was built from `df_val` in the same row order. Position _i_ in `y_pred` is therefore the prediction for row _i_ of `df_val`. If you had shuffled one without the other, you would be filtering the wrong customers with no error.

**Fragility of `.customerid`:**  
Attribute access breaks if the column name has spaces or collides with a DataFrame method or attribute (`.count`, `.size`, and so on). More robust forms are `df_val.loc[churn_decision, "customerid"]` or `df_val[churn_decision]["customerid"]`.

- determining accuracy
- ![image](.attachments/d556393dcc78eadc5cafc8959e5323a23164a4c0.png)
- 80% predictions match!
- ![image](.attachments/c149ee4842448d2c767102dfe6953fc7062688c7.png)
- ![image](.attachments/fbb3ed76a7b8ade2c3180068f699c58c894bdc4e.png)
- ![image](.attachments/3bf4599af19a9ebed6c654667cec9811ea1dd5c9.png)
- ![image](.attachments/7a993eea8dcfda43d354cc0af22bb3272f3e5b1e.png)
- 