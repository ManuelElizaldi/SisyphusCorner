2025-5-6
Tags: [[Programming]] [[Game Development]] [[Gaming]] [[Python]]

Using pygame to start with
## Basic Game components
### Window
This is the screen where the game takes place. We declare our width, height and use the code:

```python
screen_width = 800
screen_height = 600

screen = pygame.display.set_mode((screen_width, screen_height))
```

### Game Loop
This is a simple while loop to determine when the game is running. 

```python
run = True
while run:
	# game code here:

	pygame.display.update()
```

At the end of the while loop you must include pygame.display.update() to capture all changes within the game loop.

Here I learned that you can do "while run:" and this will run until run = False. 

### Event Handler
This piece of code looks at all the events. Here I learned about frame rate, meaning, the rate at which the screen updates. FPS -> How many times per second. 

This is related to the game loop, every iteration of the Game Loop is one frame. 
	_Note, this piece of knowledge made me ask myself, how to best use the ram of a computer/console to optimize the framerate_

Inside the event handler, we look at all the events (clicks, movement, etc.) happening inside the window/screen:

```python
for event in pygame.event.get():
	if event.type == pygame.QUIT():
		run = False
```

But, all the drawing, movement, etc code is written on top of this event handler


## Movement
You can capture input movement by using the command:

```python
key = pygame.key.get_pressed()
```

- key.get_pressed(): get the state of all keyboard buttons


What is init()?


---
### Reference

[Tutorial](https://www.youtube.com/watch?v=y9VG3Pztok8)

[Great Stackover flow article](https://stackoverflow.com/questions/62998806/how-to-make-a-bouncy-ball-in-pygame-python) on basics of movement
