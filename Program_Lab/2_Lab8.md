# 


1. 사람 클래스를 정의하고 배운 내용들을 메소드로 추가하고 객체를 생성한 후 구현한 기능을 확인하는 프로그램을 작상하시오.

2. 다음 클래스에 데이터를 저장하고 main 함수의 세 경우가 얕은 복사가 이루어지는지 깊은 복사가 이루어지는지 확인 후 깊은 복사가 이루어지도록 메소드를 재정의하시오.
또한 소멸자가 호출될 때 오류가 생기지 않도록 수정하시오.

```cpp
class myArray {
  int length; //실제 저장된 데이터 수
  int *buf; 
public:
  myArray(int size) { length = 0; buf = new int[size];} // 데이터 저장 공간을 동적 메모리 할당하기
  // myArray(const myArray& arr); 
  // myArray& opertor = (const myArray& arry);
  ~myArray();
  int& operator [](int idx);  // idx 에 해당되는 것에 저장된 값을 가져오거나 저장이 가능하도록 하는 것
  void pushback(int value);   // 맨 앞에서 부터 저장
  friend ostream& operator << (ostram& os, myArray& obj);
};

int main(int argc, char const *argv[])
{
	myArray arrA(20);  // 제거 불가
	myArray arrB(arrA);  // 제거  불가
	myArray arrC = arrA;   // 제거 불가
	for(int i = 0; i < 10; i++)
		arrA.pushback(i);

	cout<< arrA[2] << endl;
	cout<< arrB[2] << endl;
	cout<< arrC[2] << endl;

	arrC = arrB;   // 제거 불가

	arrB[5] = 20;
	cout << arrC[4] << endl;

	return 0;
}
```

3. 1번의 객체를 vector 클래스에 저장한 후 count_if 알고리즘과 sort 알고리즘을 적용시키는 프로그램을 작성하시오.
  
4. 익명함수를 정의하고 STL 알고리즘에 적용시켜서 확인하는 프로그램을 작성하시오. 
