import pygame
import math
import random

pygame.init()
screen = pygame.display.set_mode((800, 800))
font = pygame.font.SysFont('Arial', 30)
#Create clock
clock = pygame.time.Clock()

#Images
char_f1 = pygame.image.load('char_f1.png')
char_f2 = pygame.image.load('char_f2.png')
char_f3 = pygame.image.load('char_f3.png')
char_b1 = pygame.image.load('char_b1.png')
char_b2 = pygame.image.load('char_b2.png')
char_b3 = pygame.image.load('char_b3.png')
char_l1 = pygame.image.load('char_l1.png')
char_l2 = pygame.image.load('char_l2.png')
char_l3 = pygame.image.load('char_l3.png')
char_r1 = pygame.image.load('char_r1.png')
char_r2 = pygame.image.load('char_r2.png')
char_r3 = pygame.image.load('char_r3.png')
bg = pygame.image.load('superherobg.png')
bg = pygame.transform.scale(bg, (800, 800))

#Image lists
char_f = [char_f1, char_f2, char_f3] 
char_b = [char_b1, char_b2, char_b3]
char_l = [char_l1, char_l2, char_l3]
char_r = [char_r1, char_r2, char_r3]

#Variables for character location
charx = 100
chary = 100
bulletx = -200
bullety = -200
enemyx = 1000
enemyy = random.randint(0, 1000)
enemy2x = -100
enemy2y = random.randint(0, 1000)
bulletstate = False
direction = 'right'
life = 100
char_direction = 'right'
charIndex = 0

#Put all drawing stuff in here
def draw_screen():
  screen.fill((255,255,255))
  screen.blit(bg, (0,0))
  char_image = pygame.transform.scale(char_r[charIndex], (50,50))
  if char_direction == 'left':
    char_image = pygame.transform.scale(char_l[charIndex], (50,50))
  elif char_direction == 'up':
    char_image = pygame.transform.scale(char_b[charIndex], (50,50))
  elif char_direction == 'down':
    char_image = pygame.transform.scale(char_f[charIndex], (50,50))
  char_image.set_colorkey((0,255,0))
  screen.blit(char_image, (charx, chary))
  pygame.draw.rect(screen, (0,255,0), (bulletx, bullety, 10, 10))
  pygame.draw.rect(screen, (255,0,0), (enemyx, enemyy, 50, 50))
  pygame.draw.rect(screen, (255,0,0), (enemy2x, enemy2y, 50, 50))
  #Health draw
  pygame.draw.rect(screen, (0,255,0), (charx - 25, chary - 20, life, 10))
  
def isCollision(x1, y1, x2, y2):
  distance = math.sqrt(math.pow(x1-x2, 2)+math.pow(y1-y2,2))
  if distance < 50:
    return True
  else:
    return False
    
def animate(image_list):
  global charIndex
  
  if charIndex < len(image_list) - 1:
    charIndex += 1
  else:
    charIndex = 0

while True:
  #The clock is to prevent the character from moving really fast
  clock.tick(60)
  #events activation
  for event in pygame.event.get():
    if event.type == pygame.QUIT:
      pygame.quit()
    if event.type == pygame.KEYDOWN:
      if event.key == pygame.K_SPACE:
        if bulletstate == False:
          bulletx = charx + 20
          bullety = chary + 20
          bulletstate = True
  #Movement is a key hold rather key press so it must be done using and array
  keys = pygame.key.get_pressed()
  if keys[pygame.K_RIGHT]:
    char_direction = 'right'
    animate(char_r)
    if charx < 750:
      if bulletstate == False:
        direction = 'right'
      charx += 5
  elif keys[pygame.K_LEFT]:
    char_direction = 'left'
    animate(char_l)
    if charx > 0:
      if bulletstate == False:
        direction = 'left'
      charx -=5
  elif keys[pygame.K_UP]:
    char_direction = 'up'
    animate(char_b)
    if chary > 0:
      if bulletstate == False:
        direction = 'up'
      chary -=5
  elif keys[pygame.K_DOWN]:
    char_direction = 'down'
    animate(char_f)
    if chary < 550:
      if bulletstate == False:
        direction = 'down'
      chary +=5
      
  #Enemy Movement
  if enemyx > charx:
    enemyx -= 2
  else:
    enemyx += 2
  
  if enemyy > chary:
    enemyy -= 2
  else:
    enemyy += 2
  
  if enemy2x > charx:
    enemy2x -= 2
  else:
    enemy2x += 2
  
  if enemy2y > chary:
    enemy2y -= 2
  else:
    enemy2y += 2
    
  #Collision check with enemy and char  
  if isCollision(enemyx, enemyy, charx, chary):
    life -= 1
  if isCollision(enemy2x, enemy2y, charx, chary):
    life -= 1
  
  #Bullet movement
  if bulletstate:
    if isCollision(bulletx, bullety, enemyx, enemyy):
      enemyx = 1000
      enemyy = random.randint(0, 1000)
      bulletx = -200
      bullety = -200
      bulletstate = False
    elif isCollision(bulletx, bullety, enemy2x, enemy2y):
      enemy2x = -100
      enemy2y = random.randint(0, 1000)
      bulletx = -200
      bullety = -200
      bulletstate = False
    if direction == 'right':
      if bulletx < 800:
        bulletx += 10
      else:
        bulletx = -200
        bullety = -200
        bulletstate = False
    elif direction == 'left':
      if bulletx > 0:
        bulletx -= 10
      else:
        bulletx = -200
        bullety = -200
        bulletstate = False
    elif direction == 'up':
      if bullety > 0:
        bullety -= 10
      else:
        bulletx = -200
        bullety = -200
        bulletstate = False
    elif direction == 'down':
      if bullety < 800:
        bullety += 10
      else:
        bulletx = -200
        bullety = -200
        bulletstate = False
  
  #Health check
  if life <= 0:
    pygame.quit()
    
  draw_screen()
  pygame.display.update()
  
pygame.quit()
