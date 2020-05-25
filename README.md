# Pac-Sztyn
import pygame
pygame.init()

#wielkość ekranu gry

win = pygame.display.set_mode((1024,1024))

#nazwa gry

pygame.display.set_caption("Pac Man")

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
        pygame.draw.circle(win,(255,255,0), (self.x,self.y), self.promien)

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
    win.fill((0,0,64))
    pacman.ruchBohatera()
    pacman.RysujBohatera(win)
    pygame.display.update()

#ustalamy parametry gry i obiektów

pacman = bohater(512,512,24,4)
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
                wciśnięcie = False
            if wydarzenie.key == pygame.K_RIGHT and pacman.kierunek != 2 and pacman.kierunek != 0 and wcisniecie:
                pacman.kierunek = 2
                wciśnięcie = False
            if wydarzenie.key == pygame.K_UP and pacman.kierunek != 1 and pacman.kierunek != 3 and wcisniecie:
                pacman.kierunek = 1
                wciśnięcie = False
            if wydarzenie.key == pygame.K_DOWN and pacman.kierunek != 3 and pacman.kierunek != 1 and wcisniecie:
                pacman.kierunek = 3
                wciśnięcie = False



    OdswiezenieEkranu()

    wcisniecie = True
