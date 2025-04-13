---
title: 알고리즘/합병정렬
date: 2025-04-13 19:20:00 +0900
categories: [C/C++ 이론, 알고리즘,정렬]
tags:
  [
    github,
    알고리즘,
    C언어,
    C++,
	합병정렬
  ]
---

# 알고리즘 [ 합병정렬 ]

입력이 2개의 부분 문제로 분할되고, 부분 문제의 크기가 1/2로감소하는 분할 정복 알고리즘 == 결국, 합병 과정이 문제를 정복하는 것

합병 → 2개의 각각 정렬된 숫자들을 1개의 정렬된 숫자로 합치는 것

![Image](https://github.com/user-attachments/assets/6368f874-8865-42c6-b3a7-474f8a26fa64)

- 입력 크기가 n=8인 배열 A=[37, 10, 22, 30, 35, 13, 25, 24]에 대하여합병 정렬 알고리즘이 수행되는 과정
    
    ![Image](https://github.com/user-attachments/assets/8503a08f-650e-4d82-96c2-557f1ca17520)
    
- 분할하는 부분은 배열의 중간 인덱스 계산과 2번의 재귀 호출이므로O(1) 시간이 소요 됨 → 합병의 수행 시간은 입력의 크기에 비례
    
    → 2개의 정렬된 배열 A와 B의 크기가 각각 n과 m이라면, 최대 비교횟수= (n+m-1)
    
    ![Image](https://github.com/user-attachments/assets/7177fc0f-531a-48d3-838c-03e65993fe79)
    
    $$
    합병의 시간 복잡도 = O(M+N)
    $$
    
- 단점 : 공간 복잡도 O(n)
    
    추가로 입력과 같은 크기의 공간이 별도로 필요함
    

2개의 정렬된 부분을 하나로 합병하기 위해, 합병된 결과를 저장할곳이 필요하기 때문

```python
#include<iostream>
using namespace std;

int target[10] = { 3,5,7,9,1,2,4,6,8,0 };
int temp[10];

void Merge(int start, int m, int end) {
    cout << "병합! 구간: [" << start << " ~ " << end << "]\n";

    for (int i = start; i <= end; i++)
        temp[i] = target[i];

    int tempLeft = start;
    int tempRight = m + 1;
    int current = start;

    while (tempLeft <= m && tempRight <= end) {
        if (temp[tempLeft] <= temp[tempRight]) {
            target[current++] = temp[tempLeft++];
        }
        else {
            target[current++] = temp[tempRight++];
        }
    }

    while (tempLeft <= m) {
        target[current++] = temp[tempLeft++];
    }

    // 정렬된 구간 출력
    cout << "결과 : ";
    for (int i = start; i <= end; i++) {
        cout << target[i] << " ";
    }
    cout << "\n";
}

void MergeSort(int start, int end) {
    cout << "분할! 구간: [" << start << " ~ " << end << "]\n";
    if (start < end) {
        int m = (start + end) / 2;
        MergeSort(start, m);
        MergeSort(m + 1, end);
        Merge(start, m, end);
    }
}

int main() {
    MergeSort(0, 9);
    cout << "\n최종 정렬 결과: ";
    for (int i = 0; i < 10; i++) {
        cout << target[i] << " ";
    }
    cout << endl;
    return 0;
}

```