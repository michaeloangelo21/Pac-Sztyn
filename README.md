import pygame
pygame.init()
#wielkość ekranu gry

win = pygame.display.set_mode((768,768))
width=768
height= 768

#nazwa gry

pygame.display.set_caption("Pac Man")


#tło/plansza gry

picture = pygame.image.load('walls_pacman.png')
picture = pygame.transform.scale(picture, (768, 768))
class Background(pygame.sprite.Sprite):
    def __init__(self, image_file, location):
        pygame.sprite.Sprite.__init__(self)
        self.image = pygame.image.load(image_file)
        self.image = pygame.transform.scale(self.image,(768, 768))
        self.rect = self.image.get_rect()
        self.rect.left, self.rect.top = location
BackGround = Background('walls_pacman.png', [0,0])


#tworzymy klase bohatera

class bohater(object):
    def __init__(self, x, y, promien, predkosc):
        self.x = x
        self.y = y
        self.predkosc = predkosc
        self.promien = promien
        self.wcisniecie = True
        self.kierunek = ""

    def RysujBohatera(self,win):
        pygame.draw.circle(win, (255, 255, 0), (self.x,self.y),self.promien)

    def ruchBohatera(self):
        if self.kierunek == 0:
            self.x -= self.predkosc
        if self.kierunek == 1:
            self.y -= self.predkosc
        if self.kierunek == 2:
            self.x += self.predkosc
        if self.kierunek ==3:
            self.y += self.predkosc

#tworzymy funkcje budującą od nowa klatkę obrazu

def OdswiezenieEkranu():
    #to jest tu po to żeby tło działało
    win.fill([255, 255, 255])
    win.blit(BackGround.image, BackGround.rect)
    #
    pacman.ruchBohatera()
    pacman.RysujBohatera(win)
    pygame.display.update()
#ustalamy parametry gry i obiektów

pacman = bohater(384,384,18,3)
TrwanieGry = True
zegar = pygame.time.Clock()


#Główny loop

while TrwanieGry == True:

    #ustalamy ilość klatek

    zegar.tick(60)

    #pętla sprawdzająca czy wyłączyliśmy grę

    for wydarzenie in pygame.event.get():
        if wydarzenie.type == pygame.QUIT:
            TrwanieGry = False

    #ustalamy sterowanie bohaterem

        if wydarzenie.type == pygame.KEYDOWN:

            if wydarzenie.key == pygame.K_LEFT and pacman.kierunek != 0 and pacman.kierunek != 2 and wcisniecie:
                pacman.kierunek = 0
                wcisniecie = False
            if wydarzenie.key == pygame.K_RIGHT and pacman.kierunek != 2 and pacman.kierunek != 0 and wcisniecie:
                pacman.kierunek = 2
                wcisniecie = False
            if wydarzenie.key == pygame.K_UP and pacman.kierunek != 1 and pacman.kierunek != 3 and wcisniecie:
                pacman.kierunek = 1
                wcisniecie = False
            if wydarzenie.key == pygame.K_DOWN and pacman.kierunek != 3 and pacman.kierunek != 1 and wcisniecie:
                pacman.kierunek = 3
                wcisniecie = False



    OdswiezenieEkranu()
    wcisniecie = True
