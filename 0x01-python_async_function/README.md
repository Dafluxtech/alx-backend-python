## 0x01. Python - Async
`Python`  `Back-end`

![](http://djangostars.com/blog/content/images/2017/04/async_by_molen.png)

- [ASYN](https://www.linux.com/training-tutorials/asynchronous-programming-python-asyncio-0/)

## Resources

- [Async with python](https://https://realpython.com/async-io-python/#using-a-queue)

- [Getting started with async](https://realpython.com/python-async-features/)

- [AsyncIO in python](https://realpython.com/async-io-python/)

- [Aysnc python doc](https://docs.python.org/3/library/asyncio.html)

- [Docs python](https://docs.python.org/3/library/random.html#random.uniform)

## Learning Objectives

- `async` and `await` syntax
- How to execute an `async program with asyncio`
- How to run `concurrent coroutines`
- How to create `asyncio tasks`
- How to use the `random module`


## Concurrency vs Parallelism

Concurrency and parallelism can sound really similar but in programming there is an important difference. Immagine you are writing a book while cooking, even if it seems like you are doing both tasks at the same time, what you are doing is switching between the two tasks, while you wait for the water to boil you are writing your book, but while you are chopping some vegetables you pause your writing. This is called concurrency. The only way to do these two tasks in parallel is having two people, one writing and one cooking, which is what multicore CPU do.

## Coroutines

A coroutine is the result of an asynchronous function which can be declared using the keyword async before def

```python
async def my_func(args):
    return args**2

routines = my_func(args)
```
When we declare a function using the async keyword the function is not run, instead, a coroutine object is returned.

## Project Requirements

- A `README.md` file, at the root of the folder of the project, is mandatory
- Allowed editors: `vi`, `vim`, `emacs`
- All your files will be interpreted/compiled on `Ubuntu 18.04 LTS` using `python3 (version 3.7)`
- All your files should end with a new line
- All your __files must be executable__
- The length of your files will be tested using `wc`
- The first line of all your files should be exactly `#!/usr/bin/env python3`
- Your code should use the `pycodestyle style (version 2.5.x)`
- All your functions and coroutines must be type-annotated.
- All your modules should have a documentation `(python3 -c 'print(__import__("my_module").__doc__)')`
- All your functions should have a documentation (`python3 -c 'print(__import__("my_module").my_function.__doc__)`'
- A documentation is not a simple word, it’s a real sentence explaining what’s the purpose of the module, class or method (the length of it will be verified)


# :book: 0x00. 0x01. Python - Async
## :page_with_curl: Topics Covered
1. Python Async.

# :computer: Tasks.
## [0. The basics of async](0-basic_async_syntax.py)
### :page_with_curl: Task requirements.
Write an asynchronous coroutine that takes in an integer argument (max_delay, with a default value of 10) named wait_random that waits for a random delay between 0 and max_delay (included and float value) seconds and eventually returns it.

Use the random module.
```
bob@dylan:~$ cat 0-main.py
#!/usr/bin/env python3

import asyncio

wait_random = __import__('0-basic_async_syntax').wait_random

print(asyncio.run(wait_random()))
print(asyncio.run(wait_random(5)))
print(asyncio.run(wait_random(15)))

bob@dylan:~$ ./0-main.py
9.034261504534394
1.6216525464615306
10.634589756751769
```

### :wrench: Task setup.
```bash
# Create task files and set execute permission.
touch 0-basic_async_syntax.py
chmod +x 0-basic_async_syntax.py
./0-basic_async_syntax.py

# Lint checks
pycodestyle 0-basic_async_syntax.py
mypy 0-basic_async_syntax.py

# Tests
touch 0-main.py
chmod +x 0-main.py
./0-main.py
```

### :heavy_check_mark: Solution
> [:point_right: 0-basic_async_syntax.py](0-basic_async_syntax.py)


## [1. Let's execute multiple coroutines at the same time with async](1-concurrent_coroutines.py)
### :page_with_curl: Task requirements.
Import wait_random from the previous python file that you’ve written and write an async routine called wait_n that takes in 2 int arguments (in this order): n and max_delay. You will spawn wait_random n times with the specified max_delay.

wait_n should return the list of all the delays (float values). The list of the delays should be in ascending order without using sort() because of concurrency.
```
bob@dylan:~$ cat 1-main.py
#!/usr/bin/env python3
'''
Test file for printing the correct output of the wait_n coroutine
'''
import asyncio

wait_n = __import__('1-concurrent_coroutines').wait_n

print(asyncio.run(wait_n(5, 5)))
print(asyncio.run(wait_n(10, 7)))
print(asyncio.run(wait_n(10, 0)))

bob@dylan:~$ ./1-main.py
[0.9693881173832269, 1.0264573845731002, 1.7992690129519855, 3.641373003434587, 4.500011569340617]
[0.07256214141415429, 1.518551245602588, 3.355762808432721, 3.7032593997182923, 3.7796178143655546, 4.744537840582318, 5.50781365463315, 5.758942587637626, 6.109707751654879, 6.831351588271327]
[0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0, 0.0]

The output for your answers might look a little different and that’s okay.
```

### :wrench: Task setup.
```bash
# Create task files and set execute permission.
touch 1-concurrent_coroutines.py
chmod +x 1-concurrent_coroutines.py
./1-concurrent_coroutines.py

pycodestyle 1-concurrent_coroutines.py
mypy 1-concurrent_coroutines.py

# Tests
touch 1-main.py
chmod +x 1-main.py
./1-main.py
```

### :heavy_check_mark: Solution
> [:point_right: 1-concurrent_coroutines.py](1-concurrent_coroutines.py)


## [2. Measure the runtime](2-measure_runtime.py)
### :page_with_curl: Task requirements.
From the previous file, import wait_n into 2-measure_runtime.py.

Create a measure_time function with integers n and max_delay as arguments that measures the total execution time for wait_n(n, max_delay), and returns total_time / n. Your function should return a float.

Use the time module to measure an approximate elapsed time.
```
bob@dylan:~$ cat 2-main.py
#!/usr/bin/env python3

measure_time = __import__('2-measure_runtime').measure_time

n = 5
max_delay = 9

print(measure_time(n, max_delay))

bob@dylan:~$ ./2-main.py
1.759705400466919
```

### :wrench: Task setup.
```bash
# Create task files and set execute permission.
touch 2-measure_runtime.py
chmod +x 2-measure_runtime.py
./2-measure_runtime.py

pycodestyle 2-measure_runtime.py
mypy 2-measure_runtime.py

# Tests
touch 2-main.py
chmod +x 2-main.py
./2-main.py
```

### :heavy_check_mark: Solution
> [:point_right: 2-measure_runtime.py](2-measure_runtime.py)


## [3. Tasks](3-tasks.py)
### :page_with_curl: Task requirements.
Import wait_random from 0-basic_async_syntax.

Write a function (do not create an async function, use the regular function syntax to do this) task_wait_random that takes an integer max_delay and returns a asyncio.Task.
```
bob@dylan:~$ cat 3-main.py
#!/usr/bin/env python3

import asyncio

task_wait_random = __import__('3-tasks').task_wait_random


async def test(max_delay: int) -> float:
    task = task_wait_random(max_delay)
    await task
    print(task.__class__)

asyncio.run(test(5))

bob@dylan:~$ ./3-main.py
<class '_asyncio.Task'>
```

### :wrench: Task setup.
```bash
# Create task files and set execute permission.
touch 3-tasks.py
chmod +x 3-tasks.py
./3-tasks.py

pycodestyle 3-tasks.py
mypy 3-tasks.py

# Tests
touch 3-main.py
chmod +x 3-main.py
./3-main.py
```

### :heavy_check_mark: Solution
> [:point_right: 3-main.py](3-tasks.py)


## [4. Tasks](4-main.py)
### :page_with_curl: Task requirements.
Take the code from wait_n and alter it into a new function task_wait_n. The code is nearly identical to wait_n except task_wait_random is being called.
```
bob@dylan:~$ cat 4-main.py
#!/usr/bin/env python3

import asyncio

task_wait_n = __import__('4-tasks').task_wait_n

n = 5
max_delay = 6
print(asyncio.run(task_wait_n(n, max_delay)))

bob@dylan:~$ ./4-main.py
[0.2261658205652346, 1.1942770588220557, 1.8410422186086628, 2.1457353803430523, 4.002505454641153]
```

### :wrench: Task setup.
```bash
# Create task files and set execute permission.
touch 4-tasks.py
chmod +x 4-tasks.py
./4-tasks.py

pycodestyle 4-tasks.py
mypy 4-tasks.py

# Tests
touch 4-main.py
chmod +x 4-main.py
./4-main.py
```

### :heavy_check_mark: Solution
> [:point_right: 4-main.py](4-main.py)
