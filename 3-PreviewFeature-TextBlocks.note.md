# 3. Preview Feature: Text Block

## Multi-line Strings

before:

`String json = "{\n  \"firstName\": \"Sander"\n  \"lastName\" ...`

- long line
- escaping characters
- not readable

after:

```java
class Main {
    public static void main(String[] args) {
        String json = """
                {
                    "firstName": "Sander",
                    "lastName": "Mak"
                }""";
        System.out.println(json);
    }
}
```

output:

```json
{
  "firstName": "Sander",
  "lastName": "Mak"
}
```

- indentation is preserved
- takes into account incidental vs essential indentation
  - incidental comes from how we indent our code (affected by how we place our three closing double quotes)
  - essential is how we indent our string

compiler processing of text blocks:

1. normalize line-endings (Windows vs Linux) to `\n`
2. trim non-essential whitespace
3. translate remaining escape sequences

## String API Changes

### `@Deprecated` `String::stripIndent()`

- strips incidental whitespace on any string as if it were a text block
- marked as deprecated `@Deprecated` because it is closely linked to text blocks (which are a preview feature)

### `@Deprecated` `String::translateEscapes()`

translate escape sequences from text coming outside of java code, like a text file

input.txt:

```text
\"Hello\tWorld\"\n
```

becomes when translated:
```text
"Hello  World"

```

### `@Deprecated` `String::formatted`

```java
class Main {
  public static void main(String[] args) {
    String html = """
            <html>
                <head></head>
                <body>%s</body>
            <html>
            """.formatted("Hello");
  }
}
```

