# Rute
## Objective
Rute aims to be a data-interchange file format that can be used as a concise alternative to XML.
## Syntax
A Rute file contains a tree of data. Each element is declared with a name and can include attributes and/or additional child elements. All elements will follow this general pattern:
```
name (attribute1 val1, attribute2 val2) { children }
```
To declare an element, first you must write the name. This name can be non-unique.
What follows the name must be either the attributes or the children. If neither are present, the element is considered to be invalid.
Commas and linebreaks can be used interchangeably to separate elements from elements and attributes from attributes.
## Examples
```
# Define an array
inbox {
  email [
    (to "Max", from "Gracie", content "Hello brother, how are you?")
    (to "Gracie", from "Max", content "I'm doing quite well, thank you!")
  ]
}
```
