In template Class :
In order to initialise class array, we can loop in each element of our array and assign a default constructor of the type value, like so :
```c++
Array(unsigned int const& n) :  _size(n), _array(new T[n]){
			for (size_t i = 0 ; i < _size ; i++)
				_array[i] = T();
		};
```


When you write:

```cpp
iter(tab, 5, print);
```

The compiler does this:

1. Deduces `T = int`
2. Sees required function type:

   ```cpp
   void (*)(int const&)
   ```
3. Instantiates:

   ```cpp
   print<int>
   ```
4. Converts it to a function pointer

Same for:

```cpp
iter(tab2, 5, print);
```

* `T = Awesome`
* Instantiates `print<Awesome>`
* Calls `operator<<`