# Snake Game

**What will be made in the end (Click the picture to watch the video):**
[![](https://github.com/ShiyuFan0820/SnakeGame/assets/149340606/36d17043-307d-41e7-839b-94a2e7630d0b")(https://youtu.be/H59KHb27HPg)

**Follow the instructions below:**
1. Import the `Turtle` and `Screen` class from `turtle`.
2. Create a `Snake` class to generate a snake
    - Define 3 turtles and change the shape into square, change the x cordination to make the square in a line, in this way the three square will look like a simple snake.
    - Use methods built in the `Turtle` to make the snake move forward, downward, left and right.
    - Use the keys to control the movement when press the certain arrow.
    - Notice that the snake can't turn around, meaning it can't suddenly turn down when it is facing up, or to the left when it is facing right, and vice versa.
3. Create a `Bean` class to generate the bean randomly.
    - Inherite the `Tuetle` class, to generate a turtle in circle shape.
    - Set the boundaries within which beans can appear.
    - Define a method to refresh the bean's location everytime the snake get the bean.
4. Create a `Score` class to calculate the score.
    - Inherite the `Tuetle` class, to generate a scoreboard to show the score.
    - Define a method to add score if the snake get the bean.
5. Detect the collision with the walls and snake tail.

_**Note:**_  
_There are two methods to set the screen size, one is the method `turtle.screensize(canvwidth=None, canvheight=None, bg=None)`, another is the method `turtle.setup(width=_CFG["width"], height=_CFG["height"], startx=_CFG["leftright"], starty=_CFG["topbottom"])`, the difference between these two is that the `screensize()` method will not alter the drawing window, you have to use the scrollbars observe hidden parts of the canvas._

**Try to write the code in your pycharm and play the game! The completed code of this game is in the [main.py](https://github.com/ShiyuFan0820/SnakeGame/blob/main/main.py) file. (The turtle function seems to be only available on pycharm)**

