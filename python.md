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


def time_it(func):
    @wraps(func)
    def wrapper(*args, **kwargs):
        start = time.perf_counter()
        res = func(*args, **kwargs)
        end = time.perf_counter()
        print(f"{func.__name__} took {end - start:.8f}s")
        return res
    return wrapper


@time_it
def get_sum(a: int, b: int) -> int:
    return a + b


print(get_sum(2, 4))

# get_sum took 0.00000130s
# 6

```

## Контекстный менеджер

### Определение контекстного менеджера

Контекстный менеджер — это объект, который управляет ресурсом в блоке `with`: открывает/инициализирует ресурс при входе и гарантированно освобождает/закрывает его при выходе из блока, даже если внутри блока возникло исключение.

Синтаксис:

```python
with <контекстный_менеджер> as <имя>:
    # блок кода
```

### Протокол: `__enter__` и `__exit__`

```python
class CM:
    def __enter__(self):
        # код, выполняемый при входе в with
        return value  # возвращаемое значение связывается с "as"
    def __exit__(self, exc_type, exc_value, traceback):
        # код, выполняемый при выходе из with (всегда выполняется)
        # exc_type, exc_value, traceback — информация об исключении, если оно произошло
        # вернуть True, чтобы подавить исключение; вернуть False/None — исключение будет проброшено дальше
```

Особенности:

* `__enter__` выполняется до выполнения блока `with`.

* `__exit__` вызывается всегда при выходе из блока (даже при `return` или при исключении), и получает параметры исключения, если оно было.

* Если `__exit__` возвращает `True`, то исключение подавляется (не пробрасывается дальше). Если возвращает `False` или `None`, исключение повторно пробрасывается после `__exit__`.

### Пример: работа с файлом

```python
with open("file.txt", "w") as f:
    f.write("hello")
# файл автоматически закрыт при выходе из with
```

`open()` возвращает объект, реализующий протокол контекстного менеджера — поэтому `with` удобен для работы с файлами.

### Пример собственного контекстного менеджера (класс)

```python
class managed_file:
    def __init__(self, filename, mode):
        self.filename = filename
        self.mode = mode

    def __enter__(self):
        self.file = open(self.filename, self.mode)
        return self.file

    def __exit__(self, exc_type, exc_value, traceback):
        self.file.close()
        # не подавляем исключения — возвращаем None (или False)

# Использование:
with managed_file("a.txt", "w") as f:
    f.write("test")
```

### Пример через `contextlib.contextmanager` (декоратор)

`contextlib.contextmanager` позволяет реализовать контекстный менеджер как генератор:

```python
from contextlib import contextmanager

@contextmanager
def managed_file_cm(filename, mode):
    f = open(filename, mode)
    try:
        yield f # управление — сюда попадёт тело with, f будет тем, что вернулось в as
    finally:
        f.close()

# Использование:
with managed_file_cm("b.txt", "w") as f:
    f.write("hello")
```

Если внутри блока `with` возникает исключение, оно будет передано наружу, а код в `finally` выполнится — файл закроется.

Если нужно обработать или подавить исключение внутри генератора, можно использовать блок `try`/`except` вокруг `yield` и принимать решение о подавлении (через `contextmanager` нужно повторно выбросить или не выбрасывать исключение).

### Подавление исключений

Есть готовая утилита `contextlib.suppress` для подавления конкретных исключений:

```python
from contextlib import suppress

with suppress(FileNotFoundError):
    os.remove("no_file.txt")  # если файла нет — исключение подавится
```

При использовании `__exit__`, чтобы подавить исключение, нужно возвращать `True`:

```python
def __exit__(self, exc_type, exc_value, tb):
    if exc_type is SomeExpectedError:
        # обработали — подавляем
        return True
    # иначе возвращаем None/False — исключение пробросится
```

### Порядок входа/выхода при нескольких менеджерах

В строке `with A() as a, B() as b`: порядок эквивалентен вложенным `with`:

```python
with A() as a:
    with B() as b:
        ...
```

* Вход: `A.__enter__()` затем `B.__enter__()`.

* Выход (по завершении блока): `B.__exit__()` затем `A.__exit__()` (обратный порядок).

### Пример классовый менеджер / contextmanager

```python
import time


class Timer:
    def __enter__(self):
        self.start = time.perf_counter()
        return self


    def __exit__(self, exc_type, exc_value, traceback):
        elapsed = time.perf_counter() - self.start
        print(f"Elapsed: {elapsed:.6f}s")
        # не подавляем исключения (вернём False/None)


with Timer():
    print(2 + 4)

# 6
# Elapsed: 0.000049s
```

```python
import time
from contextlib import contextmanager


@contextmanager
def timer():
    start = time.perf_counter()
    try:
        yield
    finally:
        print(f"Elapsed: {time.perf_counter() - start:.6f}s")


with timer():
    print(2 + 4)
```
