# Ex.No: 02 LINEAR AND POLYNOMIAL TREND ESTIMATION

# Date: 25/07/2026

# Dataset : MICROSCOFT STOCK

### AIM:

To Implement Linear and Polynomial Trend Estiamtion Using Python.

### ALGORITHM:

Import necessary libraries (NumPy, Matplotlib)

Load the dataset

Calculate the linear trend values using least square method

Calculate the polynomial trend values using least square method

End the program

### PROGRAM:

```

import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
data = pd.read_csv('/content/Microsoft_Stock.csv')
data['Date'] = pd.to_datetime(data['Date'])
data.set_index('Date', inplace=True)
yearly = data['Close'].resample('YE').mean().to_frame()
yearly.index = yearly.index.year
years = yearly.index.tolist()
close = yearly['Close'].tolist()
X = [i - years[len(years)//2] for i in years]
n = len(X)
x2 = [i**2 for i in X]
xy = [i*j for i, j in zip(X, close)]
b = (n*sum(xy)-sum(close)*sum(X))/(n*sum(x2)-(sum(X)**2))
a = (sum(close)-b*sum(X))/n
linear = [a+b*x for x in X]
x3 = [i**3 for i in X]
x4 = [i**4 for i in X]
x2y = [i*j for i,j in zip(x2,close)]
A = np.array([
    [n,sum(X),sum(x2)],
    [sum(X),sum(x2),sum(x3)],
    [sum(x2),sum(x3),sum(x4)]
])
B = np.array([
    sum(close),
    sum(xy),
    sum(x2y)
])
a2,b2,c2 = np.linalg.solve(A,B)
poly = [a2+b2*x+c2*(x**2) for x in X]
print("Trend Equations\n")
print(f"Linear Trend: y={a:.2f} {'+' if b>=0 else '-'} {abs(b):.2f}x")
print(f"\nPolynomial Trend: y={a2:.2f} {'+' if b2>=0 else '-'} {abs(b2):.2f}x {'+' if c2>=0 else '-'} {abs(c2):.2f}x²")
plt.figure(figsize=(7,5))
plt.plot(years, close,
         color='blue',
         marker='o',
         linewidth=2,
         label='Actual')
plt.plot(years, linear,
         color='black',
         linestyle='--',
         linewidth=2,
         label='Linear Trend')
plt.title("Linear Trend Estimation")
plt.xlabel("Year")
plt.ylabel("Close Price")
plt.legend()
plt.grid(False)
plt.show()
plt.figure(figsize=(7,5))
plt.plot(years, close,
         color='blue',
         marker='o',
         linewidth=2,
         label='Actual')
plt.plot(years, poly,
         color='black',
         linestyle='--',
         linewidth=2,
         label='Polynomial Trend')
plt.title("Polynomial Trend Estimation (Degree 2)")
plt.xlabel("Year")
plt.ylabel("Close Price")
plt.legend()
plt.grid(False)
plt.show()

```

### OUTPUT

<img width="777" height="702" alt="image" src="https://github.com/user-attachments/assets/949d0cf8-97a9-424b-8344-5284f8964e62" />

<img width="772" height="602" alt="image" src="https://github.com/user-attachments/assets/07c78761-26e5-43d6-a54b-fdf831be3598" />


### RESULT:

Thus the python program for linear and Polynomial Trend Estiamtion has been executed successfully.
