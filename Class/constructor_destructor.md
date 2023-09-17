# 생성자와 소멸자  
 
## 생성자(constructor)
C++ 클래스는 객체가 생성될 때 자동으로 호출되는 생성자라는 특수한 멤버 함수를 가진다.
일반적으로 생성자를 통해 객체가 사용되기 전에 수행하여야 할 기능(예: 멤버 변수 초기화, 동적 메모리 할당 등)을 수행한다. 
생성자를 정의하는 구문은 다음과 같다.

```c++
class 이름::class 이름(인수 목록) {
   ....
}
```
### 생성자의 특징
   + 생성자는 함수이다. 
   + 생성자는 객체가 생성될 때 호출되는 함수로 객체가 생성될 때 필요한 초기 작업을 한다. 
   + 객체 생성 시 생성자는 오직 한번만 자동으로 실행한다. 
   + 생성자의 이름은 클래스 이름과 **동일**하다. 
   + 생성자는 아무것도 리턴하지 않는다 (void라고도 적을 필요가 없다).
   + 생성자는 오버로딩이 가능하다.(한 클래스에서 여러 개의 생성자를 만들 수 있다.)
   + 생성자도 함수이므로 디폴트 매개변수를 가질 수 있다.
   + 생성자가 선언되지 않으면 컴파일러가 **inline** 기본 생성자(default constructor)를 자동으로 생성한다.
   + 매개변수가 있는 생성자를 선언하는 경우 컴파일러는 기본 생성자를 자동으로 생성하지 않는다.

### 생성자의 접근성
 * 생성자는 클래스 정의 또는 상속 계층 구조의 외부의 코드가 클래스의 객체를 만들 수 있도록 일반적으로 **public** 접근성을 갖으나
   **private** 또는 **protected** 접근성을 갖도록 선언할 수 있다. 

### 생성자 오버로드
생성자는 아래의 프로그램 코드와 같이 여러 생성자를 가지는 Person 클래스이다. 

```c++
class Person {
   Person();            // 기본 생성자
   Person(string name); // 생성자 오버로드 (매개변수 한 개) 
   Person(string name, int age);  // 생성자 오버로드 (매개 변수 두 개)
   ...
};
```
### 기본 생성자(default constructor)

클래스의 객체가 생성할 때 반드시 하나의 생성자가 호출되어야 한다.
기본 생성자는 매개 변수가 없는 생성자를 말한다. 다만, 매개 변수만 없을 뿐 수동으로 기능을 구현할 수는 있다.
생성자가 하나도 선언되지 않는 클래스의 경우 컴파일러가 기본 생성자를 자동으로 생성한다.
컴파일러가 생성한 기본 생성자는 아무 코드도 실행되지 않고 바로 리턴한다.
아래 코드와 같이 컴파일로가 생성한 기본 생성자를 사용하여 객체를 생성할 경우 경고가 발생한다. 그러므로 기본 생성자를 사용하여 객체를 생성할 경우에는 괄호를 사용하지 마라.
```c++
#include <iostream>
using namespace std;

class Point { };

int main(int argc, char const *argv[])
{
	Point p();
	return 0;
}
```

#### 1. 기본 생성자를 자동 생성 

객체를 생성할 때 수행해야 할 내용이 없으며 파러미터를 가지는 생성자를 만들 필요가 없는 
경우 클래스를 정의할 때 생성자를 선언하지 않아도 된다. 
이 경우 컴파일러가 실행 코드가 없는 기본 클래스를 생성한다. 

```c++
#include <iostream>
using namespace std;

class Person{
private:
   string name;
   int age;
public:
   void setName(string n) { name = n;}
   void setAge(int a) { age = a;}
   void show() {
      cout << name << ", " << age << endl;
   }
};

int main(int argc, char const *argv[])
{
   Person s;  // 컴파일러가 자동 생성한 기본 생성자 Person() 호출 
   s.setName("Chul-soo Lee");
   s.setAge(20);
   s.show();
   return 0;
}
```
실행 결과는 다음과 같다.

``Chul-soo Lee, 20``

앞의 코드의 main 함수를 다음과 같이 수정하여 얻은 실행 파일을 실행하였을 때 결과를 살펴보자. 
```c++
int main(int argc, char const *argv[])
{
	Person man;
	man.show();
	return 0;
}
```
실행 결과의 한 예는 다음과 같이 임의의 값이 출력된다. 이는 객체가 생성되어 데이터를 저장할 수 있는 메모리 저장 공간이 할당되었으나 
저장 공간이 초기화되지 않아 임의의 값이 저장된 결과이다. 

``, 9066768``

* 컴파일러가 기본 생성자를 생성하지 못하도록 다음과 같이 명시적으로 컴파일러에서 생성된 기본 생성자를 삭제되도록 정의한다.
  다음은 앞의 Person 클래스의 기본 생성자를 생성하지 않도록 하는 예이다.
```c++
class Person{
private:
   string name;
   int age;
public:
   Person() = delete; // 컴파일러의 기본 생성자 생성을 하지 않도록 함 
   void setName(string n) { name = n;}
   void setAge(int a) { age = a;}
   void show() {
      cout << name << ", " << age << endl;
   }
};
```
#### 2. 멤버 초기화 목록

생성자는 필요에 따라 생성자 함수의 몸체가 실행되기 전에 클래스의 멥버 변수를 초기화하는 멤버 초기화 목록을 가질 수 있다. 
생성자 함수 몸체에서 멤버 변수에 값을 초기화 하는 경우보다 멤버 초기화 목록을 사용하는 것이 좋다. 멤버 초기화 목록은 멤버 변수의 메모리에 값을 직접 초기화 한다. 
다음은 콜론 다음에 ``멤버 변수명(파라미터 변수명)``의 형태로 멤버 초기화 목록 표현이다.

 ```c++
  Person(string n, int a) : name {n}, age{a} {}
```

#### 3. 기본 생성자 사용시 멤버 변수 초기화 

기본 생성자를 사용하여 멤버 변수의 값의 초기화를 아래와 같이 클래스 정의 시 멤버 변수 선언 시 초기화 할 수 있다. 

```c++
#include <iostream>
using namespace std;

class Person{
   string name {"Chul-Soo Lee"};
   int age {20};
public:
   void setName(string n) { name = n;}
   void setAge(int a) { age = a;}
   void show() {
      cout << name << ", " << age << endl;
   }
};

int main(int argc, char const *argv[])
{
	Person man;
	man.show();
	return 0;
}
```
앞의 프로그램 코드의 실행 결과는 다음과 같다.

``Chul-soo Lee, 20``

#### 4. 프로그래머가 생성자를 새롭게 정의하여 멤버 변수 초기화

앞의 프로그램 코드에서 객체를 생성할 때 이름과 나이를 초기화하는 생성자를 다음과 
같이 선언하였다.

```c++
#include <iostream>
using namespace std;

class Person{
private:
   string name;
   int age;
public:
   Person(string n, int a) : name(n), age(a) {} // 멤버 초기화 리스트를 활용한 멤버 변수 초기화 
   void setName(string n) { name = n;}
   void setAge(int a) { age = a;}
   void show() {
      cout << name << ", " << age << endl;
   }
};

int main(int argc, char const *argv[])
{
   Person father;  // [컴파일 에러 발생] 컴파일러가 기본 생성자를 생성하지 않음 
   Person son("Gil-Dong Hong", 30); //생성자 호출 
   son.show();
   return 0;
}
```

앞의 프로그램을 컴파일하면 다음과 같은 에러가 발생한다. 
```
error: no matching constructor for initialization of 'Person'
        Person father;  // [컴파일 에러 발생] 컴파일러가 기본 생성자를 생성하지 않음 
               ^
```
프로그렘에서 ```Person son("Gil-Dong Hong", 30);```는 매개 변수를 가진 생성자
```Person(string n, int a)```를  호출하기 때문에 정상적으로 컴파일된다. 
그러나 ```Person father;```는 파러미터가 없는 기본 생성자를 호출하는데 파러미터가 있는 생성자가 선언되어 있기 때문에 컴파일러가 기본 생성자를 자동적으로 만들어 주지 않는다. 
그러므로 기본 생성자를 선언 및 정의하여야 한다. 

```c++
#include <iostream>
using namespace std;

class Person{
private:
   string name {""};
   int age {0];
public:
   Person(){}            // 기본 생성자
   Person(string n) : name(n){}      // 생성자 1
   Person(string n, int a) : name(n), age(a) {} // 생성자 2
   void setName(string n) { name = n;}
   void setAge(int a) { age = a;}
   void show() {
      cout << name << ", " << age << endl;
   }
};

int main(int argc, char const *argv[])
{
   Person dad; // 기본 생성자 호출
   Person mom("Young-Hee Park");  // 생성자 1 호출
   Person son("Gil-Dong Lee", 20); // 생성자 2 호출
   dad.setName("Chul-soo Lee"), dad.setAge(52);
   mom.setAge(50);
   dad.show(), mom.show(), son.show();
   return 0;
}
```
앞의 프로그램은 여러 생성자를 중복 선언한 것이다. 
```main``` 함수에서 ```Person dad;```, ```Person mom("Young-Hee Park");```
```Person son("Gil-Dong Lee", 20);``` 의 세 개의 객체를 생성하고 있으며 
각 객체가 생성될 때 호출되는 생성자는 기본 생성자, 생성자 1, 생성자 2 이다. 
프로그램의 실행 결과는 다음과 같다.


``Chul-soo Lee, 52`` </br>
``Young-Hee Park, 50`` </br>
``Gil-Dong Lee, 20``


생성자는 앞에서 살펴본 생성자 이외에 [복사 생성자](../copy_constructor.md), ``복사 할당 연산자``, ``이동 생성자``, ``이동 할당 연산자`` 가 존재한다. 

  
## 소멸자(destructor)

객체가 소멸되면 객체에 할당된 메모리는 반환된다. 
또한 객체가 소멸 시 소멸자 함수가 반드시 호출된다.
소멸자는 객체가 소멸되는 시점에 자동으로 호출되는 클래스의 멤버 함수이다. 
소멸자를 정의하는 구문은 다음과 같다.

```cpp
class 이름::~class 이름(인수 목록) {
   ....
}
```
* 소멸자의 특징
   + 소멸자는 함수이다.
   + 소멸자는 객체가 사라질 때 필요한 마무리 작업을 하게 된다.
   + 소멸자의 이름은 클래스 이름 앞에 ~를 붙인다.
   + 소멸자는 반환 자료형(리턴 타입)이 없으며 아무것도 반환하지 않는다 
   + 소멸자는 **오직 한 개**만 존재하고 매개 변수는 가질 수 없다.
   + 소멸자가 선언되어 있지 않으면 컴파일러가 기본 소멸자(default destructor)를 자동으로 생성한다. 
   
다음은 소멸자 호출을 확인하는 프로그램이다. 

```cpp
#include <iostream>
using namespace std;

class Person{
private:
   string name;
   int age;
public:
   ~Person();
   void setName(string n) { name = n;}
   void setAge(int a) { age = a;}
   void show() {
      cout << name << ", " << age << endl;
   }
};

Person::~Person() {
   cout << "소멸자 호출" << endl;
}

int main(int argc, char const *argv[])
{
   Person s;  // 컴파일러가 자동 생성한 기본 생성자 호출 
   s.setName("Chul-soo Lee");
   s.setAge(20);
   s.show();
   return 0;
}
```
```main```함수에서 ```s.show()```를 호출 한 후 ```main```함수가 종료되면서 
객체 ```s```의 소멸자가 호출되어 "소멸자 호출"이라는 문자열이 출력된다. 
실행 결과는 다음과 같다.

``Chul-soo Lee, 20``

``소멸자 호출``
