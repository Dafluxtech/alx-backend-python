# :book: 0x02. Python - Async Comprehension.

~[](https://miro.medium.com/v2/resize:fit:720/format:webp/1*QIH11ANjUwb7Gye_aktWOQ.png)

An asynchronous comprehension allows a list, set, or dict to be created using the “async for” expression with an asynchronous iterable. We propose to allow using async for inside list, set and dict comprehensions. This will create and schedule coroutines or tasks as needed and yield their results into a list.

Python has extensive support for synchronous comprehensions, allowing to produce lists, dicts, and sets with a simple and concise syntax. We propose implementing similar syntactic constructions for the asynchronous code.

To illustrate the readability improvement, consider the following example:

```python
result = []
async for i in aiter():
    if i % 2:
        result.append(i)
```

With the proposed asynchronous comprehensions syntax, the above code becomes as short as:

```python
result = [i async for i in aiter() if i % 2]
```

The PEP also makes it possible to use the await expressions in all kinds of comprehensions:

```python
result = [await fun() for fun in funcs]
```

## Resources
- [PEP 530 Async comprehensions](https://peps.python.org/pep-0530/)

- [a brief overview](https://www.blog.pythonlibrary.org/2017/02/14/whats-new-in-python-asynchronous-comprehensions-generators/)

- [using "async for"](https://superfastpython.com/asyncio-async-for/)

- [async comprehensions in python](https://superfastpython.com/asynchronous-comprehensions/#:~:text=An%20asynchronous%20comprehension%20allows%20a,list%2C%20set%20and%20dict%20comprehensions.&text=This%20will%20create%20and%20schedule,their%20results%20into%20a%20list.)

- [asyncio.gather() method](https://superfastpython.com/asyncio-gather)

## Learning Objectives

- How to write an `asynchronous generator`
- How to use `async comprehensions`
- How to `type-annotate generators`

## Project Requirements

- Allowed editors: `vi`, `vim`, `emacs`
- All your files will be interpreted/compiled on `Ubuntu 18.04 LTS` using `python3 (version 3.7)`
- All your files should end with a new line
- The first line of all your files should be exactly `#!/usr/bin/env python3`
- A README.md file, at the root of the folder of the project, is mandatory
- Your code should `use the pycodestyle style (version 2.5.x)`
- The length of your files will be tested using `wc`
- All your modules should have a documentation (`python3 -c 'print(__import__("my_module").__doc__)'`)
- All your functions should have a documentation (python3 -c 'print(__import__("my_module").my_function.__doc__)'
- A documentation is not a simple word, it’s a real sentence explaining what’s the purpose of the module, class or method (the length of it will be verified)
- All your functions and coroutines must be type-annotated.




# :computer: Tasks.
## [0. Async Generator](0-async_generator.py)
### :page_with_curl: Task requirements.
Write a coroutine called async_generator that takes no arguments.

The coroutine will loop 10 times, each time asynchronously wait 1 second, then yield a random number between 0 and 10. Use the random module.

```
bob@dylan:~$ cat 0-main.py
#!/usr/bin/env python3

import asyncio

async_generator = __import__('0-async_generator').async_generator

async def print_yielded_values():
    result = []
    async for i in async_generator():
        result.append(i)
    print(result)

asyncio.run(print_yielded_values())

bob@dylan:~$ ./0-main.py
[4.403136952967102, 6.9092712604587465, 6.293445466782645, 4.549663490048418, 4.1326571686139015, 9.99058525304903, 6.726734105473811, 9.84331704602206, 1.0067279479988345, 1.3783306401737838]
```

### :wrench: Task setup.
```bash
# Create task files and set execute permission.
touch 0-async_generator.py
chmod +x 0-async_generator.py
./0-async_generator.py

# Lint checks
pycodestyle 0-async_generator.py
mypy 0-async_generator.py

# Tests
touch 0-main.py
chmod +x 0-main.py
./0-main.py
```

### :heavy_check_mark: Solution
> [:point_right: 0-async_generator.py](0-async_generator.py)


## [1. Async Comprehensions](1-async_comprehension.py)
### :page_with_curl: Task requirements.
Import async_generator from the previous task and then write a coroutine called async_comprehension that takes no arguments.

The coroutine will collect 10 random numbers using an async comprehensing over async_generator, then return the 10 random numbers.
```
bob@dylan:~$ cat 1-main.py
#!/usr/bin/env python3

import asyncio

async_comprehension = __import__('1-async_comprehension').async_comprehension


async def main():
    print(await async_comprehension())

asyncio.run(main())

bob@dylan:~$ ./1-main.py
[9.861842105071727, 8.572355293354995, 1.7467182056248265, 4.0724372912858575, 0.5524750922145316, 8.084266576021555, 8.387128918690468, 1.5486451376520916, 7.713335177885325, 7.673533267041574]
```

### :wrench: Task setup.
```bash
# Create task files and set execute permission.
touch 1-async_comprehension.py
chmod +x 1-async_comprehension.py
./1-async_comprehension.py

pycodestyle 1-async_comprehension.py
mypy 1-async_comprehension.py

# Tests
touch 1-main.py
chmod +x 1-main.py
./1-main.py
```

### :heavy_check_mark: Solution
> [:point_right: 1-async_comprehension.py](1-async_comprehension.py)


## [2. Run time for four parallel comprehensions](2-measure_runtime.py)
### :page_with_curl: Task requirements.
Import async_comprehension from the previous file and write a measure_runtime coroutine that will execute async_comprehension four times in parallel using asyncio.gather.

measure_runtime should measure the total runtime and return it.

Notice that the total runtime is roughly 10 seconds, explain it to yourself.
```
bob@dylan:~$ cat 2-main.py
#!/usr/bin/env python3

import asyncio


measure_runtime = __import__('2-measure_runtime').measure_runtime


async def main():
    return await(measure_runtime())

print(
    asyncio.run(main())
)

bob@dylan:~$ ./2-main.py
10.021936893463135
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

