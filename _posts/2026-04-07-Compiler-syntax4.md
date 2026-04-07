---
title: "Syntax Analysis Part 4"
excerpt: ""

categories:
  - Compiler
tags:
  - tag1
  - tag2

permalink: /Compiler/syntax4/

toc: true
toc_sticky: true

date: 2026-04-07
last_modified_at: 2026-04-07



---


# COMP321 Compiler — Syntax Analysis Part 4
**Kyungpook National University | Hwisoo So | Spring 2026**

---


## 📋 1페이지

### 🔷 문장

> Syntax Analysis – 4

👉 **해석**
구문 분석 – 4

✔ **설명**
컴파일러에서 Syntax Analysis(구문 분석) 파트의 4번째 강의라는 뜻이다.
즉, 이제 **파싱(Parsing)**의 핵심 이론으로 들어가는 단계다.

### 🔷 문장

> Hwisoo So
> Kyungpook National University

👉 **해석**
소휘수 교수
경북대학교

✔ **설명**
강의 담당 교수와 소속 학교 정보

### 🔷 문장

> COMP321 Compiler
> Spring 2026

👉 **해석**
컴파일러 과목 (COMP321)
2026년 봄학기

✔ **설명**
과목 코드 + 학기 정보

✔ **그림 설명**
- 가운데 크게 Syntax Analysis – 4
- 아래에 학교 로고
- 전형적인 강의 표지 슬라이드

👉 의미 없음 (내용 없음), 단순 타이틀 페이지

---

## 📋 2페이지

### 🔷 제목

> Outlook

👉 **해석**
전체 개요 / 앞으로 다룰 내용

### 🔷 문장

> Syntax and Semantics of Programming Languages ✓

👉 **해석**
프로그래밍 언어의 구문과 의미 ✓

✔ **설명**
이미 배운 내용 (체크 표시 있음)
- Syntax → 문법 구조
- Semantics → 의미

### 🔷 문장

> Specifying the Syntax of a programming language: ✓

👉 **해석**
프로그래밍 언어의 구문 정의 방법 ✓

✔ **설명**
문법을 정의하는 방법을 배웠다는 뜻

### 🔷 문장

> CFGs, BNF and EBNF ✓

👉 **해석**
CFG, BNF, EBNF ✓

✔ **설명**
- CFG: Context-Free Grammar
- BNF/EBNF: 문법 표기 방식

### 🔷 문장

> Grammar transformations ✓

👉 **해석**
문법 변환 ✓

✔ **설명**
- left recursion 제거
- left factoring

### 🔷 문장

> Parsing

👉 **해석**
파싱

✔ **설명**
👉 이제부터 핵심 파트 시작

### 🔷 문장

> Top-down parsing (LL) ✓

👉 **해석**
탑다운 파싱 (LL) ✓

✔ **설명**
이미 기본 개념은 배움

### 🔷 문장

> Recursive descent (LL) parser construction

👉 **해석**
재귀 하강 파서 구성

✔ **설명**
👉 직접 코드로 파서 만드는 단계

### 🔷 문장

> LL Grammars

👉 **해석**
LL 문법

✔ **설명**
👉 오늘 핵심 주제

### 🔷 문장

> AST Construction

👉 **해석**
AST 생성

✔ **설명**
파싱 결과를 트리 구조로 만드는 단계

### 🔷 문장

> Parse trees vs. ASTs

👉 **해석**
파스 트리 vs AST

✔ **설명**
둘의 차이 비교 예정

### 🔷 문장

> Chomsky's Hierarchy

👉 **해석**
촘스키 계층

✔ **설명**
문법의 분류 체계

✔ **전체 요약**
- 👉 지금까지: 문법 정의
- 👉 이제부터: 파싱 + LL(1) + FIRST/FOLLOW

---

## 📋 3페이지

### 🔷 제목

> LL(1) Grammars

👉 **해석**
LL(1) 문법

### 🔷 문장

> The presented algorithm to convert EBNF into a parser does not work for all possible grammars.

👉 **해석**
EBNF를 파서로 변환하는 알고리즘은 모든 문법에 대해 동작하지 않는다.

✔ **설명**
👉 모든 CFG가 파싱 가능한 건 아니다

### 🔷 문장

> It only works for so called "LL(1)" grammars

👉 **해석**
이 알고리즘은 LL(1) 문법에서만 동작한다.

✔ **설명**
👉 LL(1) = 우리가 사용할 수 있는 "좋은 문법"

### 🔷 문장

> LL(1) is an acronym for

👉 **해석**
LL(1)은 다음을 의미한다

### 🔷 문장

> Left-to-right parsing of the input stream

👉 **해석**
입력을 왼쪽에서 오른쪽으로 읽는다

### 🔷 문장

> Leftmost derivation

👉 **해석**
가장 왼쪽부터 유도한다

### 🔷 문장

> 1 token look-ahead

👉 **해석**
1개의 토큰만 미리 본다

### 🔷 문장

> What grammars are LL(1)?

👉 **해석**
어떤 문법이 LL(1)인가?

### 🔷 문장

> A grammar containing left-recursion is not LL(1)

👉 **해석**
left recursion이 있으면 LL(1)이 아니다

### 🔷 문장

> A grammar containing common prefixes is not LL(1)

👉 **해석**
공통 prefix가 있으면 LL(1)이 아니다

### 🔷 문장

> An ambiguous grammar is not LL(1)

👉 **해석**
모호한 문법도 LL(1)이 아니다

✔ **핵심 요약**

LL(1) 조건:
- left recursion 없음
- 공통 prefix 없음
- ambiguity 없음

---

## 📋 4페이지 — Notation and Terminology

### 🔷 제목

> Notation and Terminology

👉 **해석**
표기법과 용어

### 🔷 문장

> Given a context-free grammar G

👉 **해석**
CFG G가 주어졌을 때

### 🔷 문장

> Vt is the set of terminal symbols

👉 **해석**
Vt는 terminal 집합

✔ **설명**
토큰 (ID, +, etc)

### 🔷 문장

> Vn is the set of nonterminals

👉 **해석**
Vn은 비단말 집합

✔ **설명**
Expr, Term 같은 것

### 🔷 문장

> P is a finite set of productions

👉 **해석**
P는 생성 규칙 집합

### 🔷 문장

> V = Vt ∪ Vn

👉 **해석**
전체 기호 집합

### 🔷 문장

> a, b, c ∈ Vt

👉 **해석**
a,b,c는 terminal

### 🔷 문장

> A, B, C ∈ Vn

👉 **해석**
A,B,C는 nonterminal

### 🔷 문장

> α, β ∈ V*

👉 **해석**
α, β는 문자열

### 🔷 문장

> αAβ → αγβ

👉 **해석**
A를 γ로 치환

✔ **설명**
👉 derivation 정의

### 🔷 문장

> → , →+*

👉 **해석**
여러 단계 / 최소 1단계 유도

✔ **핵심**
👉 CFG 기본 정의 복습

---

## 📋 5페이지 — Predictive Parsing

### 🔷 제목

> Predictive Parsing (aka Recursive Descent Parsing)

👉 **해석**
예측 파싱 (재귀 하강 파싱)

### 🔷 문장

> Basic idea

👉 **해석**
기본 아이디어

### 🔷 문장

> For any two productions A → α | β ...

👉 **해석**
A → α | β가 있을 때

### 🔷 문장

> distinct way of choosing

👉 **해석**
명확하게 하나를 선택해야 한다

✔ **설명**
👉 파서가 헷갈리면 안됨

### 🔷 문장

> define FIRST(α)

👉 **해석**
FIRST(α)를 정의한다

### 🔷 문장

> tokens that appear first

👉 **해석**
맨 앞에 올 수 있는 토큰

### 🔷 문장

> FIRST(α) ∩ FIRST(β) = ∅

👉 **해석**
두 FIRST 집합은 겹치면 안 된다

✔ **핵심**
👉 이게 LL(1) 핵심 조건

### 🔷 문장

> predict with one lookahead

👉 **해석**
1개 토큰만 보고 선택 가능

✔ **핵심 정리**
👉 LL(1)의 본질: "앞 토큰 하나로 규칙 선택 가능"

### 🔥 여기까지 핵심 요약

이 1~5페이지는:
👉 "LL(1) 파싱이 뭔지 + 왜 필요한지 + 조건" 설명

핵심 3개:
1. LL(1) = 1-token lookahead
2. FIRST 집합 중요
3. 겹치면 파싱 불가능

---

## 📋 6페이지

### 🔷 제목

> Left-Recursive Grammars are not LL(1)

👉 **해석**
왼쪽 재귀 문법은 LL(1)이 아니다

### 🔷 문장

```
Expr ::= Expr "+" INT
       | INT
```

👉 **해석**
Expr는 다음 두 가지로 생성된다:
- Expr + INT
- INT

✔ **설명**
👉 이 문법의 핵심 문제:
왼쪽에서 자기 자신으로 시작함 (Expr → Expr …)
→ 이게 바로 left recursion

### 🔷 문장

> What happens if we don't perform left-recursion elimination?

👉 **해석**
left recursion 제거를 하지 않으면 어떻게 될까?

### 🔷 코드

```python
def parseExpr(self):
    match self.currentToken.kind:
        case Token.INT:
            self.parseExpr()
            self.accept(Token.PLUS)
            self.accept(Token.INT)
        case Token.INT:
            self.accept(Token.INT)
        case _: report syntax error
```

👉 **해석 + 설명**

현재 토큰이 INT면:
- parseExpr() 또 호출
- 읽고
- INT 읽음

👉 문제: case가 둘 다 Token.INT

### 🔷 문장

> Problem1: overlapping cases

👉 **해석**
문제1: case가 겹친다

### 🔷 문장

> FIRST ( Expr "+" INT ) = {INT}

👉 **해석**
Expr + INT의 FIRST는 {INT}

### 🔷 문장

> FIRST ( INT ) = {INT}

👉 **해석**
INT의 FIRST도 {INT}

✔ **설명**
👉 둘 다 시작이 INT → 구분 불가능 → LL(1) 조건 위반

### 🔷 문장

> Problem2: infinite recursion via parseExpr()

👉 **해석**
문제2: 무한 재귀 발생

✔ **설명 (진짜 중요)**

```
parseExpr → parseExpr → parseExpr → ...
```

👉 입력을 소비하기 전에 재귀 호출 → 끝없이 반복

### 🔥 핵심

left recursion 문제:
- FIRST 충돌
- 무한 재귀

---

## 📋 7페이지

### 🔷 제목

> Left-Recursive Grammars are not LL(1)

### 🔷 문장

```
Expr ::= INT
       | Expr "+" INT
```

👉 **해석**
순서를 바꿔도 여전히 left recursion

### 🔷 문장

> eliminate left-recursion

👉 **해석**
left recursion 제거

### 🔷 문장

```
Expr ::= INT ( "+" INT )*
```

👉 **해석**
Expr는:
- INT 다음에
- "+" INT가 0번 이상 반복

✔ **설명**
👉 핵심 변환:

```
Expr → Expr + INT   ❌
→ 반복 구조로 변경
```

👉 즉: 재귀 → 반복문으로 변환

### 🔷 일반식

```
N ::= X | N Y   →   N ::= X Y*
```

👉 **해석**
왼쪽 재귀는 반복으로 바꾼다

### 🔷 코드

```python
def parseExpr(self):
    self.accept(Token.INT)
    while self.currentToken.kind == Token.PLUS:
        self.accept(Token.PLUS)
        self.accept(Token.INT)
```

✔ **설명**
👉 동작:
- INT 하나 읽음
- "+" 있으면 계속 반복

👉 완전히 반복 기반 파싱

### 🔥 핵심

left recursion 제거 = 👉 재귀 → while loop

---

## 📋 8페이지

### 🔷 제목

> Grammars with Common Prefixes are not LL(1)

👉 **해석**
공통 prefix가 있는 문법은 LL(1)이 아니다

### 🔷 문장

```
Expr ::= Term "+" Expr
       | Term
```

👉 **해석**
두 규칙 모두 Term으로 시작

✔ **문제**
👉 둘 다 FIRST(Term)으로 시작

### 🔷 코드

```
case FIRST(Term):
    parseTerm()
    accept("+")
    parseExpr()

case FIRST(Term):
    parseTerm()
```

✔ **설명**
👉 둘 다 조건 동일 → 선택 불가능

### 🔷 문장

> Problem of overlapping cases in FIRST (TERM)

👉 **해석**
FIRST(Term)에서 겹침 문제 발생

### 🔷 문장

> Note: this does not lead to infinite recursion

👉 **해석**
이 경우는 무한 재귀는 발생하지 않는다

✔ **설명**
👉 이유:
- 중간에 "+"를 소비함
- → 입력이 줄어듦 → 무한루프 없음

### 🔥 핵심

공통 prefix 문제: 👉 어떤 규칙 선택할지 결정 불가능

---

## 📋 9페이지

### 🔷 제목

> perform left-factorization

👉 **해석**
left factoring 수행

### 🔷 변환

```
Expr ::= Term ( "+" Expr | ε )
```

👉 **해석**
Term 뒤에:
- Expr
- 또는 아무것도 없음

✔ **설명**
👉 공통 prefix 제거

```
Term + Expr
Term
→

Term ( + Expr | ε )
```

### 🔷 일반식

```
X Y | X Z  →  X (Y | Z)
```

### 🔷 코드

```python
def parseExpr(self):
    self.parseTerm()
    if self.currentToken.kind == Token.PLUS:
        self.accept(Token.PLUS)
        self.parseExpr()
```

✔ **설명**
👉 순서:
- Term 먼저 처리
- 있으면 추가 처리

👉 이제 분기 명확함

### 🔥 핵심

left factoring = 👉 공통 prefix를 밖으로 빼기

---

## 📋 10페이지

### 🔷 제목

> Intuition behind LL(1) Grammars

👉 **해석**
LL(1) 문법의 직관

### 🔷 문장

> parse X | Y

👉 **해석**
X 또는 Y 선택

### 🔷 코드

```
case FIRST(X): parse X
case FIRST(Y): parse Y
```

### 🔷 조건 1

> FIRST(X) and FIRST(Y) must be disjoint

👉 **해석**
FIRST(X)와 FIRST(Y)는 겹치면 안 된다

✔ **설명**
👉 겹치면 어떤 걸 선택할지 모름

### 🔷 문장

> parse X*

👉 **해석**
X 반복

### 🔷 코드

```
while token ∈ FIRST(X):
    parse X
```

### 🔷 조건 2

> FIRST(X) must be disjoint from FOLLOW(X)*

👉 **해석**
FIRST(X)와 FOLLOW(X*)도 겹치면 안 된다

✔ **설명 (중요)**
👉 언제 멈출지 결정해야 함
- 계속할지
- 끝낼지
→ 이 판단을 위해 필요

### 🔥 최종 핵심 정리

LL(1) 조건 2개:
1. FIRST끼리 안 겹침
2. FIRST vs FOLLOW도 안 겹침

### 🔥 6~10페이지 전체 핵심 요약

이 구간은 진짜 시험 핵심이다:

**1. LL(1) 깨지는 이유**
- left recursion
- common prefix

**2. 해결 방법**
- left recursion 제거 → 반복문
- left factoring → prefix 분리

**3. 핵심 조건**
- FIRST disjoint
- FIRST vs FOLLOW disjoint

---

## 📋 11페이지

### 🔷 제목

> Generality

👉 **해석**
일반성

### 🔷 문장

> Question:

👉 **해석**
질문

### 🔷 문장

> By left-factoring and elimination of left-recursion, can we transform any grammar such that it can be parsed with a single token lookahead?

👉 **해석**
left factoring과 left recursion 제거를 하면
모든 문법을 1-token lookahead로 파싱 가능한 형태로 바꿀 수 있을까?

### 🔷 문장

> Answer:

👉 **해석**
답

### 🔷 문장

> Given a context-free grammar that does not meet our conditions, it is undecidable whether an equivalent grammar exists that meets our conditions.

👉 **해석**
조건을 만족하지 않는 CFG가 주어졌을 때,
조건을 만족하는 동일한 문법이 존재하는지는 결정 불가능하다

✔ **설명**
👉 핵심:
- 모든 CFG를 LL(1)로 바꿀 수 있는 건 아님
- 심지어 가능한지조차 판단 불가능

👉 이건 이론적으로 매우 중요한 statement (undecidable)

### 🔷 수식

```
{ a^n 0 b^n } ∪ { a^n 1 b^2n }
```

👉 **해석**
두 언어의 합집합

✔ **설명**
👉 이 언어는:
- 앞에 a 많이 나오고
- 중간에 0 또는 1
- 뒤 구조가 달라짐

👉 문제:
- 초기에는 0인지 1인지 모름 → 많이 봐야 판단 가능
- → 1-token lookahead로 불가능

### 🔷 문장

> Must look past an arbitrary number of a's

👉 **해석**
a를 여러 개 넘어가야 판단 가능

### 🔷 문장

> However: most programming languages can be expressed with an LL(1) grammar

👉 **해석**
하지만 대부분의 프로그래밍 언어는 LL(1)으로 표현 가능하다

### 🔥 핵심

👉 이론적으로는 안 되는 경우 존재
👉 하지만 실전(언어 설계)은 대부분 LL(1) 가능

---

## 📋 12페이지

### 🔷 제목

> FIRST

👉 **해석**
FIRST 집합

### 🔷 문장

> For a string α, FIRST(α) is

👉 **해석**
문자열 α에 대해 FIRST(α)는

### 🔷 문장

> the set of terminal symbols that start sentences derived from α

👉 **해석**
α로부터 유도된 문자열의 시작에 올 수 있는 terminal 집합

### 🔷 수식

```
{ c ∈ Vt | α ⇒* cβ }
```

👉 **해석**
α로부터 유도했을 때 맨 앞에 올 수 있는 terminal c

### 🔷 문장

> If α ⇒ ε then ε ∈ FIRST(α)*

👉 **해석**
α가 ε로 유도될 수 있으면 ε도 포함

✔ **설명**
👉 FIRST는 결국: "이 문장이 시작할 수 있는 토큰들"

### 🔷 문장

> FIRST(α) contains the set of tokens valid in the initial position in α

👉 **해석**
FIRST는 α의 시작 위치에 올 수 있는 토큰 집합

### 🔷 알고리즘

**문장 1**

> If X ∈ Vt then FIRST(X) = {X}

👉 **해석**
X가 terminal이면 FIRST는 자기 자신

**문장 2**

> If X ::= ε then add ε

👉 **해석**
X가 ε이면 ε 추가

**문장 3**

> X ::= Y1 Y2 ... Yk

👉 **해석**
X가 여러 기호로 구성될 때

**(a)**

> Put FIRST(Y1) - {ε} in FIRST(X)

👉 **해석**
Y1의 FIRST에서 ε 제외하고 추가

**(b)**

👉 **해석**
앞에 애들이 ε이면 다음 것도 추가

✔ **설명**
- Y1, Y2 ... 가 ε 가능하면
- → Y2, Y3도 고려

**(c)**

> if all Yi derive ε → add ε

👉 **해석**
모두 ε 가능하면 ε 추가

### 🔷 문장

> Repeat until no more additions

👉 **해석**
더 이상 변화 없을 때까지 반복

### 🔥 핵심

FIRST 계산: 👉 왼쪽부터 보면서 확장

---

## 📋 13페이지

### 🔷 제목

> FIRST-Set Example 1

### 🔷 문장

```
T  ::= F T'
T' ::= "*" F T'
T' ::= ε
F  ::= "(" T ")"
F  ::= "ID"
```

### 🔷 결과

```
FIRST(F)  = { "(", "ID" }
```

👉 **해석**
F는 "(" 또는 ID로 시작

```
FIRST(T') = { "*", ε }
```

👉 **해석**
T'는 "*" 또는 ε

```
FIRST(T)  = { "(", "ID" }
```

👉 **해석**
T는 결국 F로 시작 → 동일

✔ **설명**
👉 T → F T'
→ 시작은 항상 F
→ 따라서 FIRST(T) = FIRST(F)

---

## 📋 14페이지

### 🔷 제목

> FIRST-Set Example 2

### 🔷 문장

```
T  ::= S F T'
T' ::= "*" S F T'
T' ::= ε
F  ::= "ID"
F  ::= "(" E ")"
S  ::= "-"
S  ::= ε
```

### 🔷 결과

```
FIRST(S)  = { "-", ε }
```

👉 **해석**
S는 "-" 또는 ε

```
FIRST(T') = { "*", ε }

FIRST(F)  = { "ID", "(" }
```

### 🔷 핵심 결과

```
FIRST(T) = { "-", "ID", "(" }
```

✔ **설명 (핵심)**
👉 T ::= S F T'
→ S가 ε 가능
→ 그래서 F도 고려됨

### 🔷 문장

> Because S → ε, FIRST(T) contains FIRST(F)

👉 **해석**
S가 ε이므로 F도 포함됨

### 🔥 핵심

👉 ε 있으면 다음 기호까지 본다

---

## 📋 15페이지

### 🔷 제목

> FOLLOW

👉 **해석**
FOLLOW 집합

### 🔷 문장

> For a non-terminal A, FOLLOW(A) is

👉 **해석**
비단말 A에 대해 FOLLOW(A)는

### 🔷 문장

> the set of terminals that can appear immediately to the right of A

👉 **해석**
A 바로 뒤에 올 수 있는 terminal 집합

✔ **설명**
👉 FOLLOW = "A 다음에 뭐 올 수 있냐"

### 🔷 문장

> Note: a terminal symbol has no FOLLOW set

👉 **해석**
terminal은 FOLLOW 없음

### 🔷 문장

> Put $ in FOLLOW(S)

👉 **해석**
시작기호 FOLLOW에는 $ 추가

### 🔷 알고리즘

> A ::= α B β

👉 **해석**
B 뒤에 β가 있음

**(a)**

> Put FIRST(β) - {ε} in FOLLOW(B)

👉 **해석**
β의 FIRST를 B의 FOLLOW에 추가

**(b)**

> if β = ε or ε ∈ FIRST(β)

👉 **해석**
β가 없거나 ε 가능하면

> put FOLLOW(A) in FOLLOW(B)

👉 **해석**
A의 FOLLOW를 B에 추가

### 🔷 문장

> Repeat until no more additions

👉 **해석**
변화 없을 때까지 반복

### 🔥 핵심

FOLLOW 계산:
👉 오른쪽 보고
👉 ε이면 부모 FOLLOW까지 전달

### 🔥 11~15 전체 핵심 요약

**FIRST**
- 시작 토큰 집합
- 왼쪽부터 계산
- ε 있으면 다음까지 봄

**FOLLOW**
- 뒤에 올 수 있는 토큰
- β 보고 결정
- ε이면 부모 FOLLOW 전달

**중요한 포인트**

| 개념 | 의미 |
|------|------|
| FIRST | 시작 토큰 |
| FOLLOW | 뒤에 올 토큰 |

---

## 📋 16페이지

### 🔷 제목

> FOLLOW Set Example 1

### 🔷 문장 (문법)

```
Sentence ::= Subject Verb "."
Subject  ::= "the" X Y
X        ::= "dog"
Y        ::= "owner" | ε
Verb     ::= "eats"
```

👉 **해석**
문장 구조:
- Sentence → Subject Verb "."
- Subject → "the" X Y
- X → "dog"
- Y → "owner" 또는 ε
- Verb → "eats"

### 🔷 문장

> According to Rule 2(a), FIRST(Y) - ε must be added to FOLLOW(X)

👉 **해석**
Rule 2(a)에 따라 FIRST(Y) - ε을 FOLLOW(X)에 추가

✔ **계산**

```
FIRST(Y) = { "owner", ε }
```

👉 ε 제외하면: `{"owner"}`
👉 따라서:

```
FOLLOW(X) ← {"owner"}
```

### 🔷 문장

> Because Y → ε, FOLLOW(Subject) must be added to FOLLOW(X)

👉 **해석**
Y가 ε이므로 FOLLOW(Subject)를 FOLLOW(X)에 추가

✔ **설명**
👉 구조:

```
Subject ::= "the" X Y
```

👉 Y가 ε이면:
- X 다음 → Y 없음 → Subject 다음으로 넘어감

### 🔷 문장

> FOLLOW(X) = {"owner", "eats"}

👉 **해석**
최종 FOLLOW(X) = {"owner", "eats"}

✔ **왜 "eats" 나오냐**
👉 Sentence:

```
Sentence ::= Subject Verb "."
```

👉 Subject 다음 → Verb → "eats"

### 🔥 핵심

FOLLOW 계산 핵심:
- 오른쪽 FIRST 추가
- ε이면 부모 FOLLOW 전달

---

## 📋 17페이지

### 🔷 제목

> FOLLOW-Sets: Processing Production A ::= αBβ

👉 **해석**
FOLLOW 계산에서 A ::= αBβ 처리 방법

### 🔷 문장

> For each production A ::= αBβ, Rule (2) must be applied

👉 **해석**
각 production마다 Rule(2)를 적용해야 한다

### 🔷 문장

> α is a string

👉 **해석**
α는 문자열

### 🔷 문장

> B is a single non-terminal

👉 **해석**
B는 하나의 비단말

### 🔷 문장

> β is a string

👉 **해석**
β도 문자열

### 🔷 핵심 문장

> B may match in zero, one or more positions

👉 **해석**
B는 여러 위치에 등장할 수 있다

✔ **설명**
👉 예:

```
A ::= B B B
→ B가 3번 등장
→ 각각 따로 계산해야 함
```

### 🔷 문장

> Rule (2) will have to be applied multiple times

👉 **해석**
Rule(2)는 여러 번 적용된다

### 🔥 핵심

👉 FOLLOW는 "한 번 계산하고 끝"이 아니라
👉 모든 위치에서 반복 적용

---

## 📋 18페이지

### 🔷 제목

> Anchoring the αBβ Pattern

👉 **해석**
αBβ 패턴을 어디에 적용하는지

### 🔷 문장

> Assume production T' ::= "*" F T'

👉 **해석**
T' → "*" F T'

✔ **그림 설명 (중요)**
슬라이드 그림: 👉 α B β 위치가 3개 존재

### 🔷 Position 1

> B = T'

👉 FOLLOW(T') 계산

### 🔷 Position 2

> B = F

👉 FOLLOW(F) 계산

### 🔷 Position 3

> B = "*"

👉 terminal → FOLLOW 없음

✔ **핵심 설명**
👉 하나의 production에서도:
여러 B 위치마다 따로 계산

### 🔥 핵심

👉 FOLLOW 계산은:
모든 위치에서 αBβ 형태를 찾아야 한다

---

## 📋 19페이지

### 🔷 제목

> FOLLOW-Set Example 2

### 🔷 문법

```
T  ::= F T'
T' ::= "*" F T'
T' ::= ε
F  ::= "(" T ")"
F  ::= "ID"
```

### 🔷 초기 상태

```
FOLLOW(T)  = {$}
FOLLOW(T') = {}
FOLLOW(F)  = {}
```

### 🔷 Iteration 1

👉 계산 진행

결과:
```
T:  {$, ")"}
T': {$, ")"}
F:  {"*", $, ")"}
```

### 🔷 Iteration 2

```
T:  {$, ")"}
T': {$}
F:  {"*", $}
```

### 🔷 Iteration 3 (최종)

```
T:  {$, ")"}
T': {$, ")"}
F:  {"*", $, ")"}
```

### 🔷 문장

> The order is arbitrary

👉 **해석**
계산 순서는 중요하지 않다

### 🔷 문장

> A different order may require different iterations

👉 **해석**
순서에 따라 반복 횟수는 달라질 수 있다

### 🔷 문장

> Processing terminates when no more change

👉 **해석**
더 이상 변화 없으면 종료

### 🔥 핵심

👉 FOLLOW는: 고정점 반복 (fixpoint iteration)

---

## 📋 20페이지

### 🔷 제목

> LL(1) Grammars

### 🔷 문장

> Given FIRST and FOLLOW sets, we can define LL(1)

👉 **해석**
FIRST와 FOLLOW로 LL(1) 정의 가능

### 🔷 정의

```
A → α | β
```

### 🔷 조건 1

```
FIRST(α) ∩ FIRST(β) = ∅
```

👉 **해석**
FIRST끼리 겹치면 안 됨

### 🔷 조건 2

> α ⇒* ε이면
> FIRST(β) ∩ FOLLOW(A) = ∅

👉 **해석**
α가 ε이면
β의 FIRST와 FOLLOW(A)도 안 겹쳐야 함

### 🔷 조건 3

> β ⇒* ε이면
> FIRST(α) ∩ FOLLOW(A) = ∅

👉 **해석**
β가 ε이면
α와 FOLLOW도 안 겹쳐야 함

✔ **설명 (진짜 중요)**
👉 이유:
- ε가 나오면
- → 다음 토큰으로 판단해야 함

### 🔥 최종 핵심

LL(1) 조건 3개:
1. FIRST vs FIRST disjoint
2. ε 있으면 FIRST vs FOLLOW 체크
3. 반대쪽도 동일

### 🔥 16~20페이지 전체 핵심 요약

**FOLLOW 계산 핵심**
- FIRST(β) 추가
- ε이면 FOLLOW 전달
- 모든 위치 반복

**LL(1) 정의 완성**
👉 결국: 충돌 없이 1개 토큰으로 선택 가능해야 함

**시험 핵심 포인트**
- FIRST 계산 규칙
- FOLLOW 계산 규칙
- LL(1) 조건 3개

---

## 📋 21페이지

### 🔷 제목

> An Example from our MiniC CFG: for-loops

👉 **해석**
MiniC 문법에서 for문 예제

### 🔷 문장

```
for_stmt ::= "for" "(" a_expr ";" ... ")" stmt
```

👉 **해석**
for문 구조:
- "for" ( a_expr ; ... ) stmt

### 🔷 문장

```
a_expr ::= "ID" "=" expr | ε
```

👉 **해석**
a_expr는:
- ID = expr
- 또는 없음 (ε)

### 🔷 문장

> FOLLOW(a_expr) = {";"}

👉 **해석**
a_expr 다음에는 반드시 ";"가 온다

### 🔷 문장

> FIRST(α) = {"ID"}

👉 **해석**
α (= ID = expr)는 ID로 시작

### 🔷 문장

> disjoint!

👉 **해석**
겹치지 않는다

✔ **설명**
👉 a_expr 두 경우:
- "ID" "=" expr → FIRST = {ID}
- ε → FOLLOW(a_expr) = {";"}

### 🔥 핵심 판단

👉 LL(1) 조건 체크:

```
FIRST(ID) ∩ FOLLOW(a_expr) = ∅
```

👉 ID vs ";" → 겹치지 않음

### 🔷 문장

> In conclusion, the a_expr production does not prevent the CFG from being LL(1)

👉 **해석**
결론: 이 문법은 LL(1) 조건을 깨지 않는다

### 🔥 핵심

👉 ε 있는 경우는 반드시: FIRST vs FOLLOW 충돌 체크

---

## 📋 22페이지

### 🔷 제목

> Non-LL(1) Grammar Examples

👉 **해석**
LL(1)이 아닌 문법 예제

### 🔷 LL(1) 조건 다시 제시

👉 앞에서 배운 조건 그대로 반복

### 🔷 예제 1

```
S → S a | a
```

👉 **해석**
S → Sa 또는 a

✔ **문제**
👉 left recursion 존재 → LL(1) 아님

### 🔷 예제 2

```
S → a S | a
```

✔ **문제**

```
FIRST(aS) = {a}
FIRST(a)  = {a}
```

👉 겹침 → LL(1) 아님

### 🔷 예제 3

```
S → a R | ε
R → S | ε
```

✔ **문제**
👉 ε 때문에 FOLLOW까지 고려해야 함

### 🔷 문장

> FIRST(S) ∩ FOLLOW(R) ≠ ∅

👉 **해석**
FIRST(S)와 FOLLOW(R)가 겹친다

✔ **설명**
👉 ε 때문에: 어떤 production 쓸지 모호해짐

### 🔷 예제 4

```
S → a R a
R → S | ε
```

✔ **문제**
👉 구조가 복잡하게 얽혀 있음 → FIRST/FOLLOW 충돌 발생

### 🔥 핵심

LL(1) 깨지는 3가지:
1. left recursion
2. FIRST 충돌
3. FIRST-FOLLOW 충돌

---

## 📋 23페이지

### 🔷 제목

> Outlook

👉 **해석**
정리 및 다음 내용

### 🔷 문장

> Syntax and Semantics ✓

👉 **해석**
구문과 의미 ✓ (완료)

### 🔷 문장

> CFGs, BNF, EBNF ✓

👉 **해석**
문법 정의 ✓

### 🔷 문장

> Grammar transformations ✓

👉 **해석**
문법 변환 ✓

### 🔷 문장

> Top-down parsing (LL) ✓

👉 **해석**
탑다운 파싱 ✓

### 🔷 문장

> Recursive descent parser construction ✓

👉 **해석**
재귀 하강 파서 구현 ✓

### 🔷 문장

> LL Grammars ✓

👉 **해석**
LL 문법 ✓

### 🔷 문장

> AST Construction

👉 **해석**
AST 생성 (다음 주제)

### 🔷 문장

> Parse trees vs ASTs

👉 **해석**
파스트리 vs AST

### 🔷 문장

> Chomsky's Hierarchy

👉 **해석**
촘스키 계층

✔ **설명**
👉 이번 강의: LL(1)까지 완전히 끝남
👉 다음: AST + 문법 이론

---

## 🔥 전체 강의 (1~23) 최종 핵심 정리

### 🔥 1. LL(1)의 본질
👉 1개 토큰으로 규칙 선택 가능

### 🔥 2. LL(1) 깨지는 이유
- left recursion
- common prefix
- ambiguity
- FIRST 충돌
- FIRST-FOLLOW 충돌

### 🔥 3. 해결 방법
- left recursion 제거 → 반복문
- left factoring → prefix 제거

### 🔥 4. FIRST
👉 시작 가능한 토큰

### 🔥 5. FOLLOW
👉 뒤에 올 수 있는 토큰

### 🔥 6. LL(1) 조건 (시험 핵심)
1. FIRST(α) ∩ FIRST(β) = ∅
2. ε 있으면 FIRST vs FOLLOW 체크

### 🔥 7. 실전 판단 흐름 (이거 외워라)

문법 보면:
1. FIRST 계산
2. FOLLOW 계산
3. 충돌 확인

### 🔥 진짜 시험 포인트
- FIRST 계산 문제
- FOLLOW 계산 문제
- LL(1) 판별 문제
- left recursion 제거
- left factoring
