# have-fun-don-t-jubge-my-code-
import pygame

pygame.init()
screen = pygame.display.set_mode((800, 600,))
pygame.display.set_caption('Side-Scrolling game')
clock = pygame.time.Clock()

player = [100, 450, 0, 0] #xpos,ypos,xvel,yvel
isOnGround = False
offset = 0
def move_player():
    global isOnGround
    global offset
    if keys[pygame.K_LEFT]:
      #player[2] =- 5 #update velocticy
       offset += 5
    elif keys[pygame.K_RIGHT]:
        #player[2] = 5 #update velocity
        offset -= 5 
    else:
        player[2] = 0 
        
 
    
    if keys[pygame.K_LEFT]:
        player [2] =- 5#updates the velocity
    elif keys[pygame.K_RIGHT]:
        player[2] =+ 5#updates the velocity
    else:
        player[2] = 0
    
    if isOnGround == True and keys[pygame.K_UP]:
      player[3] = -15 #player jumps
      isOnGround = False
    
    
    
    if isOnGround == False:
        player [3] += 1 #gravity 
    if isOnGround == True:
        player [3] =0
        
        
    if player[1] >= 500-50:
        player[1] = 500-50
        isOnGround=True
    
    player[0]+=player[2] #add x velocity to x positions 
    player[1]+=player[3] #add y velocity to y positions 

   
    #print(player[0],player[1])
running = True
def draw_clouds ():
    for x in range(100, 800, 300):
        pygame.draw.circle(screen, (255,255,255), (x + offset, 100),40)
        pygame.draw.circle(screen, (255,255,255), (x- 50 + offset, 125),40)
        pygame.draw.circle(screen, (255,255,255), (x+ 50 + offset, 125),40)
        pygame.draw.rect(screen, (255,255,255), (x- 50 + offset, 100, 100,65))


def draw_trees ():
    for x in range(100, 800, 300):
        pygame.draw.rect(screen,(100,100,0),(x- 20 + offset,300,30,300))
        pygame.draw.circle(screen, (0,255,0), (x + offset, 300),40)
        pygame.draw.circle(screen, (0,255,0), (x- 50 + offset, 325),40)
        pygame.draw.circle(screen, (0,255,0), (x+ 50 + offset, 325),40)
        
while running: # main game loop+++++++++++++++++++++
    clock.tick(60)
    #input section---------------------
    for event in pygame.event.get():
        if event.type == pygame.QUIT:
            running = false
            
    keys = pygame.key.get_pressed()
    #phyics section+++++++++++++++++++++++++++++++++++++++
    move_player()
    #Reder sectio+++++++++++++++++++++++++++++++++++++++++
    screen.fill((135,206,235)) # sky blue background
    draw_clouds() #function
    draw_trees()
    pygame.draw.rect(screen,(0,150,0), (0,500,800,100))
    pygame.draw.rect(screen, (0,0,0), (player[0],player[1],-20000,20000)) #player 
    pygame.display.flip()
    
pygame.quit()
