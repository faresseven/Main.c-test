# Main.c-test
#include <stdio.h>
#include "SDL/SDL.h"
#include <SDL/SDL_image.h>
#include <SDL/SDL_mixer.h>
#include<SDL/SDL_ttf.h>
#include "enigme.h"
/**
*@file main.c
* @brief testing
* @ author respawnables
*@ version 1 
*/
int main(void) {
int directionSDL=0;
   int collision = 0;
  int game =1;
   SDL_Event event;
   SDL_Surface *screen=NULL,*instruction=NULL,*pomme=NULL,*tanit=NULL,*rightanswer=NULL,*wronganswer=NULL,*enigme=NULL;
   SDL_Rect positionpomme,postanit,posanswer,posenigme,posinst;
SDL_Init(SDL_INIT_VIDEO);
pomme=IMG_Load("pomme.gif");
tanit=IMG_Load("tanit.png");
screen = SDL_SetVideoMode(1200, 600, 32, SDL_HWSURFACE | SDL_DOUBLEBUF);
positionpomme.x=20;
positionpomme.y=550;
positionpomme.w=pomme->w;
positionpomme.h=pomme->h;
postanit.x=400;
postanit.y=500;
postanit.w=tanit->w;
postanit.h=tanit->h;


instruction=IMG_Load("instruction.png");
posinst.x=30;
posinst.y=30;
SDL_Flip(screen);
SDL_EnableKeyRepeat(SDL_DEFAULT_REPEAT_DELAY,SDL_DEFAULT_REPEAT_INTERVAL);
while (game)
{
  //input from SDL
  while(SDL_PollEvent(&event)){
        switch (event.type)
        {
        // exit if the window is closed
        case SDL_QUIT:
            game = 0;
            break;
        case SDL_KEYDOWN:
        {

            if (event.key.keysym.sym == SDLK_RIGHT)
              directionSDL = 1;

            if (event.key.keysym.sym == SDLK_LEFT)
              directionSDL = 2;

        }
        break;
        case SDL_KEYUP:
          directionSDL=0;
        break;

        }
      }
        if(positionpomme.x+positionpomme.w<postanit.x)
            collision=0;
        else
            collision=1;




        if(collision == 1){
          printf("\n COLLISION RIGHT SENDING 1 TO SERIAL");
          //........................
          functionenigme(screen);
         game=0;
        }
          else {
        printf("\n NO COLLISION SENDING 0 TO SERIAL");
        //..........................
        }

        if((directionSDL == 1 ) && !collision){
             positionpomme.x += 1;
