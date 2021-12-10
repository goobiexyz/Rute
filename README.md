# Rute

## Objectives
Rute is a general purpose data-interchange file format that structures information in a relational tree. It aims to be a concise alternative to XML.

## Syntax

### Tree Structure
Much like XML, elements in a Rute file exist in a relational tree. Unlike XML, Rute does not require a root element, for the file itself is considered the root.

Child elements are contained in curly brackets that come at the end of an element declaration:
```
book (title "Example") {
  chapter {
    page (content "I just think the")
    page (content "world ought to be")
    page (content "more sort of organized.")
  }
}
```

Unlike XML, text cannot be mixed in with child elements, however text can be included as a property:
```
paragraph (text "Here's some text")
```

Don't do this:
```
paragraph {Here's some text}
```

### Elements
The general form for elements:
```
name (properties...) {
  children...
}
```

Each element has a name and may also contain properties and child elements. While properties and children are optional, a name is always required. Multiple elements are separated by linebreaks, but commas may be used if you wish to condense multiple elements on a single line.

#### Naming
The element's name must come first. Names should be semantic, meaning they describe the type of data they contain, and as such they don't need to be unique. It is up to you to uniquely identify elements, such as using a specific property as an ID:
```
button (id "main-button", text "Click me!")
```

Don't do this:
```
main_button (type "button", text "Click me!")
```

Names are case sensitive, must begin with a letter, and can contain only letters, numbers, and underscores.

#### Properties
If you chose not to omit them, the attributes will come right after the name, enclosed in parenthesis. To define an attribute, you must give its name followed by its value, separated by whitespace. Attribute names follow the same conventions as element names. Values can be either strings, numbers, or booleans:
```
element (id "example", score 94.5, win true)
```

Multiple properties are separated by commas, but line-breaks may be used instead if there is a need:
```
article (date "5-01-2021", author "Gracie"
  summary "A really long string of text should have its own line."
)
```
##### Strings
Enclose text in double quotation marks to mark it as a string.

Line-breaks in strings should be ignored, so represent them with `\n`.

If you wish to use quotation marks or backslashes in a string as normal characters, you can precede them with a backslash `\`:
```
paragraph (text "\"You're hearing things,\" said the voice in Rincewind's head.")
image (path "C:\\Pictures\\bunny.png")
```

## Examples
```
inbox {
  email (to "Max",    from "Gracie", content "Hello brother, how are you?")
  email (to "Gracie", from "Max",    content "I'm doing quite well, thank you!")
}
```
