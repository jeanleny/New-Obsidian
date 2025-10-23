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
In this case the programm will return an error :
Error: y is private