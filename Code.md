import numpy as np
import matplotlib.pyplot as plt
from mpl_toolkits.mplot3d import Axes3D

-# Определение функции
def objective_function(x1, x2):
    return (x1 - 2) ** 2 + (x2 - 1) ** 2

-# Создание сетки
x1_range = np.arange(-1, 4.5, 0.5)
x2_range = np.arange(-1, 4.5, 0.5)
x1_grid, x2_grid = np.meshgrid(x1_range, x2_range)

-# Вычисление значений функции на сетке
z_values = objective_function(x1_grid, x2_grid)

-# Построение линий уровней и 3D-графика
fig = plt.figure(figsize=(12, 6))
ax1 = fig.add_subplot(121)
ax2 = fig.add_subplot(122, projection='3d')

-# Линии уровней
contour = ax1.contour(x1_grid, x2_grid, z_values, levels=20, cmap='viridis')
ax1.set_title('Линии уровней функции')

-# 3D-график
ax2.plot_surface(x1_grid, x2_grid, z_values, cmap='viridis', alpha=0.8)
ax2.set_title('3D-график функции')

plt.show()

----

from scipy.optimize import minimize

-# Определение функции для оптимизации
def objective_function_opt(x):
    return (x[0] - 2) ** 2 + (x[1] - 1) ** 2

-# Определение функциональных ограничений
def constraint1(x):
    return x[0] - 2 * x[1] + 1

def constraint2(x):
    return -0.25 * x[0] ** 2 - x[1] ** 2 + 1

-# Определение области поиска
bounds = ((-1, 4), (-1, 4))

-# Определение функциональных ограничений
constraints = ({'type': 'ineq', 'fun': constraint1}, {'type': 'ineq', 'fun': constraint2})

-# Поиск минимума с учетом ограничений
result = minimize(objective_function_opt, (0, 0), bounds=bounds, constraints=constraints)

-# Вывод результатов
print("Минимум функции:", result.fun)
print("Значения переменных x1, x2:", result.x)

---

-# Изменение функциональных ограничений
def updated_constraint1(x):
    return x[0] - 2 * x[1] + 1

def updated_constraint2(x):
    return -0.25 * x[0] ** 2 - x[1] ** 2 + 1.5  # Измененное ограничение

-# Обновление функциональных ограничений
updated_constraints = ({'type': 'ineq', 'fun': updated_constraint1}, {'type': 'ineq', 'fun': updated_constraint2})

-# Поиск условного минимума с измененными ограничениями
updated_result = minimize(objective_function_opt, (0, 0), bounds=bounds, constraints=updated_constraints)

-# Вывод результатов
print("\nУсловный минимум функции:", updated_result.fun)
print("Значения переменных x1, x2:", updated_result.x)
