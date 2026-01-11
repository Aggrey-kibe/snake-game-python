# Snake Game — Python (Pygame)

## Overview
This project is a fully functional Snake Game implemented in Python using the Pygame framework.  
It demonstrates core programming concepts such as real-time game loops, event handling, collision detection, and state management.

The project was developed as a foundational software engineering exercise with emphasis on clean structure, readability, and correct game logic, making it suitable for portfolio and technical review.

---

## Features
- Real-time keyboard input handling  
- Dynamic snake movement and growth logic  
- Collision detection (walls and self)  
- Score tracking system  
- Game-over state handling  
- Structured game loop with frame rate control  

---

## Technical Stack
- **Language:** Python 3  
- **Framework:** Pygame  
- **Paradigm:** Event-driven programming  

---

## Project Structure

```python
import pygame
import random

# Initialize pygame
pygame.init()

# Screen size
SCREEN_WIDTH = 800
SCREEN_HEIGHT = 600
screen = pygame.display.set_mode((SCREEN_WIDTH, SCREEN_HEIGHT))
pygame.display.set_caption("Snake Game")

# Colors
COLOR_WHITE = (255, 255, 255)
COLOR_BLACK = (0, 0, 0)
COLOR_RED = (200, 0, 0)
COLOR_GREEN = (0, 200, 0)
COLOR_BLUE = (50, 153, 213)

# Clock
clock = pygame.time.Clock()

# Snake settings
BLOCK_SIZE = 10
START_SPEED = 10

# Fonts
score_font = pygame.font.SysFont("arial", 30)
message_font = pygame.font.SysFont("arial", 40)


