
---

## 🧩 First rule: Building the final program

```makefile
$(NAME): $(OBJ)
	$(CXX) $(CXXFLAGS) $(OBJ) $(DEPEND) -o $(NAME)
```

### 💡 Meaning

This defines **how to create the final executable** (named `$(NAME)`) from the list of object files `$(OBJ)`.

---

### Step-by-step breakdown

| Part          | Meaning                                                                     |
| ------------- | --------------------------------------------------------------------------- |
| `$(NAME)`     | The name of the final executable, e.g. `my_program`                         |
| `$(OBJ)`      | The list of `.o` object files (like `build/main.o build/utils/math.o`)      |
| `:`           | Separator — tells Make: "`$(NAME)` depends on `$(OBJ)`"                     |
| `$(CXX)`      | The C++ compiler (usually `g++` or `clang++`)                               |
| `$(CXXFLAGS)` | Compiler flags (like `-Wall -Wextra -O2`, etc.)                             |
| `$(DEPEND)`   | Optional list of extra dependencies or libraries (e.g. `-lm` or `-pthread`) |
| `-o $(NAME)`  | Tells the compiler the **output file name** (the executable)                |

---

### 🔧 Example

Suppose you have:

```makefile
NAME = my_app
OBJ = build/main.o build/utils/math.o
CXX = g++
CXXFLAGS = -Wall -Wextra -O2
```

Then Make runs:

```bash
g++ -Wall -Wextra -O2 build/main.o build/utils/math.o -o my_app
```

This links the object files together into the executable `my_app`.

---

## 🧩 Second rule: Building each object file

```makefile
$(BUILD_DIR)/%.o: $(SRC_DIR)/%.cpp
	mkdir -p $(@D)
	$(CXX) $(CXXFLAGS) -I$(HEADER) -c $< -o $@
```

### 💡 Meaning

This tells Make how to **compile a single `.cpp` source file** into a corresponding `.o` object file — and automatically creates the necessary directories if they don’t exist.

---

### Step-by-step breakdown

| Part               | Meaning                                                                |
| ------------------ | ---------------------------------------------------------------------- |
| `$(BUILD_DIR)/%.o` | Target: the object file (e.g. `build/utils/math.o`)                    |
| `$(SRC_DIR)/%.cpp` | Dependency: the corresponding source file (e.g. `src/utils/math.cpp`)  |
| `%`                | Wildcard — matches the same stem in both filenames (e.g. `utils/math`) |
| `mkdir -p $(@D)`   | Creates the target directory (`$(@D)` = directory part of target)      |
| `$(CXX)`           | The compiler (`g++`, `clang++`, etc.)                                  |
| `$(CXXFLAGS)`      | Compiler flags                                                         |
| `-I$(HEADER)`      | Adds an include directory (e.g. `-Iinclude`)                           |
| `-c`               | Compile *only* (don’t link) — produces a `.o` file                     |
| `$<`               | Automatic variable = the *first prerequisite* (here, the `.cpp` file)  |
| `-o $@`            | Output file = the target (`$@` = the object file name)                 |

---

### 🧮 Example

Given:

```makefile
SRC_DIR = src
BUILD_DIR = build
HEADER = include
CXX = g++
CXXFLAGS = -Wall -Wextra
```

When you build `build/utils/math.o`, Make runs:

```bash
mkdir -p build/utils
g++ -Wall -Wextra -Iinclude -c src/utils/math.cpp -o build/utils/math.o
```

---

## 🧠 TL;DR Summary

| Rule                                 | Purpose                                     | Example Command                     |
| ------------------------------------ | ------------------------------------------- | ----------------------------------- |
| `$(NAME): $(OBJ)`                    | Link all object files into final executable | `g++ ... -o my_app`                 |
| `$(BUILD_DIR)/%.o: $(SRC_DIR)/%.cpp` | Compile each source file into `.o`          | `g++ -c src/foo.cpp -o build/foo.o` |
| `mkdir -p $(@D)`                     | Make sure the output directory exists       | `mkdir -p build/foo`                |

---
