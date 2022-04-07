##main pygame

import pygame
from gun import Gun
import controls
from pygame.sprite import Group


def run():
    pygame.init()
    screen = pygame.display.set_mode((1000, 600))
    pygame.display.set_caption("SnenegrBlack")
    bg_color = (0, 105, 60)
    gun = Gun(screen)
    bullets = Group()

    while True:
        controls.events(screen,gun,bullets)
        gun.update_gun()
        controls.update(bg_color,screen,gun, bullets)
        controls.delete(bullets)

run()

##gun.py
import pygame


class Gun():
    def __init__(self, screen):
        self.screen = screen
        self.image = pygame.image.load('image/1.png')
        self.rect = self.image.get_rect()
        self.screen_rect = screen.get_rect()
        self.rect.centerx = self.screen_rect.centerx
        self.rect.bottom = self.screen_rect.bottom
        self.kright = False
        self.kleft = False
        self.kup = False
        self.kdown = False


    def output(self):
        self.screen.blit(self.image, self.rect)

    def update_gun(self):
        if self.kright and self.rect.right<self.screen_rect.right:
            self.rect.centerx += 1
        if self.kleft == True and self.rect.left>0:
            self.rect.centerx -= 1
        if self.kup == True and self.rect.height<600:
            self.rect.bottom -= 1
        if self.kdown == True and self.rect.bottom<self.screen_rect.bottom:
            self.rect.bottom += 1

##cntrl.py
import sys
import pygame
from bullet import Bullet


def events(screen,gun, bullets):
    for event in pygame.event.get():
        if event.type == pygame.QUIT:
            sys.exit()
        elif event.type == pygame.KEYDOWN:
            if event.key == pygame.K_d:
                gun.kright = True
            elif event.key == pygame.K_a:
                gun.kleft = True
            elif event.key == pygame.K_w:
                gun.kup = True
            elif event.key == pygame.K_s:
                gun.kdown = True
                pygame.mixer.music.stop()
            elif event.key == pygame.K_SPACE:
                new_bullet = Bullet(screen, gun)
                bullets.add(new_bullet)
                pygame.mixer.music.load('1.mp3')
                pygame.mixer.music.play(-1)


        elif event.type == pygame.KEYUP:
            if event.key == pygame.K_d:
                gun.kright = False
            elif event.key == pygame.K_a:
                gun.kleft = False
            elif event.key == pygame.K_w:
                gun.kup = False
            elif event.key == pygame.K_s:
                gun.kdown = False

def update(bg_color, screen, gun, bullets):
    screen.fill(bg_color)
    for bullet in bullets.sprites():
        bullet.drawBullet()
    gun.output()
    pygame.display.flip()

def delete(bullets):
    bullets.update()
    for bullet in bullets.copy():
        if bullet.rect.bottom <= 0:
            bullets.remove(bullet)
    print(len(bullets))

git clone https://github.com/CMERTbIIIaexis/CMERTbIIIaexis/new/main?filename=README.md&path=%2F&value=-+%F0%9F%91%8B+Hi%2C+I%E2%80%99m+%40CMERTbIIIaexis%0A-+%F0%9F%91%80+I%E2%80%99m+interested+in+...%0A-+%F0%9F%8C%B1+I%E2%80%99m+currently+learning+...%0A-+%F0%9F%92%9E%EF%B8%8F+I%E2%80%99m+looking+to+collaborate+on+...%0A-+%F0%9F%93%AB+How+to+reach+me+...%0A%0A%3C%21---%0ACMERTbIIIaexis%2FCMERTbIIIaexis+is+a+%E2%9C%A8+special+%E2%9C%A8+repository+because+its+%60README.md%60+%28this+file%29+appears+on+your+GitHub+profile.%0AYou+can+click+the+Preview+link+to+take+a+look+at+your+changes.%0A---%3E%0A
