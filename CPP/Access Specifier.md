An access specifier control how members or methods of a class can be accessed.
In C++, there are 3 access specifier : 

 Private :
 Members that are Private, cannot be accessed from outside the class.
 Here is an example of a Private and Public members usage
```c++
 class MyClass {
  public:    // Public access specifier
    int x;   // Public attribute
  private:   // Private access specifier
    int y;   // Private attribute
};

int main() {
  MyClass myObj;
  myObj.x = 25;  // Allowed (public)
  myObj.y = 50;  // Not allowed (private)
  return 0;
}
 ```
In this case the program will return an error on compilation :
Error: y is a private member of PhoneBook

By default, all members of a class are private if not specified.

Public :
Members that are publics are just members of a class that can be accessed and modified outside of the code.

Protected :
Like private, protected members cannot be accessed from outside the code, but they can be accessed in child classes.