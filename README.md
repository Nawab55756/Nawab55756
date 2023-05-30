import pygame

# Initialize pygame
pygame.init()

# Create the screen
screen = pygame.display.set_mode((640, 480))

# Load the background image
background = pygame.image.load("background.png")

# Create the car
car = pygame.image.load("car.png")
car_x = 200
car_y = 200

# Create the enemies
enemy1 = pygame.image.load("enemy1.png")
enemy1_x = 400
enemy1_y = 200

enemy2 = pygame.image.load("enemy2.png")
enemy2_x = 600
enemy2_y = 200

# Create the score
score = 0

# Create the clock
clock = pygame.time.Clock()

# Game loop
while True:

    # Event handling
    for event in pygame.event.get():
        if event.type == pygame.QUIT:
            pygame.quit()
            sys.exit()

        if event.type == pygame.KEYDOWN:
            if event.key == pygame.K_LEFT:
                car_x -= 5
            elif event.key == pygame.K_RIGHT:
                car_x += 5

    # Update the car position
    car_x = min(max(car_x, 0), 640 - car.get_width())

    # Update the enemies position
    enemy1_x -= 5
    enemy2_x -= 5

    # Check for collision with enemies
    if car_x < enemy1_x + enemy1.get_width() and car_x > enemy1_x and car_y < enemy1_y + enemy1.get_height() and car_y > enemy1_y:
        print("You lost!")
        break

    if car_x < enemy2_x + enemy2.get_width() and car_x > enemy2_x and car_y < enemy2_y + enemy2.get_height() and car_y > enemy2_y:
        print("You lost!")
        break

    # Draw the background
    screen.blit(background, (0, 0))

    # Draw the car
    screen.blit(car, (car_x, car_y))

    # Draw the enemies
    screen.blit(enemy1, (enemy1_x, enemy1_y))
    screen.blit(enemy2, (enemy2_x, enemy2_y))

    # Draw the score
    text = "Score: " + str(score)
    pygame.draw.rect(screen, (0, 0, 0), (500, 10, 100, 20))
    pygame.draw.rect(screen, (255, 255, 255), (500, 10, 100, 20), 2)
    pygame.draw.text(screen, text, (520, 20), (255, 255, 255))

    # Update the display
    pygame.display.update()

    # Slow down the game
    clock.tick(30)

# Quit pygame
pygame.quit()
