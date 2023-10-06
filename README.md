import pygame
import sys

# Initialize Pygame
pygame.init()

# Constants
WIDTH, HEIGHT = 800, 600
CELL_SIZE = 40
WHITE = (255, 255, 255)
BLACK = (0, 0, 0)

# Define the maze
maze = [
    "#########",
    "#S      #",
    "#   #   #",
    "#   #   #",
    "#   #   #",
    "#     E #",
    "#########"
]

# Player position
player_x, player_y = 1, 1

# Game loop
def game_loop():
    screen = pygame.display.set_mode((WIDTH, HEIGHT))
    pygame.display.set_caption("WASD Maze Game")

    while True:
        for event in pygame.event.get():
            if event.type == pygame.QUIT:
                pygame.quit()
                sys.exit()

        # Handle user input
        keys = pygame.key.get_pressed()
        if keys[pygame.K_w] and maze[player_y - 1][player_x] != "#":
            player_y -= 1
        if keys[pygame.K_s] and maze[player_y + 1][player_x] != "#":
            player_y += 1
        if keys[pygame.K_a] and maze[player_y][player_x - 1] != "#":
            player_x -= 1
        if keys[pygame.K_d] and maze[player_y][player_x + 1] != "#":
            player_x += 1

        # Check if the player has reached the exit
        if maze[player_y][player_x] == "E":
            print("Congratulations! You won!")
            pygame.quit()
            sys.exit()

        # Clear the screen
        screen.fill(BLACK)

        # Draw the maze
        for y, row in enumerate(maze):
            for x, cell in enumerate(row):
                if cell == "#":
                    pygame.draw.rect(screen, WHITE, (x * CELL_SIZE, y * CELL_SIZE, CELL_SIZE, CELL_SIZE))

        # Draw the player
        pygame.draw.circle(screen, (255, 0, 0), (player_x * CELL_SIZE + CELL_SIZE // 2, player_y * CELL_SIZE + CELL_SIZE // 2), CELL_SIZE // 2)

        pygame.display.flip()

# Run the game loop
if __name__ == "__main__":
    game_loop()
