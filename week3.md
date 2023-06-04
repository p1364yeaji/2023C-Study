## 1. equation

* equation.cpp
```` c++
#include <iostream>
#include <cmath>
using namespace std;

class Equation {
	int a;
	int b;
	int c;

public:
	Equation(int num1, int num2, int num3) { 
		a = num1;
		b = num2;
		c = num3;
	}

	int getA() {
		return a;
	}
	int getB() {
		return b;
	}
	int getC() {
		return c;
	}
	double getDiscriminant() {
		return b * b - 4 * a * c;
	}
	double getRoot1() {
		return (-b + sqrt(b * b - 4 * a * c)) / 2 * a;
	}
	double getRoot2() {
		return (-b - sqrt(b * b - 4 * a * c)) / 2 * a;
	}
};

int main() {
	int a = 0;
	int b = 0;
	int c = 0;

	cout << "Enter the three coefficients of the quadratic equation(ax^2 + bx + c = 0): ";
	cin >> a >> b >> c;
	Equation e1(a, b, c);

	if (e1.getDiscriminant() > 0)
		cout << "The equation has two different real roots: " << e1.getRoot1() << " and " << e1.getRoot2() << endl;
	else if (e1.getDiscriminant() == 0)
		cout << "The equation has multiple real roots: " << e1.getRoot1() << endl;
	else
		cout << "The equation has no real roots." << endl;


	return 0;
}
````

-----

* 실행 결과
![1](https://github.com/p1364yeaji/2023C-Study/assets/126933499/e856a927-ae1b-4e7d-a579-d3bf280390d5)

## 2. data

* data.cpp
````C++
#include <iostream>
#include <ctime>
using namespace std;


//윤년, 달마다 일 수의 차이를 계산하는 과정을 구현하지 못했습니다//

class Date {
	int year;
	int month;
	int day; 
public:
	Date() { //현재 날짜에 대한 객체 생성자
		int T = time(0);
		T = T / 60 / 60 / 24; //초를 일 단위로 변환
		year = 1970 + T / 365;
		T = T % 365;
		month = T / 31 + 1; // month의 최솟값이 1이 되도록 설정  
		day = T % 31 + 1; //day의 최솟값이 1이 되도록 설정
	};
	Date(int second) { //입력받은 초를 날짜로 변환한 객체 생성자
		int T = second;
		T = T / 60 / 60 / 24; //초를 일 단위로 변환
		year = 1970 + T / 365;
		T = T % 365 + 1;
		month = T / 30 + 1;
		day = T % 30 + 1;
	};
	Date(int y, int m, int d) { //입력받은 날짜를 가진 객체 생성자
		year = y;
		month = m;
		day = d;
	};

	int getYear() {
		return year;
	}
	int getMonth() {
		return month;
	}
	int getDay() {
		return day;
	}

	//초를 입력 받아 객체의 시간을 재설정하는 멤버함수
	void setDate(int elapseTime) {
		int T = elapseTime;
		T = T / 60 / 60 / 24;
		year = 1970 + T / 365;
		T = T % 365;
		month = T / 30 + 1;
		day = T % 30 + 1;
	}
};


int main() {
	Date d1;
	Date d2(555550);

	cout << d1.getYear() << "년 " <<  d1.getMonth() << "월 " << d1.getDay() << "일" << endl;
	cout << d2.getYear() << "년 " << d2.getMonth() << "월 " << d2.getDay() << "일" << endl;

	return 0;
}
````

-----

* 실행 결과
![2](https://github.com/p1364yeaji/2023C-Study/assets/126933499/e255e86c-3b8c-42d2-9c11-c988ee519eb3)

## 3. calendar

* calendar.h
````C++
#pragma once

class Calendar {
	int year;
	int month;

public:
	int getYear();
	int getMonth();
	void setYear(int y);
	void setMonth(int m);
	void setYearMonth(int y, int m);

	void printMonth(); //해당 연도의 달에 대한 달력 출력
	void printMonthTitle(); //달 제목 출력
	void printMonthName(); //달의 영어 이름 구하기
	void printMonthBody(); //달의 내용 출력
	int getStartDay(); //달의 첫 날짜에 대한 시작 요일 구하기
	int getTotalNumberOfDays(); //1800년 1월 1일 이후의 총 날짜 수 구하기
	int getNumberOfDaysInMonth(int num); //달의 일 수 구하기
	bool isLeapYear(int num); //윤년인지 결정
};
````

* calendar.cpp
````C++
#include <iostream>
#include <iomanip>
#include "calendar.h"
using namespace std;


int Calendar::getYear() {
	return year;
}
int Calendar::getMonth() {
	return month;
}
void Calendar::setYear(int y) {
	year = y;
}
void Calendar::setMonth(int m) {
	month = m;
}
void Calendar::setYearMonth(int y, int m) {
	year = y;
	month = m;
}

//해당 연도의 달에 대한 달력 출력
void Calendar::printMonth() {
	printMonthTitle(); //제목 출력
	printMonthBody(); //내용 출력
}

//달 제목 출력
void Calendar::printMonthTitle() {
	printMonthName();
	cout << " " << year << endl;
	cout << "------------------------------" << endl;
	cout << " Sun Mon Tus Wed Thu Fri Sat" << endl;
}

//달의 영어 이름 구하기 
void Calendar::printMonthName() {
	cout << "\t  ";
	switch (month) {
	case 1: cout << "January"; break;
	case 2: cout << "February"; break;
	case 3: cout << "March"; break;
	case 4: cout << "April"; break;
	case 5: cout << "May"; break;
	case 6: cout << "June"; break;
	case 7: cout << "July"; break;
	case 8: cout << "August"; break;
	case 9: cout << "September"; break;
	case 10: cout << "October"; break;
	case 11: cout << "November"; break;
	case 12: cout << "December";
	}
}

//달의 내용 출력
void Calendar::printMonthBody() {
	int startDay = getStartDay(); //시작 요일 구하기
	int numberOfDaysInMonth = getNumberOfDaysInMonth(month); // 날짜 수 구하기

	//첫째날 앞에 공백 넣기
	int i = 0;
	for (i = 0; i < startDay; i++)
		cout << "    ";

	//날짜 출력
	for (i = 1; i <= numberOfDaysInMonth; i++) {
		cout << setw(4) << i;
		if ((i + startDay) % 7 == 0)
			cout << endl;
	}
}

//달의 첫 날짜에 대한 시작 요일 구하기
int Calendar::getStartDay() {
	//1800년 1월 1일 이후의 총 날짜 수 구하기
	int startDay1800 = 3;
	int totalNumberOfDays = getTotalNumberOfDays();

	//시작 요일 반환
	return (totalNumberOfDays + startDay1800) % 7;
}

//1800년 1월 1일 이후의 총 날짜 수 구하기
int Calendar::getTotalNumberOfDays() {
	int total = 0;

	for (int i = 1800; i < year; i++) { //1800년도부터 연도 - 1까지의 총 날짜 수 구하기
		if (isLeapYear(i))
			total += 366;
		else
			total += 365;
	}

	for (int i = 1; i < month; i++) // 1월부터 달력의 달 바로 전날까지의 날짜 수 추가하기
		total += getNumberOfDaysInMonth(i);
	return total;
}

//달의 일 수 구하기
int Calendar::getNumberOfDaysInMonth(int num) {
	if (num == 1 || num == 3 || num == 5 || num == 7 || num == 8 || num == 10 || num == 12)
		return 31;
	else if (num == 4 || num == 6 || num == 9 || num == 11)
		return 30;
	else if (num == 2)
		return isLeapYear(year) ? 29 : 28;
	else
		return 0;
}

//윤년인지 결정
bool Calendar::isLeapYear(int num) {
	return num % 400 == 0 || (num % 4 == 0 && num % 100 != 0);
}
````

* main.cpp
````C++
#include <iostream>
#include <iomanip>
#include "calendar.h"
using namespace std;

int main() {
	Calendar c1;

	cout << "Enter full year (e.g., 2023): ";
	int year;
	cin >> year;

	cout << "Enter month in number between 1 and 12: ";
	int month;
	cin >> month;

	c1.setYearMonth(year, month);
	c1.printMonth(); //달력 출력

	return 0;
}
````

-----

* 실행 결과
![3](https://github.com/p1364yeaji/2023C-Study/assets/126933499/136b7428-c18d-475b-90a5-fd59eb3d6129)
