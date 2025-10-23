A class is like a data structure in C, a way to store a lot a data and access them easily.
They can contain data member, but also function as data members.
And an Object is an instantiation of this class, the class is like the blueprint of this object.

Like structures, classes are declared in .hpp files to create the blueprint.
Here is an exemple of a class declaration.
```c++
#ifndef	PHONE_BOOK_H
#define	PHONE_BOOK_H

class	PhoneBook
{
	public:

	PhoneBook(void);
	~PhoneBook(void);
};

#endif
```
public is an [[Access Specifier]].
