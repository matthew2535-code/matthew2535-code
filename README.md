- 👋 Hi, I’m @matthew2535-code
- 👀 I’m interested in ...
- 🌱 I’m currently learning ...
- 💞️ I’m looking to collaborate on ...
- 📫 How to reach me ...
- 😄 Pronouns: ...
- ⚡ Fun fact: ...

<!---
matthew2535-code/matthew2535-code is a ✨ special ✨ repository because its `README.md` (this file) appears on your GitHub profile.
You can click the Preview link to take a look at your changes.
--->
import pygame
import random

# Initialize Pygame
pygame.init()

# Screen dimensions
WIDTH, HEIGHT = 800, 600
screen = pygame.display.set_mode((WIDTH, HEIGHT))
pygame.display.set_caption("Haunted City")

# Colors
BLACK = (0, 0, 0)
WHITE = (255, 255, 255)
RED = (255, 0, 0)
BLUE = (0, 0, 255)

# Clock
clock = pygame.time.Clock()
FPS = 60

# Player settings
player_size = 40
player_x = WIDTH // 2
player_y = HEIGHT // 2
player_speed = 5

# Ghost settings
ghost_size = 40
ghost_speed = 2
ghosts = [{"x": random.randint(0, WIDTH - ghost_size), "y": random.randint(0, HEIGHT - ghost_size)} for _ in range(5)]

# Item settings
item_size = 20
items = [{"x": random.randint(0, WIDTH - item_size), "y": random.randint(0, HEIGHT - item_size)} for _ in range(3)]

# Fonts
font = pygame.font.Font(None, 36)

# Game variables
score = 0
game_over = False

def draw_player(x, y):
    pygame.draw.rect(screen, BLUE, (x, y, player_size, player_size))

def draw_ghost(ghost):
    pygame.draw.rect(screen, RED, (ghost["x"], ghost["y"], ghost_size, ghost_size))

def draw_item(item):
    pygame.draw.rect(screen, WHITE, (item["x"], item["y"], item_size, item_size))

def display_message(text):
    msg = font.render(text, True, WHITE)
    screen.blit(msg, (WIDTH // 2 - msg.get_width() // 2, HEIGHT // 2 - msg.get_height() // 2))

# Game loop
running = True
while running:
    screen.fill(BLACK)
    
    for event in pygame.event.get():
        if event.type == pygame.QUIT:
            running = False
    
    keys = pygame.key.get_pressed()
    if not game_over:
        if keys[pygame.K_LEFT] and player_x > 0:
            player_x -= player_speed
        if keys[pygame.K_RIGHT] and player_x < WIDTH - player_size:
            player_x += player_speed
        if keys[pygame.K_UP] and player_y > 0:
            player_y -= player_speed
        if keys[pygame.K_DOWN] and player_y < HEIGHT - player_size:
            player_y += player_speed

    # Move ghosts
    for ghost in ghosts:
        ghost["x"] += random.choice([-ghost_speed, ghost_speed])
        ghost["y"] += random.choice([-ghost_speed, ghost_speed])
        
        # Keep ghosts within bounds
        ghost["x"] = max(0, min(WIDTH - ghost_size, ghost["x"]))
        ghost["y"] = max(0, min(HEIGHT - ghost_size, ghost["y"]))

        # Check collision with player
        if (player_x < ghost["x"] + ghost_size and player_x + player_size > ghost["x"] and
            player
