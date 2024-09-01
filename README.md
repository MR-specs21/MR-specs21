import pygame
import sys

# Initialize Pygame
pygame.init()

# Set up some constants
WIDTH, HEIGHT = 800, 600
WHITE = (255, 255, 255)
RED = (255, 0, 0)
GREEN = (0, 255, 0)

# Set up the display
screen = pygame.display.set_mode((WIDTH, HEIGHT))

# Set up the font
font = pygame.font.Font(None, 36)

# Set up the classes
class Hero:
    def __init__(self, x, y):
        self.x = x
        self.y = y
        self.width = 50
        self.height = 50
        self.speed = 5
        self.health = 100
        self.weapon = "سيف"

    def draw(self):
        pygame.draw.rect(screen, GREEN, (self.x, self.y, self.width, self.height))

    def move(self, dx, dy):
        self.x += dx
        self.y += dy

class Enemy:
    def __init__(self, x, y):
        self.x = x
        self.y = y
        self.width = 50
        self.height = 50
        self.speed = 5
        self.health = 100
        self.weapon = "مسدس"

    def draw(self):
        pygame.draw.rect(screen, RED, (self.x, self.y, self.width, self.height))

    def move(self, dx, dy):
        self.x += dx
        self.y += dy

# Set up the heroes and enemies
hero = Hero(100, 100)
enemies = [Enemy(300, 300), Enemy(500, 500)]

# Set up the game loop
while True:
    for event in pygame.event.get():
        if event.type == pygame.QUIT:
            pygame.quit()
            sys.exit()

    # Move the hero
    keys = pygame.key.get_pressed()
    if keys[pygame.K_UP]:
        hero.move(0, -hero.speed)
    if keys[pygame.K_DOWN]:
        hero.move(0, hero.speed)
    if keys[pygame.K_LEFT]:
        hero.move(-hero.speed, 0)
    if keys[pygame.K_RIGHT]:
        hero.move(hero.speed, 0)

    # Move the enemies
    for enemy in enemies:
        enemy.move(1, 1)

    # Draw everything
    screen.fill(WHITE)
    hero.draw()
    for enemy in enemies:
        enemy.draw()

   
