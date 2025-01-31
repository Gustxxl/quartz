# Меры изменчивости

### Демонтрация работы скрипта

![[Pasted image 20250130161654.png]]
Вывод:
![[Figure_1.png]]

___
### Разбор кода

### **1. Импорт библиотек**
```python
import numpy as np
import matplotlib.pyplot as plt
```
- **`numpy`** — библиотека для работы с массивами и выполнения математических операций.
- **`matplotlib.pyplot`** — модуль для построения графиков и визуализации данных.

---
### **2. Загрузка данных**
```python
file_path = "/Users/vladislavbalabaev/XXL/Code/learning/datasets/numbers.csv"
numbers = np.loadtxt(file_path, delimiter=",")
```
- **`file_path`** — путь к файлу с данными.
- **`np.loadtxt(file_path, delimiter=",")`** — загружает данные из CSV-файла в массив numpy.

---
### **3. Вычисление несмещенной выборочной дисперсии**
```python
n = len(numbers)
mean_value = np.mean(numbers)
sum_squared_deviations = np.sum((numbers - mean_value) ** 2)
sample_variance = sum_squared_deviations / (n - 1)
sample_variance_rounded = round(sample_variance)
print(f"Несмещенная выборочная дисперсия: {sample_variance_rounded}")
```
- **`np.mean(numbers)`** — вычисляет среднее значение.
- **`(numbers - mean_value) ** 2`** — вычисляет квадраты отклонений от среднего.
- **`np.sum(...)`** — суммирует квадраты отклонений.
- **`sample_variance = sum_squared_deviations / (n - 1)`** — делит сумму на (n-1), вычисляя несмещенную дисперсию.
- **Округление и вывод результата.**

---
### **4. Построение гистограммы распределения**
```python
plt.figure(figsize=(8, 5))
plt.hist(numbers, bins=30, edgecolor="black", alpha=0.7)
plt.xlabel("Значения")
plt.ylabel("Частота")
plt.title("Гистограмма распределения")
plt.grid(axis='y', linestyle='--', alpha=0.7)
plt.show()
```
- **`plt.hist(numbers, bins=30)`** — строит гистограмму с 30 столбцами.
- **`plt.xlabel(...)`, `plt.ylabel(...)`, `plt.title(...)`** — добавляют подписи.
- **`plt.grid(axis='y', linestyle='--', alpha=0.7)`** — добавляет сетку для удобства.
- **`plt.show()`** — выводит график.

---
### **Вывод**
Скрипт анализирует числовые данные и выполняет:
- Вычисление **несмещенной выборочной дисперсии**.
- Визуализацию распределения значений с помощью **гистограммы**.
