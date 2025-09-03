# Python

## Типы данных

**Динамическая типизация** — Python автоматически определяет тип at runtime, без явного указания.

### Числовые типы (Numeric Types)

`int` – целые числа произвольной длины (включая отрицательные и положительные)

`float` – числа с плавающей точкой (десятичные), поддерживают экспоненциальную форму

`complex` – комплексные числа

### Логический тип (Boolean)

`bool` — значения `True` или `False`, представляет истину или ложь

В Python логические типы являются подтипом целых (`True == 1`, `False == 0`)

### Строки (Strings)

`str` — последовательность Unicode-символов, заключённая в одинарные или двойные кавычки

### Последовательности (Sequence Types)

`list` — упорядоченный изменяемый список объектов любого типа, поддерживает дублирование

`tuple` — кортеж, упорядоченная неизменяемая коллекция, допускающая дублирование, быстрее и более компактна по памяти

### Множества (Sets)

`set` — неупорядоченный изменяемый набор уникальных элементов, без дубликатов

`frozenset` — неизменяемый аналог множества

### Словари (Dictionaries)

`dict` — коллекция пар «ключ: значение», с уникальными хэшируемыми ключами; с версии Python 3.7 упорядочены по вставке

### NoneType

`NoneType` — представляет отсутствие значения, аналог NULL в других языках, используется как `None`

## Изменяемость (Mutability)

**Изменяемые (mutable)**: `list`, `dict`, `set` - содержимое можно менять после создания

**Неизменяемые (immutable)**: `int`, `float`, `complex`, `str`, `tuple`, `bool`, `NoneType`, `frozenset` — после создания нельзя менять содержимое

## ООП

**Объектно-ориентированное программирование** — это парадигма, в которой всё моделируется как объекты с данными (атрибутами) и поведением (методами).

**Основные принципы** — инкапсуляция, абстракция, наследование и полиморфизм.

```python
class Dog:
    def __init__(self, name, breed):
        self.name = name
        self.breed = breed

    def speak(self):
        print(f"{self.name} говорит Гав!")
        
dog1 = Dog("Бобик", "Лабрадор")
dog1.speak()
```

Класс — шаблон (Dog), объект — экземпляр класса (dog1)

Метод `__init__()` вызывается при создании объекта.

`self` — ссылка на текущий экземпляр класса

### Основные принципы ООП

#### Инкапсуляция

Скрытие внутреннего состояния объекта.

```python
class Example:
    def __init__(self):
        self.__private_val = 42
```

Атрибут `__private_val` доступен только внутри класса.

#### Абстракция

Сокрытие внутренней реализации, предоставление только нужного интерфейса.

#### Наследование

```python
class Parent:
    def greet(self):
        print("Привет из Parent!")

class Child(Parent):
    pass

c = Child()
c.greet()
```

`Child` наследует методы от `Parent`

#### Полиморфизм

Разные классы реализуют один и тот же интерфейс.

```python
class Animal:
    def speak(self):
        raise NotImplementedError

class Dog(Animal):
    def speak(self):
        print("Гав!")

class Cat(Animal):
    def speak(self):
        print("Мяу!")

for a in [Dog(), Cat()]:
    a.speak()
```

То же имя метода, разная реализация.

### self

В Python `self` — это ссылка на текущий экземпляр класса, которая передаётся как первый параметр в методах экземпляра. Благодаря `self` метод "видит", какой именно объект используется.

Это не ключевое слово, а просто конвенция, её можно заменить, но по PEP‑8 принято именно `self`.

В `__init__` `self` позволяет сохранять переданные аргументы как атрибуты экземпляра:

```python
class Point:
    def __init__(self, x, y):
        self.x = x
        self.y = y
```

Все обычные методы класса должны принимать `self`, чтобы иметь доступ к атрибутам и другим методам этого экземпляра.

### Переменные (атрибуты) класса и экземпляра

```python
class Car:
    wheels = 4  # атрибут класса
    def __init__(self, make):
        self.make = make  # атрибут экземпляра
```

Все экземпляры разделяют `wheels`, но каждый имеет своё `make`.

### classmethod (метод класса)

Декорируется `@classmethod` и принимает первым аргументом `cls`, то есть сам класс, а не экземпляр.

Может получать и изменять атрибуты класса, но не экземпляра:

```python
class Car:
    wheels = 4

    @classmethod
    def set_wheels(cls, n):
        cls.wheels = n

```

Часто используется как "фабричные методы" — конструкторы с альтернативными путями создания экземпляров:

```python
from datetime import date

class Person:
    def __init__(self, name, age):
        self.name = name
        self.age = age

    @classmethod
    def from_birth_year(cls, name, year):
        return cls(name, date.today().year - year)

p = Person.from_birth_year("Ivan", 1990)
```

Здесь `from_birth_year` возвращает новый объект Person с рассчитанным возрастом.

### staticmethod (статический метод)

Декорируется `@staticmethod` и не получает ни `self`, ни `cls` автоматически.

Это обычная функция, просто размещённая внутри класса по смыслу, но не связана ни с классом, ни с экземпляром:

```python
class Math:
    @staticmethod
    def add(x, y):
        return x + y
```

Используется для утилитарных функций, логически относящихся к классу, но не работающих с его состоянием.

## Декораторы

### Определение декоратора

**Декоратор** — это функция (или объект), которая принимает другую функцию и возвращает новую функцию (или объект), обычно расширяя поведение исходной функции без изменения её кода.

Фактически это синтаксический сахар:

```python
@dec
def f(...):
    ...
```

эквивалентно

```python
def f(...):
    ...
f = dec(f)

```

**Ключевая идея**: применение декоратора происходит в момент определения функции (import/загрузка модуля), а не при вызове. Возвращаемая "обёртка" вызывается позже — при вызове функции.

### Пример декоратора

```python
def my_decorator(func):
    def wrapper(*args, **kwargs):
        print("До вызова")
        result = func(*args, **kwargs)
        print("После вызова")
        return result
    return wrapper

@my_decorator
def greet(name):
    print(f"Hello, {name}!")

greet("Anna")

# Вывод:
# До вызова
# Hello, Anna!
# После вызова
```

### Применение functools.wraps

Если просто возвращать wrapper, то метаданные исходной функции (`__name__`, `__doc__`, сигнатура) будут потеряны — это мешает отладке и тестам. Решение — использовать `functools.wraps`:

```python
from functools import wraps

def my_decorator(func):
    @wraps(func)
    def wrapper(*args, **kwargs):
        # ...
        return func(*args, **kwargs)
    return wrapper
```

`@wraps` копирует `__name__`, `__doc__` и прочее у `func` в `wrapper`.

### Декоратор с аргументами (фабрика декораторов)

Если нужно передать параметры в декоратор, делаем ещё один внешний уровень:

```python
from functools import wraps

def repeat(n):
    def decorator(func):
        @wraps(func)
        def wrapper(*args, **kwargs):
            for _ in range(n):
                func(*args, **kwargs)
        return wrapper
    return decorator

@repeat(3)
def say_hi():
    print("Hi")

say_hi()
# Выведет "Hi" три раза
```

### Класс-декоратор

Можно реализовать декоратор через класс с методом `__call__`:

```python
class CountCalls:
    def __init__(self, func):
        self.func = func
        self.count = 0

    def __call__(self, *args, **kwargs):
        self.count += 1
        print(f"Вызвано {self.count} раз")
        return self.func(*args, **kwargs)

@CountCalls
def f(x):
    return x * 2

f(1)  # Вызвано 1 раз
f(2)  # Вызвано 2 раз
```

Преимущество — можно хранить состояние в экземпляре.

### Декораторы и методы (self/cls)

Декоратор для метода — обычный декоратор; важно корректно принимать self/cls:

```python
from functools import wraps

def debug(func):
    @wraps(func)
    def wrapper(self, *args, **kwargs):
        print(f"Calling {func.__name__} with {args}, {kwargs}")
        return func(self, *args, **kwargs)
    return wrapper

class A:
    @debug
    def m(self, x):
        return x + 1

A().m(5)
```

Если декоратор написан с *args, **kwargs, то self не требует отдельной обработки — это просто первый аргумент.

### Стек декораторов — порядок применения

Если несколько декораторов:

```python
@d1
@d2
def f(): 
    ...
```

то при загрузке модуля происходит f = d1(d2(f)). То есть декораторы применяются **снизу вверх** (снизу ближе к def применяется первым внутри выражения).

### Пример. Таймер

```python
import time
from functools import wraps


def timeit(func):
    @wraps(func)
    def wrapper(*args, **kwargs):
        start = time.perf_counter()
        res = func(*args, **kwargs)
        end = time.perf_counter()
        print(f"{func.__name__} took {end - start:.8f}s")
        return res
    return wrapper


@timeit
def get_sum(a: int, b: int) -> int:
    return a + b


print(get_sum(2, 4))

# get_sum took 0.00000130s
# 6

```
