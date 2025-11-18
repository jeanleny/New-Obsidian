
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

In this operator overload, here what's happening step by step
with $3 \times 2$ because we are shifting bits to get the fixed points value, the calculation becomes wrong
When shifting bits : $3 \times 1 000 000 \times 2 \times 1 000 000 = 6 000000000000$

So we prefer shift back all the result to get the right value 
Here, the long is used to store a potentially overflowed value, this way we can use it, even if its wrong because its how normal operators works.

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
Same as before, we're shifting bits to get the fixedpoint value.
In this case, a simplification is made, so we have to set it back.
# $\frac{3 \times 1 000 000} {2 \times 1 000 000}$

Becomes : 
# $\frac{3}{2}$

Which is wrong in our case so we shift everything back
# $\frac{3}{2} \times 1 000 000$
And the long is also used to store the overflowed value.
```c++
Fixed Fixed::operator/(Fixed const & rhs) const
{
	Fixed	result;
	
	long tmp = (1 << _fBits) * this->_value ;
	result._value = roundf(tmp / (float)rhs._value);
	return (result);
}
```

