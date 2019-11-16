# 🛠 fix-a-bug

## Setup

Clone this repo.

```bash
git clone https://github.com/datamade/fix-a-bug.git && cd fix-a-bug
```

Install the requirements. (Feel free to use a virtual environment!)

```bash
pip install -r requirements.txt
```

Run the tests.

```bash
pytest -sv
```

## Challenge

The code in `fix_me.py` contains four errors that are preventing the test from
passing. Debug and correct each error. As you identify the errors, fill out
a description of the problem and an explanation of the root cause and your fix
in the section below.

### Error 1

**Description:**
The first error we see is `IndexError: list index out of range` meaning we tried accessing an array index that doesn't exist on line 16.

**Explanation:**
We see this error because we are accidentally switching index, and value on line 28 in the for loop. It should be `for index, value in enumerate(self.DATA):` so that we get the right values for index and value in the loop.

### Error 2

**Description:**
The second error we see is `TypeError: 'int' object is not iterable` on line 29.

**Explanation:**
The `sum` python method expects an iterable as the first argument, but instead, we are passing the output of the `get_previous` which is an integer. Since we are only adding two numbers together, we can replace line 29 with `transformed_value = self.get_previous(index) + value`.

### Error 3

**Description:**
The third error we see is `AssertionError`. The test is expecting the output to be `[4, 9, 11]` but instead we are getting `[16, 15, 17]`.

**Explanation:**
The `Transformer` class is inheriting 2 parent classes `ParentA` and `ParentB`. If you look at the `DATA` for `ParentA`, the output we are currently getting checks out since `ParentA`'s `DATA` is `[7,8,9]` and

```
7+9 = 16
7+8 = 15
8+9 = 17
```

To fix it for the sake of the test, we can switch the order on line 9 to be `class Transformer(ParentB, ParentA):`

### Error 4

**Description:**
The fourth error we see is `AssertionError`. The test is expecting the output to be `[4, 9, 11]` but instead we are now getting `[10, 9, 11]`.

**Explanation:**
The last two numbers of the final array are correct, but the first one is not. This is because, we are currently outputting `self.DATA[current_index - 1]` in the `get_previous` method. So the first time we loop through the `DATA` array, we are are really adding `self.DATA[0 - 1]` which is the value of the last index of the `DATA` array to the next value of the array. To fix this, we need to return 0 if there is no previous index. To do this we can return `self.DATA[current_index - 1] if current_index > 0 else 0` in the `get_previous` method.
