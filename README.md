# Ruby Documentation

## Class Structure

Each of the custom classes you write in OCS should be documented on a class level as follows:

- **Class:** This is just the class name.
- **Description:** Quick one or two sentence description of the class. As much as possible, treat each class as though it's in a vacuum
- **Data Members:** Any attribute variables. When we get into ActiveRecord associations, you'll also want to include your `has` and `belongs_to` associations. Each attribute variable should have the variable name, the type, and a quick description of what the variable actually is.
- **Public Interface:** These are the public-facing methods that other classes might use to interact with your object. Note that a fair number of methods you write for a given class will *only* be called by other methods of that class; any method that is not meant to be called by objects of other classes should not be listed as part of the public interface. Note that we're not listing any meaningful descriptions for these methods -- that's for later.

Once the docs are done, you can write your class. It is usually best practice to update your docs as you go, rather than to try to get it all done in one fell swoop ahead of time.

```ruby
# Class: Dog
#
# Models our canine pals.
#
# Attributes:
# @name   - String: the dog's name.
# @breed  - String: the dog's breed.
# @age    - Integer: the dog's age in months. Must be positive.
# @weight - Integer: the dog's weight in pounds. Must be positive.
# @good   - Boolean: whether this dog is a good dog (true) or not (false).
#
# Public Methods:
# #bark
# #wag
# #drool
# #run

class Dog
  # ... The actual class code goes here.
end
```

## Method Documentation

We use a slightly modified version of the [TomDoc](http://tomdoc.org) method documentation format.

The format is pretty simple, and you'll include this for every custom method you write. Your methods will need to include:

- Whether the method is part of the public interface (**Public**) or a method that is only called by other methods in the same class (**Private**).
- The method's name, preceded by a hash.
- A quick description of the method (in a sentence).
- A list of parameters, one per line. Each parameter should include the parameter name, the expected parameter type, and a quick description of what this value represents.
- The return value(s) and their type(s). If there is special significance to the set of possible return values, you should write that out.
- Any state changes, i.e. any changes this method makes to the attributes of the object to which it belongs, or to any other objects it might interact with.

```ruby
# Public: #play
# Starts and then plays the game with the provided players.
#
# Parameters:
# player1 - Player: One of the players.
# player2 - Player: Another player.
# player3 - Player: This isn't a real parameter for this method, but it's here to demonstrate
#           how you would type a very long description of a parameter.
#
# Returns:
# Player: Whoever was victorious.
#
# State Changes:
# Sets @winning_player and @losing_player.
```

Without looking at the method itself, we can tell that the above method plays our game, requires two parameters, and returns the victorious player. We also know which attributes of the `Game` class will be modified. We don't need to worry about which `Player` object gets returned... we just have to know that a `Player` object will be returned.

Here's another example with parameters and some different return values:

```ruby
# Private: #compare_moves
# Compares two moves to see which is victorious.
#
# Params:
# move1 - String: The first move.
# move2 - String: The second move.
#
# Returns:
# Integer: 0 if the moves tie or if there is an error.
#   1 if the first move wins.
#   -1 if the second move wins.
#
# State Changes:
# None.
```

This one takes two parameters (`move1` and `move2`, both Strings), and has some special return values, in that it will only ever return -1, 0, or 1 (Integer values). We don't have any idea how this method actually turns two moves into a -1, 0, or 1, but that's the whole point of methods -- the less we have to know about *how* each part of our program does its job, the more thought-space we have for other things.
