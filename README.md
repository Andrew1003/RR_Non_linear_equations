# Пакет для розв'язання нелінійних рівнянь

## Деталі проєкту
- **Предмет:** Чисельні методи
- **Тема:** Розв'язання нелінійних рівнянь
- **Члени команди:**
  - Андрій Літинець


## Огляд пакету
Пакет `nonlinear_solver` надає числові методи для розв'язання нелінійних рівнянь. Він включає алгоритми, такі як метод бісекції, метод Ньютона, ітераційний метод фіксованої точки, метод золотого перетину та метод сікання.

## Основні функції
1. **Метод бісекції:** Розв'язує нелінійні рівняння шляхом ітеративного звуження інтервалу кореня.
2. **Метод Ньютона:** Використовує похідну для швидкої збіжності до кореня.
3. **Ітераційний метод фіксованої точки:** Застосовує ітеративно функцію трансформації для пошуку кореня.
4. **Метод золотого перетину:** Ділить інтервал на основі золотого перетину для збіжності.
5. **Метод сікання:** Ітераційний метод з використанням сікання для наближення кореня.

## Приклад використання
```python
from nonlinear_solver.equation_solver import EquationSolver
from nonlinear_solver.visualization import FunctionPlotter

# Створити об'єкт FunctionPlotter
plotter = FunctionPlotter()

# Ввести рівняння
equation = plotter.input_equation()

# Ввести інтервал для розв'язку
a = float(input("Введіть нижню межу інтервалу: "))
b = float(input("Введіть верхню межу інтервалу: "))

# Візуалізувати функцію
plotter.plot_function(equation, a, b)

# Створити об'єкт EquationSolver
solver = EquationSolver(equation)

# Обрати метод для розв'язання
method = input("Оберіть метод (bisection/newton/fixed_point/golden_ratio/secant): ").lower()

# Розв'язати рівняння за допомогою обраного методу
if method == 'bisection':
    root, iterations = solver.solve_bisection(a, b)
elif method == 'newton':
    root, iterations = solver.solve_newton(initial_guess=(a + b) / 2)
elif method == 'fixed_point':
    root, iterations = solver.solve_fixed_point_iteration(initial_guess=(a + b) / 2)
elif method == 'golden_ratio':
    root, iterations = solver.solve_golden_ratio(a, b)
elif method == 'secant':
    x0 = float(input("Введіть першу початкову точку: "))
    x1 = float(input("Введіть другу початкову точку: "))
    root, iterations = solver.solve_secant(x0, x1)
else:
    print("Невірний вибір методу. Вихід.")
    root, iterations = None, None

# Показати результати
if root is not None:
    print(f"{method.capitalize()} Method: Root = {root}, Iterations = {iterations}")
