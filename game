#include <graphics.h>		// 引用图形库头文件
#include <stdio.h>
#include <conio.h>//该文件包含主要由MS-DOS编译器使用的控制台输入/输出函数。
#include <stdlib.h>//随机
#include<math.h>
#define SNAKE_NUM 500

enum DIR//枚举
{
	UP,
DOWN,
LEFT,
RIGHT,
};

struct Snake//蛇属性
{
	int size, dir, speed;
	POINT coor[SNAKE_NUM];//坐标
}snake;

struct Food//食物属性
{
	int x, y,r;
	bool flag;
	DWORD color;
	  
 }food;

void GameInit()//游戏初始化
{
	initgraph(640, 480/*,SHOWCONSOLE*/);//设置窗口
	srand(GetTickCount());//？？？//srand() 用来设置 rand() 产生随机数时的随机数种子。GetTickCount返回（retrieve ）从操作系统启动到现在所经过（elapsed ）的毫秒数
	snake.size = 3;
	snake.speed = 10;
	snake.dir=RIGHT; 
	for (int i = 0; i < snake.size; i++) 
	{
		snake.coor[i].x = 40-10*i;
		snake.coor[i].y = 10;
	}
	 
	food.x = rand() % 640;
	food.y = rand() % 480;
	food.color = RGB(rand() % 256, rand() % 256, rand () % 256);
	food.r = rand() % 10+ 20;
	food.flag = true;
}

void GameDraw()
{
	BeginBatchDraw();//双缓冲绘图，防止闪屏
	setbkcolor(RGB(28, 115, 119));
	cleardevice();

	setfillcolor(RED);
	for (int i = 0; i < snake.size; i++) 
	{
		solidcircle(snake.coor[i].x, snake.coor[i].y, 5);//画⚪
	}
	if (food.flag)
		solidcircle(food.x, food.y, food.r);
	EndBatchDraw();//双缓冲绘图，防止闪屏
}

void snakemove()
{
	for (int i = snake.size-1; i > 0; i--)
	{
		snake.coor[i] = snake.coor[i - 1];
	}
		switch (snake.dir)
		{
		case UP:
			snake.coor[0].y-= snake.speed ;
			if (snake.coor[0].y <= 0)
				snake.coor[0].y = 480;
			break;
		case DOWN:
			snake.coor[0].y+= snake.speed;
			if (snake.coor[0].y >= 480)
				snake.coor[0].y =0;
			break;
		case LEFT:
			snake.coor[0].x-= snake.speed;
			if (snake.coor[0].x <= 0)
				snake.coor[0].x= 640;
			break;
		case RIGHT:
			snake.coor[0].x+= snake.speed;
			if (snake.coor[0].x>=640)
				snake.coor[0].x=0;
			break;
		}
}


void keyControl()
{
	if (_kbhit())//检查控制台窗口的按键是否被按下。
	{
		switch (_getch())//从控制台中获取输入的字符，在获取输入的字符之后，并不会在控制台中显示该字符
		{
		case 'w':
		case 'W':
			if(snake.dir!=DOWN)
			snake.dir = UP;
			break;
		case 's':
		case 'S':
			if (snake.dir != UP)
			snake.dir = DOWN;
			break;
		case 'a':
		case 'A':
			if (snake.dir != RIGHT)
			snake.dir = LEFT;
			break;
		case 'd':
		case 'D':
			if (snake.dir != LEFT)
			snake.dir = RIGHT;
			break;
		case ' ':
			system("pause");
		}
	}
}

void EatFood()
{
	if (food.flag && sqrt(pow(snake.coor[0].x - food.x, 2) + pow(snake.coor[0].y - food.y, 2)) <=10+ food.r)
	{
		food.flag = false;
		snake.size++;
	}

	if (!food.flag)
	{
		food.x = rand() % 640;
		food.y = rand() % 480;
		food.color = RGB(rand() % 256, rand() % 256, rand() % 256);
		food.r = rand() % 10 + 5;
		food.flag = true;
	}
}


int main()
{
	GameInit();
	GameDraw();
	while (1)
	{
		GameDraw();
		snakemove();
		keyControl();
		EatFood();
		Sleep(20);
	}
	return 0;
}
