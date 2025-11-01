# Функции 2

# def
Функции в общем виде:
```python
def название_функции(параметры):
	тело_функции
```

Напишем функцию
```python
def make_a_sound():
	print("Hoog riiider")

make_a_sound()
```

Функция берет и делает то, что мы ей скажем. Мы можем добавить разнообразия

```python
def make_a_sound(is_hog_rider):
	if is_hog_rider:
		print("Hoog riiider")
	else
		print("😢")
		
make_a_sound(True)
make_a_sound(False)
```

То есть мы можем писать какую-то логику и использовать ее несколько раз. Вот пример ближе к жизни:

Нужно написать код, который генерирует 3 списка разной длинны (10, 100, 1000) и замеряет время, за которое найдет в них максимальный элемент

1. Один не случайный список
```python
numbers = [1,3,4,3,5,74,6,3,6]  
max = float("-inf")  # Минус бесконечность  
  
for number in numbers:  
    if number > max:  
        max = number  
  
print(max)
```

2. Один случайный список
```python
import random

lenth = 10
numbers = [random.randint(0, 100) for _ in range(lenth)]
max = float("-inf")  # Минус бесконечность

for number in numbers:
    if number > max:
        max = number

print(numbers)
print(max)
```

3. Один случайный список с замером времени
```python
import random
from time import time, process_time

lenth = 10
numbers = [random.randint(0, 100) for _ in range(lenth)]
max = float("-inf")  # Минус бесконечность
stat_time = time()

for number in numbers:
    if number > max:
        max = number

print(numbers)
print(max)
print(time() - stat_time)
```

4. 3 Случайных списка c замером времени
```python
import random
from time import time, process_time

lenth = 10
numbers = [random.randint(0, 100) for _ in range(lenth)]
max = float("-inf")
stat_time = time()

for number in numbers:
    if number > max:
        max = number

print(numbers)
print(max)
print(time() - stat_time)
# ----
lenth = 100
numbers = [random.randint(0, 1000) for _ in range(lenth)]
max = float("-inf")
stat_time = time()

for number in numbers:
    if number > max:
        max = number

print(numbers)
print(max)
print(time() - stat_time)
# ---
lenth = 1000
numbers = [random.randint(0, 10000) for _ in range(lenth)]
max = float("-inf")
stat_time = time()

for number in numbers:
    if number > max:
        max = number

print(numbers)
print(max)
print(print(time() - stat_time))
```

Видите, у нас много повторяющегося кода. Представьте, что завтра выйдет новая версия Python, которая это все меняет и нам прийдется это все переписывать

1. Отдельная функция для поиска максимального элемента
```python
import random
from time import time

def get_max(numers):
    max = float("-inf")  # Минус бесконечность

    for number in numbers:
        if number > max:
            max = number

    return max

lenth = 10
numbers = [random.randint(0, 100) for _ in range(lenth)]
stat_time = time()
max = get_max(numbers)

print(numbers)
print(max)
print(time() - stat_time)
# ----
lenth = 100
numbers = [random.randint(0, 1000) for _ in range(lenth)]
stat_time = time()
max=get_max(numbers)

print(numbers)
print(max)
print(time() - stat_time)
# ---
lenth = 1000
numbers = [random.randint(0, 10000) for _ in range(lenth)]
stat_time = time()
max = get_max(numbers)

print(numbers)
print(max)
print(print(time() - stat_time))
```

2. Отдельная функция для замера времени
```python
import random
from time import time

def check_time(f, *args):
    start_time = time()
    result = f(*args)
    print(time() - start_time)
    return result

def get_max(numers):
    max = float("-inf") 

    for number in numbers:
        if number > max:
            max = number

    return max

lenth = 10
numbers = [random.randint(0, 100) for _ in range(lenth)]
max = check_time(get_max, numbers)

print(numbers)
print(max)
# ----
lenth = 100
numbers = [random.randint(0, 1000) for _ in range(lenth)]
max = check_time(get_max, numbers)

print(numbers)
print(max)
# ---
lenth = 1000
numbers = [random.randint(0, 10000) for _ in range(lenth)]
max = check_time(get_max, numbers)

print(numbers)
print(max)
```

3. Функция для генерации случайного списка
```python
import random
from time import time

def check_time(f, *args):
    start_time = time()
    result = f(*args)
    print(time()-start_time)
    return result

def get_max(numers):
    max = float("-inf")

    for number in numbers:
        if number > max:
            max = number

    return max

def get_random_list(lenght, min_limit, max_limit):
    return [random.randint(min_limit, max_limit) for _ in range(lenght)]
    

length = 10
numbers = get_random_list(length, 0, 100)
max = check_time(get_max, numbers)

print(numbers)
print(max)
# ----
length = 100
numbers = get_random_list(length, 0 , 1000)
max = check_time(get_max, numbers)

print(numbers)
print(max)
# ---
length = 1000
numbers = get_random_list(length, 0 , 10000)
max = check_time(get_max, numbers)

print(numbers)
print(max)
```

Сама значимая часть кода сжалась до
```python
length = 10
numbers = get_random_list(length, 0, 100)
max = check_time(get_max, numbers)

print(numbers)
print(max)
# ----
length = 100
numbers = get_random_list(length, 0 , 1000)
max = check_time(get_max, numbers)

print(numbers)
print(max)
# ---
length = 1000
numbers = get_random_list(length, 0 , 10000)
max = check_time(get_max, numbers)

print(numbers)
print(max)
```
Разберем, что здесь может вызывать вопросы:

# return
```python
def divide(a, b):
    print(a / b)
```

Функция рабочая, но предположим, что нам нужно не просто вывести на экран, а получить обратно в код, чтобы и дальше считать числа

```python
def divide(a, b):  
    return a / b  
  
sum_1 = divide(2, 5)  
sum_2 = divide(4, 5)  
sum_3 = divide(sum_1, sum_2)  
  
print(sum_3)
```
Теперь наша функция возвращает какие-то значения обратно в код и мы можем присвоить результат вычислений функции переменной

# `*args`
```python
def add(a, b):
    return a + b

sum = add(2,4)
```

Не очень прикольно? Давайте сделаем так, чтобы сколько бы мы чисел не передали - сложило бы все

```python
def add(*args):
    result = 0
    for num in args:
        result += num
    return result

sum = add(2, 4, 5, 5, 6)
print(sum)
```

Функция теперь принимает в себя сколько угодно значений и воспринимает их как кортеж args. Вы можете в этом убедиться, заменив код функции кодом ниже:

```python
def add(*args):
    print(args)
```

>Принято вот такие аргументы без четкого имени называть `args`

# `**kwargs`

```python
def greet(name, surname):
    print(f"Hello {name} {surname}")
    
greet('Эддарт', 'Старк')
```

По нашей функции не очень понятно в каком порядке передвать значения, мы можем решить это так:

```python
def greet(name, surname):
    print(f"Hello {name} {surname}")

greet(name='Эддарт', surname='Старк')
greet(name='Грейджой', surname='Теон')
```

Теперь мы можем передавать значения как нам хочется, по аналогии с args мы можем передавать сколько угодно таких значений

```python
def greet(**kwargs):
    print('Hello', end=', ')
    for key, value in kwargs.items():
        print(f'your {key} is {value}', end=', ')
    print('')

greet(name='Эддарт', surname='Старк')
greet(name='Грейджой', surname='Теон')
```

>Принято называть `kwags` от key word arguments

Чтобы показать, что мы будем передавать значения в другой форме - используются другие обозначения. И действительно, мы получаем значения в виде словаря

# Строгая типизация
Честно, думаю никто не знает всех матодов, которые мы можем делать со строками в python, а когда мы используем их в функции, то python не уверен в том, что он получит и не предлагает дополнить за нас код. Мы можем сказать python что в функции мы будем ожидать строку, или любой другой тип данных

```python
def to_upper(text:str):  
    print(text.upper())  
  
to_upper('aboba')
```

когда вы будете писать вторую строку, то vs code сам будет подсказывать вам разные методы, относящиеся только к строкам

# Декораторы
Помните, что мы писали функцию:

```python
def check_time(f, *args):
    start_time = time()
    result = f(*args)
    print(time() - start_time)
    return result
```

Мы можем ее переделать чуть веселее. Как вы думаете, можем ли мы вернуть не какое то значение, а целую функцию?

```python
from time import time, sleep

def check_time(f, *args, **kwargs):
    def wrapper():
        start_time = time()
        result = f(*args, **kwargs)
        print(time() - start_time)
        return result
    return wrapper


def do_some_long_stuff():
    sleep(2)
    print("Done")

check_how_long_is_stuff = check_time(do_some_long_stuff)
check_how_long_is_stuff()
```

- У нас есть функция, чью длину мы хотим измерить (`do_some_long_stuff`)
- Есть функция, которая принимает в себя другую функцию и добавляет к ней вой код (check_time)
- Мы создаем новую функцию из уже существующей и используем

Это частое явление в python и для этого придумали *декораторы*
```python
from time import time, sleep

def check_time(f, *args, **kwargs):
    def wrapper():
        start_time = time()
        result = f(*args, **kwargs)
        print(time() - start_time)
        return result
    return wrapper

@check_time
def do_some_long_stuff():
    sleep(2)
    print("Done")

do_some_long_stuff()
```

Мы навсегда обернули код нашей функции в код с проверкой времени. Смотрите на декораторы как на гирлянды на елке: они не меняют саму ее суть, а только добавляют своих приколов к дереву

>На самом деле это не что-то что так часто вы будете делать самостоятельно, но при работе с чужим кодом такое встречается: при написании api, чат ботов...

