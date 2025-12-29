In template Class :
In order to initialise class array, we can loop in each element of our array and assign a default constructor of the type value, like so :
```c++
Array(unsigned int const& n) :  _size(n), _array(new T[n]){
			for (size_t i = 0 ; i < _size ; i++)
				_array[i] = T();
		};
```
