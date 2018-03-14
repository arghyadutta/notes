In this file I will write down the general good practices which are to be followed, in general. I am not entirely sure about all of them, so I will try to reference the source from where I  got it.

General resources:
* [C++ best practices](https://www.gitbook.com/book/lefticus/cpp-best-practices/details)

# Index:

* [Array](#S-array)
    * [std::array::at](#S-array-at)
    * [std::size_t](#S-array-size_t)
* [Naming](#S-naming) 

================================================================================
## <a name="#S-naming"> </a> Naming conventions 

[Source](https://lefticus.gitbooks.io/cpp-best-practices/content/03-Style.html)

Use descriptive names, and be consistent in the style. Two styles: CamelCase and snake_case.

* Types start with upper case: MyClass.
* Functions and variables start with lower case: myMethod.
* Constants are all upper case: const double PI=3.14159265358979323;.
* Macro names use upper case with underscores: INT_MAX.
* Template parameter names use camel case: InputIterator.
* All other names use snake case: unordered_map.
* Don't Name Anything Starting With _ . If you do, you risk colliding with names reserved for compiler and standard library implementation use: [StackOverflow](
http://stackoverflow.com/questions/228783/what-are-the-rules-about-using-an-underscore-in-a-c-identifier)
* Name private data with a m_ prefix to distinguish it from public data. m_ stands for "member" data.
* Name function parameters with an t_ prefix. t_ can be thought of as "the", but the meaning is arbitrary. The point is to distinguish function parameters from other variables in scope while giving us a consistent naming strategy.

================================================================================

## <a name="S-array"> </a> Array [Cplusplus](http://www.cplusplus.com/doc/tutorial/arrays/)


Use std::array over normal c-style ones. Slightly slower, but safer and you can access different fucntions like sort, size directly.

`std::array` is a container built on top of a C-style array. Supports common container operations such as sorting.
```
std::array<int, 3> a = {2, 1, 3};
std::sort(a.begin(), a.end()); // a == { 1, 2, 3 }
for (int& x : a) x *= 2; // a == { 2, 4, 6 }
```

### <a name="S-array-at"> </a> `std::vector::at` or `std::array::at`(C++11) [cplusplus](http://www.cplusplus.com/reference/array/array/at/)

This returns a reference to the element at position n of the vector or array. It is better than accessing by `A[n]` as if n is out of bounds, it throws an exception, while `[]` operator does not.

Use:

```
// array::at
#include <iostream>
#include <array>
int main ()
{ std::array<int,10> myarray;
  // assign some values:
  for (int i=0; i<10; i++) myarray.at(i) = i+1;
  // print content:
  std::cout << "myarray contains:";
  for (int i=0; i<10; i++)
    std::cout << ' ' << myarray.at(i);
  std::cout << '\n';
  return 0;
}
```
### <a name="#S-array-size_t"> </a> `std::size_t` [cppreference](http://en.cppreference.com/w/cpp/types/size_t)

`std::size_t` is an unsigned integer type and is the result of `sizeof` operator. It is commonly used for **array indexing** and **loop indexing**. It is safer than declaring plain unsigned integer.

Use:
```
int main()
{
    const std::size_t N = 10;
    int* a = new int[N];

    for (std::size_t n = 0; n < N; ++n)
        a[n] = n;
}
```

## Standard output precision

```
double d{1.12345}
std::cout.precision(5);
std::cout<<std::fixed<<d<<'\n';
```

will print exactly 1.12345. If we want to print 1.1234500, set precision to 7. 
In this file I will write down the general good practices which are to be followed, in general. I am not entirely sure about all of them, so I will try to reference the source from where I  got it.

General resources:
* [C++ best practices](https://www.gitbook.com/book/lefticus/cpp-best-practices/details)

# Index:

* [Array](#S-array)
    * [std::array::at](#S-array-at)
    * [std::size_t](#S-array-size_t)
* [Naming](#S-naming) 

================================================================================
## <a name="#S-naming"> </a> Naming conventions 

[Source](https://lefticus.gitbooks.io/cpp-best-practices/content/03-Style.html)

Use descriptive names, and be consistent in the style. Two styles: CamelCase and snake_case.

* Types start with upper case: MyClass.
* Functions and variables start with lower case: myMethod.
* Constants are all upper case: const double PI=3.14159265358979323;.
* Macro names use upper case with underscores: INT_MAX.
* Template parameter names use camel case: InputIterator.
* All other names use snake case: unordered_map.
* Don't Name Anything Starting With _ . If you do, you risk colliding with names reserved for compiler and standard library implementation use: [StackOverflow](
http://stackoverflow.com/questions/228783/what-are-the-rules-about-using-an-underscore-in-a-c-identifier)
* Name private data with a m_ prefix to distinguish it from public data. m_ stands for "member" data.
* Name function parameters with an t_ prefix. t_ can be thought of as "the", but the meaning is arbitrary. The point is to distinguish function parameters from other variables in scope while giving us a consistent naming strategy.

================================================================================

## <a name="S-array"> </a> Array [Cplusplus](http://www.cplusplus.com/doc/tutorial/arrays/)


Use std::array over normal c-style ones. Slightly slower, but safer and you can access different fucntions like sort, size directly.

`std::array` is a container built on top of a C-style array. Supports common container operations such as sorting.
```
std::array<int, 3> a = {2, 1, 3};
std::sort(a.begin(), a.end()); // a == { 1, 2, 3 }
for (int& x : a) x *= 2; // a == { 2, 4, 6 }
```

### <a name="S-array-at"> </a> `std::vector::at` or `std::array::at`(C++11) [cplusplus](http://www.cplusplus.com/reference/array/array/at/)

This returns a reference to the element at position n of the vector or array. It is better than accessing by `A[n]` as if n is out of bounds, it throws an exception, while `[]` operator does not.

Use:

```
// array::at
#include <iostream>
#include <array>
int main ()
{ std::array<int,10> myarray;
  // assign some values:
  for (int i=0; i<10; i++) myarray.at(i) = i+1;
  // print content:
  std::cout << "myarray contains:";
  for (int i=0; i<10; i++)
    std::cout << ' ' << myarray.at(i);
  std::cout << '\n';
  return 0;
}
```
### <a name="#S-array-size_t"> </a> `std::size_t` [cppreference](http://en.cppreference.com/w/cpp/types/size_t)

`std::size_t` is an unsigned integer type and is the result of `sizeof` operator. It is commonly used for **array indexing** and **loop indexing**. It is safer than declaring plain unsigned integer.

Use:
```
int main()
{
    const std::size_t N = 10;
    int* a = new int[N];

    for (std::size_t n = 0; n < N; ++n)
        a[n] = n;
}
```

## Standard output precision

```
double d{1.12345}
std::cout.precision(5);
std::cout<<std::fixed<<d<<'\n';
```

will print exactly 1.12345. If we want to print 1.1234500, set precision to 7. 
