In CPP, a Great way of protecting values in complex Classes is to use const.
In C we're using const to declare a constant value.
In CPP, we can use const in values but also in fonction/Constructor...

Example :
hpp
```c++
#ifndef	PHONE_BOOK_H
# define	PHONE_BOOK_H

class	PhoneBook
{
	public:

	char		oui;
	char		non;
	int			oskour;
	float const	pi;
	int			lavaleurdeoui(void);
	void		mapotitefonction(void) const;
	PhoneBook(char c1, char c2, int i3, float const p);
	~PhoneBook(void);
};

#endif
```

```c++
#include <iostream>
#include "../include/PhoneBook.hpp"

PhoneBook::PhoneBook(char c1, char c2, int i3, float p) : oui(c1), non(c2), oskour(i3), pi(p)
{
	std::cout << "c1 =" << c1 << std::endl;
	std::cout << "c2 =" << c2 << std::endl;
	std::cout << "i3 =" << i3 << std::endl;
}

PhoneBook::~PhoneBook(void)
{
	std::cout<<"elle sont parties"<<std::endl;
	return;
}

int	PhoneBook::lavaleurdeoui(void)
{
	return (76896);
}

void	PhoneBook::mapotitefonction(void) const
{
	std::cout<<this->pi<<std::endl;
	std::cout<<this->oskour<<std::endl;
}

int	main(void)
{
	PhoneBook a('o', 'i', 123, 3.14);
		
	std::cout<<a.oui<<std::endl;
	a.mapotitefonction();
	a.pi = 8;
	return (1);
}
```

in this case the program won't compile !
We're trying to change the value of the member pi which is a const.

Its a common thing to write Setters and Getters in const.
Getters because result of getters will stay the same.
```c++
std::string	getDarkestSecret(void) const;
```

Setters because the value to set will alays be the same.\
```c++
void	setFirstName(const std::string &firstName);
```


# const on constructors
Const, by definition, cannot be changed, that so, on constructors calls, const variable cannot be assigned by overload operators.
But, they can through initialisation list.
Because, on initialisation list, const variable are not considered initialized, so you can set values on them.

Great use of const :
```c++
const int test = 6;
```


Won't compile :
```c++
const int test;
test = 6;
```

```c++

class Base
{
public:
	Base();
	Base(const Base& other);
	Base& operator=(const Base& other);
};

Base::Base() {}

Base::Base(const Base& other)
{
	(void) other;
}

void Base::operator=(const Base& other)
{
	(void) other;
	return (*this);
}

///////////

int main(void)
{
	Base b1;// Default constructor
	
	Base b2(b1);// Copy constructor
	
	Base b3 = b1;// Copy constructor
	
	Base b4;// Default constructor
	b4 = b1;// Assignement operator
}

int a = int();
```