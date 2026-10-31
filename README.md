# Ex.No: 02 LINEAR AND POLYNOMIAL TREND ESTIMATION
Date: 31-10-2026
### AIM:
To implement Linear Trend Estimation and Polynomial Trend Estimation using Python.

### Dataset Name : AirPassenger

### ALGORITHM:
1. Import the required libraries (Pandas, NumPy, and Matplotlib).
2. Load the AirPassengers dataset.
3. Convert the Month column into Date-Time format.
4. Remove missing values, if any.
5. Calculate the Linear Trend using the Least Squares Method.
6. Calculate the Polynomial Trend (Degree 2) using the Least Squares Method.
7. Display the trend equations.
8. Plot the Linear Trend graph.
9. Plot the Polynomial Trend graph.
10. End the program.

### PROGRAM:
A - LINEAR TREND ESTIMATION
```python
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt

df = pd.read_csv("AirPassengers.csv")

df["Month"] = pd.to_datetime(df["Month"])
df = df.dropna(subset=["#Passengers"])

df = df.reset_index(drop=True)

period = df["Month"]
passengers = df["#Passengers"].tolist()

n = len(passengers)

X = [i - n//2 for i in range(n)]
x2 = [i**2 for i in X]
xy = [i*j for i, j in zip(X, passengers)]

b = (n*sum(xy) - sum(passengers)*sum(X)) / (n*sum(x2) - (sum(X)**2))
a = (sum(passengers) - b*sum(X)) / n

linear_trend = [a + b*X[i] for i in range(n)]

print("Linear Trend Equation")
print(f"y = {a:.2f} + ({b:.2f})X")

plt.figure(figsize=(12,6))
plt.plot(period, passengers, marker='o', label="Passengers")
plt.plot(period, linear_trend, 'k--', linewidth=2, label="Linear Trend")

plt.title("Linear Trend Estimation")
plt.xlabel("Month")
plt.ylabel("Passengers")
plt.legend()
plt.grid(True)
plt.show()
```

B- POLYNOMIAL TREND ESTIMATION
```python
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt

df = pd.read_csv("AirPassengers.csv")

df["Month"] = pd.to_datetime(df["Month"])
df = df.dropna(subset=["#Passengers"])

df = df.reset_index(drop=True)

period = df["Month"]
passengers = df["#Passengers"].tolist()

n = len(passengers)

X = [i - n//2 for i in range(n)]
x2 = [i**2 for i in X]
xy = [i*j for i, j in zip(X, passengers)]

x3 = [i**3 for i in X]
x4 = [i**4 for i in X]
x2y = [i*j for i, j in zip(x2, passengers)]

coeff = [
    [n, sum(X), sum(x2)],
    [sum(X), sum(x2), sum(x3)],
    [sum(x2), sum(x3), sum(x4)]
]

Y = [
    sum(passengers),
    sum(xy),
    sum(x2y)
]

A = np.array(coeff)
B = np.array(Y)

a_poly, b_poly, c_poly = np.linalg.solve(A, B)

poly_trend = [
    a_poly + b_poly*X[i] + c_poly*(X[i]**2)
    for i in range(n)
]

print("Polynomial Trend Equation")
print(f"y = {a_poly:.2f} + ({b_poly:.2f})X + ({c_poly:.2f})X²")

plt.figure(figsize=(12,6))
plt.plot(period, passengers, marker='o', label="Passengers")
plt.plot(period, poly_trend, 'r--', linewidth=2, label="Polynomial Trend")

plt.title("Polynomial Trend Estimation")
plt.xlabel("Month")
plt.ylabel("Passengers")
plt.legend()
plt.grid(True)
plt.show()
```
### OUTPUT
A - LINEAR TREND ESTIMATION
<img width="971" height="563" alt="image" src="https://github.com/user-attachments/assets/fb6bc7c0-b246-4666-af81-c9274b4adbf0" />


B- POLYNOMIAL TREND ESTIMATION
<img width="972" height="567" alt="image" src="https://github.com/user-attachments/assets/0a2f8ab7-f433-479d-a194-3f562a8d7c55" />


### RESULT:
Thus, the Python program for Linear Trend Estimation and Polynomial Trend Estimation using the Least Squares Method was implemented and executed successfully, and the corresponding trend graphs were obtained.
