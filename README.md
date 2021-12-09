# Rute

## Objective
Rute is a data-interchange file format that aims to be a concise alternative to XML.

## Syntax
Much like XML, a Rute file contains a tree of data. Each element is declared with a name and can include attributes and/or additional child elements.

Unlike XML, elements can only contain other elements. If you wish to include text with an element, it must be included as an attribute. For example,
```
paragraph (text "XML sucks!")
```
The general form for elements is as follows:
```
name (attribute1 val1, attribute2 val2) { children }
```
The element's name must come first. Element names do not have to be unique, as they should describe the type of data they represent rather than be a unique identifier for the data. It is up to you to uniquely identify elements, which most likely will involve using a specific attribute to hold a key.
Bad:
```
mainbutton (type "button", text "Click me!")
```
Good:
```
button (id "main-btn", text "Click me!")
```
To declare an element, first you must write the name. This name can be non-unique.
What follows the name must be either the attributes or the children. If neither are present, the element is considered to be invalid.
Commas and linebreaks can be used interchangeably to separate elements from elements and attributes from attributes.
## Examples
```
inbox {
  email (to "Max", from "Gracie", content "Hello brother, how are you?")
  email (to "Gracie", from "Max", content "I'm doing quite well, thank you!")
}
```
