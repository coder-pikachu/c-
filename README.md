# C++ Tutorial
> Nobody is perfect. So, any effort to highlight mistakes in this work will be highly appreciated.

1. [From Source to Execution](https://github.com/arorabharat/C-Tutorial/blob/master/README.md#from-source-to-execution)
2. [Operator Overloading](https://github.com/arorabharat/C-Tutorial/blob/master/README.md#operator-overloading)
3. [Function Overloading](https://github.com/arorabharat/C-Tutorial/blob/master/README.md#function-overloading)
4. [Function Templates](https://github.com/arorabharat/C-Tutorial/blob/master/README.md#function-templates)
5. [Default Constructor](https://github.com/arorabharat/C-Tutorial/blob/master/README.md#default-constructor)
6. [Reference Vs Pointers](https://github.com/arorabharat/C-Tutorial/blob/master/README.md#reference-vs-pointers)
7. [Request for Member](https://github.com/arorabharat/C-Tutorial/blob/master/README.md#request-for-member)
8. [Initialiser List](https://github.com/arorabharat/C-Tutorial/blob/master/README.md#initialiser-list)
9. [Destructor](https://github.com/arorabharat/C-Tutorial/blob/master/README.md#destructor)
10. [Map](https://github.com/arorabharat/C-Tutorial/blob/master/README.md#map)

## From Source to Execution
1. **Source file** eg source.cpp
2. **Preprocessing** processes the instruction which starts with `# .... ` in c++ and copy all the declaration in header in source file. Command to generate a preprocessed file is `
```bash
g++ -E source.cpp -o pre.cpp
```
3. **Compile** means generating a assembly code (inclusive of step 2).Generated file has .s extension. Command to generate it is 
```bash
g++ -S source.cpp
```
4. **Assemble** generate a file not of readable format called as object file. Generated file has .o extension. Command is 
```bash
g++ -c source.cpp`
```
5. **Linking** is done by Linker. All the files of the projects are specified during compilation and the linker link to the corresponding definition  of variable and function. There should not be multiple declaration of the same thing. Command is 
```bash
g++ file1.o file2.o ... 
``` 
Finally we get the executable a.out

## Operator Overloading
```cpp
class Name{
    return_type operator+(parameter list){
    }
};

struct Name{
    return_type operator+(parameter list){
    }
};
```
## Function Overloading
```cpp
int func (int a, int b){
  return (a*b);
}

double func (double a, double b){
  return (a/b);
}
```
## Function Templates
```cpp
template <class type1, class type2>
type1 sum (type1 a, type1 b){
    // where type2 can be used here
      return a+b;
}
```
Function to call to generic function
```
x = sum<type1,type2>(10,20);
```
If compiler can also automatically map the types if they are unambiguous.
It can also be used to pass constant integers like in cuda kernel.

## Default Constructor
*only inserted in the class implicitly if there is no user defined constructor
```cpp
class Name{
  // compiler will insert default construct here 
};
```
Declaration and  Instantiation of object 
```cpp
Name n1;
Name n2();
```

## Reference Vs Pointers

1. pointers can  be null but reference need to be initialised at the time of declaration.
2. reference can  not be reassigned but pointers can be.


## Request for Member
1. Pointer can only request a member of a class by -> operator.
2. Non-pointer type can request a member of a class by dot or . operator.


## Initialiser List
it is used to species the default values to parameter in case user do not provide them. Consider exmaple 
```cpp
class Point{
public:
    int x,y;
    Point(int x=0,int y=0):x(x),y(y){
    }
};
```
Declaration and  Instantiation of object 
```cpp
Point p; //or
Point p(1,2);
```


## Destructor
Destructor can not take any argument and can not return anything

```cpp
~className(){
  //remove whatever dynamic memory you want to remove
}
```

## Map

```cpp
bool fncomp (char lhs, char rhs) {return lhs<rhs;}
```

custom comparator
```cpp
struct classcomp {
  bool operator() (const char& lhs, const char& rhs) const
  {return lhs<rhs;}
};

  map<char,int> first;
  first['a']=10;
  first['b']=30;

  map<char,int> second (first.begin(),first.end());

  map<char,int> third (second);

  map<char,int,classcomp> fourth;                

  bool(*fn_pt)(char,char) = fncomp;
  map<char,int,bool(*)(char,char)> fifth (fn_pt);
```

Copying map
```cpp
map_new = map_old // copies the content of old map into new map
```
Traversing the elemets of the map
```cpp
for (map<T,U>::iterator it=m.begin(); it!=m.end(); ++it){
   T key_value     = it->first;
   U mapped_value  = it->second;
}
```
Finding an element
```cpp
map<T,U>::iterator = m.find(key); //It return pointer to end or found element
```
Inerting an element
```cpp
pair< map<T,U>::iterator, bool > p= m.insert(element);  //pointer to inserted element
itr = p.first;
isInseted = p.second;
```

## Extern 
extern is used for telling the compiler that don’t worry the variable or func is defined externally, if we have not defined the function. global part is common for the all the .o file so we can not define x (variable) globally in two different files. It will be multiple declaration. Static is used to tell linker don’t look for definition in other files or translational unit. This variable is just file_global not program_global.

assume file 1 contains the main function.

| case |file 1 | file 2 | output file 1 | output file 2 |
| --- | --- | --- | --- | --- |
| case 1 | int x=10; | int x=100; | error: multiple definition | error: multiple definition |
| case 2 | extern int x=10; | int x=100; | error: multiple definition | error: multiple definition |
| case 3 | extern int x; | int x=100; | 100 | 100 |
| case 4 | static int x=10; | int x=100; | 10 | 100 (if used in func) |







