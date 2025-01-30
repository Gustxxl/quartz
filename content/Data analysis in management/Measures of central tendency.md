# Меры центральной тенденции
### Демонтрация работы скрипта

![[Pasted image 20250130150646.png]]
Вывод:
![[Pasted image 20250130150832.png]]

___
### Разбор кода
### **1. Импорт библиотек**
```python
import numpy as np
from scipy import stats
```
- **`numpy`** — библиотека для работы с массивами и выполнения математических операций.
- **`scipy.stats`** — модуль для статистического анализа, включая вычисление моды.

---
### **2. Загрузка данных**
```python
file_path = "/Users/vladislavbalabaev/XXL/Code/learning/datasets/numbers.csv"
numbers = np.loadtxt(file_path, delimiter=",")
```
- **`file_path`** — содержит путь к файлу с данными.
- **`np.loadtxt(file_path, delimiter=",")`** — загружает данные из CSV-файла в массив numpy.

---
### **3. Вычисление среднего значения**
```python
mean_value = np.mean(numbers)
rounded_mean = round(mean_value)
print(f"Среднее значение: {rounded_mean}")
```
- **`np.mean(numbers)`** — находит среднее арифметическое всех чисел в массиве.
- **`round(mean_value)`** — округляет среднее значение до целого числа.
- **`print(f"Среднее значение: {rounded_mean}")`** — выводит результат.

---
### **4. Вычисление медианы**
```python
median_value = np.median(numbers)
rounded_median = round(median_value)
print(f"Медиана: {rounded_median}")
```
- **`np.median(numbers)`** — вычисляет медиану (центральное значение отсортированного набора данных).
- **`round(median_value)`** — округляет медиану до целого числа.
- **Выводится результат.**

---
### **5. Вычисление моды**
```python
mode_result = stats.mode(numbers, keepdims=True)
mode_value = mode_result.mode[0]
rounded_mode = round(mode_value)
print(f"Мода: {rounded_mode}")
```
- **`stats.mode(numbers, keepdims=True)`** — находит наиболее часто встречающееся число.
- **`.mode[0]`** — берёт первое значение моды (если их несколько).
- **`round(mode_value)`** — округляет результат.
- **Выводится мода.**

---
### **Вывод**
Cкрипт анализирует числовой набор данных и вычисляет:
- **Среднее значение** (основная характеристика набора данных).
- **Медиану** (центральное значение, устойчивое к выбросам).
- **Моду** (самое частое значение).