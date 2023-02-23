# 2. Java 13 API Updates

## Introducing Java 13

- Java 9: module system
- Java 10: var
- Java 11: LTS
- Java 12: Switch Expressions (Preview Feature)

## API Updates

### ByteBuffer

- it's all about reading and manipulatin blocks of bytes that belong together
- it's different from a `byte[]` array
  - byte array: fixed size, always allocated on the java heap, mutable 
  - not true for ByteBuffer
- provide a view through an interface on bytes of some underlying storage
- offers methods for efficiently manipulating the underlying bytes
- direct & indirect ByteBuffers
- used a lot in the new I/O APIs of Java
- improvements
  - put and get in bulk
    - `ByteBuffer get(int index, byte[] dst)`
    - `ByteBuffer put(int index, byte[] src)`
    - `ByteBuffer get(int index, byte[] dst, int offset, int length)`
    - `ByteBuffer put(int index, byte[] src, int offset, int length)`

### Removal: `javax.security.cert`

- most important types
  - `javax.security.cert.Certificate` -->  `java.security.cert.Certificate`
  - `javax.security.cert.X509Certificate` --> `java.security.cert.X509Certificate` 

## Switch Expressions Update

the `break` keyword was replaced by a new keyword `yield` to return from a case

```java
class Main {
    public static void main(String[] args) {
        int monthNumber = 1;
        String monthName = switch (monthNumber) {
            case 1 -> {
                String month = "January";
                yield month;
            }
            case 2 -> {
                String month = "February";
                yield month;
            }
            // ...
            default -> "Unknown";
        };
        System.out.println("monthName = " + monthName);
    }
}
```

## Localization & Garbage Collection

### Unicode 12.1 Support

- 4 new scripts (languages)
- 555 new characters
- 61 new emoji characters
- CLDR (Common Locale Data Repository) 35.1: supports Japanewse new era, Reiwa

### ZGC: Uncommit Unused Memory

- after a delay of 5min unused memory is returned to the OS by ZGC
- still experimental GC
