# Rute

## Objective
Rute is a general purpose data-interchange file format that aims to be a concise alternative to XML.

## Syntax
The general form for elements:
```
name (attributes...) {
  children...
}
```

Much like XML, a Rute file contains a tree of data. Each element will have a name and may also contain attributes or child elements. While attributes and children are optional, a name is always required. Multiple elements are separated by commas or linebreaks.

Unlike XML, the children of an element can only contain other elements, not text. If you wish to include text in an element, you must do so in an attribute.

Do this:
```
paragraph (text "Here's some text")
```

Don't do this:
```
paragraph {Here's some text}
```

### Name
The element's name must come first. Names are case insensitive, can contain only letters, numbers, and underscores, and must start with a letter. They do not have to be unique, as they should describe the type of data they represent rather than be a unique identifier for the data. It is up to you to uniquely identify elements, which most likely will involve using a specific attribute as an ID.

Do this:
```
button (id "main-button", text "Click me!")
```

Don't do this:
```
main_button (type "button", text "Click me!")
```

### Attributes
If you chose not to omit them, the attributes will come right after the name, enclosed in parenthesis. To define an attribute, you must give its name followed by its value, separated by whitespace. Attribute names follow the same conventions as element names. Multiple attributes are separated by commas or linebreaks. Values can be either strings, numbers, or booleans.

Acceptable values:
```
element (id "example", score 94.5, win true)
```

## Examples
```
inbox {
  email (to "Max", from "Gracie", content "Hello brother, how are you?")
  email (to "Gracie", from "Max", content "I'm doing quite well, thank you!")
}
```
