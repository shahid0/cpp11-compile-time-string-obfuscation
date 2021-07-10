# cpp11-obfuscation
a mini project to obfuscate strings/hex and const char strings/objective c strings look at the obfuscate.h file

```cpp
    OBFUSCATE("som text"); // OBFUSCATE const char strings
    OBFUSCATE("hidden");
    OBFUSCATE("0x123456"); // can do conversions
     
    /*
     * only ios can use FBEncrypt
     */
    FBEncrypt("some text); // OBFUSCATE NSStrings disable
    FBEncrypt("hidden");
    FBEncrypt("0x123456"); // can do conversions

    OBFUSCATEHEX("0x12"); // OBFUSCATE hex 0x123456
    OBFUSCATEHEX("0x123456");
    OBFUSCATEHEX("0x123456789); // can encrypt long hex

    #define getRealOffset(offset) getAbsoluteOffset(OBFUSCATEHEX(offset))
    uint64_t getAbsoluteOffset(uint64_t offset);
    uint64_t getAbsoluteOffset(uint64_t offset){
        return (base + offset)
    }

    #define protectAbsoluteChar(str1, str2, str3) protectMeChar(OBFUSCATE(str1), OBFUSCATE(str2), OBFUSCATE(str3))
    void protectMeChar(const char *, const char *, const char *);
    void protectMeChar(const char *str1, const char *str2, const char *str3){
        OBFUSCATE("hidden");
        OBFUSCATE("absolutely hidden");

        str1 = (const char *)"str1 VALUE NOT HIDDEN";
        str2 = (const char *)"str2 VALUE NOT HIDDEN";
        str3 = (const char *)"str3 VALUE NOT HIDDEN";

        str1 = OBFUSCATE("str1 VALUE HIDDEN");
        str2 = OBFUSCATE("str2 VALUE HIDDEN");
        str3 = OBFUSCATE("str3 VALUE NOT HIDDEN");

        const char *mainValueH = OBFUSCATE("HIDDEN");                         // Contains a value to hide
        const char *mainValueNH = (const char *)"NOT HIDDEN";                 // Contains a value not to hide
        NSLog(@"mainValueNH: %s\nmainValueH: %s\n", mainValueNH, mainValueH); // iOS
        LOGD("mainValueNH: %s\nmainValueH: %s\n", mainValueNH, mainValueH);   // Android
    }

    /*
     * iOS Only.
     */
    #define protectAbsoluteNSString(str1, str2, str3) protectMeChar(FBEncrypt(str1), FBEncrypt(str2), FBEncrypt(str3))
    void protectMeNSString(NSString *, NSString *, NSString *);
    void protectMeNSString(NSString *str1, NSString *str2, NSString *str3){
        FBEncrypt("hidden");
        FBEncrypt("absolutely hidden");

        str1 = @"str1 VALUE NOT HIDDEN";
        str2 = @"str2 VALUE NOT HIDDEN";
        str3 = @"str3 VALUE NOT HIDDEN";

        str1 = FBEncrypt("str1 VALUE HIDDEN");
        str2 = FBEncrypt("str2 VALUE HIDDEN");
        str3 = FBEncrypt("str3 VALUE NOT HIDDEN");

        NSString *mainValueH = FBEncrypt("HIDDEN");                         // Contains a value to hide
        NSString *mainValueNH = @"NOT HIDDEN";                 // Contains a value not to hide
        NSLog(@"mainValueNH: %@\nmainValueH: %@\n", mainValueNH, mainValueH); // iOS
    }

    int main(){
       // Calling getRealOffset("hex")
       // Calling getAbsoluteOffset(0x123)

       uint64_t realOffset = getRealOffset("0x123456"); // must only be hex
       NSLog(@"getRealOffset: 0x%llx", realOffset);     // iOS
       LOGD("getRealOffset: 0x%llx", realOffset);       // Android(must define it)
  
       uint64_t absoluteOffset = getAbsoluteOffset(OBFUSCATEHEX("0x12345")); //    
       NSLog(@"absoluteOffset: 0x%llx", absoluteOffset);                     // iOS
       LOGD("absoluteOffset: 0x%llx", absoluteOffset);                       // Android(must define it)

      // calling our void functions
      protectAbsoluteChar("hidden", "hidden", "hidden");
      protectMeChar("NOT HIDDEN", "NOT HIDDEN", "NOT HIDDDEN");
      protectMeChar(OBFUSCATE("HIDDEN"), OBFUSCATE("HIDDEN"), OBFUSCATE("HIDDDEN"));

      // iOS only obj c
      protectAbsoluteNSString("HIDDEN", "HIDDEN", "HIDDEN");
      protectMeNSString(@"NOT HIDDEN", @"NOT HIDDEN", @"NOT HIDDEN");
      protectMeNSString(FBEncrypt("HIDDEN"), FBEncrypt("HIDDEN"), FBEncrypt("HIDDEN"));

    }
```
