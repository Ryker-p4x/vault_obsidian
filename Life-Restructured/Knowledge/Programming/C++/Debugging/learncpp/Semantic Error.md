Unlike a syntax error, it won't crash the compiler or break the code. Instead, it's a logic error where the error makes it so that the logic is flawed. For example say you got a add function but instead of adding the values together it substracts them.

``` cpp
int add(int x, int y) // this function is supposed to perform addition
{
    return x - y; // but it doesn't due to the wrong operator being used
}
```

