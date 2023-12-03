# 2학기 평가

## **전제조건**

프로그램의 변수 이름에는 자신 이름의 이니셜이 들어갈 수 있도록 하고 주석을 최소한 3개 이상 작성하시오. 

###1. 다음 [프로그램 코드](../SampleCodes/FinalExam/prob_1.cpp)는 이름을 입력받아 출력하는 프로그램입니다. 이 프로그램의 출력 부분을 변경하여 출력 형태와 같이 출력되도록 출력 코드를 추가하시오. (10)

```c++
#include <iostream>
#include <string>

using namespace std;

int main(int argc, char const *argv[])
{
	cout << "이름을 입력하시요: ";
	string name;  // 변수 이름 변경한 후 처리하시오.

	cin >> name;

	cout << name;

	return 0;
}
```

* 출력 형태

```c++
이름을 입력하시오: Peter

=====================
|                   |
| Peter 님, 안녕하세요! |
|                   |
=====================
```

### 2. 다음 [프로그램 코드](../SampleCodes/FinalExam/prob_2.cpp)를 활용하여 키보드로 부터 실수를 입력받아 ``vector<double> scores`` 에 저장한 후 평균, 최소값, 최대값, 중간값(저장된 값을 정렬 한 후 원소의 개수가 홀 수 개 이면 중간 위치의 값, 원소의 개수가 짝수 개이면 정렬 후 두번 째 영역의 첫 원소의 값, 예로 개수가 8이면 다섯 번째 원소). (10)

```cpp
#include <iostream>
#include <vector>

using namespace std;

int main(int argc, char const *argv[])
{
	vector<double> scores;
	double score; 

	cout << "실수를 입력하시오. (음수가 입력되면 입력을 중지)" << endl;
	cout << "100.0 보다 큰 점수가 입력되면 다시 입력 받음" << endl;
	
	do {
		cin >> score;
		if(score > 100) { cout << "다시 입력하시요" << endl; continue; }
		if(score >= 0) cout << "data:" << score << endl;
	}while(score >= 0);

	return 0;
}
```

### 3. 다음 [프로그램 코드](../SampleCodes/FinalExam/prob_3.cpp)를 활용하여 키보드로 부터 단어를 "q"를 입력할 때까지 입력받아 set words에 저장한 후 저장된 내용을 출력하고 for_each와 단어의 길이가 4 이상인 단어의 개수를 변수 count에 저장한 후 화면에 출력 하는 코드를 작성하시오.   (10)

```cpp
#include <iostream>
#include <string>
#include <set>
#include <algorithm>

using namespace std;

int main(int argc, char const *argv[])
{
	string word;
	set<string> words;
	int count = 0;   // 단어의 크기

	cout << "단어를 입력하시오('q' 입력할 때 까지): " << endl;

	do {
		cin >> word;
		// set 에 단어 저장 
	}while(word != "q"); 

	// set<string> words 에 저장된 단어 출력


	// for_each와 단어의 길이가 4 이상인 단어의 개수를 계산하는 lambda 함수를 정의해서 
	// 단어의 개수가 4 이상의 개수를 count에 저장

	
	cout << count << endl; // 입력한 단어 중 길이가 4 이상인 단어의 개수 출력 

	return 0;
}
```

### 4. 키보드롤 부터 양의 정수를 입력받아 ``vector`` 컨테이너에 저장한 후 lambda 함수와 for_each 를 활용해서 짝수는 10을 더하고 홀 수는 50을 더한다. 그   lambda함수 외부에서``vector`` 컨테이너에 저장된 값을 iterator를 활용해서 출력하시오. (10)

### 5. 다음 클래스를 정의하고 ``main``함수에서 각 도형 클래스의 객체를 생성하여 <vector>를 활용하여 저장 관리하며 Shape 클래스의 인스턴스를 활용하여 각 도형의 메소드를 호출하며 테스트하는 프로그램 작성하시오. (25점)

* Shape 클래스(추상클래스) 정의
* 2차원의 점을 표현하는 Point 클래스 정의 
* Rectangle, Circle, Triangle 클래스를 Shape 클래스를 상속받아 정의 
	+ 생성자 함수를 정의 
 	+ 4개의 클래스는 다음 메소드를 공통으로 가짐
 		- rotate(), getArea(), draw(), reSize(), move(), changeColor() [각 메소드의 입력 파러미터와 리턴타입은 각자 정의]
 	+ 4개의 클래스는 다음의 멤버 변수를 공통으로 가짐
		- color, area
 	+ 각 클래스는 Point 클래스를 활용하여 도형의 각 점을 표현
 	+ 각 클래스는 필요에 따라 추가적인 멤버변수와, 멤버함수를 선언하고 정의 

### 6. 육면체 Box 클래스를 정의하고 ``main`` 함수에서 클래스의 연산자를 검증하는 프로그램을 작성하시오. (25점)

* 멤버 변수: length, width, height (모두 실수)
* 생성자
	+ 각 값이 주어지면 주어진 값으로 초기화
	+ 값이 주어지지 않으면 0으로 초기화
* setLength(), setWidth(), setHeight() 멤버함수 정의 
* getVolume() 멤버함수 정의 
	+ 부피를 구하여 반환 
* + 연산자 재 정의
	+ length, width, height 각 값을 더하기
* == 연산자 재 정의
	+ 두 객체의 각 멤버 변수의 값이 같을 때, true 반환 
* \> 연산자 재 정의 
	+ 두 객체의 부피를 비교 (앞 객체의 부피가 뒤 객체의 부피보다 크면  true)
* << 연산자 재 정의

### 7. 배열의 시작주소(arr)와 배열의 원소 개수(num)을 입력받아 배열에서 최대 값을 구하는 아래의 함수를 템플릿 함수(getMax)로 정의하고 ``main`` 함수에서 프로그램을 작성하여 검증하시오. (10점)

```c++
int getMax(int *arr, int num);
double getMax(double *arr, int num);
long getMax(long *arr, int num);
float getMax(float *arr, int num);
```
