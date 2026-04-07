---
title: "Syntax Analysis 2"
excerpt: ""

categories:
  - Compiler
tags:
  - tag1
  - tag2

permalink: /Compiler/syntax2/

toc: true
toc_sticky: true

date: 2026-04-07
last_modified_at: 2026-04-07



---
# COMP321 Compiler — Syntax Analysis 2
**Kyungpook National University | Hwisoo So | Spring 2026**

---

## 📋 1페이지 — 제목

### Syntax Analysis – 2

> **해석:** 구문 분석 – 2

✔ **설명**
이 강의는 **Syntax Analysis(구문 분석)**의 두 번째 파트다.
즉,

- Lexical Analysis(토큰화) 이후 단계
- 실제 문장 구조를 분석하는 단계

를 본격적으로 다루기 시작하는 강의다.

---

**Hwisoo So**  
**Kyungpook National University**

> **해석:** 소희수 / 경북대학교

✔ **설명:** 강의 담당 교수 정보.

---

**COMP321 Compiler**  
**Spring 2026**

> **해석:** COMP321 컴파일러 과목 / 2026년 봄 학기

✔ **설명:** 과목 정보 + 학기.

#### 🖼 그림 설명

(페이지 전체)

- 중앙에 "Syntax Analysis – 2" 크게 있음
- 아래에 교수 이름 + 학교
- 하단에 경북대학교 로고

> 👉 의미: 이건 그냥 강의 타이틀 슬라이드라서 개념 내용 없음.

---

## 📋 2페이지

**Syntax Analysis COMP321@KNU**

> **해석:** 구문 분석 (경북대 컴파일러 과목)

### Outlook

> **해석:** 개요 / 앞으로 배울 내용

---

**Syntax and Semantics of Programming Languages ✓**

> **해석:** 프로그래밍 언어의 구문과 의미 ✓

✔ **설명:** 이미 이전 강의에서

- syntax (형식)
- semantics (의미)

를 배웠다는 뜻.

---

**Specifying the Syntax of a programming language: ✓**

> **해석:** 프로그래밍 언어의 구문을 정의하는 방법 ✓

---

**– CFGs, BNF and EBNF ✓**

> **해석:** CFG, BNF, EBNF ✓

✔ **설명:** 문법 정의 방식들 이미 학습 완료.

---

**– Grammar transformations ✓**

> **해석:** 문법 변환 ✓

✔ **설명:** left recursion 제거, factoring 같은 것.

---

**Parsing**

> **해석:** 파싱

✔ **설명:** 👉 지금부터 핵심 — scanner 다음 단계 = parser

---

**– Top-down parsing (LL)**

> **해석:** 탑다운 파싱 (LL)

---

**– Recursive descent (LL) parser construction**

> **해석:** 재귀 하강 파서 구현

---

**– LL Grammars**

> **해석:** LL 문법

---

**AST Construction**

> **해석:** AST 생성

---

**– Parse trees vs. ASTs**

> **해석:** 파스 트리 vs AST

---

**Chomsky's Hierarchy**

> **해석:** 촘스키 계층 구조

✔ **설명:** 이 슬라이드는 앞으로 배울 것 로드맵이다.

핵심 흐름:

> 문법 정의 → 파싱 → AST 생성 → 이론

특히 중요한 건:

> 👉 이제부터 "Parsing" 파트 시작

---

## 📋 3페이지

### Parsing

> **해석:** 파싱

---

**We will now look at parsing.**

> **해석:** 이제 파싱을 살펴볼 것이다.

---

**Topics:**

> **해석:** 다룰 내용:

---

**Derivations and parse trees**

> **해석:** 유도 과정과 파스 트리

---

**Ambiguous grammars**

> **해석:** 모호한 문법

---

**– Operator precedence**

> **해석:** 연산자 우선순위

---

**– Operator associativity**

> **해석:** 연산자 결합 방향

---

**Recursive descent parsing**

> **해석:** 재귀 하강 파싱

---

**– What it is.**

> **해석:** 그게 무엇인지

---

**– How to implement it given an EBNF specification.**

> **해석:** EBNF 명세를 기반으로 어떻게 구현하는지

✔ **설명:** 이 페이지 핵심:

👉 parser 공부에서 중요한 3개

- derivation (문장 생성 과정)
- parse tree (구조 표현)
- ambiguity (모호성)

그리고

> 👉 실제 구현: recursive descent

---

## 📋 4페이지

### Grammars: Definition

> **해석:** 문법: 정의

---

**Typically, languages are specified as grammars**

> **해석:** 일반적으로 언어는 문법으로 정의된다

✔ **설명:** 프로그래밍 언어 = CFG로 정의됨

---

**Formally, a grammar is a tuple (N, Σ, S, P) where**

> **해석:** 형식적으로 문법은 (N, Σ, S, P)로 구성된다

---

**N is a finite set of non-terminal symbols**

> **해석:** N은 유한한 비단말 집합이다

✔ **설명:** `<expr>`, `<stmt>` 같은 것

---

**Σ is a set of terminal symbols**

> **해석:** Σ는 단말 기호 집합이다

✔ **설명:** 실제 토큰 (if, +, id 등)

---

**S ∈ N is the start symbol**

> **해석:** S는 시작 기호이다

✔ **설명:** 문법의 출발점

---

**P ⊆ (N ∪ Σ)∗ × (N ∪ Σ)∗ are the production rules**

> **해석:** P는 생성 규칙 집합이다

✔ **설명:** A → B 형태

---

```
N = {<prog>, <expr>, <var>}
```
> 👉 비단말 집합

```
Σ = {True, False, ;, &, |, a, b, …}
```
> 👉 단말 집합

```
S = <prog>
```
> 👉 시작 심볼

---

#### Production rules

```
<prog> →
<prog> → <expr>; <prog>
```
> 👉 프로그램은 여러 expr로 구성됨

```
<expr> → True / False
```
> 👉 boolean 값

```
<expr> → <var>
```
> 👉 변수

```
<expr> → !<expr>
```
> 👉 NOT 연산

```
<expr> → <expr> & <expr>
<expr> → <expr> | <expr>
```
> 👉 AND, OR

```
<var> → Var(_)
```
> 👉 변수 생성

✔ **핵심 설명:**

> 👉 "문법 = 언어를 정의하는 수학적 구조"

---

## 📋 5페이지

### Grammars: Language

> **해석:** 문법이 정의하는 언어

---

**The language of a grammar is the set of words that can be derived from the start symbol by applying production rules**

> **해석:** 문법의 언어란 시작 기호로부터 생성 규칙을 적용하여 만들어질 수 있는 모든 문자열의 집합이다

✔ **설명:** 👉 매우 중요 — Grammar → Language 생성

---

#### Example derivation

```
<prog>
⇒ <expr>; <prog>
⇒ <expr>;
⇒ <expr>&<expr>;
⇒ <var>&<expr>;
⇒ foo&<expr>;
⇒ foo&<var>;
⇒ foo&bar;
```

> **해석 + 설명:** 이건 문자열을 만드는 과정이다.

단계별:

- `<prog>`
- → `<expr>;`
- → `<expr>&<expr>;`
- → `<var>&<expr>;`
- → `foo&<expr>;`
- → `foo&<var>;`
- → `foo&bar;`

> 👉 최종 결과 문자열 생성됨

---

#### 🖼 그림 설명 (중요)

슬라이드 하단 트리

> 👉 parse tree 구조:

```
루트: <prog>
중간: <expr> & <expr>
리프: foo, bar
```

> 👉 의미: `foo & bar;` 이 구조를 트리로 표현한 것

✔ **핵심 정리:**

> 👉 "문법은 문자열을 생성하는 규칙이고, 그 결과 집합이 언어다"

---

## 🔥 1~5페이지 핵심 요약

- 문법(CFG)은 언어를 정의하는 수학적 구조
- (N, Σ, S, P)로 구성됨
- production rule을 통해 문자열을 생성
- derivation = 생성 과정
- parse tree = 구조 표현

---

## 📋 6페이지

### Grammars for Regular Languages

> **해석:** 정규 언어를 위한 문법

---

**Can we place a restriction on the form of a grammar to ensure that it describes a regular language?**

> **해석:** 문법의 형태에 제한을 두어 그것이 정규 언어를 표현하도록 만들 수 있을까?

✔ **설명:** 👉 핵심 질문 — "모든 CFG 말고 정규언어만 표현하는 문법 따로 만들 수 있냐?"

---

**Provable fact:**

> **해석:** 증명 가능한 사실:

---

**For any RE r, there is a grammar g such that L(r) = L(g).**

> **해석:** 임의의 정규표현식 r에 대해, L(r) = L(g)를 만족하는 문법 g가 존재한다.

✔ **설명:** 👉 RE ↔ Grammar 대응 가능 — 즉, 정규표현식 == 정규문법

---

**The grammars that generate regular sets are called regular grammars**

> **해석:** 정규 집합을 생성하는 문법을 정규 문법이라고 한다

---

**Definition:**

> **해석:** 정의:

---

**In a regular grammar, all productions have one of two forms:**

> **해석:** 정규 문법에서는 모든 생성 규칙이 다음 두 형태 중 하나이다

---

1. `A → aA` (or `A → Aa`)

> **해석:** A → aA (또는 A → Aa)

✔ **설명:** 👉 재귀 (문자 + 상태)

---

2. `A → a` (or `A → ε`)

> **해석:** A → a (또는 A → ε)

✔ **설명:** 👉 종료 조건

---

**where A is any non-terminal and a is any terminal symbol**

> **해석:** 여기서 A는 비단말, a는 단말이다

---

**These are also called type 3 grammars (Chomsky)**

> **해석:** 이것을 촘스키 타입 3 문법이라고 한다

✔ **설명:** 촘스키 계층:

- Type 3 → Regular
- Type 2 → CFG

✔ **핵심:** 👉 정규문법은 형태 제한 있음

---

## 📋 7페이지

### Grammars for Regular Languages

> **해석:** 정규 언어 문법

---

**In a regular grammar (Type-3 grammar), all productions have one of two forms**

> **해석:** 정규 문법에서는 생성 규칙이 두 형태만 가진다

```
A → aA
A → a
```

---

**Operations:**

> **해석:** 연산:

---

**(1) Symbol: a**

> **해석:** 기호: a

```
A → a
```
> **해석:** A는 a로 생성

---

**(2) Alternation: (a | b)**

> **해석:** 선택 (a 또는 b)

```
A → a
A → b
```
> **해석:** A → a 또는 A → b

✔ **설명:** 👉 OR 연산

---

**(3) Concatenation: a∙b**

> **해석:** 연결: a 다음 b

```
A → aB
B → b
```
> **해석:** a 다음 b 생성

✔ **설명:** 👉 순서 연결

---

**(4) Repetition (Kleene Star): a\***

> **해석:** 반복: a\*

```
A → aA
A → ε
```
> **해석:** 반복하거나 종료

✔ **설명:** 👉 a\* 구현

✔ **핵심:** 👉 정규표현식 연산을 문법으로 구현 가능

---

## 📋 8페이지

### Parse Trees

> **해석:** 파스 트리

---

**Correspondence between a derivation and a parse tree:**

> **해석:** 유도 과정과 파스 트리는 서로 대응된다

✔ **설명:** 👉 derivation ↔ tree

---

문법:

```
expr ::= id | int | - expr | ( expr ) | expr op expr
op ::= + | - | * | /
```

> **해석:** expr는 다음 중 하나 / op는 연산자

---

**generate string "slope \* x + intercept":**

> **해석:** "slope \* x + intercept" 생성

---

#### derivation 과정

```
expr → expr op expr
     → expr op id
     → expr + id
     → expr op expr + id
     → expr op id + id
     → expr * id + id
     → id * id + id
```

> 👉 최종: `slope * x + intercept`

---

#### 🖼 그림 설명 (매우 중요)

슬라이드 오른쪽 트리:

```
        expr
       /  |   \
    expr op  expr
     |     |     |
   expr    +   id(intercept)
   / | \
 id  *  id
```

> 👉 의미: `(slope * x) + intercept`

✔ **핵심:**

- 👉 derivation = linear 과정
- 👉 parse tree = 구조 표현

---

## 📋 9페이지

### Parse Trees (cont.)

> **해석:** 파스 트리 (계속)

---

**Correspondence between a derivation and a parse tree**

> **해석:** 유도와 파스 트리 대응

---

**The parse tree's internal nodes are nonterminals**

> **해석:** 내부 노드는 비단말이다

---

**The children of a node are the terminals and nonterminals on the right-hand side**

> **해석:** 자식은 RHS 구성 요소

---

**The leaves of the parse tree are the terminals (tokens)**

> **해석:** 리프는 토큰이다

---

**When read from left to right, the leaves make up the sentence**

> **해석:** 리프를 왼→오 읽으면 문장이 된다

---

#### 🖼 그림 설명

트리 구조:

```
루트: expr
내부: expr, op
리프: id(slope), *, id(x), +, id(intercept)
```

> 👉 읽으면: `slope * x + intercept`

✔ **핵심:** 👉 parse tree는 "문장의 구조"를 정확히 보여준다

---

## 📋 10페이지

### Ambiguous Grammars

> **해석:** 모호한 문법

---

**Ambiguity: one sentential form has several distinct parse trees**

> **해석:** 모호성: 하나의 문장이 여러 파스 트리를 가질 수 있다

---

**Example: slope \* x + intercept**

> **해석:** 예시

---

**(slope \* x) + intercept**

> **해석:** 곱 먼저

---

**slope \* (x + intercept)**

> **해석:** 덧셈 먼저

---

#### 🖼 그림 설명 (핵심)

두 개 트리 존재:

1️⃣
```
   +
  / \
 *   intercept
/ \
slope x
```
> 👉 `(slope * x) + intercept`

2️⃣
```
   *
  / \
slope  +
       / \
      x intercept
```
> 👉 `slope * (x + intercept)`

---

**Problem: Operator precedence!**

> **해석:** 문제: 연산자 우선순위

---

**In the 2nd tree, "+" has precedence over "\*"!**

> **해석:** 두 번째 트리에서는 +가 \*보다 우선됨

✔ **핵심 설명:**

> 👉 grammar가 모호하면: 같은 코드 → 다른 의미

> 👉 컴파일러 입장에서 치명적

---

## 🔥 6~10페이지 핵심 요약

- 정규문법 = 형태 제한된 CFG
- RE ↔ Grammar 대응 가능
- derivation ↔ parse tree 대응
- parse tree는 문장 구조를 표현
- ambiguous grammar는 절대 사용하면 안됨
- 문제 원인 = operator precedence

---

## 📋 11페이지

### Ambiguous Grammars (cont.)

> **해석:** 모호한 문법 (계속)

---

**When more than one distinct derivation of a sentence exists (which means there exist several distinct parse trees), the grammar is ambiguous.**

> **해석:** 하나의 문장에 대해 여러 서로 다른 유도 과정이 존재하면 (즉 여러 개의 파스 트리가 존재하면) 그 문법은 모호하다

✔ **설명:** 👉 핵심 정의

> 여러 derivation ⇔ 여러 parse tree ⇔ ambiguous

---

**A programming language construct should have only one parse tree to avoid misinterpretation by a programmer/compiler.**

> **해석:** 프로그래밍 언어 구조는 오해를 방지하기 위해 하나의 파스 트리만 가져야 한다

✔ **설명:** 👉 컴파일러는 "의미가 하나로 고정"되어야 함

---

**For expression grammars, precedence and associativity of operators are used to disambiguate the productions.**

> **해석:** 표현식 문법에서는 연산자 우선순위와 결합 방향을 사용하여 모호성을 제거한다

---

**We rewrite the grammar to make it un-ambiguous:**

> **해석:** 문법을 다시 작성하여 모호성을 제거한다

---

```
expr   ::= term | expr add_op term
term   ::= factor | term mult_op factor
factor ::= id | number | - factor | ( expr )
add_op ::= + | -
mult_op ::= * | /
```

> **해석 + 설명:**

- `expr` → 👉 덧셈/뺄셈 담당
- `term` → 👉 곱셈/나눗셈 담당
- `factor` → 👉 가장 기본 단위

---

#### 🖼 그림 설명

오른쪽 노란 박스:

> 👉 "+를 \*보다 위에 두지 말고 아래로 내려라"

→ 즉: `* > +`

왼쪽 노란 박스:

> 👉 left associativity

```
a - b - c = (a - b) - c
```

✔ **핵심:** 👉 문법 구조로 우선순위를 강제한다

---

## 📋 12페이지

### Ambiguous if-then-else

> **해석:** if-then-else의 모호성

---

**A well-known example of an ambiguous grammar are the following productions for if-then-else**

> **해석:** 잘 알려진 모호한 문법 예시는 if-then-else이다

---

```
stmt ::= IF expr THEN stmt
       | IF expr THEN stmt ELSE stmt
```

> **해석:** if문 정의

---

**Example: IF a THEN IF b THEN x=false; ELSE x=true;**

> **해석:** 예제

✔ **설명 (핵심):**

> 👉 문제: ELSE가 어느 IF에 붙는가?

---

**This grammar can be repaired, but the above problem indicates a programming language design problem.**

> **해석:** 이 문법은 수정할 수 있지만, 이 문제는 언어 설계 문제를 의미한다

---

**Ada uses a different syntax to avoid this problem**

> **해석:** Ada는 다른 문법으로 해결한다

---

```
stmt ::= IF expr THEN stmt END IF
       | IF expr THEN stmt ELSE stmt END IF
```

> **해석:** END IF 추가

✔ **핵심:**

> 👉 dangling else 문제

> 👉 해결: 구조를 명확하게 만든다

---

## 📋 13페이지

### Some Terminology

> **해석:** 용어 정리

---

**Recognition**

> **해석:** 인식

---

**To answer the question "Does the input conform to the syntax of the language?"**

> **해석:** 입력이 문법에 맞는지 확인하는 것

---

**A recognizer uses a CFG to check the syntax of the program.**

> **해석:** recognizer는 CFG를 사용하여 문법을 검사한다

---

**It answers "Yes" or "No"**

> **해석:** Yes/No로 판단

✔ **설명:** 👉 recognizer = 문법 체크기

---

**Parsing**

> **해석:** 파싱

---

1. **Recognize the input program.**

> **해석:** 입력이 맞는지 확인

---

2. **Determine the phrase structure**

> **해석:** 구조를 분석

---

**A parser uses a CFG to parse a sentence or a program.**

> **해석:** parser는 CFG를 이용해 문장을 분석한다

---

**It constructs the leftmost or rightmost derivation**

> **해석:** 좌측/우측 유도를 생성한다

---

**builds the AST**

> **해석:** AST를 만든다

✔ **핵심 비교:**

| | 역할 |
|---|---|
| Recognizer | Yes/No |
| Parser | 구조 생성 (AST) |

---

## 📋 14페이지

### Context-Free Grammar Classes

> **해석:** CFG 클래스

---

**For an arbitrary CFG, parsing can take O(n³) time**

> **해석:** 일반 CFG 파싱은 O(n³)

---

**too slow for practical applications**

> **해석:** 너무 느림

---

**For several classes of grammars, a parser that takes O(n) time can be constructed**

> **해석:** 특정 문법에서는 O(n) 가능

---

**Top-down LL parsers**

> **해석:** LL 파서

---

**Bottom-up LR parsers**

> **해석:** LR 파서

---

**LL = Left-to-right scanning, Left-most derivation**

> **해석:** LL = 좌→우, 좌측 유도

---

**LR = Left-to-right scanning, Right-most derivation**

> **해석:** LR = 좌→우, 우측 유도

---

**The class of LR grammars is a proper superset of the class of LL grammars**

> **해석:** LR ⊃ LL

#### 🖼 그림 설명

```
LL ⊂ LR
```

> 👉 LR이 더 강력함

---

## 📋 15페이지

### Parser Motivation

> **해석:** 파서의 목적

---

**Given a grammar G and an input string s, we need an algorithm to:**

> **해석:** 문법 G와 문자열 s가 주어졌을 때

---

**Decide whether s is in L(G)**

> **해석:** s가 언어에 속하는지 판단

---

**If so, generate a parse tree**

> **해석:** 맞으면 파스 트리 생성

---

**We will see two algorithms**

> **해석:** 두 가지 알고리즘을 본다

---

**Each with different tradeoffs in time and space**

> **해석:** 시간/공간 트레이드오프 존재

✔ **핵심:**

> 👉 parser의 역할 2개

1. 판별 (membership)
2. 구조 생성 (parse tree)

---

## 🔥 11~15페이지 핵심 요약

- ambiguous grammar → 반드시 제거
- precedence + associativity로 해결
- dangling else = 대표적 문제
- recognizer vs parser 차이
- LL vs LR 구조
- parser 목적 = 판별 + 트리 생성

---

## 📋 16페이지

### CYK Algorithm

> **해석:** CYK 알고리즘

---

**Cocke-Younger-Kasami (CYK) Algorithm**

> **해석:** Cocke, Younger, Kasami가 만든 알고리즘

---

**Parsing algorithm for context-free grammars**

> **해석:** CFG를 위한 파싱 알고리즘이다

---

**Invented by John Cocke, Daniel Younger, and Tadao Kasami**

> **해석:** 세 사람이 만든 알고리즘

---

**Basic idea given string s with n tokens:**

> **해석:** 길이 n인 문자열 s가 주어졌을 때 기본 아이디어

---

1. **Find production rules that cover 1 token in s**

> **해석:** 길이 1짜리 토큰을 생성할 수 있는 규칙 찾기

---

2. **Use 1. to find rules that cover 2 tokens**

> **해석:** 길이 2짜리 구간 생성

---

3. **Use 2. to find rules that cover 3 tokens**

> **해석:** 길이 3짜리 구간 생성

---

**…**

> **해석:** 계속 반복

---

**N. Use N-1. to find rules that cover n tokens**

> **해석:** 최종적으로 전체 문자열 생성

---

**If succeeds then s is in L(G), else it is not**

> **해석:** 성공하면 언어에 속함

✔ **핵심 설명:**

> 👉 CYK 핵심 구조

```
길이 1 → 길이 2 → 길이 3 → … → 전체
```

> 👉 bottom-up 방식

---

## 📋 17페이지

### A graphical way to visualize CYK

> **해석:** CYK를 그래프로 표현

---

**Initial graph: the input (terminals)**

> **해석:** 초기 그래프 = 입력

---

**Repeat: add non-terminal edges until no more can be added**

> **해석:** 비단말 노드를 계속 추가

---

**An edge is added when adjacent edges form RHS of a grammar production**

> **해석:** 인접한 노드가 RHS 규칙을 만족하면 추가

---

#### 🖼 그림 설명 (핵심)

입력:

```
a + a * a
```

그래프 구조:

- 아래: terminals (`a`, `+`, `a`, `*`, `a`)
- 위로 올라가면서 E 추가

> 👉 의미:

```
E → a
E → E + E
E → E * E
```

✔ **핵심:** 👉 그래프 = parsing 과정 시각화

---

## 📋 18페이지

### CYK: the algorithm

> **해석:** CYK 알고리즘

---

**CYK is easiest for grammars in Chomsky Normal Form**

> **해석:** CYK는 CNF에서 가장 쉽다

---

**O(N³) time, O(N²) space**

> **해석:** 시간 O(N³), 공간 O(N²)

---

**Chomsky Normal Form**

> **해석:** 촘스키 정규형

---

`A → BC`

> **해석:** 비단말 두 개

---

`A → d`

> **해석:** 터미널 하나

---

`S → ε`

> **해석:** 빈 문자열

✔ **설명:**

> 👉 CNF 조건:
> - `A → BC`
> - `A → a`

> 👉 이유: CYK는 2개씩 쪼개면서 계산하기 때문

---

## 📋 19페이지

### CYK Implementation

> **해석:** CYK 구현

---

**CYK uses a table e(N,N)**

> **해석:** NxN 테이블 사용

---

**set e(i,j) to true if substring input[i:j] can be derived**

> **해석:** input[i:j]를 생성할 수 있으면 true

---

**input[i:j] is input from index i to j-1**

> **해석:** i부터 j-1까지

---

**For the grammar**

> **해석:** 문법

```
E → a | E + E | E * E
```

---

#### 규칙

1. `e(i,i+1)` if `input[i] == 'a'`

> **해석:** 길이 1이면 a인지 확인

2. `e(i,j)` if `e(i,k)`, `input[k]=='+'`, `e(k+1,j)`

> **해석:** `+` 기준으로 분할

3. `e(i,j)` if `e(i,k)`, `input[k]=='*'`, `e(k+1,j)`

> **해석:** `*` 기준 분할

✔ **핵심:**

> 👉 분할 정복: i ~ j 구간을 k에서 쪼갬

---

## 📋 20페이지

### CYK Implementation

> **해석:** CYK 구현

---

**This is a form of dynamic programming**

> **해석:** DP 알고리즘이다

---

**We use a table to store temporary results**

> **해석:** 중간 결과 저장

---

**we use the temp results to compute new ones**

> **해석:** 기존 결과로 새로운 계산

---

**Alternative: recursive checking**

> **해석:** 대안: 재귀

---

**But we will end up re-doing a lot of computation**

> **해석:** 중복 계산 발생

✔ **핵심 설명:**

> 👉 CYK = DP 이유: 같은 구간을 여러 번 계산하지 않기 위해

---

## 🔥 16~20페이지 핵심 요약

**1. CYK 본질**
> Bottom-up parsing + DP

**2. 동작 방식**
> 길이 1 → 2 → 3 → … → 전체

**3. 핵심 연산**
> `e(i,j)` = 구간 i~j가 생성 가능한가

**4. 분할**
> i ~ j → i~k + k+1~j

**5. 조건**
> CNF (A → BC)

**6. 복잡도**
> 시간: O(n³) / 공간: O(n²)

