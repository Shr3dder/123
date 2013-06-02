123
===

#include <windows.h>
#include <math.h>
#include <string>
#include <time.h>
using namespace std;

#include "functions.h"
#include "opengl.h"
#include "window.h"

int WINAPI WinMain( HINSTANCE hInstance, HINSTANCE hPrevInstance, LPSTR lpCmdLine, int nCmdShow )
{
  // Создаем окно
	if ( !createWindow( "OpenGL", 0, 0, 640, 480 ) )
		return 0;
	else
	{
		initEngine();
		if ( !initGame() ) return 0;
	}

	// Переменные цикла
	unsigned char currentStep = 0, gameSpeed = 60;
	float timePerStep = 1000.0 / gameSpeed;
	unsigned int timeStart = clock();
	MSG msg;

	/* Основной цикл */
	while(game)
	{
		if (PeekMessage( &msg, NULL, 0, 0, PM_REMOVE ))
		{
			TranslateMessage(&msg);
			DispatchMessage(&msg);
		}
		else if (windowActive)
		{
			//Step();
			//Render();

			currentStep++;
			while(timeStart + currentStep*timePerStep > clock());

			if (timeStart + 1000 <= clock())
			{
				fps = currentStep;
				currentStep = 0;
				timeStart = clock();
			}
		}
	}
	/* Основной цикл */

	// Выключение
	destroyWindow();
	return ( msg.wParam );
}
