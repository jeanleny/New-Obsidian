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

# Members in Class

Members, as its name suggest, are just variables, functions or even classes stored in that class.

You can call any of them and change them unless the [[Access Specifier]] does not allow you to do it.
	
In C, when you wanted to add function in structures, you had to create a pointer on funtions, redirect the pointers and dereference it to use it.
In CPP it's easier, you only have to declare it in your .hpp, write the logic of your function in your .cpp and call it whenever you want.

Here is an example :
```c++
#ifndef	PHONE_BOOK_H
#define	PHONE_BOOK_H

class	PhoneBook
{
	public:
	
	int	oui;
	int	lavaleurdeoui(void);
	PhoneBook(void);
	~PhoneBook(void);
};

#endif

```
```c++
int	PhoneBook::lavaleurdeoui(void)
{
	return (76896);
}

int	main(void)
{
	PhoneBook a;

	a.oui = a.lavaleurdeoui();
	std::cout<<a.oui<<std::endl;
	return (1);
}
```

Values can also be set by [[This Pointer]].