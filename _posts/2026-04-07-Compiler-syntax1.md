---
title: "Syntax Analysis 1"
excerpt: ""

categories:
  - Compiler
tags:
  - tag1
  - tag2

permalink: /Compiler/syntax1/

toc: true
toc_sticky: true

date: 2026-04-07
last_modified_at: 2026-04-07



---
# COMP321 Compiler — Syntax Analysis 1
**Kyungpook National University | Hwisoo So | Spring 2026**

---

## 📋 1페이지 — 제목

### Syntax Analysis – 1
> **구문 분석 – 1**

컴파일러에서 **Syntax Analysis(구문 분석)** 단계에 대한 첫 번째 강의다.  
즉, 지금부터 **parser(문법 검사기)** 파트를 본격적으로 시작한다는 의미.

- **Hwisoo So** → 소휘수 (강의자 이름)
- **Kyungpook National University** → 경북대학교
- **COMP321 Compiler Spring 2026** → 컴파일러 과목 (2026년 봄학기)

---

## 📋 2페이지 — Outlook / Today's agenda

### Outlook / Today's agenda
> **강의 개요 / 오늘 배울 내용**

#### Syntax and Semantics of Programming Languages
**프로그래밍 언어의 구문과 의미**

앞으로 계속 나오는 핵심 개념:
- **Syntax** = 형태 (문법)
- **Semantics** = 의미

#### Specifying the Syntax of a programming language
**프로그래밍 언어의 구문을 정의하는 방법**

- **CFGs, BNF and EBNF** → CFG, BNF, EBNF
  - CFG → 문법 정의 이론
  - BNF → 문법 표현 방식
  - EBNF → 더 편한 확장 버전

- **Grammar transformations** → 문법 변환  
  파서 만들기 쉽게 문법을 바꾸는 과정 (→ LL 파서 만들 때 필수)

#### Parsing
**파싱 (구문 분석 과정)**

- **Top-down parsing (LL)** → 탑다운 파싱 (LL)
- **Recursive descent (LL) parser construction** → 재귀 하강 파서 구현
- **LL Grammars** → LL 문법  
  LL 파서는 왼쪽부터 읽고(L), 왼쪽부터 유도(L)

#### AST Construction
**AST 생성**

- **Parse trees vs. ASTs** → 파스 트리 vs AST
  - Parse Tree = 문법 그대로
  - AST = 실제 의미 중심

#### Chomsky's Hierarchy
**촘스키 계층** — 언어 이론 (정규, CFG 등)

---

## 📋 3페이지 — 컴파일러 구조 복습

### Recapitulate: the structure of a compiler...
> **복습: 컴파일러의 구조**

#### 그림 설명 — 컴파일러 전체 파이프라인

```
Source Code
    ↓
Lexical Analyzer
    ↓  [Tokens]
Syntax Analyzer
    ↓  [Abstract Syntax Tree (AST)]
Semantic Analyzer
    ↓  [Decorated AST]
Intermediate Code Generator
    ↓  [Intermediate Representation (IR)]
Code Optimizer
    ↓
Code Generator
    ↓
Target Assembly
```

| 단계 | 출력 |
|------|------|
| Lexical Analyzer | Tokens |
| Syntax Analyzer | AST |
| Semantic Analyzer | Decorated AST |
| Intermediate Code Generator | IR |

- **Compiler Frontend (Analysis)** → 컴파일러 앞단: Lexical + Syntax + Semantic
- **Compiler Backend (Synthesis)** → 컴파일러 뒷단: IR 생성 이후

> **…each phase transforms the program…**  
> 각 단계는 프로그램을 다른 형태로 변환한다

컴파일러는 "번역기"가 아니라 **단계별 변환기 파이프라인**이다.

---

## 📋 4페이지 — 컴파일러 구조 복습 (코드 예시)

### Recapitulate: the structure of a compiler...
> **컴파일러 구조 복습**

#### 코드 예시

```
position = initial + rate * 60
```

심볼 테이블 연결:

| 번호 | 식별자 |
|------|--------|
| 1 | position |
| 2 | initial |
| 3 | rate |
| 4 | 60 |

- **Symbol Table** (심볼 테이블) → 변수 정보 저장: 이름 / 타입 / 위치

#### 단계별 변환

**1단계: Tokens** (scanner 결과)
```
id, =, id, +, id, *, intliteral
```

**2단계: AST** (구조만 표현)
```
        =
       / \
      id   +
           / \
          id   *
               / \
              id  int
```

**3단계: Decorated AST** → 타입 정보 추가됨 (예: int → float 변환)

> **Note: all variables are of type real**  
> 모든 변수는 real 타입 → 타입 변환 발생 (int → float)

---

## 📋 5페이지 — Syntax and Semantics (영어 예시)

### English Language: Syntax and Semantics
> **영어에서의 구문과 의미**

| 문장 | 해석 |
|------|------|
| John eats apples. | 존은 사과를 먹는다 |
| Apples eat John. | 사과가 존을 먹는다 |

#### Syntax (구문)

- **The form or structure of English sentences** → 문장의 형태 또는 구조
- **Not concerned with the meaning** → 의미는 고려하지 않는다
- **Specified by the English grammar** → 문법에 의해 정의된다

> Syntax는 "맞는 문장인지"만 본다  
> `Apples eat John` → 문법적으로는 맞음, 의미는 이상함

#### Semantics (의미)

- **The meaning of English sentences** → 문장의 의미
- **Semantic definition?** → 의미를 어떻게 정의할 것인가?

> Semantics는 "말이 되는지" 본다

---

## 🔥 1~5페이지 핵심 요약

1. **컴파일러 구조**: Lexical → Syntax → Semantic
2. **Syntax vs Semantics**: Syntax = 문법 / Semantics = 의미
3. **Syntax Analysis 역할**: 토큰을 받아서 구조(트리) 만든다
4. **AST 중요성**: 이후 모든 단계의 기반

---

## 📋 6페이지 — Programming Languages: Syntax and Semantics

### Programming Languages: Syntax and Semantics
> **프로그래밍 언어: 구문과 의미**

#### 코드 예시

```c
b = b + 1;
if (b==2) printf("too small\n");
```

- `b = b + 1;` → b는 b+1로 갱신 (문법 + 의미 모두 정상)
- `if (b==2) printf("too small\n");` → 조건문 예시 (문법 + 의미 모두 정상)

#### Syntax (구문)

- **The form or structure of programs** → 프로그램의 형태 또는 구조
- **Not concerned with the meaning of programs** → 프로그램의 의미는 고려하지 않는다
- **Specified by a context-free grammar (CFG)** → 문맥 자유 문법(CFG)에 의해 정의된다

> 핵심: 프로그래밍 언어의 문법은 전부 **CFG**로 정의됨

#### Semantics (의미)

- **The meaning of programs** → 프로그램의 의미
- **Specified by:**
  - operational, denotational or axiomatic semantics → 연산적 / 지시적 / 공리적 의미론
  - **attribute grammars** (will be covered by this course) → 속성 문법 (이 수업에서 다룸)
  - informal English descriptions (as with C, Java, MiniC) → 비공식적 영어 설명

---

## 📋 7페이지 — Context-free Grammars (CFGs)

### Context-free Grammars (CFGs)
> **문맥 자유 문법**

#### Example: CFG for micro-English

```
Sentence ::= Subject Verb Object .
Subject  ::= I | A Noun | The Noun
Object   ::= me | a Noun | the Noun
Noun     ::= cat | mat | rat | ε
Verb     ::= like | is | see | sees
```

| 기호 | 의미 |
|------|------|
| `::=` | 정의 |
| `\|` | 선택 |
| `ε` | 아무것도 없음 (빈 문자열) |

#### CFG 기본 개념

- **Context-free grammars consist of productions of the form:**  
  CFG는 다음 형태의 production으로 구성된다

```
<nonterminal> ::= sequence of (non) terminals
```

- **a terminal of a grammar is a token** → terminal은 토큰이다
- **the symbol "|" denotes alternative forms** → `|`는 선택을 의미한다
- **ε denotes the empty string** → `ε`는 빈 문자열을 의미한다

---

## 📋 8페이지 — Context-free Grammars (derivation)

### Context-free Grammars
> **문맥 자유 문법 — derivation**

> **A derivation shows how to generate a syntactically valid string.**  
> 유도(derivation)는 문법적으로 올바른 문자열을 생성하는 과정을 보여준다

#### 예시

```
Sentence  →  Subject Verb Object .
          →  I Verb Object .
          →  I see Object .
          →  I see the Noun .
          →  I see the cat .
```

- derivation = "문장을 한 단계씩 생성하는 과정"
- **The non-terminal to be replaced next is underlined**  
  다음에 치환할 non-terminal은 밑줄로 표시된다

---

## 📋 9페이지 — Context-free Grammars (문장 예시)

### Context-free Grammars
> **micro-English에서 가능한 문장들**

#### 포함되는 문장 (valid)

| 문장 | 해석 | 비고 |
|------|------|------|
| I like the cat. | 나는 고양이를 좋아한다 | 문법 OK |
| The cat like the mat. | 고양이가 매트를 좋아한다 | 문법 OK, 영어는 틀림 (likes여야 함) |
| The mat is the rat. | 매트는 쥐다 | 문법 OK, 의미 이상 |

> Syntax vs Semantics 차이 다시 등장

#### 포함되지 않는 문장 (invalid)

- **I like the black cat.** → adjective(형용사) 없음 → 생성 불가

#### How many sentences can be derived?
**몇 개의 문장을 만들 수 있는가?**

> **Just a few, i.e., finitely many**  
> 몇 개 안 된다 (유한 개) → 이 CFG는 표현력이 제한됨

---

## 📋 10페이지 — Derivations

### Derivations
> **유도**

- **From a grammar we can derive strings** → 문법으로부터 문자열을 생성할 수 있다
- **by generating sequences of tokens** → 토큰의 시퀀스를 생성함으로써
- **In each derivation step, a nonterminal is replaced** → 각 단계에서 nonterminal이 치환된다
- **by a right-hand side of a production** → 해당 production의 RHS로

#### 핵심 개념

| 용어 | 의미 |
|------|------|
| **Sentential form** | 중간 과정의 문자열 (terminal + nonterminal 혼재) |
| **Sentence** | terminal만 있는 최종 상태 |

- **A context-free grammar is a generator of a language**  
  CFG는 언어 생성기다
- **the set of all strings that can be derived**  
  유도 가능한 모든 문자열의 집합
- **A sentence that cannot be derived is syntactically illegal**  
  유도할 수 없는 문장은 문법적으로 틀린 것이다

> CFG = "가능한 모든 프로그램 정의"  
> parser 역할 = 이 문장이 CFG로 만들어질 수 있는지 검사

---

## 🔥 6~10페이지 핵심 요약

1. **Syntax vs Semantics**: Syntax = 구조 (CFG) / Semantics = 의미
2. **CFG 핵심 구성**: terminal = 토큰 / nonterminal = 문법 변수 / production = 규칙 / ε = empty
3. **derivation**: 문장을 단계적으로 생성 / sentential form → 중간 상태 / sentence → 최종 상태
4. **핵심 정의**: CFG = language generator / "생성 가능 = 문법적으로 correct"

---

## 📋 11페이지 — Context-free Grammars (정의)

### Context-free Grammars
> **CFG 정의**

> **A context free grammar specifies all valid strings (a.k.a. programs) of a given programming language!**  
> CFG는 주어진 프로그래밍 언어에서 가능한 모든 올바른 문자열(즉, 프로그램)을 정의한다.

> **→ Formal description of the syntax of a programming language.**  
> → 프로그래밍 언어의 구문에 대한 형식적 정의

#### Elements of CFGs (CFG의 구성 요소)

**Terminal Symbols (Terminals)** — 단말 기호
- 예: `<=`, `while`, `if`, `>`, `==`, `ID`, `INTLITERAL`
- 실제 코드에서 나오는 토큰들

**Nonterminal Symbols (Non-terminals)** — 비단말 기호
- Particular class of phrases in the language → 언어에서 특정한 구조를 나타내는 기호
- 예: `Program`, `Command`, `Expression`, `Declaration`
- 문법의 "변수" 역할

**Start Symbol** — 시작 기호
- One of the nonterminals → 비단말 중 하나
- usually the lefthand-side of the first production → 보통 첫 번째 production의 왼쪽
- 예: `sentence`

**Productions** — 생산 규칙
- 예: `sentence ::= noun verb`

> **CFG = (Terminal, Nonterminal, Start, Production)**

---

## 📋 12페이지 — CFG in BNF

### Context-free Grammars
> **BNF 표현**

> **CFGs can be expressed in BNF (Backus-Naur Form)**  
> CFG는 BNF로 표현할 수 있다

> To recognize P. Naur's contribution… and J. W. Backus…  
> BNF는 Naur와 Backus의 기여를 기리기 위해 이름 붙여졌다

#### Example in BNF

```
Program       ::= Command
Command       ::= single-Command
               | Command ; single-Command
single-Command ::= V-name := Expression
               | begin Command end
```

| 기호 | 의미 |
|------|------|
| `::=` | 문법 정의 |
| `:=` | 실제 코드 대입 연산자 |
| `\|` | 선택 |

> ⚠️ `::=`와 `:=` 구분 중요 — 헷갈리면 시험에서 틀린다

- 재귀 있음 (`Command ::= Command ; ...`) → "문장 여러 개 이어붙이기" 표현

---

## 📋 13페이지 — EBNF

### Context-free Grammars
> **EBNF**

> **For our convenience, we will use EBNF**  
> 편의를 위해 EBNF를 사용한다

> **EBNF = BNF + regular expressions**  
> EBNF = BNF + 정규표현식

#### BNF vs EBNF 비교

**BNF**
```
Command ::= single-Command
          | Command ; single-Command
```

**EBNF**
```
Command ::= single-Command (; single-Command)*
```

> **`*` means 0 or more occurrences**  
> `*`는 0번 이상 반복

BNF → 복잡한 재귀 필요  
EBNF → 훨씬 직관적으로 표현 가능

---

## 📋 14페이지 — CFG for extended micro-English

### A CFG for extended micro-English
> **확장된 micro-English용 CFG**

> **Verify if "Peter passed the test" is a sentence?**  
> "Peter passed the test"가 문장인지 확인하라

#### 문법

```
sentence  ::= subject predicate
subject   ::= NOUN | ARTICLE NOUN
predicate ::= VERB object
object    ::= NOUN | ARTICLE NOUN
```

#### 판단 과정

| 단어 | 분류 |
|------|------|
| Peter | NOUN |
| passed | VERB |
| the | ARTICLE |
| test | NOUN |

→ 전부 규칙 만족 → ✔ **valid sentence**

---

## 📋 15페이지 — Two derivations

### Two derivations of "Peter passed the test"
> **두 가지 유도 방법**

**derivation 1 (leftmost)**
```
sentence  →  subject predicate
          →  NOUN predicate
          →  NOUN VERB object
          →  NOUN VERB ARTICLE NOUN
```

**derivation 2 (rightmost)**
```
sentence  →  subject predicate
          →  subject VERB object
          →  subject VERB ARTICLE NOUN
          →  NOUN VERB ARTICLE NOUN
```

> 두 방식 모두 같은 결과 생성:  
> **Sentence: NOUN VERB ARTICLE NOUN**

- **Sentential forms** → 중간 과정들
- 같은 문장도 **여러 derivation 가능** → CFG는 비결정적 구조

---

## 🔥 11~15페이지 핵심 요약

1. **CFG 구성 요소 (필수)**: Terminal / Nonterminal / Start Symbol / Production
2. **BNF vs EBNF**: BNF = 기본 / EBNF = 반복(`*`, `+`, `?`) 가능
3. **derivation 핵심**: 문장 생성 과정, 여러 방식 가능
4. **핵심 문제 유형**: "이 문장이 CFG로 생성 가능한가?"
5. **매우 중요**: 같은 문자열 = 여러 derivation 가능

---

## 📋 16페이지 — Leftmost and Rightmost Derivations

### Leftmost and Rightmost Derivations
> **좌측 유도와 우측 유도**

> **At each step in the derivation, two choices are made:**  
> 유도 과정의 각 단계에서 두 가지 선택이 존재한다

1. **Which nonterminal to replace?** → 어떤 nonterminal을 치환할 것인가?
2. **Which alternative to use for that nonterminal?** → 어떤 규칙을 사용할 것인가?

#### Two types of useful derivations (유용한 두 가지 유도 방식)

| 방식 | 설명 | 연결되는 파서 |
|------|------|-------------|
| **Leftmost derivation** | 항상 가장 왼쪽 nonterminal을 치환 | **LL parser** |
| **Rightmost derivation** | 항상 가장 오른쪽 nonterminal을 치환 | **LR parser** |

> ⭐ 시험 핵심: Leftmost → LL / Rightmost → LR

---

## 📋 17페이지 — Conventions for writing CFGs

### Conventions for writing CFGs
> **CFG 작성 규칙**

#### Start symbol
- The left-hand side of the first production → 첫 번째 production의 왼쪽
- The letter S, whenever it appears → 보통 S를 사용

#### Nonterminals (비단말)
- lower-case names such as "sentence", "expr"
- capital letters like A, B, C

#### Terminals (단말)
- boldface names such as **ID** and **INTLITERAL**
- digits, operators, punctuation characters: `1`, `+`, `[`
- Sometimes in double quotes → 가끔 따옴표로 표현

---

## 📋 18페이지 — Example Grammar for Pascal

### Example Grammar for Pascal
> **Pascal 언어 문법 예시**

```
program      ::= PROGRAM id ( id more_ids ) ; block .
block        ::= variables BEGIN stmt more_stmts END
more_ids     ::= , id more_ids | ε
variables    ::= VAR id more_ids : type ; more_variables | ε
more_variables ::= id more_ids : type ; more_variables | ε
stmt         ::= id := exp
               | READ ( id more_ids )
               | IF exp THEN stmt ELSE stmt
               | WHILE exp DO stmt
               | BEGIN stmt more_stmts END
more_stmts   ::= ; stmt more_stmts | ε
exp          ::= num | id | exp + exp | exp – exp
type         ::= integer | boolean | char
```

#### 핵심 포인트

1. **program 구조** → `PROGRAM` 시작 → `block` → 끝에 `.`
2. **block** → 변수 선언 + `BEGIN ~ END`
3. **stmt 종류**: 대입 / READ / IF / WHILE / BEGIN-END
4. **ε** → optional (없어도 됨)

> **Note: The productions for 'num' and 'id' have been omitted**  
> num과 id 정의는 생략됨 (lexical 단계에서 이미 정의된 토큰)

---

## 📋 19페이지 — Pascal 문법 검사 예제

### Example Grammar for Pascal (cont.)

> **Does the following program adhere to the Pascal syntax?**  
> 다음 프로그램이 Pascal 문법을 만족하는가?

```pascal
PROGRAM foo (input, output);
BEGIN
  IF a THEN a:= a+1; b := 22 ENDIF;
END;
```

#### 핵심 분석

Pascal 문법에서 IF문 규칙:
```
IF exp THEN stmt ELSE stmt
```

→ 반드시 **ELSE 필요**  
→ 이 코드는 ELSE 없음 + ENDIF 구조도 Pascal 스타일 아님  
→ **문법 오류 가능성 있음**

---

## 📋 20페이지 — Grammar & Program, side-by-side

### Grammar & Program, side-by-side
> **문법과 프로그램 비교**

왼쪽: CFG / 오른쪽: 실제 코드를 나란히 비교

#### 매칭 과정

| 코드 | 문법 |
|------|------|
| PROGRAM | ok |
| foo | id |
| (input, output) | ok |
| BEGIN ~ END | block |

#### 오류 부분

```pascal
IF a THEN a:= a+1; b := 22 ENDIF;
```

CFG 규칙: `IF exp THEN stmt ELSE stmt`  
→ **ELSE 없음** → 문법 불일치 → **syntax error**

---

## 🔥 16~20페이지 핵심 요약

1. **derivation 종류 (매우 중요)**: Leftmost → LL parser / Rightmost → LR parser
2. **CFG 작성 규칙**: Start symbol / Terminal / Nonterminal 구분
3. **ε 의미**: optional (없어도 됨)
4. **실제 시험 핵심 유형**: 코드가 CFG에 맞는지 판단
5. **중요 포인트**: CFG는 "가능한 프로그램 정의" / parser는 "그 안에 포함되는지 검사"

---

## 📋 21페이지 — Lexical Analyzer 역할

### Lexical Analyzer (Scanner, Tokenizer)

#### 원본 코드

```pascal
PROGRAM foo (input, output);
VAR a, b: integer;
BEGIN
  IF a <> 0 THEN BEGIN a:= a+1; b := 22 END
END.
```

#### scanner 출력 (토큰들)

```
PROGRAM  foo  (  ,  output  )  ;
IF  a  THEN
a  :=  a  +  1  ;  b  :=  22
END  .
;
BEGIN
VAR  a  ,  b  :  integer  ;
input
<>  0
END
BEGIN
```

#### 핵심 설명

scanner 역할:
- 문자열 → 토큰 나열 ✔
- 문법 체크 ❌
- 구조 이해 ❌

> Lexical Analyzer는 "의미"나 "구조"를 모른다 — 단순히 문자열 → 토큰으로 쪼갤 뿐이다

---

## 📋 22페이지 — Syntax Analyzer 역할

### Syntax Analyzer (Parser)

#### 흐름

```
Tokens  →  Parser  →  Parse Tree
```

| 단계 | 역할 |
|------|------|
| scanner | 토큰 생성 |
| parser | 구조 생성 (트리) |

- **Scanner** → 토큰 나열
- **Syntax Analyzer (Parser)** → 토큰을 입력으로 받아 문법 구조(Parse Tree) 생성

---

## 📋 23페이지 — Syntax Error 예시

### Syntax Error 발생

#### 문제 코드

```pascal
PROGRAM foo (input, output);
BEGIN
  IF a THEN a:= a+1; b := 22 ENDIF;
END;
```

#### parser 에러

```
Expected token: ELSE
Actual token from the scanner: (실제 scanner가 준 토큰)
```

#### 핵심

- CFG 규칙: `IF exp THEN stmt ELSE stmt`
- 실제 코드: ELSE 없음 → 규칙 불일치

> scanner는 문제 없음  
> **parser에서 에러 발생**  
> **Syntax Error = parser 단계에서 발생**

---

## 📋 24페이지 — Grammar & Program (Reminder)

### Grammar & Program, side-by-side (Reminder)
> **문법과 프로그램 비교 (다시 보기)**

왼쪽: CFG / 오른쪽: 코드를 나란히 비교해서 문법 위반 찾기

```pascal
PROGRAM foo (input, output);
BEGIN
  IF a THEN a:= a+1; b := 22 ENDIF;
END;
```

- **IF → ELSE 필요** (없음 → 오류)
- **ENDIF → Pascal 문법 아님**
- → **CFG로 생성 불가 → syntax error**

---

## 📋 25페이지 — SYNTAX ERROR 확정

### SYNTAX ERROR!

```
SYNTAX ERROR!
Expected token: ELSE
Actual token from the scanner: ...
```

parser는 항상:

```
기대한 토큰  vs  실제 토큰  →  mismatch  →  Syntax Error
```

---

## 🔥 21~25페이지 핵심 요약

1. **scanner vs parser**: scanner → 토큰 생성 / parser → 문법 검사
2. **Syntax Error 발생 위치**: parser 단계
3. **error 원인**: CFG 규칙 불일치
4. **대표 예**: IF에 ELSE 없음 → 오류
5. **중요한 개념 흐름**:
   ```
   input → scanner → tokens → parser → parse tree
                                ❌ 실패 시 syntax error
   ```

---

## 📋 26페이지 — Extended BNF

### Extended BNF
> **확장된 BNF**

> **Extended BNF combines BNF with RE**  
> EBNF는 BNF와 정규표현식을 결합한 것이다

#### EBNF production 형태

```
LHS ::= RHS
```

- **LHS** → nonterminal symbol
- **RHS** → extended regular expression (terminal + nonterminal로 구성)

#### EBNF가 BNF에 추가하는 기호

| 기호 | 의미 |
|------|------|
| `( )` | 그룹화 |
| `*` | 0번 이상 반복 |
| `+` | 1번 이상 반복 |
| `?` | 0 또는 1번 |

> ⭐ 이 4개는 무조건 기억

> **The miniC grammar is given in EBNF**  
> miniC 문법은 EBNF로 주어진다

---

## 📋 27페이지 — EBNF Example

### Extended BNF Example

#### 간단한 표현식 언어

```
Expression  ::= PrimaryExp (Operator PrimaryExp)*
PrimaryExp  ::= Literal | Identifier | "(" Expression ")"
Identifier  ::= Letter (Letter | Digit)*
Literal     ::= Digit Digit*
Letter      ::= "a" | ... | "z"
Digit       ::= "0" | ... | "9"
Operator    ::= "+" | "-" | "*" | "/"
```

#### 핵심

- `(Operator PrimaryExp)*` → 연산 여러 번 가능
- `a + b * c` 같은 표현식 생성 가능

---

## 📋 28페이지 — Kleene Closure (`*`)

### An EBNF example from miniC: Kleene Closure

> **A miniC program that consists of a sequence of zero or more declarations**  
> miniC 프로그램은 선언이 0개 이상으로 구성된다

#### BNF (복잡한 재귀)

```
program   ::= decl-list
decl-list ::= decl-list func-decl
            | decl-list var-decl
            | ε
```

#### EBNF (한 줄로)

```
program ::= (func-decl | var-decl)*
```

> **`*` = Kleene Closure = 0개 이상 반복**

---

## 📋 29페이지 — Positive Closure (`+`)

### An EBNF example from miniC: Positive Closure

> **one or more declarations** → 하나 이상 선언

#### BNF

```
decl-list ::= decl-list func-decl
            | decl-list var-decl
            | func-decl
            | var-decl
```

#### EBNF

```
program ::= (func-decl | var-decl)+
```

> **`+` = 1개 이상**

---

## 📋 30페이지 — Option (`?`)

### An EBNF example from miniC: Option ?

> **The if-statement with an optional else-part**  
> else가 선택적인 if문

#### BNF

```
stmt ::= if "(" expr ")" stmt
       | if "(" expr ")" stmt else stmt
       | other
```

#### EBNF

```
stmt ::= if "(" expr ")" stmt (else stmt)?
       | other
```

> **`?` = 있을 수도 있고 없을 수도 있음**

> 이것이 **dangling else 문제**의 시작이다

---

## 🔥 26~30페이지 핵심 요약

| 기호 | 의미 |
|------|------|
| `*` | 0 이상 (Kleene Closure) |
| `+` | 1 이상 (Positive Closure) |
| `?` | 선택 (Option) |
| `()` | 그룹화 |

- **BNF vs EBNF**: EBNF는 "축약 표현"
- 모든 복잡한 문법도 결국 RE처럼 표현 가능

---

## 📋 31페이지 — Grammar Transformations (이론)

### A little bit of useful theory
> **약간의 유용한 이론**

> **We will now look at a very few useful bits of theory.**  
> 이제 몇 가지 유용한 이론을 살펴본다

> **These will be necessary later when we implement parsers.**  
> 이것들은 나중에 parser를 구현할 때 필요하다

#### Grammar transformations (문법 변환)

> **A grammar can be transformed in a number of ways without changing the meaning**  
> 문법은 의미를 바꾸지 않고 여러 방식으로 변환될 수 있다

> (i.e., the set of strings that it generates)  
> 즉, 생성하는 문자열 집합은 동일하게 유지

변환 이유: 파서 만들기 쉽게 하기 위해

---

## 📋 32페이지 — Grammar Transformations (1)

### Grammar Transformations (1)
> **문법 변환 1 — Left Factorization (좌측 인수분해)**

#### 기존 문법

```
single-Command ::= V-name := Expression
                 | if Expression then single-Command
                 | if Expression then single-Command else single-Command
```

문제: 두 규칙이 같은 prefix (`if Expression then single-Command`)

#### 변환 후

```
single-Command ::= V-name := Expression
                 | if Expression then single-Command ( ε | else single-Command )
```

#### 일반 형태

```
N ::= X Y | X Z   →   N ::= X (Y | Z)
```

> "앞부분 같으면 묶어라"  
> LL parser에서 필수

---

## 📋 33페이지 — Grammar Transformations (2)

### Grammar Transformations (2)
> **문법 변환 2 — Elimination of Left Recursion (좌측 재귀 제거)**

#### 문제 문법

```
N ::= X | N Y
```

→ LL parser에서 무한 루프 발생

#### 예시

```
Identifier ::= Letter
             | Identifier Letter
             | Identifier Digit
```

#### 변환 후

```
Identifier ::= Letter (Letter | Digit)*
```

#### 변환 원리

```
N → X
  → X Y
  → X Y Y
  → ...
  → X Y*
```

> **Left recursion → Kleene star (`*`)**

---

## 📋 34페이지 — Grammar Transformations (3)

### Grammar Transformations (3)
> **문법 변환 3 — Substitution of non-terminal symbols (비단말 치환)**

#### 기본 형태

```
N ::= X
M ::= α N β
```

변환 후:

```
M ::= α X β
```

중간 단계 제거 → 직접 연결

#### 예시

```
single-Command ::= for contrVar := Expression
                   to-or-dt Expression do single-Command

to-or-dt ::= to | downto
```

변환 후:

```
single-Command ::= for contrVar := Expression
                   (to | downto) Expression do single-Command
```

> **nonterminal 제거 → inline 처리**

---

## 📋 35페이지 — Outlook (정리)

### Outlook
> **정리 및 이후 내용**

#### 완료된 내용 ✔

- Syntax and Semantics of Programming Languages ✔
- Specifying the Syntax of a programming language ✔
  - CFGs, BNF and EBNF ✔
  - Grammar transformations ✔

#### 다음 내용

- **Parsing**
  - Top-down parsing (LL)
  - Recursive descent
  - LL Grammars
- **AST Construction**
- **Chomsky's Hierarchy**

> 지금까지는 "문법 정의"  
> 이제부터는 "파싱 구현"

---

## 🔥 31~35페이지 핵심 요약

| 변환 | 목적 |
|------|------|
| **Left Factorization** | 공통 prefix 제거 |
| **Left Recursion 제거** | LL parser 필수 조건 |
| **Substitution** | 비단말 inline 처리 |

- Grammar Transformation 목적: 파서 만들기 쉽게

---

## 🔥 전체 강의 핵심 요약 (1~35페이지)

### ⭐ 시험 핵심 6가지

| 항목 | 내용 |
|------|------|
| ⭐ 1. CFG | 언어 정의 핵심 |
| ⭐ 2. Derivation | 문장 생성 과정 |
| ⭐ 3. Syntax vs Semantics | 무조건 구분 |
| ⭐ 4. EBNF 기호 | `*` / `+` / `?` / `()` |
| ⭐ 5. Grammar Transformation | Left factoring / Left recursion 제거 |
| ⭐ 6. Parser 역할 | CFG 기반 문법 검사 |

### 컴파일러 전체 흐름

```
input → scanner → tokens → parser → parse tree
                              ❌ 실패 시 Syntax Error
```

### Grammar Transformation 요약

```
RE → NFA → DFA → 최소 DFA  (lexical)

CFG → Left Factoring → Left Recursion 제거 → Parser  (syntax)
```
