2025-5-6
Tags: [[Programming]] [[Game Development]] [[Gaming]] [[Python]]

Using pygame to start with
# Week 1
In this week we covered the basics of any game developed in pygame. Screen/window, game loop and event handler. We also created a "player" object represented by a square that had basic movement: up, down, left and right. In addition to this I added a strafing mechaisim which was not covered in the tutorial I was following but created from my own imagination. Good job Manuel! 

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
	_Note, this piece of knowledge made me ask myself, how to best use the ram of a computer/console to optimize the framerate. Started to think about the future knowledge I could acquire_

Inside the event handler, we look at all the events (clicks, movement, etc.) happening inside the window/screen:

```python
for event in pygame.event.get():
	if event.type == pygame.QUIT():
		run = False
```

But, all the drawing, movement, etc code is written on top of this event handler to be captured. 

In this if statement, we are looking for the event.type QUIT(), meaning if the player presses the X. If he does, the program stops running. This stops the game loop/while loop
- we pair the run = False with pygame.quit() at the end of the script to stop the python program 

### Movement & Coordinates
You can capture input movement by using the command:

```python
key = pygame.key.get_pressed()
```

- key.get_pressed(): get the state of all keyboard buttons. I did a print key, and it shows all the keyboard buttons as False, but if you click one, that key == True. So we can do the following:

```python
if key[pygame.K_a] == True:

        player.move_ip(-1, 0)

    elif key[pygame.K_d] == True:

        player.move_ip(1, 0)

    elif key[pygame.K_w] == True:

        player.move_ip(0, -1)

    elif key[pygame.K_s] == True:

        player.move_ip(0, 1)

    elif key[pygame.K_q] == True:

        player.move_ip(-1, -1)

    elif key[pygame.K_e] == True:

        player.move_ip(1, -1)
```

This is an if elif statement to determine which key is being pressed: key[pygame.K_a] -> a, etc. if this is true, then you set the movement coordinates in: player.move_ip(-1, 0).
- move_ip -> stands for move in place

This is how coordinates work in 2D games:
![[Pasted image 20250514163525.png]]
- Moving left is (-1, 0)
- Moving right is (1, 0)
- Moving up is (0, -1)
- Moving down is (0, 1)

Here I am proud of myself because I figured out strafing for myself. Might seem like nothing but it's important to celebrate the small wins:

- Strafing left is (-1, -1)
- Strafing right is (-1, 1)
	- I tried doing float values but it didn't let me. I could research this in the future

## Stopping the python program
At the end of any script you need to place this code:
```python
pygame.quit()
```

# Week 2

In this week I worked on creating a bouncing ball. The ball starts in the center and then hits a wall and bounces to the other side. This could be improved to mimic a more realistic bounce but I will leave it like that for now. 

## Bouncing





what is init()

---
### Reference

[Tutorial](https://www.youtube.com/watch?v=y9VG3Pztok8)

[Great Stackover flow article](https://stackoverflow.com/questions/62998806/how-to-make-a-bouncy-ball-in-pygame-python) on basics of movement
