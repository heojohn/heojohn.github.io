---
title: "1. Basic Concepts"
excerpt: ""

categories:
  - Compiler
tags:
  - tag1
  - tag2

permalink: /Compiler/1/

toc: true
toc_sticky: true

date: 2026-04-07
last_modified_at: 2026-04-07



---

# COMP321 Compiler — Lexical Analysis Part 2
**Kyungpook National University | Hwisoo So | Spring 2026**

---

## 📋 1페이지 — 제목

### Lexical Analysis – Part 2
> **어휘 분석 – 2번째 파트**

컴파일러의 Lexical Analysis(스캐너 단계) 두 번째 강의.  
Part 1에서 기본 개념을 다뤘고, 지금부터는 **자동자(Automata) + 정규표현식 + DFA/NFA 변환**으로 들어간다.

- **Hwisoo So** → 소휘수 (교수 이름)
- **Kyungpook National University** → 경북대학교
- **COMP321 Compiler / Spring 2026** → 컴파일러 과목 / 2026년 봄학기

---

## 📋 2페이지 — Outline (강의 개요)

### The role of a scanner ✔
**스캐너의 역할**
- scanner = lexical analyzer
- 역할: 문자 스트림 → 토큰
- 이미 이전 시간에 다룸 (✔ 표시)

### Scanner concepts ✔
**스캐너 개념**

#### Tokens, Lexemes, Patterns
- **Token**: 타입 (ex: IDENTIFIER, NUMBER)
- **Lexeme**: 실제 문자열 (ex: "abc", "123")
- **Pattern**: 정규식으로 정의된 규칙

### Regular Expression & Automata (to be continued…)
**정규표현식과 오토마타 (계속 진행 중)**  
지금부터 핵심 파트 시작: 정규표현식 → NFA → DFA → 최소화

| 항목 | 상태 |
|------|------|
| Definitions of REs, DFAs and NFAs | ✔ 완료 |
| REs → NFA (Thompson Construction) | ✔ 완료 |
| NFA → DFA (Subset Construction) | ← 이번 핵심 |
| DFA → minimal-state DFA | 다음 주제 |
| Scanner generators (lex/flex) | 이후 |

### Today's agenda
- **NFA → DFA**
- **DFA 최소화**

이 두 개가 오늘의 핵심이다.

---

## 📋 3페이지 — Subset Construction (NFA→DFA 핵심 개념)

### Subset Construction (NFA→DFA)
> **부분집합 구성법 (NFA를 DFA로 변환)**

#### 문제: NFA의 비결정성
> "Instead of guessing in state s1 on symbol a"  
> **상태 s1에서 입력 a에 대해 추측하는 대신**

NFA는 갈림길이 있다 (비결정적):
- a 읽으면: s1 → s1 또는 s1 → s2
- 둘 중 하나를 "guess" 해야 함 → 문제

#### 해결: 두 전이를 동시에 따라간다
> "we can follow both transitions in parallel"  
> **두 전이를 동시에 따라갈 수 있다**

- 하나만 선택 ❌
- 둘 다 동시에 추적 ✅

#### 가상 상태 도입
> "We introduce a virtual state"  
> **우리는 "가상 상태"를 도입한다**

DFA에서의 상태 = NFA 상태들의 **집합**  
예: `{s1, s2}` → 이게 하나의 DFA 상태가 됨

#### 질문과 답
> "if we are in {s1, s2}, where can we go on b?"  
> **{s1, s2} 상태에서 b를 읽으면 어디로 가는가?**

각 상태에서 갈 수 있는 곳을 합친다:
- s1 → s1
- s2 → s3
- **결과: {s1, s3}**

#### 그림 설명 (하단)
- NFA에서 s1에서 a로 갈 때 두 갈래 존재
- 예시 1 (성공): "abb" → s0 → s1 → s2 → s3 → s4 (accept)
- 예시 2 (실패): s0 → s1 → s1 → s1 → s1 (fail)
- **NFA는 "운빨"** → 잘못 고르면 틀림
- **해결: 모든 경우를 동시에 추적 → DFA**

---

## 📋 4페이지 — DFA 구성 결과

### A "virtual state" is a subset
> **가상 상태는 상태 집합의 부분집합이다**

S = {S0, S1, S2, S3, S4}  
DFA 상태 예: {S0, S1}, {S1, S2}, ...

#### 표: Table encoding DFA (핵심)

| 상태 | a 입력 | b 입력 |
|------|--------|--------|
| {s0,s1} | {s1,s2} | {s1} |
| ... | ... | ... |

→ DFA transition table

#### 오른쪽 그림 (DFA 그래프)
- 상태: {s0,s1}, {s1,s2}, {s1,s3}, ...
- NFA → DFA 변환 완료 상태

---

## 📋 5페이지 — 알고리즘: NFA→DFA

### Algorithm: NFA→DFA
> **NFA를 DFA로 변환하는 알고리즘**

> "We need to build a simulation of the NFA"  
> **NFA를 시뮬레이션해야 한다**

DFA = NFA를 동시에 추적하는 시뮬레이터

#### 핵심 함수 두 가지

| 함수 | 의미 |
|------|------|
| `Move(si, a)` | 상태 집합 si에서 a로 갈 수 있는 상태 집합 |
| `ε-closure(si)` | ε 전이로 갈 수 있는 모든 상태 (공짜 이동) |

#### 시작 상태
- S0 = ε-closure({s0})
- 시작부터 ε로 확장

#### 반복 과정
```
각 입력 α에 대해:
  Move → ε-closure → 반복
새 상태 생성 → 계속 추가 → 더 이상 없으면 끝
```

> "Iterate until no more states are added"  
> **더 이상 상태가 추가되지 않을 때까지 반복** → **fixed-point**

> "Sounds more complex than it is…"  
> **보기보다 그렇게 복잡하지 않다** — 실제로는 집합 계산 반복일 뿐

---

## 📋 6페이지 — Subset Construction 알고리즘 상세

### 알고리즘 전체 코드

```
Dstates ← { }
add ε-closure(s0) as an unmarked state to Dstates

while ( there is an unmarked state T in Dstates )
    mark T
    for each α ∈ ∑
        U ← ε-closure(Move(T, α))
        if ( U ∉ Dstates ) then add U
        δ[T, α] ← U
```

#### 각 줄 해석

| 코드 | 해석 |
|------|------|
| `Dstates ← { }` | DFA 상태 집합을 빈 집합으로 초기화 |
| ε-closure(s0) 추가 | 시작 상태 생성, 아직 처리 안 했으니 "unmarked" |
| `while (unmarked T)` | 아직 처리 안 된 상태 T가 있으면 반복 |
| `mark T` | T를 처리 완료로 표시 |
| `for each α ∈ ∑` | 모든 입력 문자에 대해 반복 |
| `U ← ε-closure(Move(T,α))` | 핵심 계산: Move → ε-closure |
| `if U ∉ Dstates` | 새 상태면 추가 |
| `δ[T, α] ← U` | DFA 전이 테이블 작성 |

#### 종료 이유

1. **Dstates contains no duplicates** — 중복 상태 없음
2. **2^|S| is finite** — NFA 상태 n개면 DFA 최대 2ⁿ개 (유한)
3. **monotone** — 상태는 추가만 되고 삭제 안 됨

> **결론: 루프는 반드시 종료됨**

#### 중요 규칙
> "Any DFA state containing a final state becomes final"  
> **NFA의 final state를 포함하는 DFA 상태는 final이다**  
> 예: {s1, s4} → s4가 final이면 → 이 상태도 final

---

## 📋 7페이지 — Fixed-point 개념

### Example of a fixed-point computation
> **고정점 계산의 예**

| 개념 | 설명 |
|------|------|
| Monotone construction | 상태가 계속 추가됨 (절대 줄지 않음) |
| Halts when it stops adding | 더 이상 추가 없으면 종료 |
| Proofs of halting & correctness are similar | 종료성과 정당성 증명이 비슷하다 |
| These computations arise in many contexts | 컴파일러 전반에서 이런 계산이 등장한다 |

> **이 알고리즘 = fixed-point algorithm**  
> 계속 반복 → 더 이상 변화 없음 → 종료

---

## 📋 8페이지 — 예제: NFA→DFA (a(b|c)*)

### 정규식: a(b|c)*
> **a 다음에 b 또는 c가 0번 이상 반복**

#### Transition Table

| 상태 | a | b | c |
|------|---|---|---|
| s0 | {q1,q2,q3,q4,q6,q9} | none | none |
| s1 | - | {q5,q8,q9,q3,q4,q6} | {q7,q8,q9,q3,q4,q6} |

→ DFA transition 계산 과정 (subset construction 실제 적용)

#### 그림 설명 (왼쪽 NFA)
- ε-transition 많음, branching 구조
- 복잡한 NFA → DFA로 단순화하는 과정

---

## 📋 9페이지 — 완성된 DFA: a(b|c)*

### The DFA for a(b|c)*

> "Ends up smaller than the NFA"  
> **이 경우 DFA가 NFA보다 더 작다**  
> (일반적으로는 DFA가 더 커지는데, 이 예시는 특이하게 더 작아짐)

> "All transitions are deterministic"  
> **모든 전이는 결정적이다** — 항상 하나의 경로, 선택 없음

> "Use the same code skeleton as before"  
> **이전 코드 구조 그대로 사용**

#### Transition Table

| 상태 | a | b | c |
|------|---|---|---|
| S0 | S1 | - | - |
| S1 | - | S2 | S3 |

#### 그림 설명
- S0 → a → S1
- S1 → b/c 반복 (루프)

> "But remember our goal"  
> **하지만 우리의 목표를 기억하라**  
> DFA 만드는 게 끝이 아님 → **최소화가 최종 목표**

---

## 📋 10페이지 — 정리 (Outline 업데이트)

### 전체 흐름 정리

| 단계 | 상태 |
|------|------|
| RE → NFA | ✔ 완료 |
| NFA → DFA | ✔ 방금 배운 내용 |
| DFA → minimal-state DFA | ← **다음 핵심 주제** |
| Scanner generators | 이후 |

```
정규표현식 → NFA → DFA → 최소 DFA
```

---

## 📋 11페이지 — DFA Minimization 개념 핵심

### DFA Minimization Overview
> **DFA 최소화 개요**

### The Big Picture
> "Discover distinguishable states"  
> **구별 가능한 상태들을 찾아라**

#### distinguishable 정의
> "Two states p and q are distinguishable by input string w iff..."  
> **두 상태 p, q는 문자열 w에 의해 구별된다**  
> ↔ p에서 시작하면 w를 accept하지만 q에서는 reject인 경우

∃ w : p → accept, q → reject → **구별 가능**

> "Two states p and q are distinguishable if..."  
> **어떤 문자열 하나라도 존재하면 구별 가능**

#### indistinguishable 정의
모든 문자열에 대해 같은 결과 → **완전히 동일한 behavior**

> "States that cannot be distinguished can be represented by a single state"  
> **구별할 수 없는 상태들은 하나로 합칠 수 있다** → minimization 핵심

#### 그림 설명 (오른쪽)
- s2, s3 비교 → s2 ≡ s3 (구별 불가능) → 하나로 합침: **s2s3**

---

## 📋 12페이지 — Partition 개념

### 상태 집합 분할

> "The set of states is divided into subsets"  
> **상태 집합을 여러 부분집합으로 나눈다**

> "S is partitioned into P"  
> **S를 P라는 분할로 나눈다**

> "Each state s ∈ S is in exactly one set"  
> **각 상태는 정확히 하나의 그룹에만 속한다** — 중복 없음

> "States in the same set have not been distinguished yet"  
> **같은 그룹에 있는 상태는 아직 구별되지 않은 상태**

> "States from different sets are distinguishable"  
> **다른 그룹이면 이미 구별됨**

#### 초기 분할

> "Initially the partition P consists of 2 sets"  
> **처음에는 2개 그룹으로 시작**

> "accepting states F / non-accepting states S-F"  
> **accept 상태 / non-accept 상태**

```
P0 = { F , S-F }
```

> "distinguishable by ε"  
> **ε(빈 문자열)로도 구별됨** — accept vs non-accept는 기본적으로 다름

#### 반복 과정

> "algorithm repeatedly picks a set"  
> **알고리즘은 계속 그룹을 선택해서**

> "tries to distinguish"  
> **구별을 시도한다**

> "split pi along α"  
> **입력 α에 따라 그룹을 쪼갠다**

---

## 📋 13페이지 — Split 개념

### Splitting of a State Set along Symbol α
> **입력 α에 따른 상태 집합 분할**

> "repeatedly picks a set"  
> **계속 집합을 선택하고**

> "tries to distinguish between states"  
> **그 안의 상태들을 구별하려고 한다**

> "Eventually no more set can be split"  
> **더 이상 쪼갤 수 없으면 종료**

#### 두 가지 경우 (그림 설명)

| 경우 | 설명 |
|------|------|
| α does not split pi | α로 구별 안 됨 → 상태들이 동일하게 행동 → 그대로 유지 |
| α splits pi into {sa} and {sb, sc} | α로 인해 집합이 둘로 나뉨 → 일부가 다른 곳으로 감 → 구별됨 |

> **핵심: 같은 그룹 → 입력 넣어서 다르면 쪼갠다**

---

## 📋 14페이지 — Minimization 알고리즘

### DFA 최소화 알고리즘

```
P ← { F, S-F }

while ( P is still changing )
    T ← { }
    for each set p ∈ P
        T ← T ∪ Split(p)
    P ← T

Split(p):
    if α splits p into p1 and p2
        return {p1, p2}
    return p
```

#### 각 줄 해석

| 코드 | 해석 |
|------|------|
| `P ← { F, S-F }` | 초기 partition 설정 |
| `while (P is still changing)` | partition이 변하는 동안 반복 (핵심 루프) |
| `T ← { }` | 새 partition 저장용 초기화 |
| `T ← T ∪ Split(p)` | p를 쪼개서 T에 넣음 |
| `P ← T` | 새 partition으로 갱신 |
| `if α splits p into p1, p2` | α로 쪼개지면 두 집합 반환 |
| `return p` | 안 쪼개지면 그대로 반환 |

#### 그림: 예제 DFA → (a|b)*abb

초기 partition:
```
P0 = { {s4}, {s0,s1,s2,s3} }
- accept:     {s4}
- non-accept: {s0,s1,s2,s3}
```

---

## 📋 15페이지 — 알고리즘 시작 상태

### 현재 상태

```
P0 = { {s4}, {s0,s1,s2,s3} }
T = {}
```

#### 그림 설명
- 아직 아무것도 분할 안 한 초기 상태
- 처리 순서:
  1. p = {s4}
  2. p = {s0,s1,s2,s3}

---

## 📋 16페이지 — 첫 번째 집합 처리 시작

### 현재 상태

```
P0 = { {s4}, {s0,s1,s2,s3} }
T = { }
p = {s4}
∑ = {a, b}
```

> **지금 하는 것: p = {s4}를 쪼갤 수 있는지 확인**

#### 그림 설명
- DFA 구조 그대로 유지
- s4는 accept 상태
- 단일 상태 집합

---

## 📋 17페이지 — Split 함수 설명

### Invoke Split(p) function
> **Split(p) 함수 실행**

> "Determines whether p can be split"  
> **p를 나눌 수 있는지 판단**

> "If states can be distinguishable by α"  
> **입력 α로 구별 가능하면 분할**

핵심 판단 기준:
- 같은 집합 안에서
- 어떤 입력 넣었을 때
- 다른 집합으로 가면 → 쪼갠다

> "If X and Y are two states in a DFA, we can combine them when they are not distinguishable"  
> **두 상태가 구별되지 않으면 하나로 합칠 수 있다** → minimization의 목적

---

## 📋 18페이지 — α = a 검사

### α = a
> **입력 a로 검사**

> "Does a split p = {s4}?"  
> **a로 {s4}를 쪼갤 수 있는가?**

현재 p = {s4} → **상태가 하나뿐임**

> **결론: 절대 못 쪼갬**

쪼개려면 최소 2개 상태 필요

---

## 📋 19페이지 — α = a 결과

### 결론

> "Are there any two subsets distinguishable?"  
> **구별 가능한 두 상태가 있는가?**

> "Nope"  
> **없다**

> "(we cannot split a set which has a single element…)"  
> **원소 하나짜리 집합은 쪼갤 수 없다**

> ⭐ **시험 포인트: |p| = 1 → split 불가능**

---

## 📋 20페이지 — α = b 검사

### α = b
> **입력 b로 검사**

> "Does b split p = {s4}?"  
> **b로 쪼갤 수 있는가?**

> "Nope"  
> **불가능**

이유 동일:
- p = {s4}
- 원소 1개
- 무조건 유지

### 결과
```
Split({s4}) = {s4}
T = { {s4} }
```

---

## 📋 21페이지 — 다음 집합 처리 준비

### 현재 상태

```
P0 = { {s4}, {s0,s1,s2,s3} }
T = { {s4} }
p = {s0,s1,s2,s3}
```

> **s4는 이미 처리 완료, 이제 큰 집합 처리 시작**

∑ = {a, b}

> **이 집합에서 split이 실제로 발생한다**

---

## 📋 22페이지 — Split 준비 상태

### 현재 T

```
T = { } ∪ Split({s4}) = { {s4} }
```

> **T에 {s4} 추가 완료**

### 이제 해야 할 것
```
Split({s0,s1,s2,s3})
```

> **지금부터가 진짜 minimization 핵심**

---

## 📋 23페이지 — 집합 처리 시작

### 현재 상태

```
T = { {s4} }
p = {s0,s1,s2,s3}
∑ = {a, b}
```

> **입력 a, b로 각각 검사 시작**

---

## 📋 24페이지 — α 선택 준비

### α = ?
> **어떤 입력으로 검사할지 선택**

순서대로 진행:
1. α = a 검사
2. α = b 검사

---

## 📋 25페이지 — α = a 검사 시작

### α = a
> **입력 a로 검사**

#### 각 상태의 a 이동

| 상태 | a 이동 |
|------|--------|
| s0 | s1 |
| s1 | s1 |
| s2 | s1 |
| s3 | s1 |

#### 결과 분석
> **모든 상태 → s1 → 동일 behavior**

> **결론: α = a로는 split 불가능**

이유:
- 같은 partition 내부로만 이동
- 구별 안 됨

---

## 📋 26페이지 — α = a 최종 확인

### α = a

#### 각 상태의 a 이동 (재확인)

| 상태 | a 이동 |
|------|--------|
| s0 | s1 |
| s1 | s1 |
| s2 | s1 |
| s3 | s1 |

> "Split on a: None"  
> **a로는 분할 없음**

이유:
- 같은 partition 내부로만 이동
- 구별 불가
- split 없음

---

## 📋 27페이지 — α = a 결론 확정

### None…
> **분할 없음**

> **같은 집합 안에서 같은 행동 → 유지**

다음 단계: α = b 검사로 이동

---

## 📋 28페이지 — 🔥 α = b에서 split 발생 (시험 핵심)

### α = b
> **입력 b로 검사**

#### 각 상태의 b 이동

| 상태 | b 이동 | 속하는 partition |
|------|--------|-----------------|
| s0 | s2 | {s0,s1,s2,s3} |
| s1 | s3 | {s0,s1,s2,s3} |
| s2 | s2 | {s0,s1,s2,s3} |
| s3 | s4 | **{s4}** ← 다른 그룹! |

#### 결정적 차이
- **s3 → {s4} (accept group)**
- **나머지 → non-accept group**

> **→ split 발생!**

---

## 📋 29페이지 — Split 결과 반환

### Return '{{s0,s1,s2}, {s3}}'
> **집합을 두 개로 나눠서 반환**

#### 그림 의미
기존: `{s0,s1,s2,s3}`  
→ 이제: `{s0,s1,s2}` / `{s3}`

이게 minimization의 핵심 결과

---

## 📋 30페이지 — Partition 업데이트

### Split 결과

```
Split(p) = '{{s0,s1,s2},{s3}}'
```

### T 업데이트

```
기존: T = { {s4} }
업데이트 후: T = { {s4}, {s0,s1,s2}, {s3} }
```

### Partition 변화

```
P0 = { {s4}, {s0,s1,s2,s3} }
       ↓ (split 발생 후)
P1 = { {s4}, {s0,s1,s2}, {s3} }
```

---

## 📋 31페이지 — Partition 업데이트 완료 상태

### 현재 상태

```
P = { {s4}, {s0,s1,s2}, {s3} }
T = { {s4}, {s0,s1,s2}, {s3} }
```

1차 split 완료 → partition 3개로 증가

이제부터: 각 집합을 다시 검사 시작

---

## 📋 32페이지 — 다음 iteration 시작

### P1

```
P1 = { {s4}, {s0,s1,s2}, {s3} }
```

> **while loop 계속**  
> partition이 변했기 때문에 반복 조건 만족 → 계속

→ fixed-point 아직 아님

---

## 📋 33페이지 — 다음 처리 준비

### 다음 집합 순회 준비

순서:
1. {s4}
2. {s0,s1,s2}
3. {s3}

---

## 📋 34페이지 — 새 iteration 초기화

### T = { }
> **새 partition 초기화**

이전 P를 다시 쪼개기 시작

---

## 📋 35페이지 — 🔥 2차 split 발생

### 현재 상태

```
P1 = { {s0,s1,s2}, {s3}, {s4} }
p = {s0,s1,s2}
```

### α = b 검사

각 상태의 b 이동:

| 상태 | b 이동 | 속하는 partition |
|------|--------|-----------------|
| s0 | s2 | {s0,s1,s2} |
| s1 | s3 | **{s3}** ← 다른 그룹! |
| s2 | s2 | {s0,s1,s2} |

#### 결정적 차이
- **s1 → {s3}**
- **s0, s2 → {s0,s1,s2}**

> **→ split 발생!**

#### 결과

```
{s0,s2} / {s1}
```

### Partition 업데이트

```
P1 = { {s4}, {s0,s1,s2}, {s3} }
       ↓ (2차 split 발생)
P2 = { {s4}, {s0,s2}, {s1}, {s3} }
```

---

## 📋 36페이지 — Partition 확정 상태

### 현재 상태

```
이전: T = { {s4} }
2차 split 후: T = { {s4}, {s0,s2}, {s1}, {s3} }
```

이제 partition 4개:
- 각 상태 거의 다 분리됨

---

## 📋 37페이지 — P2 상태 유지

### P2

```
P2 = { {s0,s2}, {s1}, {s3}, {s4} }
```

### T = 동일
> **더 이상 변화 없음**

중요한 신호: **split 더 이상 없음**

---

## 📋 38페이지 — iteration 확인

### 1st iter / 2nd / 3rd / 4th…

여러 번 반복해서 확인했지만:
- partition 변화 없음

> **fixed-point 도달**

---

## 📋 39페이지 — 최종 확인

### P2 유지

```
P2 = { {s0,s2}, {s1}, {s3}, {s4} }
```

> **더 이상 split 불가능**

모든 상태가 distinguishable 상태로 분리 완료

---

## 📋 40페이지 — 알고리즘 종료

### While loop comes to a halt
> **while 루프 종료**

> "P does not be changed"  
> **partition이 더 이상 변하지 않는다** → 종료 조건 만족

### 최종 상태

```
P2 = { {s0,s2}, {s1}, {s3}, {s4} }
```

s0와 s2는 완전히 동일한 behavior:
- 어떤 입력 넣어도 동일하게 행동
- → 합쳐도 문제 없음

---

## 📋 41페이지 — 최소 DFA 결과

### 최종 Partition

```
P = { {s0,s2}, {s1}, {s3}, {s4} }
```

각 partition이 하나의 상태가 된다:
- {s0,s2} → 하나의 상태
- {s1} → 하나의 상태
- {s3} → 하나의 상태
- {s4} → 하나의 상태

#### 그림 설명
- 기존 DFA → 최소 DFA 변환
- s0, s2 → 합쳐짐
- 나머지는 그대로

> **같은 behavior → 하나로 합침**

---

## 📋 42페이지 — 왜 이 알고리즘은 종료되는가?

### Why does this terminate?

> "p ∈ 2^S"  
> **partition은 상태 집합의 부분집합** → 가능한 partition 수는 유한

> "Start with 2 subsets"  
> **처음엔 F / S-F 2개로 시작**

> "While loop takes Pi → Pi+1"  
> **반복하면서 partition이 점점 쪼개짐**

> "Pi+1 is closer to |S| sets"  
> **점점 상태 개수만큼 쪼개짐**

> "Maximum of |S| splits"  
> **최대 |S|번만 split 가능**

> "Partitions are never combined"  
> **합쳐지는 일은 없음 — 오직 split만 존재**

> "algorithm eventually terminates"  
> **결국 종료된다**

> **핵심: 유한 + split만 있음 → 반드시 종료**

---

## 📋 43페이지 — 왜 이 알고리즘이 올바른가?

### Why does this work?

> "maintains 2 invariants"  
> **두 가지 불변 조건 유지**

| 불변 조건 | 의미 |
|-----------|------|
| same set → not distinguished | 같은 집합에 있으면 아직 구별 안 됨 |
| different sets → distinguishable | 다른 집합이면 구별 가능 |

> **핵심 보장: 같은 집합 = 같은 상태로 합쳐도 안전**

> "final partition"  
> **최종 partition은 구별 가능한 상태 집합**

> "Proof sketch"  
> **증명은 교재 참고**

partition 구조 자체가 정답을 보장한다.

---

## 📋 44페이지 — 최종 결과 + 직관

### DFA Minimization Example

> "Applying the minimization algorithm"  
> **알고리즘 적용 결과**

> "produce minimal DFA"  
> **최소 DFA 생성**

#### 그림 설명 (두 DFA 비교)
- 왼쪽: 복잡한 DFA
- 오른쪽: 최소 DFA

> "human would design a simpler automaton"  
> **사람은 더 단순한 오토마타를 만든다**  
> 알고리즘이 결국 사람이 직관적으로 만든 것과 동일한 결과를 생성한다.

> "every RE language can be recognized by a minimal DFA"  
> **모든 정규표현식은 최소 DFA로 표현 가능**

> "unique up to state names"  
> **상태 이름만 다르고 구조는 유일**

> ⭐ **매우 중요: 최소 DFA는 "유일하다"**

---

## 📋 45페이지 — 알고리즘 형태 재정리

### 알고리즘 재정리

```
P ← { F, S-F }

while (P is changing)
    Split(p)

∑ = {a, b, c, ...}
```

전체 알고리즘 구조를 다시 한번 확인하는 슬라이드.

---

## 📋 46페이지 — 전체 과정 요약 표

### Partition 변화 과정

| Partition | Split on a | Split on b | 결과 |
|-----------|-----------|-----------|------|
| P0: {s0,s1,s2,s3} | no split | split 발생 | → {s0,s1,s2}, {s3} |
| P1: {s0,s1,s2} | no split | split 발생 | → {s0,s2}, {s1} |
| P2: {s0,s2}, {s1}, {s3}, {s4} | no split | no split | → 종료 |

#### 그림 설명
- before DFA / after (최소) DFA 비교 시각화

---

## 📋 47페이지 — 최종 정리 (Outline 완료)

### 전체 흐름 완료

| 단계 | 상태 |
|------|------|
| RE → NFA | ✔ 완료 |
| NFA → DFA | ✔ 완료 |
| DFA → minimal DFA | ✔ 완료 |
| Scanner generators | → 다음 주제로 넘어감 |

---

## 🔥 전체 강의 핵심 요약 (시험용)

### 전체 흐름
```
정규표현식 → NFA → DFA → 최소 DFA
```

### 각 단계 요약

| 단계 | 방법 | 핵심 개념 |
|------|------|----------|
| RE → NFA | Thompson Construction | ε-transition |
| NFA → DFA | Subset Construction | ε-closure, Move |
| DFA → min DFA | Partition Refinement | distinguishable |

### Subset Construction 핵심
- `Move(T, α)`: 상태 집합 T에서 α로 이동하는 상태들
- `ε-closure(T)`: ε 전이로 도달 가능한 모든 상태들
- 반복: 더 이상 상태 추가 없을 때까지 (fixed-point)

### Minimization 과정 단계별 요약

```
Step 1: P0 = { {s4}, {s0,s1,s2,s3} }
Step 2: b로 split → P1 = { {s4}, {s0,s1,s2}, {s3} }
Step 3: b로 또 split → P2 = { {s4}, {s0,s2}, {s1}, {s3} }
Step 4: 더 이상 split 없음 → 종료
```

### ⭐ 가장 중요한 문장 (시험 한 줄 요약)
> **"상태가 아니라 상태의 행동(transition)을 비교해서 나눈다"**

### ⭐ split 절대 불가 조건
> **집합 크기 = 1 이면 split 불가능**

### ⭐ 최소 DFA의 유일성
> **최소 DFA는 구조적으로 유일하다 (unique up to state names)**
