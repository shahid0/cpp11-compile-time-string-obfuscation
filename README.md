# cpp11-obfuscation
a mini project to obfuscate strings/hex and const char strings/objective c strings look at the obfuscate.h file

```cpp
    OBFUSCATE("som text"); // OBFUSCATE const char strings
    /*
     * iOS only can use FBEncrypt
     */
    FBEncrypt("some text); // OBFUSCATE NSStrings disable
    OBFUSCATEHEX("obfuscate some hex"); // OBFUSCATE hex 0x123456
```
