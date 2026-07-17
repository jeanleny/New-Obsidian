The :: is called the Scope resolution operator, this operator is used to refer a value in different instance like namespace or class.

These scope are used to add class logic in .cpp files, like so :
```c++
class World
{
	public
		World() //<--Default constructor
		~World()
}

World::World() //<--DEfault constructor has been called by scope resolution operator
{
	std::cout << "default constructor called" << std::endl;
}
```