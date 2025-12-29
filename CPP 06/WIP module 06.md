Floating points are just value with a floating point that can store exponants and decimal value to add precision.
Usually we call floating points  single-precision-floating-point format wich is a value stored in 32bits.

Doubles are the same but more precise because stored in 64bits.

In static cast, STATIC means that its happening during compilation, unlike DYNAMIC that occurs during runtime.

When a static cast is done on too big value, the value is rounded to the max possible :
```c++
long double nb = 100000000000000000;
std::cout << std::fixed << static_cast<float>(nb) << std::endl;
```
	result = 99999998430674944.00000

this happens because this value cannot be stored in a float, so its being round up

Type is the format of data we are working with, but we also have family of type.
Pointers are parts of the same family of pointer, reference aswell , same for floats and double.