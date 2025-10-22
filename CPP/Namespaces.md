Namespace are groups of values that are used to organize code into logical groups avoiding name collision.
```c++
int i = 4;
int f(void)
{
	return (40);
}

namespace Foo
{
	int i = 0;
	int f(void)
	{
		return (1);
	}
}

i = 4
Foo::i = 0;

f() = 40;
Foo::f() = 1;

```
We're accessing the data with the [[Scope resolution operator]]


