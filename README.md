![Rute](logo.png)
====

Rute is a general purpose data-interchange file format that structures information in a relational tree. It aims to be a concise alternative to XML.

## Syntax

### Comparison to XML

#### XML
```
<blog title="My Blog" link="https://example.com">
  <post id="1" date="10-19-2021" title="Example" read="false">
    XML has so many unnecessary characters
  </post>
  <post id="0" date="10-19-2021" title="Example" read="true">
    Closing tags look cluttered
  </post>
</blog>
```
#### Rute
```
blog (title "My Blog", link "https://example.com) {
  post (
    id    1
    date  "10-19-2021"
    title "Example"
    read  false
    body  "Rute is much less tedious"
  )
  post (
    id    0
    date  "10-19-2021"
    title "Example"
    read  true
    body  "It's easier to read too"
  )
}
```

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

Each element has a name and may also contain properties and child elements. While properties and children are optional, a name is always required.

Rute can also be minified, since whitespace doesn't matter except for seperating properties from values. Commas can be used to separate elements on the same line that **don't** have child contexts:
```
item,item(id "example"),item{item}item
```
Otherwise, use linebreaks to seperate elements.

#### Naming
The element's name must come first. Names should be semantic, meaning they describe the type of data they contain, and as such they don't need to be unique. It is up to the programmer to uniquely identify elements, such as using a specific property as an ID, for example:
```
button (id "submit", text "Click me!")
```

Names are case sensitive, must begin with a letter, and can contain only letters, numbers, and underscores.

#### Properties
If you chose not to omit them, the properties will come right after the name, enclosed in parenthesis. To define an property, you must give its name followed by its value, separated by whitespace. Property names follow the same conventions as element names. Values can be either strings, numbers, or booleans:
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

Line-breaks in strings are ignored, so represent them with `\n`.

If you wish to use quotation marks or backslashes in a string as normal characters, you can precede them with a backslash `\`:
```
paragraph (text "\"You're hearing things,\" said the voice in Rincewind's head.")
image (path "C:\\Pictures\\bunny.png")
```

### Comments
Annotate your code with comments by prefixing them with `#`, and any text that follows will be ignored until a newline is reached:
```
# This is a comment
```

The `#` should be treated as a regular character if inside a string:
```
element (property "# This will not be ignored")
```

## More Examples

Simple email inbox:
```
inbox {
  email (to "Max",    from "Gracie", content "Hello brother, how are you?")
  email (to "Gracie", from "Max",    content "I'm doing quite well, thank you!")
}
```

Gui layout:
```
menu (id "main-menu") {
  grid (rows 2, cols 2) {
    button (
      text "Start"
      ref "load-game"
      color "red"
    )
    button (
      text "Level Select"
      ref "level-select"
      color "blue"
    )
    button (
      text "Settings"
      ref "settings"
      color "green"
    )
    button (
      text "Quit"
      ref "quit"
      color "razzmatazz"
    )
  }
}
```

## How to Help
I'm currently making a Rute parser in Go because that's what I need it for right now, but please feel free to help bring Rute to more people by writing your own parsers in other languages! And please let me know if you do, I'd love to hear about it!
