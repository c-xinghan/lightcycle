# *LightCycle*
Replica of the [Tron arcade game](https://en.wikipedia.org/wiki/Tron_(video_game)).

https://github.com/c-xinghan/lightcycle/assets/23093512/2369ee9c-8aa5-488c-848f-28ef1dd77031

## Background
This was my contribution to a group project for my first-year undergraduate studies at SUTD. I was responsible for:
- Creating a terminal-based main menu to serve as a 'launcher' for each group member's game
- Creating this game

The rubrics dictate that we use only Python standard libraries. This necessitated building a helper class to handle vector calculations.

Full project (including all other members' work) can be found [here](https://github.com/WindJammer6/17.-Projects-from-School/tree/main/5.%20Arcade%20Minigames%20(Python)%20Project).

## Instructions
1. Run MainMenu.py in your favourite terminal.
2. Type <kbd>5</kbd> and press the <kbd>Enter</kbd> key to select the *LightCycle* game.
> Files for the other games are not included in this repository; they can be acquired seperately [here](https://github.com/WindJammer6/17.-Projects-from-School/tree/main/5.%20Arcade%20Minigames%20(Python)%20Project).
3. Choose a desired resolution and difficulty level. The difficulty level determines the speed of both players.
4. Player 1 ( ![#00ffff](https://placehold.co/15x15/00ffff/00ffff.png) `cyan`) moves using the <kbd>WASD</kbd> keys. Player 2 ( ![#ff8000](https://placehold.co/15x15/ff8000/ff8000.png) `orange`) moves using the <kbd>← → ↑ ↓</kbd> (arrow) keys.
5. To win, make your opponent collide with the map boundaries or any player's "tail".
> Pressing <kbd>Esc</kbd> quits the game instance.

## Documentation

### MainMenu.py
| Function | Description | Parameter(s) |
| ------------- | ------------- | ------------- | 
| `choose_option(filename)` | <ul><li>Opens the text file defined in the string `filename`.</li><li>Prompts user for input with a message consisting of first line in text file + each option's Displayed value and the corresponding input to select it.</li><li>User will be prompted for input until a valid input is received.</li><li>Once a valid input is received, its corresponding Actual value will be executed.</li><li>After execution is complete, this function then calls itself recursively, unless the user inputs ‘exit’.</li><li>This is to allow the main menu to stay open after returning from a mini-game.</li></ul> | `String filename`<br>Name of text file, in string format (e.g. “settings.txt”). The first line of the text file contains a message to be displayed. Subsequent lines contain the list of options to choose from (one option per line). Each option should have a Displayed value followed by an Actual value, separated by a pipe <kbd>\|</kbd>. The Actual value should be a callable function/method. |

### LightCycle.py
| Function | Description | Parameter(s) | Returned value(s) |
| ------------- | ------------- | ------------- | ------------- |
| `choose_option(filename)` | <ul><li>Opens the text file defined in the string `filename`.</li><li>Prompts user for input with a message consisting of first line in text file + each option's Displayed value and the corresponding input to select it.</li><li>User will be prompted for input until a valid input is received.</li><li>Once a valid input is received, its corresponding Actual value will be executed.</li><li>After execution is complete, this function then calls itself recursively, unless the user inputs ‘exit’.</li><li>This is to allow the main menu to stay open after returning from a mini-game.</li></ul> | `String filename`<br>Name of text file, in string format (e.g. “settings.txt”). The first line of the text file contains a message to be displayed. Subsequent lines contain the list of options to choose from (one option per line). Each option should have a Displayed value followed by an Actual value, separated by a pipe <kbd>\|</kbd>. The Actual value should be a callable function/method. | NIL |
| `draw_square(size, colour, x_offset, y_offset, fill=True)` | <ul><li>Uses a `Turtle` instance and the parameters passed in to draw a square.</li></ul> | `Integer size`<br>length of square’s sides<br><br>`String colour`<br>colour of square’s outline and/or fill<br><br>`Integer x_offset`<br>x position of square<br><br>`Integer y_offset`<br>y position of square<br><br>`Boolean fill`<br>whether to fill square with colour (defaults to `True`) | NIL |
|`in_boundary(head, res)`| <ul><li>Derives boundaries from the integer `res`, and checks if the `x` and `y` attributes of `head` are within those boundaries.</li></ul> | `Vector head`<br>`Vector` instance to check<br><br>`Integer res`<br>resolution of game window | `Boolean`<br>`True` if `x` and `y` attributes of `head` are within boundaries, `False` otherwise. |
| `render()` | <ul><li>Represents a single frame of the game.</li><li>Game advances as this function calls itself recursively until the game concludes</li><li>Moves players forwards using the `Vector.translate()` method.</li><li>Uses `in_boundary()` and the `in` operator to check for collisions with trails or boundaries.</li><li>If collision is detected, announce the winner and return `None` to exit the recursive loop.</li><li>Adds the `Vector` instance representing the current position to a `Set` of trails.</li><li>Uses function `draw_square()` to draw a new square representing the players’ current positions.</li><li>Calls itself to render the next frame</li></ul> | NIL | NIL |
| `main()` | <ul><li>Called to start the game.</li><li>Prints welcome message from a .txt file</li><li>Calls function `choose_option()` to let the user specify game options</li><li>Counts down to game start using a countdown message</li><li>Instantiates `Vector` objects representing each player’s starting position and direction vectors</li><li>Defines empty `Set`s, which will later contain `Vector` instances representing each player’s trails.</li><li>Instantiates `turtle.Screen()` and `turtle.Turtle()` objects, calls a series of methods on those instances</li><li>Binds controls to change direction by associating keypresses with calls to the `Vector.rotate()` method</li><li>Calls function `render()` to start the game</li><li>Binds control to exit game by associating the <kbd>Esc</kbd> key with calls to the `Turtle.Screen.bye()` method</li></ul> | NIL | NIL |

### helper.py

### Vector class

| Attribute | Description |
| ------------- | ------------- |
| `x` | Instance attribute. Represents the x-component of the `Vector`. |
| `y` | Instance attribute. Represents the y-component of the `Vector`. |
| `dir` | Instance attribute. A `String` describing the direction of the `Vector`. Can be any of the `String`s from the `directions` class attribute. |
| `hash` | Instance attribute. Stores the hash value of the `Vector` instance, or `None` if the `Vector` is not hashed. |
| `directions` | Class attribute. A `List` containing the possible `dir`s a `Vector` can have. |
| `unit_vectors` |  Class attribute. A `Dictionary` containing unit vectors as keys referencing their corresponding `dir` strings. |

| Method | Description | Parameter(s) | Returned value(s) |
| ------------- | ------------- | ------------- | ------------- |
| `__init__()` | <ul><li>Instantiates a `Vector` object. Assigns input parameters to `x` and `y` attributes, evaluates x and y components of its unit vector and looks up this unit vector in `unit_vectors` to find and assign the suitable `String` to assign to the `dir` attribute.</li></ul> | `Integer/Float x`<br>x-component of the vector.<br><br>`Integer/Float y`<br>y-component of the vector. | `Vector` instance |
| `x()` | <ul><li>Getter method for instance attribute `x`.</li></ul> | NIL | Instance attribute `x` |
| `x(new_x)` | <ul><li>Setter method for instance attribute `x`.</li></ul> | `Integer new_x`<br>Value to assign to instance attribute `x` | NIL |
| `y()` | <ul><li>Getter method for instance attribute `y`.</li></ul> | NIL | Instance attribute `y` |
| `y(new_y)` | <ul><li>Setter method for instance attribute `y`.</li></ul> | `Integer new_y`<br>Value to assign to instance attribute `y` | NIL |
| `dir()` | <ul><li>Getter method for instance attribute `dir`.</li></ul> | NIL | Instance attribute `y` |
| `translate(translator)` | <ul><li>Performs vector summation by adding `translator`'s `x` and `y` components to `self`’s `x` and `y` components respectively.</li></ul> | `Vector translator`<br><br>`Vector` to be added to `self`. | NIL |
| `rotate(new_dir)` | <ul><li>Performs rotation transformation on `self`.</li><li>Firstly, the number of 90 degree quadrants to rotate the vector by is calculated by comparing the indexes of parameter `new_dir` and instance attribute `dir` within class attribute `directions`.</li><li>The method then checks for 0 or 180 degree rotations and prevents them from happening.</li><li>Parameter `new_dir` is then assigned to instance attribute `dir`.</li><li>Lastly, these equations $$x_2 =  x_1 \cos \theta - y_1 \sin \theta$$ $$y_2 = x_1 \sin \theta + y_1 \cos \theta$$ as seen [here](https://matthew-brett.github.io/teaching/rotation_2d.html) are used to calculate and assign the new `x` and `y` attributes. | `String new_dir`<br>Intended `dir` after rotation transformation is complete. | NIL |
| `copy()` | <ul><li>Creates a new `Vector` instance with identical attributes to `self` and returns it.</li></ul> | NIL | `Vector` instance |
| `__eq__(other)` | <ul><li>Overrides default `==` operator behaviour, causing it to return `True` if two `Vector` instances being compared have identical `x` and `y` components. | `Vector other`<br>A `Vector` to perform the equality check against.</li></ul> | NIL |
| `__hash__()` | <ul><li>Hashes the `Vector` instance if it is not hashed.</li></ul> | NIL | NIL |
