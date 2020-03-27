import pygame # chama biblioteca pygame
from pygame.locals import *
from random import randint
import time

pygame.init() # inicia o pygame
screen = pygame.display.set_mode((900, 500), 0, 32) # define tamanho da tela
pygame.display.set_caption('Ping-Pong')

color = (255, 255, 255)
left_pos = 200; right_pos = left_pos
x_bowl = 450; y_bowl = 250
var_bowl = 20
rand_bowl = 0

var_font = pygame.font.get_default_font() # configura a fonte
font_sys = pygame.font.SysFont(var_font, 30)
left_goal = 0; right_goal = 0

clock = pygame.time.Clock()

def goal_sound():
    pygame.mixer.music.load('gol_mismarcadores.mp3') # som do gol
    pygame.mixer.music.play()
    time.sleep(3)

while True:
    clock.tick(40)
    x_bowl += var_bowl

    screen.fill((0, 0, 0))

    pos_text = 350
    text_list = ['P1', left_goal, 'Vs', right_goal, 'P2']

    for text in text_list:
        screen.blit(font_sys.render(str(text), True, color), (pos_text, 30))
        pos_text += 50

    left_pad = (30, left_pos, 5, 100); right_pad = (870, right_pos, 5, 100)
    pads_list = [left_pad, right_pad]

    for pad in pads_list:
        pygame.draw.rect(screen, color, pad)

    y_bowl = y_bowl + rand_bowl
    if y_bowl > 480:
        rand_bowl = randint(-4, -2)
    if y_bowl < 80:
        rand_bowl = randint(2, 4)

    bowl = pygame.Rect(x_bowl, y_bowl, 15, 15)
    pygame.draw.rect(screen, color, bowl)

    if bowl.collidelist(pads_list) >= 0:
        rand_bowl = randint(-5, 5)
        var_bowl = -1 * var_bowl
        pygame.mixer.music.load('ping_pong_huawei.mp3')
        pygame.mixer.music.play()

    if x_bowl < -10:
        right_goal += 1
        y_bowl = 250; x_bowl = 450
        left_pos = 200; right_pos = left_pos
        goal_sound()
    if x_bowl > 900:
        left_goal += 1
        y_bowl = 250; x_bowl = 450
        left_pos = 200; right_pos = left_pos
        goal_sound()

    for event in pygame.event.get():
        if event.type == QUIT:
            pygame.quit()

        if event.type == KEYDOWN:
            if event.key == K_w and left_pos != 80:
                left_pos -= 40
            if event.key == K_s and left_pos < 400:
                left_pos += 40
            if event.key == K_UP and right_pos != 80:
                right_pos -= 40
            if event.key == K_DOWN and right_pos < 400:
                right_pos += 40

    pygame.display.update()
