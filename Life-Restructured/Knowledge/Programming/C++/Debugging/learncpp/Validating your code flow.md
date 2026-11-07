When debugging you can use std:cerr to print whether a function got called and ran. Example:

```cpp
#include <iostream>

int getValue()
{
std::cerr << "getValue() called\n";
	return 4;
}

int main()
{
std::cerr << "main() called\n";
    std::cout << getValue << '\n';

    return 0;
}
// Not indenting the std::cerr can make it easier to later find them in code.
```