# Snake Game

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

**The code is:**
```py
from turtle import Turtle, Screen
from random import randint
import time


STARTING_POSITION = [(0, 0), (-20, 0), (-40, 0)]
MOVE_DISTANCE = 20
UP = 90
DOWN = 270
LEFT = 180
RIGHT = 0


class Snake:
    def __init__(self):
        self.m_snake = []
        self.add_snake()
        self.m_head = self.m_snake[0]

    def snake_body(self, position): # Create a segment of the snake.
        new_turtle = Turtle("square")
        new_turtle.penup()
        new_turtle.color("white")
        new_turtle.goto(position)
        self.m_snake.append(new_turtle)

    def add_snake(self):  # Create 3 segments in the beginning.
        for position in STARTING_POSITION:
            self.snake_body(position)

    def grow(self):  # Add a new segment to the last segment of the snake.
        self.snake_body(self.m_snake[-1].position())

    def move_forward(self):
        for turtle_num in range(len(self.m_snake) - 1, 0, -1):
            new_x = self.m_snake[turtle_num - 1].xcor()
            new_y = self.m_snake[turtle_num - 1].ycor()
            self.m_snake[turtle_num].goto(new_x, new_y)
        self.m_head.forward(MOVE_DISTANCE)

    def up(self):
        if self.m_head.heading() != DOWN:
            self.m_head.setheading(UP)

    def down(self):
        if self.m_head.heading() != UP:
            self.m_head.setheading(DOWN)

    def left(self):
        if self.m_head.heading() != RIGHT:
            self.m_head.setheading(LEFT)

    def right(self):
        if self.m_head.heading() != LEFT:
            self.m_head.setheading(RIGHT)


class Beans(Turtle):
    def __init__(self):
        super().__init__()
        self.shape("circle")
        self.penup()
        self.shapesize(stretch_wid=0.5, stretch_len=0.5)
        self.color("yellow")
        self.speed("fastest")
        x_cor = randint(-280, 280)
        y_cor= randint(-280, 280)
        self.goto(x_cor, y_cor)
        self.refresh()

    def refresh(self):
        x_cor = randint(-280, 280)
        y_cor = randint(-280, 280)
        self.goto(x_cor, y_cor)


class ScoreRecord(Turtle):
    def __init__(self):
        super().__init__()
        self.score = 0
        self.color("white")
        self.penup()
        self.goto(0, 270)
        self.write(f"Score: {self.score}", align="center", font=("Arial", 24, "normal"))
        self.hideturtle()

    def add_score(self):
        self.score += 1
        self.clear()
        self.write(f"Score: {self.score}", align="center", font=("Arial", 24, "normal"))

    def game_over(self):
        self.goto(0,0)
        self.write("GAME OVER!", align="center", font=("Arial", 24, "normal"))


# Define the game screen.
screen = Screen()
screen.setup(width=600, height=600)
screen.bgcolor("black")
screen.tracer(0)

# Define objects.
snake = Snake()
bean = Beans()
score_record = ScoreRecord()

# Control the movement of the snake by keys.
screen.listen()
screen.onkey(snake.up, "Up")
screen.onkey(snake.down, "Down")
screen.onkey(snake.left, "Left")
screen.onkey(snake.right, "Right")

is_game_on = True
while is_game_on:
    screen.update()
    time.sleep(0.1)
    snake.move_forward()

    # Check if the snake get the bean.
    if snake.m_head.distance(bean) < 15:
        bean.refresh()
        snake.grow()
        score_record.add_score()

    # Detect the collision with walls.
    if snake.m_head.xcor() > 280 or snake.m_head.xcor() < -300 or snake.m_head.ycor() > 280 or snake.m_head.ycor() < -280:
        is_game_on = False
        score_record.game_over()

    # Detect the collision with tail.
    for body in snake.m_snake[1:]:  # Loop through the item in the snake.m_snake list other than the first one.
        if snake.m_head.distance(body) < 10:
            is_game_on = False
            score_record.game_over()

screen.exitonclick()

```

_**Notifications:**_  
_1. There are two methods to set the screen size, one is the method `turtle.screensize(canvwidth=None, canvheight=None, bg=None)`, another is the method `turtle.setup(width=_CFG["width"], height=_CFG["height"], startx=_CFG["leftright"], starty=_CFG["topbottom"])`, the difference between these two is that the `screensize()` method will not alter the drawing window, you have to use the scrollbars observe hidden parts of the canvas._
