In order to initialize values while constructing classes, we can use [[This Pointer]] or [[Initialization lists]].

Those lists allow us to set each value directly in the constructor call next to the parameters.
When using this method, we're not attributing, we're INITIALIZING values, which is different.
This means its only possible to use them in Constructors.
Example
.hpp
```c++
#ifndef	PHONE_BOOK_H
# define	PHONE_BOOK_H

class	PhoneBook
{
	public:

	char	oui;
	char	non;
	int		oskour;
	int	lavaleurdeoui(void);
	PhoneBook(char c1, char c2, int i3);
	~PhoneBook(void);
};

#endif

```

```c++
#include <iostream>
#include "../include/PhoneBook.hpp"

PhoneBook::PhoneBook(char c1, char c2, int i3) : oui(c1), non(c2), oskour(i3)
{
	std::cout << "c1 =" << c1 << std::endl;
	std::cout << "c2 =" << c2 << std::endl;
	std::cout << "i3 =" << i3 << std::endl;
}

PhoneBook::~PhoneBook(void)
{
	std::cout<<"Destroy"<<std::endl;
	return;
}

int	PhoneBook::lavaleurdeoui(void)
{
	return (76896);
}

int	main(void)
{
	PhoneBook a('o', 'i', 123);
		
	std::cout<<a.oui<<std::endl;
	return (1);
}
```
In this exemple, the class members becomes the parameters of the given constructor.
