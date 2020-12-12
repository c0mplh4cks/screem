# screem

A package containing multiple functions to make a graphical user interfaces in the terminal.

## Usage

### Decorating strings

```
from c0mplh4cks.screem import decorate
x = decorate( "Hello world!", fg=(255,160,0), bg=(0,0,255), bold=1, italic=1, underline=1, blink=1, invert=0 )
print(x)
```
This snippet of code prints 'Hello World!' on the screen with orange as foreground color and blue as background color in **bold** and *italic* with an underline while blinking. When invert is True, the foreground color changes to the background color and the other way around. Everything will continue with the same decorations when printing while the end argument is set to False.


### Operating the Cursor
For the following examples we import the 'cursor' class like this:
```
from c0mplh4cks.screem import cursor
```

---

#### Changing the visibility of the cursor
```
cursor.hide()
cursor.show()
```
The above hides the terminal cursor and instantly after that shows the cursor to make it visible again. *This does not affect anything printed.*

---

#### Changing the visibility of printed text
```
cursor.conceal()
print( "This should not be visible" )
cursor.reveal()
```
`conceal` will hide everything that gets printed and `reveal` makes everything that gets printed visible again.

---

#### Moving the cursor by direction
```
cursor.move.up(1)
cursor.move.down(2)
cursor.move.left(3)
cursor.move.right(4)
```
This snippet of code moves the cursor up by one row, down by two rows, left by three columns and finally moves the cursor with four columns to the right.

---

#### Moving the cursor by line
```
cursor.move.nextline(2)
cursor.move.prevline(3)
```
This moves the cursor down by 2 rows and also moves the cursor to the beginning of the line, and after that moves the cursor up by three rows and also moves the cursor to the beginng of the line.

---

#### Moving the cursor by row and column
```
cursor.move.position(3, 5)
```
This function moves the cursor to the third row and the fifth column. *Note that the first row and column are 1 and not 0!*

---

#### Clearing parts of the screen
```
cursor.clear.display(0)
cursor.clear.display(1)
cursor.clear.display(2)
cursor.clear.display(3)
```
The first line clears from the cursor to the end of the screen, the second line clears from the cursor to the beginning of the screen, the third line clears the entire screen and the fourth line clears the entire screen and clears the scrollback buffer. *Note that some of these functions do not work when used alone*

---

#### Clearing parts of the line
```
cursor.clear.line(0)
cursor.clear.line(1)
cursor.clear.line(2)
```
When given 0, the function clears from the cursor to the end of the screen. When given 1, the function clears from the cursor to the beginning of the screen. When given 2, the function clears the whole line.


### Using the Screen object
For the following examples we import the 'Screen' object like this:
```
from c0mplh4cks.screem import Screen
```

---

#### Displaying the terminal size
After initializing the object, there are two attributes which could be used `w` and `h`. Those attributes contain the width and height of the terminal. The method `terminalsize` sets those attributes and for that reason also gets called when initializing the Screen object. An example which prints the terminal width and height:
```
screen = Screen()
print( f"width of terminal: { screen.w }" )
print( f"height of terminal: { screen.h }" )
```

---

#### Printing decorated text with coordinates
```
decorations = { "bold":1, "fg":(255,0,0) }
screen = Screen()
screen.write( "Hello world!", 2, 4, dec=decorations )
```
The above is an example for the `write` method which is a combination of the `cursor.move.position` function and the `decorate` function. It prints 'Hello World!' on the second row and fourth column with the decorations dictionary as decorations.

---

#### Clearing the screen
```
screen = Screen()
screen.clear()
```
The method `clear` clears the screen, clears the scrollback buffer and resets the cursor position to the first row and column.

---

#### Proper usage
```
screen = Screen()
screen.start()
print("This should disappear when screen.stop() gets called")
key = screen.key()
screen.stop()
print( f"pressed key: { key }" )

```
The `start` method enables alternate screen buffer and modifies sys.stdin to be able to read single key inputs with the `key` method. The `stop` method, which should be used when using `start`, disables alternate screen buffer and sets the sys.stdin settings back to normal.

---

#### Cleaning the screen
```
screen = Screen()
screen.clean()
```
The `clean` method could be used instead of the `stop` method, since it also calls `stop` and on top of that automatically calls `cursor.show` and `cursor.reveal`. It also prevents the `decorate` function messing up the terminal by disabling decorations.
