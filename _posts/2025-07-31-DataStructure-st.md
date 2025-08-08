---
title: "1. Basic Concepts"
excerpt: ""

categories:
  - DataStructure
tags:
  - tag1
  - tag2

permalink: /DataStructure/st/

toc: true
toc_sticky: true

date: 2025-08-01
last_modified_at: 2025-08-01



---


## 1. Introduction
소프트웨어 개발 과정에서의 System Life Cycle을 설명   
<blockquote>문제 해결을 위해 다음 5단계를 따름:  
<br>

1. Requirement (요구사항: 입력/출력 정의)  
2. Analysis (문제 분해: manageable sub-problems로 나눔)  
3. Design (ADT와 알고리즘 수준의 설계)  
4. Coding (구현)  
5. Verification (검증, 테스트 및 오류 제거)  
</blockquote>

---
  
## 2. Algorithms
알고리즘 정의: 특정 작업을 수행하는 유한 개의 명령어 집합  
<blockquote> 조건:  
<br>

- 입력 (0개 이상)  
- 출력 (최소 1개)  
- 명확성 (Definiteness)  
- 유한성 (Finiteness)  
- 효과성 (Effectiveness) </blockquote> 

알고리즘 ≠ 프로그램  
(알고리즘은 개념적 단계, 프로그램은 구체적 구현)  
  
---
  
## 3. Pseudo Code
코드 유사 형식의 알고리즘 표현 방법 (영어+프로그래밍 논리 혼합)

<blockquote> 장점:  </blockquote>  

- 언어 독립적  
- 로직 설계에 집중 가능  

<blockquote> 3가지 구조:  </blockquote>  

- 순차 (Sequence)
- 선택 (Selection)
- 반복 (Loop)

실제 실행은 안 되지만, 프로그램 설계의 중간 단계로 활용됨
  
---
  
## 4. Abstract Data Type (ADT)
ADT란?: 데이터 + 그에 대한 연산의 집합을 추상적으로 정의

“무엇을 할 수 있는가”에 집중 (What it does)

내부 표현과 구현은 숨김 (How it is done)

<blockquote>예시:  
<br>

- 자연수 ADT: Add, Subtract, Is_Zero 등
- 리스트 ADT: insert, retrieve 등 </blockquote>
  
---
  
## 5. ADT Implementations
<blockquote>ADT를 구현하는 두 가지 대표 방식: </blockquote>

1. Array 기반: 인덱스를 이용한 순차적 접근  
2. Linked List 기반: 포인터를 이용한 동적 연결 구조  

<br>
<blockquote>관련 개념: </blockquote>

- 포인터 (Pointer)
- 구조체 (Structure)
- self-referential 구조 (struct Node { int data; struct Node *next; })

선형 리스트와 비선형 리스트 구현도 소개됨
  
---
  
## 6. Generic Code for ADT’s
다양한 타입의 자료형에 대해 일반화된 구현이 필요함
<blockquote>C언어에서의 방법: </blockquote>

- void* 포인터를 활용한 자료형 독립성   
- function pointer를 통한 연산 일반화

C++, Java에서는 템플릿(generic programming) 지원으로 더 간단하게 처리 가능
<blockquote>예시: </blockquote>

- void* createNode(void* itemPtr);

- 비교 함수 포인터: int (*compare)(void*, void*)
  
---
  
## 7. Algorithm Efficiency
알고리즘의 성능을 수학적으로 분석

복잡도 표기: 시간/공간 복잡도, 특히 시간 복잡도 분석

<blockquote>분석 방법:
<br>

- 반복문 (linear: O(n), quadratic: O(n²), logarithmic: O(log n) 등)
- 중첩 반복문 (nested loop)의 총 수행 횟수 계산</blockquote>

  
**Big-O 표기법**: 최악의 경우 복잡도 표현
- O(1), O(n), O(log n), O(n log n), O(n²), O(2ⁿ), O(n!) 등

**핵심: 입력 크기가 커질수록 차수(지수)의 차이가 훨씬 중요하며, 상수 계수는 중요하지 않음**

## 결론
이 Agenda는 자료구조 수업의 기반을 형성하는 핵심 구성 요소로서, 단순히 코드 구현이 아니라 문제 해결 절차, 추상화, 성능 분석까지 포함하는 전반적인 설계 철학을 담고 있다.


---

## System Life Cycle: Problem ->Problem solving -> Solution

### Problem Solving단계(4단계)  

1. Requirement (요구사항 분석)
- 입력과 출력 정의
- 문제에 필요한 기능 또는 조건들을 명확히 설정

2. Analysis (분해 분석)
- 문제를 더 작은 단위로 나누어 이해
- 각 구성 요소가 어떤 역할을 하는지 파악

3. Design (설계)
- **추상 자료형(ADT), 알고리즘 설계**
- 효율적인 해결 방안을 설계

4. Coding(코딩)
- 설계를 기반으로 프로그램 코드 작성


## Solution: Program Code

## 이후 단계
5. Verification(검증)
- 프로그램이 올바르게 작동하는지 테스트
- 요구사항을 제대로 충족하는지 확인


## 이 흐름은 전형적인 문제 해결 절차로써 자료구조와 알고리즘을 설계할 때도 이런 절차를 따른다.



