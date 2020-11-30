# html
C++ HTML
使用WinInet中的InternetOpen InternetOpenUrl InternetReadFile

#include "stdafx.h"
#include<stdio.h>
#include<Windows.h>
#include<wininet.h>
#include <iostream>
#include <iomanip>
#include <fstream>

using namespace std;

#define MAXSIZE 1024
#pragma comment(lib, "Wininet.lib")

int main()
{
	int i = 1;
	SetConsoleOutputCP(65001);
	TCHAR* url = (TCHAR*)_T("https://baike.baidu.com/item/wininet.dll/10959530?fr=aladdin");
	ofstream os("Tu.html");
	HINTERNET Open = InternetOpen(_T("test"), INTERNET_OPEN_TYPE_PRECONFIG, NULL, NULL, 0);//使用默认代理
	if (Open != NULL)
	{
		HINTERNET URL = InternetOpenUrl(Open, url, NULL, 0, INTERNET_FLAG_DONT_CACHE, 0);//不保存到缓存

		if (URL != NULL)
		{
		   char Temp[MAXSIZE];
		   unsigned long Number =1;
		   while (Number != 0)
			{
				InternetReadFile(URL, Temp, MAXSIZE-1, &Number);
				Temp[Number] = '\0';
                printf("%s", Temp);
				os << Temp;
			}
			os.close();
			InternetCloseHandle(URL);
			URL = NULL;
			InternetCloseHandle(Open);
			Open = NULL;
		}
	}

	system("pause");
	return 0;
}
