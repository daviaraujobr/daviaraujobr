<img width=100% src="https://capsule-render.vercel.app/api?type=waving&color=808080&height=120&section=header&text=&fontSize=30&fontColor=&animation=twinkling&fontAlignY=35"/>

## Olá eu sou o Davi de Araujo, estudante de engenharia, programação e tecnologia!
<div align="center">
  <a href="https://github.com/daviaraujobr">
  <img height="165em" src="https://github-readme-stats.vercel.app/api?username=daviaraujobr&show_icons=true&theme=dark&include_all_commits=true&count_private=true"/>     <img height="159em" src="https://github-readme-stats.vercel.app/api/top-langs/?username=daviaraujobr&layout=compact&langs_count=7&theme=dark"/>
</div>

<div style="display: inline_block"><br>
  <img align="center" alt="Davi-Js" height="30" width="40" src="https://raw.githubusercontent.com/devicons/devicon/master/icons/javascript/javascript-plain.svg">
  <img align="center" alt="Davi-HTML" height="30" width="40" src="https://raw.githubusercontent.com/devicons/devicon/master/icons/html5/html5-original.svg">
  <img align="center" alt="Davi-CSS" height="30" width="40" src="https://raw.githubusercontent.com/devicons/devicon/master/icons/css3/css3-original.svg">
  <img align="center" alt="Davi-C" height="30" width="40" src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/c/c-original.svg" />
  <img align="center" alt="Davi-Vscode" height="30" width="40" src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/vscode/vscode-original.svg" />
  <img align="right" alt="Davi-Imagem" height="150" style="border-radius:70px;" src="https://avatars.githubusercontent.com/u/84422077?s=400&u=6535ccc0d8b6bd81e0b8732d48cc62829352a828&v=4"><br>
</div>
  
  ##
 
<div>
  
  <a href="https://www.instagram.com/daviaraujo_zs/" target="_blank"><img src="https://img.shields.io/badge/-Instagram-%23E4405F?style=for-the-badge&logo=instagram&logoColor=white" target="_blank"></a>  
 <a href="https://discord.gg/J E A N M#2227" target="_blank"><img src="https://img.shields.io/badge/Discord-7289DA?style=for-the-badge&logo=discord&logoColor=white" target="_blank"></a> 
  <a href = "mailto:daviaraujobr@gmail.com"><img src="https://img.shields.io/badge/-Gmail-%23333?style=for-the-badge&logo=gmail&logoColor=white" target="_blank"></a>
  <a href="https://www.linkedin.com/in/davi-de-araujo-5b3942212/" target="_blank"><img src="https://img.shields.io/badge/-LinkedIn-%230077B5?style=for-the-badge&logo=linkedin&logoColor=white" target="_blank"></a>
 
  
 ## Sistemas operacionais que uso.
  <div>
  <a href="" target="_blank"><img src="https://img.shields.io/badge/Windows-0078D6?style=for-the-badge&logo=windows&logoColor=white"></a>
    <a href="" target="_blank"><img src="https://img.shields.io/badge/mac%20os-000000?style=for-the-badge&logo=apple&logoColor=white"></a>
    <a href="" target="_blank"><img src="https://img.shields.io/badge/iOS-000000?style=for-the-badge&logo=ios&logoColor=white"></a>
    <a href="" target="_blank"><img src="https://img.shields.io/badge/Linux-FCC624?style=for-the-badge&logo=linux&logoColor=black"></a>
  </div>
  
  
 ![Snake animation](https://github.com/daviaraujobr/daviaraujobr/blob/output/github-contribution-grid-snake.svg)
  
</div>
  
  <img width=100% src="https://capsule-render.vercel.app/api?type=waving&color=808080&height=120&section=footer"/>
  
  #include <math.h>
#include <stdio.h>
#include <string.h>
#include <unistd.h>

float A, B, C;

float cubeWidth = 20;
int width = 160, height = 44;
float zBuffer[160 * 44];
char buffer[160 * 44];
int backgroundASCIICode = '.';
int distanceFromCam = 100;
float horizontalOffset;
float K1 = 40;

float incrementSpeed = 0.6;

float x, y, z;
float ooz;
int xp, yp;
int idx;

float calculateX(int i, int j, int k) {
  return j * sin(A) * sin(B) * cos(C) - k * cos(A) * sin(B) * cos(C) + j * cos(A) * sin(C) + k * sin(A) * sin(C) + i * cos(B) * cos(C);}

float calculateY(int i, int j, int k) {
  return j * cos(A) * cos(C) + k * sin(A) * cos(C) - j * sin(A) * sin(B) * sin(C) + k * cos(A) * sin(B) * sin(C) - i * cos(B) * sin(C);}

float calculateZ(int i, int j, int k) {
  return k * cos(A) * cos(B) - j * sin(A) * cos(B) + i * sin(B);
}

void calculateForSurface(float cubeX, float cubeY, float cubeZ, int ch) {
  x = calculateX(cubeX, cubeY, cubeZ);
  y = calculateY(cubeX, cubeY, cubeZ);
  z = calculateZ(cubeX, cubeY, cubeZ) + distanceFromCam;

  ooz = 1 / z;

  xp = (int)(width / 2 + horizontalOffset + K1 * ooz * x * 2);
  yp = (int)(height / 2 + K1 * ooz * y);

  idx = xp + yp * width;
  if (idx >= 0 && idx < width * height) {
    if (ooz > zBuffer[idx]) {
      zBuffer[idx] = ooz;
      buffer[idx] = ch;
    }
  }
}

int main() {
  printf("\x1b[2J");
  while (1) {
    memset(buffer, backgroundASCIICode, width * height);
    memset(zBuffer, 0, width * height * 4);
    cubeWidth = 20;
    horizontalOffset = -2 * cubeWidth;
    // first cube
    for (float cubeX = -cubeWidth; cubeX < cubeWidth; cubeX += incrementSpeed) {
      for (float cubeY = -cubeWidth; cubeY < cubeWidth; cubeY += incrementSpeed) {
        calculateForSurface(cubeX, cubeY, -cubeWidth, '@');
        calculateForSurface(cubeWidth, cubeY, cubeX, '$');
        calculateForSurface(-cubeWidth, cubeY, -cubeX, '~');
        calculateForSurface(-cubeX, cubeY, cubeWidth, '#');
        calculateForSurface(cubeX, -cubeWidth, -cubeY, ';');
        calculateForSurface(cubeX, cubeWidth, cubeY, '+');
      }
    }
    cubeWidth = 10;
    horizontalOffset = 1 * cubeWidth;
    // second cube
    for (float cubeX = -cubeWidth; cubeX < cubeWidth; cubeX += incrementSpeed) {
      for (float cubeY = -cubeWidth; cubeY < cubeWidth;cubeY += incrementSpeed) {
        calculateForSurface(cubeX, cubeY, -cubeWidth, '@');
        calculateForSurface(cubeWidth, cubeY, cubeX, '$');
        calculateForSurface(-cubeWidth, cubeY, -cubeX, '~');
        calculateForSurface(-cubeX, cubeY, cubeWidth, '#');
        calculateForSurface(cubeX, -cubeWidth, -cubeY, ';');
        calculateForSurface(cubeX, cubeWidth, cubeY, '+');
      }
    }
    cubeWidth = 5;
    horizontalOffset = 8 * cubeWidth;
    // third cube
    for (float cubeX = -cubeWidth; cubeX < cubeWidth; cubeX += incrementSpeed) {
      for (float cubeY = -cubeWidth; cubeY < cubeWidth;cubeY += incrementSpeed) {
        calculateForSurface(cubeX, cubeY, -cubeWidth, '@');
        calculateForSurface(cubeWidth, cubeY, cubeX, '$');
        calculateForSurface(-cubeWidth, cubeY, -cubeX, '~');
        calculateForSurface(-cubeX, cubeY, cubeWidth, '#');
        calculateForSurface(cubeX, -cubeWidth, -cubeY, ';');
        calculateForSurface(cubeX, cubeWidth, cubeY, '+');
      }
    }
    printf("\x1b[H");
    for (int k = 0; k < width * height; k++) {
      putchar(k % width ? buffer[k] : 10);
    }

    A += 0.05;
    B += 0.05;
    C += 0.01;
    usleep(8000 * 2);
  }
  return 0;
}

