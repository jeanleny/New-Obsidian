
Fixed networking : 

FACTOR 1/1000
1.2= 50

| 256 | 128 | 64  | 32  | 16  | 8   | 4   | 2   | 1   | radix | 1/2 |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | ----- | --- |
| 3   | 2   | 6   | 8   | 4   | 3   | 9   | 3   | 5   | .     | 9   |


# Overload Operator

ADD operator '+'
to add the value of an object to another we have to create an object to store the result
```c++
Fixed Fixed::operator+(Fixed const & rhs) const
{
	Fixed	result;

	result._value = this->_value + rhs._value;
	return (result);
}
```

SUB operator '-'
same for the 
```c++
Fixed Fixed::operator-(Fixed const & rhs) const
{
	Fixed	result;

	result._value = this->_value - rhs._value;
	return (result);
}
```

MULTIPLY operator 'x'


```c++
Fixed Fixed::operator*(Fixed const & rhs) const
{
	Fixed	result;

	long tmp = this->_value * rhs._value;
	result._value = tmp / (1 << _fBits);
	return (result);
}
```

DIVIDE operator '/'
```c++
Fixed Fixed::operator/(Fixed const & rhs) const
{
	Fixed	result;
	
	long tmp = (1 << _fBits) * this->_value ;
	result._value = roundf(tmp / (float)rhs._value);
	return (result);
}
```

