---
title: "Lexical Analysis2"
excerpt: ""

categories:
  - Compiler
tags:
  - paser
  - scanner

permalink: /Compiler/lexicalanalysis2/

toc: true
toc_sticky: true

date: 2026-04-07
last_modified_at: 2026-04-07



---

📘 Page 1

🔷 제목
Lexical Analysis – Part 2

👉 해석
어휘 분석 2부

✔ 설명

이 슬라이드는 표지다.
이번 강의가 컴파일러에서 lexical analysis의 두 번째 파트라는 것을 의미한다.

👉 Part 1에서는:

token / lexeme / pattern
RE, DFA, NFA 기본 개념

👉 Part 2에서는:

NFA → DFA 변환
DFA 최소화

👉 즉, 이론 → 실제 구현 단계로 넘어가는 파트

🔷 다음 문장
Hwisoo So

👉 해석
소휘수

✔ 설명

강의를 진행하는 교수 이름이다.

🔷 다음 문장
Kyungpook National University

👉 해석
경북대학교

✔ 설명

강의가 진행되는 학교

🔷 다음 문장
COMP321 Compiler

👉 해석
컴파일러 과목

✔ 설명

이 슬라이드가 속한 과목 이름

🔷 다음 문장
Spring 2026

👉 해석
2026년 봄 학기

✔ 설명

강의 시기

📘 Page 2

🔷 제목
Outline

👉 해석
개요

✔ 설명

이 슬라이드는 Part 2 전체 흐름을 보여주는 지도다.
지금 어디까지 했고, 앞으로 뭘 할지 알려준다.

🔷 1번째 문장
The role of a scanner ✔

👉 해석
scanner의 역할 (완료됨)

✔ 설명

이미 배운 내용이다.

👉 scanner의 역할:

문자열 → token 변환

👉 예:

"abc" → identifier
"123" → number

👉 컴파일러의 첫 단계

🔷 2번째 문장
Scanner concepts ✔

👉 해석
scanner 개념 (완료됨)

✔ 설명

scanner를 이해하기 위한 기본 개념

🔷 다음 문장
Tokens, Lexemes, Patterns

👉 해석
토큰, 렉심, 패턴

✔ 설명

이 3개 관계가 핵심이다:

lexeme = 실제 문자열
pattern = 규칙
token = 분류 결과

👉 흐름:

lexeme → pattern 매칭 → token

🔷 다음 문장
Regular Expression & Automata (to be continued…)

👉 해석
정규표현식과 오토마타 (계속됨)

✔ 설명

이 부분이 Part 2 핵심

👉 의미:

RE → Automata → Scanner

👉 이론 → 구현 연결

🔷 다음 문장
Definitions of REs, DFAs and NFAs ✔

👉 해석
RE, DFA, NFA 정의 (완료됨)

✔ 설명

이미 배운 내용:

RE = 패턴 정의
DFA = 결정적 오토마타
NFA = 비결정적 오토마타

🔷 다음 문장
REs→NFA ✔

👉 해석
RE를 NFA로 변환 (완료됨)

✔ 설명

👉 Thompson construction

👉 핵심:

RE → NFA

🔷 다음 문장
NFA→DFA

👉 해석
NFA를 DFA로 변환

✔ 설명

👉 이제부터 배우는 핵심

👉 이유:

NFA → 구현 어려움
DFA → 구현 쉬움

🔷 다음 문장
DFA→minimal-state DFA

👉 해석
DFA 최소화

✔ 설명

👉 불필요한 상태 제거

👉 목적:

속도 향상
메모리 감소

🔷 다음 문장
Scanner generators

👉 해석
scanner 생성기

✔ 설명

👉 최종 목표

👉 예:

Lex
Flex

👉 역할:

RE → 자동으로 코드 생성

🔷 마지막 문장
Today’s agenda

👉 해석
오늘의 강의 내용

✔ 설명

👉 오늘 핵심:

NFA → DFA
DFA 최소화
📘 Page 3

🔷 제목
Subset Construction (NFA→DFA)

👉 해석
부분집합 구성법

✔ 설명

👉 NFA를 DFA로 바꾸는 핵심 알고리즘

🔷 1번째 문장
Instead of guessing in state s1 on symbol a,

👉 해석
상태 s1에서 입력 a에 대해 추측하는 대신

✔ 설명

👉 NFA에서는:

s1 --a--> s1
s1 --a--> s2

👉 두 가지 선택 있음

🔷 다음 문장
we can follow both transitions (s1→s1 and s1→s2) in parallel.

👉 해석
두 전이를 동시에 따라갈 수 있다

✔ 설명

👉 핵심 아이디어:

둘 다 동시에 고려

🔷 다음 문장
We introduce a “virtual state”

👉 해석
가상 상태를 도입한다

✔ 설명

👉 새로운 개념:

상태 집합 = 하나의 상태

🔷 다음 문장
that combines the states that we reach from s1 on symbol a.

👉 해석
s1에서 a를 읽고 도달 가능한 상태들을 합친다

✔ 설명

👉 결과:

{s1, s2}

🔷 다음 문장
The new virtual state contains states s1 and s2

👉 해석
새 상태는 s1과 s2를 포함한다

✔ 설명

👉 DFA 상태:

하나 = 여러 상태 묶음

🔷 다음 문장
we write {s1, s2} for the virtual state.

👉 해석
이 상태를 {s1, s2}라고 쓴다

✔ 설명

👉 집합 표기

🔷 다음 문장
A question: if we are in the virtual state {s1, s2},

👉 해석
질문: {s1, s2} 상태에 있다면

✔ 설명

👉 다음 입력 처리 문제

🔷 다음 문장
where can we go when we read symbol b?

👉 해석
b를 읽으면 어디로 가는가

✔ 설명

👉 핵심 질문

🔷 다음 문장
Answer: the virtual state takes us anywhere that one of its member states takes us on symbol b

👉 해석
답: 각 상태가 갈 수 있는 모든 곳으로 간다

✔ 설명

👉 union 개념

🔷 다음 문장
(either s1 or s3 in the above NFA).

👉 해석
(s1 또는 s3로 이동)

✔ 설명

👉 결과 상태:

{s1, s3}

🔷 다음 문장
So we introduce a second virtual state {s1 , s3}.

👉 해석
그래서 {s1, s3} 상태를 만든다

✔ 설명

👉 새로운 DFA 상태 생성

🔷 다음 문장
(continued on next slide.)

👉 해석
다음 슬라이드에서 계속

✔ 설명

👉 계산 이어짐

📘 Page 4

🔷 제목
Subset Construction (NFA→DFA)

👉 해석
부분집합 구성법

✔ 설명

👉 실제 계산 결과를 보여주는 슬라이드

🔷 문장
A “virtual state” is a subset of the set of states S={S0, S1, S2, S3, S4} of the NFA.

👉 해석
가상 상태는 NFA 상태 집합의 부분집합이다

✔ 설명

👉 핵심:

DFA 상태 = NFA 상태들의 집합

🔷 다음 문장
Table encoding DFA

👉 해석
DFA 전이표

✔ 설명

👉 δ 함수 표 형태

✔ 핵심 설명

👉 예:

{s1, s2} --b--> {s1, s3}

👉 집합 기반 전이

📘 Page 5

🔷 제목
Algorithm: NFA→DFA with Subset Construction

👉 해석
NFA→DFA 알고리즘

✔ 설명

👉 공식 알고리즘 설명

🔷 1번째 문장
We need to build a simulation of the NFA

👉 해석
NFA를 시뮬레이션해야 한다

✔ 설명

👉 DFA는 NFA 동작을 모방

🔷 다음 문장
Two key functions

👉 해석
두 가지 핵심 함수

✔ 설명

👉 핵심 연산

🔷 다음 문장
Move(si , a) : gives set of states reachable from set si by a

👉 해석
Move 함수: a를 읽고 갈 수 있는 상태 집합

✔ 설명

👉 입력 기반 이동

🔷 다음 문장
ε-closure(si) : gives set of states reachable from set si by ε

👉 해석
ε-closure: ε로 이동 가능한 상태 집합

✔ 설명

👉 입력 없이 이동

🔷 다음 문장
Start state derived from s0 of the NFA

👉 해석
시작 상태는 s0에서 유도

✔ 설명

👉 DFA 시작 상태 = ε-closure(s0)

🔷 다음 문장
Take its ε-closure S0 = ε-closure({s0})

👉 해석
시작 상태는 ε-closure(s0)

✔ 설명

👉 초기 상태 확장

🔷 다음 문장
Take the image of S0, Move(S0, α)

👉 해석
Move로 다음 상태 계산

✔ 설명

👉 입력 기반 이동

🔷 다음 문장
and take its ε-closure

👉 해석
그 결과에 ε-closure 적용

✔ 설명

👉 항상 closure 적용

🔷 다음 문장
Iterate until no more states are added

👉 해석
새 상태가 없을 때까지 반복

✔ 설명

👉 고정점 도달

🔷 마지막 문장
Sounds more complex than it is…

👉 해석
겉보기보다 복잡하지 않다

✔ 설명

👉 실제로는 반복 구조일 뿐

🔥 한 줄 핵심

👉
NFA의 상태 집합을 DFA 상태로 만들어서 모든 가능성을 한 번에 처리한다
