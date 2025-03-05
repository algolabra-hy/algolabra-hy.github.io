---
layout: page
title: Dependency Injection
permalink: /dependency-injection-en
lang: en # fi or en
ref: dependency_injection_python # same as the markdown filename
---
_These instructions have been translated from the [material of the course Software Production](https://ohjelmistotuotanto-hy.github.io/riippuvuuksien_injektointi_python/)_

First, read <http://jamesshore.com/Blog/Dependency-Injection-Demystified.html>

Below is a simple calculator:

```python
class Calculator:
    def execute(self):
        while True:
            number1 = int(input("Number 1:"))

            if number1 == -9999:
                return

            number2 = int(input("Number 2:"))

            if number2 == -9999:
                return

            result = self._calculate_sum(number1, number2)

            print(f"Sum: {result}")

    def _calculate_sum(self, number1, number2):
        return number1 + number2

def main():
    calculator = Calculator()

    calculator.execute()

if __name__ == "__main__":
    main()
```
The downside of the program is that the <code>Calculator</code> class has a *concrete dependency* on the functions handling output and input: <code>print</code> and <code>input</code>.

Concrete dependencies make testing more difficult and complicate program expansion.
### Eliminating Direct Dependency
Let's isolate the output and input handling into a separate `ConsoleIO` object:
```python
class ConsoleIO:
    def read(self, text):
        return input(text)

    def write(self, text):
        print(text)
```
Let's modify the `Laskin` class so that it receives an object as a constructor parameter, which will handle communication with the user:
```python
class Calculator:
    def __init__(self, io):
        self._io = io

    def execute(self):
        while True:
            number1 = int(self._io.read("Number 1:"))

            if number1 == -9999:
                return

            number2 = int(self._io.read("Number 2:"))

            if number2 == -9999:
                return

            result = self._calculate_sum(number1, number2)

            self._io.write(f"Sum: {result}")

    def _calculate_sum(self, number1, number2):
        return number1 + number2

```
The application is now started in such a way that the communication-handling object is *injected* as a constructor parameter:
```python
def main():
    io = ConsoleIO()
    calculator = Calculator(io)

    calculator.execute()

main()
```
### Testing
Now, unit tests can be easily written for the program. For testing purposes, we create a fake class, a stub, which externally behaves the same way as `ConsoleIO` objects:
```python
class StubIO:
    def __init__(self, inputs):
        self.inputs = inputs
        self.outputs = []

    def read(self, text):
        return self.inputs.pop(0)

    def write(self, text):
        self.outputs.append(text)
```
The stub can be given "user inputs" as a constructor parameter. After execution, the program's outputs can be retrieved from the stub.
Here is the test:
```python
class TestCalculator(unittest.TestCase):
    def test_one_sum_correct(self):
        io = StubIO(["1", "3", "-9999"])
        calculator = Calculator(io)
        calculator.execute()

        self.assertEqual(io.outputs[0], "Sum: 4")
```
### Summary
Dependency injection is actually an extremely simple technique, and many have likely used it already in basic programming courses.

Consider, for example, computer games, which often rely on random numbers. If a game is coded as follows, automated testing becomes very difficult:
```python
class Game: 
    def moving_player(self):
      direction = random.randint(0, 8)
```
If, on the other hand, the random number generator is _injected_ into the game as follows
```python
class Game: 
    def __init__(self, generator):
        self._generator = generator

  def moving_player(self):
    direction = self._generator.randint(0, 8)
```
we can inject a version of the random number generator during testing that allows us to control the numbers it generates. For example, here is a version of the random number generator that always returns the number 1 when the _randint_ method is called:
```python
class Generator:
    def randint(self, a, b):
        return 1
```

{% include typo_instructions_en.md %}
