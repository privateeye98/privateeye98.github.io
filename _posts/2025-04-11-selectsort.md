---
title: 자료구조/알고리즘 들어가기 앞서..
date: 2025-04-11 15:35:00 +0900
categories: [C/C++ 이론, 알고리즘,정렬]
tags:
  [
    github,
    알고리즘,
    C언어,
    C++,
	선택정렬
  ]
---

# 알고리즘 [ 선택정렬 ]

정렬되지 않은 전체 자료 중에서 **해당 위치에 맞는 자료를 선택하여 위치를 교환**하는 정렬

1. 입력 배열 전체에서 **최솟값**을 전택
2. 배열의 **0번** 원소와 자리를 바꾸고 다음엔 0번 원소를 제외한 나머지 원소에서 최솟값을 선택하여, 배열의 1번 원소와 자리를 바꿔가며 정렬
3. 마지막에 2개의 원소중 최솟값을 선택하여 자리를 바꿈으로써 오름차순의 정렬을 마친다.

제자리 정렬 알고리즘

작은 파일들에서 잘 동작함 → 매우 큰 값과 작은 키를 가진 파일들의 정렬시 사용

- **장점**
    
    원리가 간단하여 구현이 쉽다.
    
    제자리 정렬 방식이므로 추가적인 **저장 공간이** 필요하지 않다.
    
- 단점
    
    확장성이 좋지 않다. n^2
    

## 알고리즘 예제
![Image](https://github.com/user-attachments/assets/82d5735a-66db-4fd4-9752-334e12cedccf)

```cpp
#include<iostream>
# define SWAP(x, y, temp) ( (temp)=(x), (x)=(y), (y)=(temp) )
#define MAXSIZE 10

using namespace std;

void selection_sort(int arr[], int N) {
	int minIndex,temp;
	for (int i = 0; i < N - 1; i++) {
		minIndex = i; // minIndex에 i를 저장 0~9까지 순서대로 진행저장 됨.

		for (int j = i+1; j < N; j++) { //-> i보다 1이 커야 겹치는현상이 없으므로 i+1
			if (arr[j] < arr[minIndex])
				minIndex = j; //-> 만약 arr[minIndex(i)]가 arr[j]보다 작다면 
			//-> minIndex에 j를 저장함 WHY? 당연히 arr[j]가 최소값 이었을테니,
		}

		if (i != minIndex) {
			SWAP(arr[i], arr[minIndex], temp);
		} //-> 스왑함수를 통해 i 와 minIndex의 값을 변경해줌으로써 최솟값을 앞으로 보내는 작업을 함.
	}
	for (int k = 0; k < 10; k++) {
		cout << arr[k] << " ";
	}
}

int main() {
	
	int arr[10] = {4,8,1,2,5,7,9,10,12,18};

	selection_sort(arr, 10);

	

}
```
