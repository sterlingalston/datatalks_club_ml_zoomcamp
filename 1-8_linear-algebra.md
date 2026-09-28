https://www.youtube.com/watch?v=zZyKUeOR4Gg&list=PL3MmuxUbc_hIhxl5Ji8t4O6lPAOpHaCLR&index=10

![image](.attachments/99c6025d8fba28e5c0d052d18d410d5bc47f5299.png) ![image](.attachments/331858fc5fceb253feb31143ab945139179a7bfe.png) 

![image](.attachments/e7b04e08c52bdf76aa811c725ccca5be0cf1fedf.png) 

- dot product produces a number
- ![image](.attachments/f02a67b48aa520069566638a18be91c7eb9f2e76.png)
- ![image](.attachments/639689bf2c04bef6bfb8131f2aa17fcf2f142012.png)
- ![image](.attachments/33104800269c3b1241524fd7ed88212ebd5fa495.png)
- ![image](.attachments/9fde981fb49dcec6871002a14933d3db5a6a33c7.png) 
- ![image](.attachments/ef82b1f55a8403c261367df2aa2d715cec26182a.png)
- matrix-vector -- you take each row in the matrix and multiply by the other vector
  - basically vector vector multiplication (dot-product)
- ![image](.attachments/99b13338e4a2c08278cd88527d9a85510f206100.png)
- ![image](.attachments/0940c0b7d8e2b358c71a820dbe06c3c94b4e2e64.png)
  - returns a vector with dot product in each row; same number of rows as the matrix
- ![image](.attachments/2b560f57c8342db9c758cf41e575ff6885b9c7e9.png)
- ![image](.attachments/af604decf586c59540bf4cea58f1dc944c9f95ad.png)
- ![image](.attachments/c57379c43d3d1610aa627cdbbcd8dabf7c7e2d7e.png)
- ![image](.attachments/418e9111563878e4161cf800c9bb0eef5f0cd479.png)
- ![image](.attachments/90812d871dd21824b594ffb6a9556edc149df7b4.png)
- identity matrix
- ![image](.attachments/7cf5f5242f62226f75222a75b6e888fa895cad57.png)
- ![image](.attachments/4d835fdba51e382b40d8178682adde8eb261029d.png)
- ![image](.attachments/d5de19e9781fc6f90ca753f297ab0d1206e23b8b.png)
- ![image](.attachments/3cdd3ed7618517abd9645ac71eea62a18e0eab5f.png)
- Python

```
import numpy as np

# Matrix A: 3 rows, 4 columns
A = np.ones((3, 4))
# Vector v: 4 rows (4x1)
v = np.ones((4, 1))

# Matrix-vector product
res = np.matmul(A, v)

print("A shape:", A.shape)
print("v shape:", v.shape)
print("Result shape:", res.shape)

```

Code output

```
A shape: (3, 4)
v shape: (4, 1)
Result shape: (3, 1)

```

Matrix multiplication dimensions follow the standard rule:

  

$$(m \times n) \cdot (n \times p) = (m \times p)$$

For this operation:

  

-   Matrix dimensions: $3 \times 4$ ($3 \text{ rows} \times 4 \text{ columns}$)
    
      
    
-   Column vector dimensions: $4 \times 1$ ($4 \text{ rows} \times 1 \text{ column}$)
    
      
    

Since the inner dimensions match ($4 = 4$), the multiplication is valid, and the result is defined by the outer dimensions:

  

$$(3 \times 4) \cdot (4 \times 1) = 3 \times 1$$

Multiplying a $3 \times 4$ matrix by a $4 \times 1$ vector indeed yields a vector of **3 rows**.

- inverse -- only squar matrices have inverses
- ![image](.attachments/6be160e0d2a7cacb7aa12ab88a4b86bd4fc57e82.png) 
- useful for linear regression!