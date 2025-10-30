Most of the time, members in classes are in Private [[Access Specifier]].
In order to set or get private values, we're using setters and getters.
Basically, these are just function that are called specifically called to set and get values and nothing else.
There are still function, so they can set values under conditions.
HPP
```c++
#ifndef	PHONE_BOOK_H
# define	PHONE_BOOK_H

class	PhoneBook
{
	public:

	int	getOui(void) const;
	void	setOui(int value);
	PhoneBook(void);
	~PhoneBook(void);

	private :
	int	_oui;
};

#endif
```

```c++
#include <iostream>
#include "../include/PhoneBook.hpp"

PhoneBook::PhoneBook()
{
	std::cout << "oui sa kkonstrui" << std::endl;
	return ;
}

PhoneBook::~PhoneBook()
{
	std::cout << "la daisstruktion" << std::endl;
	return ;
}

void	PhoneBook::setOui(int value)
{
	this->_oui = value;
	return;
}

int	PhoneBook::getOui()const
{
	return (_oui);
}

int	main(void)
{
	PhoneBook test;
	test.setOui(42);
	std::cout << test.getOui() << std::endl;
	test.setOui(2);
	std::cout << test.getOui() << std::endl;
}
```