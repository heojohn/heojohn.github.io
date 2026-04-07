---
title: "Lexical Analysis Part 3"
excerpt: ""

categories:
  - Compiler
tags:
  - tag1
  - tag2

permalink: /Compiler/3/

toc: true
toc_sticky: true

date: 2026-04-07
last_modified_at: 2026-04-07



---
# COMP321 Compiler — Lexical Analysis Part 3
**Kyungpook National University | Hwisoo So | Spring 2026**

---

## 📋 1페이지 — 제목

### Lexical Analysis – Part 3
> **어휘 분석 – 3번째 파트**

컴파일러의 **Lexical Analysis(스캐너 단계)**를 다루는 강의의 세 번째 파트다.  
즉, 지금까지 배운 내용의 연장선 + 더 심화된 내용이라고 보면 된다.

- **Hwisoo So** → 소휘수 (강의자 이름) — 이 강의를 진행하는 교수님 이름이다.
- **Kyungpook National University** → 경북대학교 — 강의가 진행되는 소속 대학
- **COMP321 Compiler Spring 2026** → 컴파일러 과목 (COMP321), 2026년 봄학기 — 이 강의가 어떤 과목이고 언제 진행되는지 명시

#### 🖼 그림 설명
- 중앙: Lexical Analysis – Part 3 (제목)
- 아래: 교수 이름 + 학교 로고

이 페이지는 **완전한 표지(slide cover)**다. 내용 없음, 단순히 강의 시작 알림 역할.

---

## 📋 2페이지 — Outline (강의 개요)

### The role of a scanner ✔
**스캐너의 역할 ✔**  
이미 배운 내용이라는 의미 → scanner = 문자열 → 토큰으로 쪼개는 역할

### Scanner concepts ✔
**스캐너 개념 ✔**

#### Tokens, Lexemes, Patterns — 핵심 3개 개념
- **Lexeme**: 실제 문자열 (예: "if", "abc")
- **Token**: 분류 (예: IF, ID 등)
- **Pattern**: 규칙 (정규식)

### Regular Expression & Automata (to be continued…)
**정규표현식과 오토마타 (계속 진행 예정)**  
이 파트가 지금 강의의 핵심 주제

| 항목 | 상태 |
|------|------|
| Definitions of REs, DFAs and NFAs | ✔ 완료 — 이미 배운 내용 |
| REs → NFA | ✔ 완료 — Thompson construction 사용 |
| (Thompson's construction, Algorithm…) | 책 기준 알고리즘 번호까지 명시 → 시험 범위 느낌 강함 |
| NFA → DFA (subset construction…) | 핵심 알고리즘 → 이후 슬라이드에서 자세히 나옴 |
| DFA → minimal-state DFA | 상태 최소화 → 성능 최적화 단계 |
| Scanner generators | 이번 강의에서 새로 나올 핵심 |
| Extra materials | 추가 자료 |

### Today's agenda — 오늘의 강의 계획
이 페이지는 전체 강의 흐름 정리 → 지금부터 **scanner generator** 중심으로 간다

---

## 📋 3페이지 — Scanner Generators

### Scanner Generators
**스캐너 생성기**

핵심 메시지: **"스캐너는 직접 짤 수도 있지만 자동 생성도 가능하다"**

#### Scanners generated in C (C로 생성되는 스캐너)
- **lex (UNIX)** → 가장 전통적인 lexer 생성기
- **flex (GNU's fast lex, UNIX)** → lex의 업그레이드 버전
- **Mks lex (MS-DOS, Windows, OS/2)** → 윈도우 계열

#### Scanners generated in Java (Java로 생성되는 스캐너)
- **Jlex (Princeton University)** → 프린스턴 대학
- **JFlex**
- **JavaCC (SUN Microsystems → now, Oracle)**

앞으로는 **JLex 기준**으로 설명 진행

---

## 📋 4페이지 — The Scanner Spec in JLex

### The Scanner Spec in JLex
**JLex에서의 스캐너 명세**

JLex 파일은 **세 부분 구조**로 되어 있다:

```
[유저 코드]
%%
[선언]
%%
[정규식 규칙]
```

| 구간 | 의미 |
|------|------|
| user code | 사용자 코드 — 여기에 작성한 코드는 그대로 생성된 scanner 코드에 들어감 |
| %% | 구분자 |
| JLEX directives (declarations) | JLex 지시문 (선언) — 변수, 정의 등 작성 |
| %% | 구분자 |
| regular expression rules | 정규표현식 규칙 — 핵심 부분, 토큰 정의하는 곳 |

> 이 구조는 **시험에 자주 나옴**

---

## 📋 5페이지 — How a Scanner Generator Works

### How a Scanner Generator Works
**스캐너 생성기가 어떻게 동작하는가**

#### 내부 동작 흐름 (매우 중요)

```
RE → NFA → DFA → 최소 DFA
```

1. 사람이 정규식 작성
2. 컴퓨터가 자동으로 NFA 생성
3. DFA로 변환
4. 상태 최소화
5. 최종 scanner 코드 생성

이게 **컴파일러 이론 핵심 흐름**이다.

#### 두 가지 구현 방식

| 방식 | 설명 |
|------|------|
| **Table-driven code (JLex)** | 테이블 기반 코드 — 입력에 대해 DFA를 시뮬레이션, 상태 전이를 테이블로 관리 |
| **Hard-wired code (Direct-coded)** | 하드코딩 방식 — 우리가 직접 if문으로 만든 scanner, like our hand-crafted scanner for Assignment #1 |

- **Assignment #1 = Scanner + Parser** → 과제1은 스캐너 + 파서였다

#### 이 페이지 핵심 요약
스캐너 만드는 두 가지 방법: 자동 생성(JLex) vs 직접 구현(Assignment)  
내부 원리는 동일: **RE → NFA → DFA → 최소 DFA**

---

## 📋 6페이지 — Table-driven vs. Directed-coded Scanners

### Table-driven vs. Directed-coded Scanners
**테이블 기반 vs 직접 코드 기반 스캐너**

#### Direct-coded 방식 예시 (코드)

```java
switch (currentChar) {
    case '+': return token representation for '+';
    case '<':
        takeIt();
        if (currentChar == '=')
            return token representation for '<=';
        else
            return token representation for '<';
}
```

- `case '+'`: '+'이면 + 토큰 반환 → 직접 구현 방식, 문자 하나 보고 바로 토큰 결정
- `case '<'`: '<'를 읽고 다음 문자가 '='이면 "<=" 아니면 "<"

**Direct-coded 방식의 대표 예시**: `<` 읽음 → 다음 문자 확인(lookahead) → 조건문으로 처리  
즉, 코드 흐름 자체가 상태 머신 역할을 함

#### 왼쪽 표 — Table encoding RE (DFA transition table)

- 상태: s0, s1, s2, se
- 입력: 0~9, 기타 문자
- δ(state, input) = next state  
  예: s0에서 숫자 → s1 / s1에서 숫자 → s2 / 완전히 자동 생성된 형태

#### 오른쪽 코드 — Skeleton recognizer (Table-driven scanner 핵심 구조)

```
Char ← next character
State ← s0
while (Char ≠ EOF)
    State ← δ(State, Char)
    Char ← next character
if (State is a final state)
    then report success
else report failure
```

- 문자 하나 읽고 상태 갱신 → EOF까지 반복 → 마지막 상태가 final이면 성공
- 상태 전이는 함수 δ로 처리, 실제 구현은 "테이블 lookup"

#### 🔥 핵심 비교

| 방식 | 특징 |
|------|------|
| Table-driven | 테이블 기반 DFA |
| Direct-coded | if/switch 기반 |

---

## 📋 7페이지 — Ease of Implementation & Performance

### Ease of Implementation & Performance
**구현 난이도와 성능**

#### Table-driven scanner
> "테이블 기반 스캐너는 오토마타를 큰 테이블로 표현한다"

- **Costly lookup** → 상태 + 입력 → 테이블 index 계산 필요, cache 효율 안 좋음
- **Easy, automated way to implement** → JLex 같은 도구가 이 방식
- **Hard to implement manually** → 직접 구현은 어렵다

#### Direct-coded scanner
> "직접 구현 스캐너는 프로그램 흐름 자체로 오토마타를 표현한다"

- if문 / switch문 자체가 상태 머신
- **Automated and manual implementations feasible** → 자동 생성도 가능하고 직접 구현도 가능
- **No table and thus no table lookup needed** → 테이블이 없어서 lookup 필요 없음
- **More complex control flow** → 제어 흐름이 더 복잡함
- **Ok for architectures with good branch prediction** → x86 같은 CPU에서는 괜찮다
- **Tends to be faster than table-driven scanner** → 일반적으로 더 빠름

#### 🔥 핵심 정리

| 방식 | 특징 |
|------|------|
| Table-driven | 구현 쉬움, 느림 |
| Direct-coded | 구현 어려움, 빠름 |

---

## 📋 8페이지 — JLex Example Spec

### JLex Example Spec
**JLex 예제 명세**

```
%%
LETTER=[a-zA-Z_]
DIGIT=[0-9]

"if" { return new Token(Token.IF, "if", src_pos); }
"<"  { ... }
"<=" { ... }
{LETTER}({LETTER}|{DIGIT})* { return new Token(Token.ID, "spelling", src_pos); }
```

- **LETTER=[a-zA-Z_]** → 알파벳 + 언더바
- **DIGIT=[0-9]** → 숫자
- **"if" { return new Token(Token.IF, ...) }** → keyword 처리, "if"가 나오면 IF 토큰 반환
- **"<"** → LESS 토큰
- **"<="** → LESS_EQ 토큰
- **{LETTER}({LETTER}|{DIGIT})\*** → 문자로 시작하고 이후 문자/숫자 반복 → **identifier 정의**
- **return new Token(Token.ID, ...)** → ID 토큰 반환

#### 두 가지 핵심 규칙 (Two rules)

1. **첫 번째 패턴 우선 (우선순위 = 위에 있는 규칙)**  
   여러 패턴이 매칭되면 첫 번째 사용 → 예: `if`는 identifier가 아니라 keyword(IF)로 처리

2. **Longest match (가장 긴 문자열 매칭)**  
   `<=` vs `<` → `<=` 선택됨

---

## 📋 9페이지 — NFA for JLex Example Spec

### NFA for JLex Example Spec
**JLex 예제의 NFA**

> "The NFAs for the different REs are combined as above"  
> 각 정규식의 NFA를 합친다

구조:
```
s0
├─ ε → if 패턴 NFA
├─ ε → < 패턴 NFA
├─ ε → <= 패턴 NFA
└─ ε → id 패턴 NFA
```

ε-transition으로 연결 → 하나의 큰 NFA로 합침 → 이후 DFA로 변환됨

> "Instead of an NFA, a DFA can also be used" → NFA 대신 DFA도 가능

#### 🖼 그림 설명
- 시작 상태 s0에서 여러 ε transition으로 각 패턴별 NFA로 분기

---

## 📋 10페이지 — NFA for JLex Example Spec (detail)

### NFA for JLex Example Spec (detail)
**JLex 예제 NFA 상세**

| 패턴 | 상태 전이 | 설명 |
|------|----------|------|
| if | s1 → s2 → s3 | i → f → "if" 인식 |
| < | s4 → s5 | "<" |
| <= | s6 → s7 → s8 | "<=" |
| identifier | s9 → s10 (loop) | LETTER → (LETTER or DIGIT 반복) |

#### 🔥 핵심 구조
- 하나의 시작 상태 s0에서 ε로 각 패턴 시작
- 각 패턴 NFA 따로 존재
- 최종적으로: 모든 토큰을 하나의 NFA로 합친 것

---

## 🔥 6~10페이지 핵심 요약

이 파트 핵심 3개:

1. **스캐너 구현 방식 2가지**: Table-driven / Direct-coded
2. **JLex 규칙**: 위에 있는 규칙 우선 / longest match
3. **NFA 구성**: 각 패턴 NFA 생성 → ε로 합쳐서 하나의 NFA

---

## 📋 11페이지 — Limitations of Regular Languages

### Limitations of Regular Languages
**정규언어의 한계**

이 페이지부터는 아주 중요하다. 지금까지는 정규표현식(RE)과 오토마타가 scanner를 만드는 데 얼마나 유용한지를 봤다. 그런데 여기서는 반대로, **"정규표현식이 그렇게 좋다면, 프로그래밍 언어 전체를 다 정규표현식으로 표현하면 되지 않나?"**라는 질문에 답하려고 한다.

이 슬라이드의 핵심 흐름:
- RE는 강력하다
- 하지만 모든 걸 표현할 수는 없다
- 그래서 컴파일러에는 scanner 말고 **parser가 따로 필요**하다

---

### Advantages of Regular Expressions
**정규표현식의 장점**

#### Simple & powerful notation for specifying patterns
패턴을 명시하기 위한 단순하면서도 강력한 표기법이다.

정규표현식은 짧은 문법으로 많은 문자열 집합을 표현할 수 있다. 예를 들어:
- `[0-9]+` → 숫자가 하나 이상
- `[a-zA-Z_][a-zA-Z0-9_]*` → identifier 형태

즉, RE의 장점은 **"문자열 패턴을 기술하는 데 매우 압축적이고 명확하다"**는 것이다.

#### Automatic construction of fast recognizers (scanners)
빠른 인식기(스캐너)를 자동으로 구성할 수 있다.

RE를 써 놓으면 거기서 끝나는 게 아니라:
```
RE → NFA → DFA → 최소 DFA → scanner code 생성
```
이런 과정을 통해 실제로 실행 가능한 스캐너를 만들 수 있다. 즉, 정규표현식은 이론용 기호가 아니라 자동화 도구(JLex, flex 등)와 바로 연결되는 실용적인 표현 방식이다.

#### Many patterns can be specified with REs
많은 패턴들을 정규표현식으로 명시할 수 있다.

scanner 단계에서 다룰 대부분의 토큰들은 RE로 충분히 표현 가능하다:
- 키워드: if, while, return
- identifier
- 정수 literal, 실수 literal
- 연산자: +, -, <=
- 구두점: ;, (, )

---

### Example — an expression grammar
예시 — 식(expression) 문법

교수님이 일부러 expression을 예로 든다. 왜냐하면 **expression은 딱 RE로는 부족하고 CFG가 필요한 대표 사례**이기 때문이다.

#### Term: `[a-zA-Z] ([a-zA-Z] | [0-9])*`
항(Term): 알파벳 하나로 시작하고, 그 뒤에 알파벳이나 숫자가 0개 이상 오는 형태

구조: 첫 글자 = 알파벳, 이후 = 알파벳 또는 숫자 반복  
→ abc, a1, x99 같은 문자열. 이건 정규표현식으로 잘 정의되는 부분이다.

#### Op: `+ | - | * | /`
연산자: + 또는 - 또는 * 또는 /  
이것도 역시 RE로 표현이 쉽다.

#### Expr: `( Term Op )* Term`
식: (Term Op)가 0번 이상 반복되고 마지막에 Term 하나가 오는 형태

표면적으로는 그럴듯해 보이지만, **괄호가 중첩되는 일반적인 expression 전체를 표현하지 못한다**. 예를 들면:
- `(a+b)`, `((a+b)*c)`, `a*(b+c)` 같은 구조는 단순히 `(Term Op)* Term`로는 안 된다.
- 왜냐하면 Term 안에 또 Expr가 들어갈 수 있어야 하기 때문이다.
- 즉, expression의 진짜 본질은 **재귀 구조**인데, RE는 그런 재귀적 중첩을 제대로 표현하지 못한다.

#### Of course, this would generate a DFA…
"그래, 이런 단순화된 형태는 DFA로 만들 수 있지. 그런데 진짜 프로그래밍 언어의 식 전체를 다룰 수 있느냐? **그건 아니다.**"

---

### If REs are so useful … Why not use them for everything?
정규표현식이 그렇게 유용하다면 — **왜 모든 것에 정규표현식을 쓰지 않는가?**

이 문장이 이 페이지의 핵심 질문이다. 이제부터는 **RE의 표현력 한계(expressive power)**를 설명하겠다는 예고다.

---

## 📋 12페이지 — Limitations of Regular Languages (cont.)

### Limitations of Regular Languages (cont.)
**정규언어의 한계 (계속)**

#### Regular expressions are limited in what can be expressed.
정규표현식은 표현할 수 있는 것에 한계가 있다.

핵심: RE로 표현 가능한 언어 / RE로 절대 표현 불가한 언어 — 이건 "실력 차이"가 아니라 **"형식 자체의 한계"**다.

---

#### Example: 0ⁿ1ⁿ
정규표현식으로 표현 **불가능**한 대표 예시

이 언어는 다음과 같다: 01 / 0011 / 000111 / 00001111 …  
조건: 앞에는 0만 / 뒤에는 1만 / **0의 개수와 1의 개수가 정확히 같아야 함**

문제는 마지막 조건이다. RE나 DFA는 문자열을 왼쪽에서 오른쪽으로 보면서 **현재 상태만 기억**한다. 0이 몇 개 나왔는지 무한히 정확하게 기억해 두었다가 뒤의 1 개수와 맞춰야 하므로, **유한한 상태만 가진 DFA/정규언어 체계로는 안 된다**.

---

#### For the same reason, we cannot specify the set of arithmetic expressions for which left and right parentheses match.
같은 이유로, 왼쪽 괄호와 오른쪽 괄호가 서로 정확히 맞는 산술식들의 집합도 정규표현식으로 명시할 수 없다.

예: `(a)` 맞음 / `((a))` 맞음 / `(()` 안 맞음 / `())` 안 맞음

이 "괄호 짝 맞추기" 문제는 0ⁿ1ⁿ와 본질이 같다:
- 열린 괄호 `(`를 몇 개 봤는지 기억해야 하고
- 닫힌 괄호 `)`가 나올 때 하나씩 대응시켜야 하며
- 중간에 중첩도 가능하기 때문이다

즉, RE는 "이 글자 다음엔 저 글자" 같은 **평면적인 패턴**에는 강하지만, "앞에서 열어 놓은 구조를 뒤에서 정확히 닫아야 한다" 같은 **계층적 구조**는 다루지 못한다.

**예시**: `(a)`, `((a))`, `(((a)))`, `((((a))))` — 중첩 깊이가 무한히 증가 가능

---

#### Regular expressions only usable to specify keywords, identifiers, literals, operators and punctuation characters of a programming language.
정규표현식은 프로그래밍 언어의 **키워드, 식별자, 리터럴, 연산자, 구두점 문자**를 명시하는 데에만 사용할 수 있다.

이 문장은 컴파일러 구조를 정확히 나눠준다:
- RE가 맡는 일 = **lexical level** (토큰 하나하나의 모양)

#### For everything else (expressions, statements, nested statements, …) we need a more powerful mechanism
그 밖의 모든 것들을 위해서는 **더 강력한 메커니즘**이 필요하다.

여기서 "more powerful mechanism"이 바로 **CFG와 parser**다. 왜냐하면:
- expression 안에 expression 들어감
- if문 안에 statement 들어감
- while문 안에 block 들어감
- block 안에 또 if/while 들어감

그래서 scanner 다음에 **parser가 반드시 필요**하다.

---

## 📋 13페이지 — Regular Expressions and Context-Free Grammars

### Regular Expressions and Context-Free Grammars
**정규표현식과 문맥자유문법**

여기서는 RE와 CFG를 단순 도구 비교가 아니라 **형식언어의 표현력 관점**에서 구분한다.

---

> "The 'languages' that can be defined by REs and Context-free grammars (CFGs) have been extensively studied by theoretical computer scientists."

정규표현식과 문맥자유문법으로 정의할 수 있는 "언어들"은 이론 컴퓨터과학자들에 의해 매우 광범위하게 연구되어 왔다.

여기서 "language"는 자연어가 아니라 **문자열 집합**이라는 뜻이다: identifier들의 집합 / 올바른 arithmetic expression들의 집합 / 괄호가 짝 맞는 문자열들의 집합 등.

---

#### RE are a "weaker" formalism than CFGs
정규표현식은 CFG보다 **"더 약한"** 형식 체계이다.

여기서 "weaker"는 성능이 나쁘다거나 쓸모없다는 뜻이 아니다. **표현할 수 있는 언어의 범위가 더 좁다**는 뜻이다.

> **RE로 표현 가능한 언어 ⊂ CFG로 표현 가능한 언어**

#### Any language expressible by a RE can be expressed by a CFG but not the other way around!
정규표현식으로 표현 가능한 모든 언어는 CFG로도 표현할 수 있지만, **그 반대는 성립하지 않는다**.

- regular language → CFG로 표현 가능
- 하지만 모든 CFG language가 regular인 건 아님
- 예: identifier 집합 → RE 가능, CFG도 가능 / 괄호 짝 맞는 문자열 → CFG 가능, **RE 불가**

즉 CFG가 **strictly more powerful** 하다. 그래서 parser는 scanner보다 더 강한 형식을 사용한다.

---

#### The languages expressible as RE are called regular languages
정규표현식으로 표현 가능한 언어들을 **정규언어**라고 부른다.
- RE로 표현 가능 = DFA/NFA로 인식 가능 = regular language

---

#### Generally: a language that exhibits "self embedding" cannot be expressed by a RE.
일반적으로 **"자기 내포(self embedding)"**를 보이는 언어는 정규표현식으로 표현할 수 없다.

self embedding이란 **구조 안에 같은 종류의 구조가 다시 들어가는 것**이다:
- expression 안에 expression
- statement 안에 statement
- parentheses 안에 parentheses

즉, "나와 같은 종류의 구조가 내 안에 또 들어온다"는 재귀적 성질이다.  
예: `expr → (expr)`

RE는 이런 자기 내포를 표현하지 못한다. 반면 자기 내포는 **깊이가 무한히 증가할 수 있는 계층 구조**를 요구한다.

---

#### Programming languages exhibit self embedding.
프로그래밍 언어는 자기 내포를 보인다.

이건 곧, **프로그래밍 언어는 RE만으로는 다룰 수 없다**는 말이다.  
즉, 프로그래밍 언어는 본질적으로 **parser가 필요하도록 설계**되어 있다.

---

#### Example: an expression can contain another expression
하나의 식은 또 다른 식을 포함할 수 있다 → self embedding의 대표 사례

예: `a+b` / `(a+b)*c` / `((a+b)*(c-d))` — 식 안에 식이 또 들어간다. 이게 parser가 필요한 이유다.

---

#### expr ::= id | integer | - expr | ( expr ) | expr op expr

| 규칙 | 의미 | 예시 |
|------|------|------|
| `expr ::= id` | 식은 식별자 하나 | x |
| `expr ::= integer` | 식은 정수 하나 | 3 |
| `expr ::= - expr` | 식 앞에 unary minus | -x, -(a+b) |
| `expr ::= ( expr )` | 괄호 안에 식 | (x+1) |
| `expr ::= expr op expr` | 식과 식 사이에 연산자 | a+b, x*y |

핵심: **expr의 정의 안에 또 expr이 등장** → 이게 재귀고, 이게 self embedding이다.

#### op ::= + | - | * | /
연산자(op)는 +, -, *, / 중 하나이다. 이 부분 자체는 RE로도 가능하다.

---

#### How many expressions can be derived? Infinitely many.
몇 개의 식이 유도될 수 있는가? **무한히 많다.**

재귀 때문에 표현 가능한 구조의 깊이에 제한이 없다는 뜻이다. 즉, expression grammar는 길이만 긴 게 아니라 **구조가 무한히 중첩**될 수 있다. 이런 성질이 regular language의 범위를 넘는다.

---

## 📋 14페이지 — Extra Materials: Training for Lexical Analysis

### Extra Materials: Training for Lexical Analysis
**추가 자료: Lexical Analysis 연습**

이 페이지는 본강의 내용이라기보다 **추가 연습 파트가 시작된다는 표지**다.

- 앞 11~13페이지: 이론 설명
- 15페이지부터: 연습문제

#### 🖼 그림 설명
- 중앙 큰 제목: Extra Materials
- 그 아래: Training for Lexical Analysis
- 하단: 학교 로고

1페이지와 마찬가지로 실질 내용보다는 **"이제 연습 섹션 시작"**을 알려주는 표지 역할이다.

---

## 📋 15페이지 — Writing Regular Expressions

### Writing Regular Expressions
**정규표현식 작성하기**

이제부터는 앞에서 배운 내용을 실제로 써보는 연습이다.

> Write a regular expression for each of the following sets of tokens:  
> 다음 각각의 토큰 집합에 대해 정규표현식을 작성하시오.

정규식을 쓸 때 확인해야 할 것들:
- 반드시 특정 접두어가 있어야 하는지
- 반복이 되는지
- underscore가 어디에나 가능한지
- 마지막 글자 제약이 있는지

---

#### 1) Ruby binary literals
"0b" 다음에 이진수가 오는 Ruby의 이진 리터럴  
예: `0b001011`, `0b01`

#### 2) Ruby binary literals (with optional underscore)
두 개의 이진 숫자 사이에 선택적으로 underscore `_`가 들어갈 수 있는 Ruby 이진 리터럴  
예: `0b0_101`, `0b11_01` 가능 / `0b_1`, `0b1_` 불가

#### 3) Ada identifiers
문자(letter) 하나로 시작하고, 그 뒤에 문자·숫자·underscore가 임의 개수 올 수 있다.  
단, **underscore로 끝나면 안 되고**, **underscore가 두 번 연속 나와서도 안 된다**.

#### 4) Floating-point number
하나 이상의 숫자(정수부) 뒤에 소수점 `.`이 오고, 그 뒤에 하나 이상의 숫자(소수부)가 오는 형태  
예: `2.24`, `0.1234`

#### 5) Floating-point number in scientific notation
위와 같은 부동소수점 수 뒤에, 선택적으로 `e` 또는 `E`와 부호 있는 정수 지수가 따라올 수 있다.  
예: `1.2e-2`, `2.3E+34`, `2.3E34`

---

## 📋 16페이지 — 연습문제 1번: Ruby Binary Literals

### 1) Ruby binary literals consisting of "0b" followed by the binary number.
**"0b" 다음에 이진수가 오는 Ruby의 이진 리터럴**  
예: `0b001011`, `0b01`

#### 문제 의미 설명

| 허용 | 이유 |
|------|------|
| 0b0 | 조건 만족 |
| 0b1 | 조건 만족 |
| 0b01 | 조건 만족 |
| 0b101010 | 조건 만족 |

| 불허 | 이유 |
|------|------|
| 0b | 뒤에 이진수 없음 |
| 0b102 | 2가 들어감 |
| 0B01 | 대문자 B |
| 00b01 | 시작 형식 다름 |

#### 정규표현식

```
0b[01]+
```

또는 동일한 표현:

```
0b(0|1)+
```

#### 왜 `+`가 필요한가?
- `[01]*` 라고 쓰면 `0b` 뒤에 아무것도 없는 경우도 허용됨
- 예시와 문제 문맥상 binary number가 와야 하므로 **최소 1자리 필요**
- 따라서 `[01]+`이 맞다

---

## 📋 17페이지 — 연습문제 2번: Ruby Binary Literals (with optional underscore)

### 2) Ruby binary literals, with an optional underscore ("_") between a pair of binary digits.
**두 개의 이진 숫자 사이에 선택적으로 underscore가 들어갈 수 있는 Ruby 이진 리터럴**  
예: `0b0_101`, `0b11_01` 가능 / `0b_1`, `0b1_` 불가

#### 문제 의미 설명

핵심: `_`는 아무 데나 붙는 게 아니라, **반드시 binary digit와 binary digit 사이에만** 올 수 있다.

| 허용 | 이유 |
|------|------|
| 0b0_1 | digit _ digit |
| 0b10_10 | digit 사이 underscore |
| 0b0_101 | digit 사이 underscore |

| 불허 | 이유 |
|------|------|
| 0b_1 | 시작 직후 underscore (앞쪽 digit 없음) |
| 0b1_ | 끝이 underscore (뒤쪽 digit 없음) |
| 0b__1 | underscore 연속 |
| 0b0__1 | 연속 underscore |

#### 잘못된 접근 (함정)

```
0b[01_]+   ← 틀림!
```

이렇게 쓰면 `0b_1`, `0b1_`, `0b___` 같은 것도 허용해 버린다. 단순 허용 문자 집합 나열만으로는 **위치 제약을 반영 못함**.

#### 정확한 정규표현식

```
0b[01](_?[01])*
```

구조 분석:
- 첫 글자는 반드시 `[01]` → `0b_1` 막힘
- 반복 단위 `(_?[01])`: underscore가 오면 반드시 뒤에 `[01]`가 따라옴 → `0b1_` 막힘
- underscore 연속 불가 (`_?`는 최대 하나) → `0b0__1` 막힘

---

## 📋 18페이지 — 연습문제 3번: Ada Identifiers

### 3) Ada identifiers: a letter followed by any number of letters, digits, and underlines.
**Ada 식별자: 문자 하나로 시작하고, 그 뒤에 문자, 숫자, underscore가 임의 개수 올 수 있다.**  
단, **underscore로 끝나면 안 되고**, **underscore가 두 번 연속 나와서도 안 된다**.

#### 문제 의미 설명

단순히 쓰면 틀리기 쉬운 함정 문제다. 처음 보면 이렇게 쓰고 싶어진다:

```
[a-zA-Z][a-zA-Z0-9_]*   ← 틀림!
```

이 식은 `abc_`, `ab__cd` 같은 금지된 패턴도 허용해 버린다.

| 조건 | 예시 불허 | 이유 |
|------|----------|------|
| underscore로 끝나면 안 됨 | `abc_`, `x1_` | 끝 underscore |
| underscore 두 번 연속 금지 | `ab__cd`, `x__1` | 연속 underscore |

| 허용 | 불허 |
|------|------|
| a, abc, a1, a_b | _abc (시작이 letter 아님) |
| a1_b2_c3 | abc_ (끝 underscore) |
| | ab__cd (연속 underscore) |

#### 핵심 사고법

underscore를 "마음대로 반복 가능한 문자"로 보면 안 된다. underscore는 **오직 정상 문자 사이를 이어주는 연결 문자**처럼 생각해야 한다.

즉 구조:
- underscore가 오려면 반드시 그 뒤에 letter 또는 digit가 와야 함

#### 정규표현식

```
[a-zA-Z]([a-zA-Z0-9]|_[a-zA-Z0-9])*
```

왜 이 식이 맞는가:
- 시작 문자 `[a-zA-Z]`: 반드시 letter로 시작
- 반복 단위 `([a-zA-Z0-9]|_[a-zA-Z0-9])`:
  - 그냥 letter/digit 하나 오거나
  - underscore + letter/digit 오거나
- 이렇게 하면: `_` 혼자 끝에 못 옴 / `__` 불가 / underscore 뒤에는 무조건 letter/digit가 옴

---

## 📋 19페이지 — 연습문제 4번: Floating-point Number

### 4) A floating-point number: one or more digits (whole-number part) followed by a decimal point (".") and one or more digits (fractional part).
**부동소수점 수**: 하나 이상의 숫자(정수부) 뒤에 소수점 `.`이 오고, 그 뒤에 하나 이상의 숫자(소수부)가 오는 형태  
예: `2.24`, `0.1234`

#### 핵심 제약 세 가지

1. 정수부가 최소 1자리 있어야 함
2. 소수점이 반드시 있어야 함
3. 소수부도 최소 1자리 있어야 함

#### 정규표현식

```
[0-9]+\.[0-9]+
```

| 부분 | 정규식 | 이유 |
|------|--------|------|
| 정수부 | `[0-9]+` | one or more digits |
| 소수점 | `\.` | 실제 마침표 문자 (`.`는 메타문자라 escape 필요) |
| 소수부 | `[0-9]+` | one or more digits |

#### 왜 점을 escape해야 하나?
정규표현식에서 `.`은 "아무 문자 하나"라는 특별한 의미를 가진다. 실제 소수점 문자 `.` 자체를 의미하려면 반드시 `\.`로 써야 한다.

| 허용 | 불허 | 이유 |
|------|------|------|
| 2.24, 0.1234 | .5 | 정수부 없음 |
| | 5. | 소수부 없음 |
| | 12 | 소수점 없음 |
| | 12.a | 소수부가 digit 아님 |

---

## 📋 20페이지 — 연습문제 5번: Floating-point in Scientific Notation

### 5) Floating-point number in scientific notation: same as above, but optionally followed by "e" or "E", and a signed integer exponent.
**과학적 표기법의 부동소수점 수**: 위와 같되, 선택적으로 `e` 또는 `E`와 부호 있는 정수 지수가 따라올 수 있다.  
예: `1.2e-2`, `2.3E+34`, `2.3E34`

#### 구조

기본 뼈대 (19페이지) + optional exponent suffix:

```
[0-9]+\.[0-9]+([eE][+-]?[0-9]+)?
```

| 부분 | 정규식 | 이유 |
|------|--------|------|
| 기본 float | `[0-9]+\.[0-9]+` | 19페이지와 동일 |
| exponent 전체 | `([eE][+-]?[0-9]+)?` | optional |
| e 또는 E | `[eE]` | 둘 다 가능 |
| 부호 (optional) | `[+-]?` | 있어도 되고 없어도 됨 |
| 지수 숫자 | `[0-9]+` | 최소 1자리 이상 |

#### examples 해석

| 예시 | 해석 |
|------|------|
| 1.2e-2 | 기본 float 1.2 + 지수 e-2 |
| 2.3E+34 | 기본 float 2.3 + 지수 E+34 (양수 부호 명시) |
| 2.3E34 | 기본 float 2.3 + 지수 E34 (부호 생략) |

#### 불허 예시

| 불허 | 이유 |
|------|------|
| 1.2e | 지수 숫자 없음 |
| 1.2e+ | 부호만 있고 숫자 없음 |
| 1.2e+3.4 | exponent는 정수여야 함 |
| .2e3 | 기본 float 조건 위반 |
| 2.e3 | 기본 float 조건 위반 |

---

## 🔥 16~20페이지 핵심 정리

| 문제 | 정규표현식 |
|------|-----------|
| 16페이지 — Ruby binary | `0b[01]+` |
| 17페이지 — Ruby binary + underscore | `0b[01](_?[01])*` |
| 18페이지 — Ada identifier | `[a-zA-Z]([a-zA-Z0-9]|_[a-zA-Z0-9])*` |
| 19페이지 — Floating-point | `[0-9]+\.[0-9]+` |
| 20페이지 — Scientific notation | `[0-9]+\.[0-9]+([eE][+-]?[0-9]+)?` |

---

## 📋 21페이지 — Subset Construction with Animation

### Subset Construction with Animation
**부분집합 구성법 (애니메이션)**

> **Reminder) subset construction: NFA to DFA**  
> 복습: subset construction은 NFA를 DFA로 변환하는 방법이다

NFA의 핵심 특징:
- 같은 입력에서 **여러 경로 가능**
- 예: s1에서 a 입력 → s1 갈 수도 있고 s2 갈 수도 있음 → 이걸 "guess"라고 표현

---

#### Instead of guessing in state s1 on symbol a, we can follow both transitions in parallel.
상태 s1에서 입력 a가 들어왔을 때 추측하는 대신, **우리는 두 경로를 동시에 따라갈 수 있다**.

NFA의 비결정성을 제거하는 핵심 아이디어: "하나만 고르는 게 아니라 **둘 다 간다**고 생각한다"

---

#### We introduce a "virtual state"
**우리는 "가상 상태"를 도입한다**

- 새로운 개념: `{s1, s2}` — 여러 상태를 묶은 하나의 상태
- DFA에서는 상태 하나가 실제로는 **NFA 상태들의 집합**이 된다
- 표기: `{s1, s2}` (집합으로 표현)

---

#### A question: if we are in {s1, s2}, where can we go on b?
질문: 우리가 `{s1, s2}` 상태에 있을 때 b를 읽으면 어디로 가는가?

> **Answer: wherever s1 or s2 can go**  
> 답: s1이나 s2가 갈 수 있는 **모든 상태로** 간다

```
Move({s1, s2}, b) = Move(s1, b) ∪ Move(s2, b)
```

#### 🖼 그림 설명
- 상태 s1에서 a → s1 또는 s2
- 상태 s2에서 b → s3
- 최종 s4는 accepting state
- NFA는 "갈림길 존재" → DFA는 "갈림길 제거 → 상태 묶기"

---

## 📋 22페이지 — Example: Simulating an NFA "on the fly"

### Example: Simulating an NFA "on the fly"
**예: NFA를 즉석에서 시뮬레이션하기**

#### On-the-fly simulation: useful when a regular expression is used only once
NFA를 즉석에서 시뮬레이션하는 것은 **정규표현식이 한 번만 사용될 때 유용하다**

용도 예시: IDE의 find / grep — DFA로 변환 안 하고 그냥 NFA로 처리 가능

---

#### In a compiler, ... used over and over again → need a more efficient approach
컴파일러에서는 정규표현식이 **반복적으로 사용**된다 → 더 효율적인 방법이 필요하다 → **DFA 사용**

scanner는 모든 입력에 대해 계속 사용됨

#### 🔥 핵심 비교

| 방식 | 특징 |
|------|------|
| NFA 직접 사용 | 간단, 느림 |
| DFA 변환 후 사용 | 복잡, 빠름 |

#### 🖼 그림 설명
- s0 → s1 → s2 → s3 → s4 (입력: a, b, b)
- 문자열 "abb" 처리 과정 — NFA는 여러 경로 시도 가능

---

## 📋 23페이지 — Algorithm: NFA → DFA with Subset Construction

### Algorithm: NFA → DFA with Subset Construction
**알고리즘: subset construction으로 NFA → DFA**

#### 핵심 개념

- **Subset construction works on sets of NFA states**: DFA 상태 = NFA 상태 집합
- **Each set of NFA states becomes a DFA state**: 예: `{s0, s1}`, `{s1, s2}`, `{s1}`

#### 두 가지 핵심 함수 (Two key functions)

| 함수 | 의미 |
|------|------|
| **Move(S, a)** | 상태 집합 S에서 입력 a로 갈 수 있는 상태 집합 |
| **ε-closure(S)** | ε-transition(입력 없이 이동)으로 도달 가능한 모든 상태 집합 |

#### 알고리즘 흐름

1. **Start state = ε-closure({s0})**: 시작 상태는 s0의 ε-closure (그냥 s0가 아니라 ε로 갈 수 있는 모든 상태 포함)
2. **Compute Move(S0, α)**: 각 입력 α에 대해 Move 계산
3. **take ε-closure**: 그 결과에 대해 ε-closure 적용
4. **Iterate until no more states**: 새 상태가 안 생길 때까지 반복

---

## 📋 24페이지 — 알고리즘 상세 코드

### 알고리즘 코드

```
Dstates ← {}
add ε-closure(s0) as unmarked state to Dstates

while (unmarked state T exists)
    mark T
    for each α ∈ Σ
        U ← ε-closure(Move(T, α))
        if (U ∉ Dstates) add U
        δ[T, α] ← U
```

#### 각 줄 해석

| 코드 | 해석 |
|------|------|
| `Dstates ← {}` | DFA 상태 집합 초기화 |
| `add ε-closure(s0)` | 시작 상태 추가 |
| `while (unmarked T exists)` | 아직 처리 안 한 상태가 있으면 반복 |
| `mark T` | 현재 상태 처리 완료 표시 |
| `for each α ∈ Σ` | 모든 입력 문자에 대해 |
| `U ← ε-closure(Move(T, α))` | **핵심**: Move → ε-closure 순서로 계산 |
| `if (U ∉ Dstates) add U` | 새 상태면 추가 |
| `δ[T, α] ← U` | transition 기록 |

이건 그냥 외우는 게 아니라 **상태 확장 과정 이해**해야 함

---

## 📋 25페이지 — 알고리즘 시작 상태

### 초기 상태 설정

```
Dstates = {}
ε-closure(s0) = {s0, s1}
```

초기 상태는 `{s0, s1}` — 왜 s1까지 포함되는가?

> **ε-transition 때문**: s0에서 입력 없이 s1 갈 수 있음

- 시작 상태는 단일 상태가 아니라 **집합 상태**
- `add as unmarked state` → 미처리 상태로 추가

#### 🖼 그림 설명
- s0 → ε → s1
- DFA 시작 상태: **ε-closure(s0)** ← 시험 포인트

---

## 🔥 21~25페이지 전체 핵심 요약

1. **핵심 아이디어**: NFA는 여러 경로 / DFA는 하나의 경로 → 해결: 여러 상태를 하나로 묶는다

2. **DFA 상태 정의**: DFA state = NFA 상태 집합

3. **핵심 함수**:

| 함수 | 의미 |
|------|------|
| `Move(S, a)` | 상태 집합 S에서 a로 이동 가능한 상태들 |
| `ε-closure(S)` | ε 전이로 도달 가능한 모든 상태들 |

4. **알고리즘 흐름**:
   - 초기: S0 = ε-closure(s0)
   - 반복: U = ε-closure(Move(T, α))
   - 새 상태면 추가

5. **중요한 포인트**: "guess 하지 않는다" → "모든 가능성을 동시에 포함한다"

---

## 🔥 전체 강의 핵심 요약 (1~25페이지)

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

### RE의 한계

| RE로 잘 되는 것 | RE로 안 되는 것 |
|----------------|----------------|
| keyword | 0ⁿ1ⁿ |
| identifier | 괄호 짝 맞추기 |
| literal | 중첩된 expression/statement 전체 |
| operator, punctuation | self embedding 구조 |

### 이론 관계
- **RE < CFG** — 모든 regular language는 CFG로 표현 가능, 하지만 모든 CFL이 regular인 건 아님

### 정규표현식 문제 정답 모음

| 문제 | 정규표현식 |
|------|-----------|
| Ruby binary | `0b[01]+` |
| Ruby binary + `_` | `0b[01](_?[01])*` |
| Ada identifier | `[a-zA-Z]([a-zA-Z0-9]|_[a-zA-Z0-9])*` |
| Floating-point | `[0-9]+\.[0-9]+` |
| Scientific notation | `[0-9]+\.[0-9]+([eE][+-]?[0-9]+)?` |

### Subset Construction 시험 포인트
- `Move(T, α)`: 상태 집합 T에서 α로 이동하는 상태들
- `ε-closure(T)`: ε 전이로 도달 가능한 모든 상태들
- 반복: 더 이상 상태 추가 없을 때까지 (fixed-point)
- DFA 시작 상태: **반드시 ε-closure(s0)**


# COMP321 Compiler — Lexical Analysis Part 3
**Kyungpook National University | Hwisoo So | Spring 2026**

---

## 📋 26페이지 — 시작 상태 확인

### 현재 상태

```
Dstates = { {s0, s1} }
```

DFA 상태 집합에는 현재 `{s0, s1}` 하나만 있다.

---

#### Dstates contains now one element…
Dstates에는 현재 하나의 상태 `{s0, s1}`가 있다.

이 상태는 어디서 왔냐?

```
ε-closure(s0) = {s0, s1}
```

즉 **시작 상태**다.

---

#### Note1: unmarked states are printed in red
아직 처리되지 않은 상태는 빨간색으로 표시된다.

#### Note2: Dstates means "deterministic states"
Dstates는 **DFA 상태들**을 의미한다.

---

#### 🔥 핵심

| 현재 상태 | 처리 여부 |
|----------|----------|
| `{s0, s1}` | 아직 처리 안 함 (unmarked) |

---

## 📋 27페이지 — 첫 상태 처리 시작

### Now we pick state {s0, s1} and mark it
이제 `{s0, s1}` 상태를 선택하고 **처리 완료로 표시**한다.

subset construction 핵심 흐름:
1. unmarked 상태 선택
2. 처리
3. mark

#### marked states are printed in green
처리된 상태는 초록색으로 표시된다.

#### 🔥 핵심
상태 `{s0, s1}` → 이제 처리 시작 → 이후 transition 계산할 대상

---

## 📋 28페이지 — 입력 집합 확인

### T = {s0, s1}, Σ = {a, b}
현재 상태 T는 `{s0, s1}`, 입력 집합은 `{a, b}`

DFA는 **모든 입력에 대해 transition**이 필요하다. 즉:
- a에 대해? → 계산 필요
- b에 대해? → 계산 필요

#### The for loop iterates over all symbols
for문은 모든 입력 문자에 대해 반복한다.

#### 🔥 핵심 — 지금 해야 할 것

```
Move({s0, s1}, a) = ?
Move({s0, s1}, b) = ?
```

---

## 📋 29페이지 — α = a 계산

### Move(T, a) = {s1, s2}
`{s0, s1}`에서 a를 읽으면 `{s1, s2}`로 간다.

#### 왜 이렇게 되는가? 계산 과정

| 상태 | a 입력 | 결과 |
|------|--------|------|
| s0에서 a | s0 → s1 | s1 |
| s1에서 a | s1 → s1, s1 → s2 | s1, s2 |

합치면: `{s1, s2}`

---

#### ε-closure({s1, s2}) = {s1, s2}
ε-transition으로 더 갈 곳 없음 → 그대로 `{s1, s2}`

#### U = {s1, s2}
다음 상태는 `{s1, s2}`

#### 🔥 핵심

```
δ({s0,s1}, a) = {s1, s2}
```

---

## 📋 30페이지 — 새 상태 추가

### State U is not in Dstates → add it
이 상태 `{s1, s2}`는 아직 없으므로 **추가**한다.

#### Dstates 업데이트

```
이전: Dstates = { {s0, s1} }
      ↓
이후: Dstates = { {s0, s1}, {s1, s2} }
```

#### 🖼 그림 설명
`{s0, s1}` --a--> `{s1, s2}`

#### 🔥 핵심
DFA 상태 확장 시작됨

---

## 🔥 26~30페이지 전체 흐름 요약

| 단계 | 내용 |
|------|------|
| 1. 시작 상태 | `{s0, s1}` = ε-closure(s0) |
| 2. 처리 시작 | T = `{s0, s1}` mark |
| 3. a에 대해 | Move(`{s0,s1}`, a) = `{s1, s2}` |
| 4. ε-closure | = `{s1, s2}` |
| 5. 상태 추가 | Dstates = `{ {s0,s1}, {s1,s2} }` |

#### 이 구간 핵심 감각

- **NFA는 "갈림길"** → **DFA는 "모든 갈림길을 한 번에 포함"**
- 한 상태 = 여러 상태의 묶음

#### 🔥 시험 포인트

| 해야 할 것 | 내용 |
|-----------|------|
| Move 계산 | 각 상태에서 갈 수 있는 모든 상태 합집합 |
| ε-closure 적용 | 입력 없이 갈 수 있는 상태까지 포함 |
| 새로운 상태 판별 | 없으면 추가 |

---

## 📋 31페이지 — 전이 함수 δ 구성 시작

### Here we start assembling the transition function δ
이제 **전이 함수 δ를 구성하기 시작**한다.

지금까지 한 건 "상태 찾기"였고, 이제부터는 **"전이표 만들기"**다.

---

#### If we read an a in state T, then DFA moves to {s1, s2}
상태 T에서 a를 읽으면 DFA는 `{s1, s2}`로 이동한다.

이미 구한 것:

```
δ({s0, s1}, a) = {s1, s2}
```

#### δ 전이표 (현재)

| 상태 | a | b |
|------|---|---|
| `{s0,s1}` | `{s1,s2}` | |

#### 🔥 핵심
DFA transition table 만들기 시작

---

## 📋 32페이지 — b 처리 시작

### 현재 상태

```
Dstates = { {s0, s1}, {s1, s2} }
```

#### Second iteration: α = b
두 번째 반복: **입력 b**

- a는 끝났고
- 이제 b 처리 차례

#### 🔥 핵심 — 지금 해야 할 것

```
Move({s0,s1}, b) = ?
```

---

## 📋 33페이지 — α = b 계산

### Move(T, b) = {s1}
`{s0, s1}`에서 b를 읽으면 `{s1}`로 간다.

#### 왜 이렇게 되는가? 계산 과정

| 상태 | b 입력 | 결과 |
|------|--------|------|
| s0에서 b | 이동 없음 | — |
| s1에서 b | s1 → s1 | s1 |

결과: `{s1}`

---

#### ε-closure({s1}) = {s1}
ε 이동 없음 → 그대로 `{s1}`

#### 🔥 핵심

```
δ({s0,s1}, b) = {s1}
```

---

## 📋 34페이지 — 새 상태 {s1} 추가

### State U is not in Dstates → add it
`{s1}`는 아직 없으므로 **추가**한다.

#### Dstates 업데이트

```
이전: Dstates = { {s0,s1}, {s1,s2} }
      ↓
이후: Dstates = { {s0,s1}, {s1,s2}, {s1} }
```

#### 🔥 핵심
새로운 DFA 상태 `{s1}` 등장

---

## 📋 35페이지 — δ 테이블 업데이트

### If we read b in state T, DFA moves to {s1}
상태 T에서 b를 읽으면 `{s1}`로 이동한다.

#### δ 전이표 (업데이트)

| 상태 | a | b |
|------|---|---|
| `{s0,s1}` | `{s1,s2}` | `{s1}` |

첫 번째 상태 `{s0,s1}`에 대한 transition **완성**

---

## 🔥 31~35페이지 전체 흐름 요약

#### 상태 {s0,s1} 처리 완료

| 입력 | 결과 |
|------|------|
| a | `{s1,s2}` |
| b | `{s1}` |

#### 현재 DFA 상태

```
{s0,s1}   → (완료)
{s1,s2}   → (미처리)
{s1}      → (미처리)
```

#### 현재 전이 구조

```
{s0,s1}
  ├─ a → {s1,s2}
  └─ b → {s1}
```

#### 🔥 시험 핵심 포인트

| 실수 유형 | 내용 |
|----------|------|
| ❌ s0에서 b 안 가는데 포함시키는 경우 | s0 → b 이동 없음 확인 필수 |
| ❌ ε-closure 빼먹는 경우 | Move 후 반드시 ε-closure 적용 |
| ❌ 기존 상태인데 또 추가하는 경우 | 이미 있으면 절대 추가 안 함 |

---

## 📋 36페이지 — 다음 처리 대상 선택

### 현재 상태

```
Dstates = { {s0,s1}, {s1,s2}, {s1} }
```

#### Dstates contains now two unmarked states: {s1,s2} and {s1}
아직 처리 안 된 상태는 `{s1,s2}`와 `{s1}` 두 개

| 상태 | 처리 여부 |
|------|----------|
| `{s0,s1}` | ✔ 완료 |
| `{s1,s2}` | ❌ 미처리 |
| `{s1}` | ❌ 미처리 |

다음 처리 대상: **T = {s1, s2}**

#### 🔥 핵심
이제 `{s1,s2}` 상태를 처리해야 함

---

## 📋 37페이지 — {s1,s2} 처리 시작

### T = {s1, s2}
현재 처리할 상태는 `{s1,s2}`

#### 해야 할 것

```
Move({s1,s2}, a) = ?
Move({s1,s2}, b) = ?
```

#### 🔥 핵심
새로운 상태 만들어질 가능성 있음

---

## 📋 38페이지 — α = a 계산

### α = a
입력 a에 대해 계산

#### 계산 과정

| 상태 | a 입력 | 결과 |
|------|--------|------|
| s1에서 a | s1 → s1, s1 → s2 | s1, s2 |
| s2에서 a | 이동 없음 | — |

결과: `{s1, s2}`

---

#### ε-closure({s1, s2}) = {s1, s2}
추가 ε 이동 없음 → 그대로 `{s1, s2}`

#### 🔥 핵심

```
δ({s1,s2}, a) = {s1,s2}
```

👉 자기 자신으로 돌아옴 **(self-loop)**

---

## 📋 39페이지 — 중복 상태 확인

### U = {s1,s2} already in Dstates
이 상태는 **이미 존재**함

- 새로운 상태가 아님
- Dstates 변화 없음

#### 🔥 핵심
기존 상태면 **추가 안 함** — 전이 기록만 함

---

## 📋 40페이지 — 처리 완료 (a)

### Nothing to be done here
추가 작업 없음 — 이미 있는 상태 → skip

#### 현재까지 transition

```
{s1,s2} --a--> {s1,s2}   (self-loop)
```

---

## 🔥 36~40페이지 전체 흐름 요약

| 단계 | 내용 |
|------|------|
| 1. 처리 대상 | T = `{s1,s2}` |
| 2. a 입력 | Move(`{s1,s2}`, a) = `{s1,s2}` |
| 3. ε-closure 적용 | = `{s1,s2}` |
| 4. 상태 존재 여부 | 이미 있음 → 추가 X |
| 5. transition 추가 | δ(`{s1,s2}`, a) = `{s1,s2}` |

#### 현재 누적 전이

```
{s0,s1}
  ├─ a → {s1,s2}
  └─ b → {s1}

{s1,s2}
  └─ a → {s1,s2}   (self-loop)
```

#### 🔥 중요한 패턴 — self-loop

```
{s1,s2} --a--> {s1,s2}
```

이런 구조는 **상태 안정화** 느낌 — 시험에서 자주 나오는 구조

#### 이 구간 핵심 포인트

1. **상태 중복 체크**: 이미 있으면 절대 추가하지 않음
2. **self-loop 이해**: 상태가 자기 자신으로 돌아올 수 있음
3. **Move 계산 정확히**: 집합 안 모든 상태 다 고려해야 함

---

## 📋 41페이지 — δ 표 확정 (a 부분)

### 현재 δ 전이표

| 상태 | a | b |
|------|---|---|
| `{s0,s1}` | `{s1,s2}` | `{s1}` |
| `{s1,s2}` | `{s1,s2}` | |

`{s1,s2}`에서 a에 대한 계산 결과를 전이표에 공식 반영한 단계.

#### 왜 자기 자신으로 가는가?

```
s1에서 a → s1, s2
s2에서 a → 이동 없음
합치면: {s1, s2}
```

즉 `{s1,s2}`에서 a를 읽어도 그대로 `{s1,s2}`에 머문다 → **self-loop**

#### 🔥 핵심

```
{s1,s2} --a--> {s1,s2}
```

---

## 📋 42페이지 — α = b 계산 시작

### T = {s1, s2}  α = b
현재 상태는 `{s1,s2}`, 이번에는 **입력 b**에 대해 계산한다.

- a는 끝났고
- 남은 입력 b를 처리하는 차례

#### 해야 할 계산

```
Move({s1,s2}, b) = ?
```

여기서 **새 상태가 나올 가능성**이 있다.

#### 🔥 핵심
상태: `{s1,s2}` / 입력: `b` → 계산 시작

---

## 📋 43페이지 — 새 상태 {s1,s3} 등장

### U = {s1, s3}
다음 상태 U는 **{s1, s3}**이다.

#### 왜 이렇게 되는가? 계산 과정

```
Move({s1,s2}, b):
  s1에서 b → s1 → s1
  s2에서 b → s2 → s3

합치면: {s1, s3}
```

#### ε-closure({s1,s3}) = {s1,s3}
추가 ε 이동 없음 → 그대로 `{s1, s3}`

---

#### 이 상태가 중요한 이유

| 상태 | 의미 |
|------|------|
| s1 | 계속 반복 구조 쪽 상태 |
| s3 | accepting state s4 **바로 직전** 상태 |

즉 `{s1,s3}`는 **"아직 반복도 가능하고, 한편으로는 수용 상태에 가까워진 상태"**다.

#### 🔥 핵심

```
δ({s1,s2}, b) = {s1,s3}
```

---

## 📋 44페이지 — 새 상태 여부 확인

### 현재 상황

```
U = {s1, s3}
T = {s1,s2}
α = b
Dstates = { {s0,s1}, {s1,s2}, {s1} }
```

현재 Dstates에는 `{s1,s3}`가 **들어 있지 않다**.

#### 결론

```
{s1,s3} 는 새로운 DFA 상태 → 추가 필요
```

---

## 📋 45페이지 — Dstates 업데이트

### 업데이트 결과

```
Dstates = { {s0,s1}, {s1,s2}, {s1}, {s1,s3} }
```

DFA 상태 집합이 이제 **네 개**가 된다.

#### δ 전이표 업데이트

| 상태 | a | b |
|------|---|---|
| `{s0,s1}` | `{s1,s2}` | `{s1}` |
| `{s1,s2}` | `{s1,s2}` | `{s1,s3}` |

`δ({s1,s2}, b) = {s1,s3}` 공식 반영 완료.

#### 이 상태가 중요한 이유

`{s1,s3}`는 앞으로 입력 b를 하나 더 읽으면 **s4(accepting) 쪽**으로 갈 수 있다.  
즉, 이제 DFA가 accepting NFA state를 포함하는 상태로 이어질 준비를 한 셈이다.

---

## 🔥 41~45페이지 전체 흐름 요약

| 단계 | 내용 |
|------|------|
| 1. `{s1,s2}`에서 a | δ(`{s1,s2}`, a) = `{s1,s2}` → self-loop |
| 2. `{s1,s2}`에서 b | Move(`{s1,s2}`, b) = `{s1,s3}` |
| 3. ε-closure 적용 | = `{s1,s3}` |
| 4. 상태 추가 | Dstates = `{ {s0,s1}, {s1,s2}, {s1}, {s1,s3} }` |
| 5. 전이표 업데이트 | δ(`{s1,s2}`, b) = `{s1,s3}` |

#### 현재까지 전체 DFA 구조

```
{s0,s1}
  ├─ a → {s1,s2}
  └─ b → {s1}

{s1,s2}
  ├─ a → {s1,s2}   (self-loop)
  └─ b → {s1,s3}
```

#### 🔥 시험에서 중요한 포인트

| 포인트 | 설명 |
|--------|------|
| 여러 상태의 이동은 합집합 | Move(`{s1,s2}`, b) = Move(s1,b) ∪ Move(s2,b) |
| 기존 상태인지 항상 확인 | 이미 있으면 추가 X, 없으면 추가 O |
| accepting 포함 여부 나중에 체크 | 현재 `{s1,s3}`는 아직 s4 없음, 곧 `{s1,s4}` 등장 예정 |

---

## 📋 46페이지 — 다음 처리 대상: {s1}

### 현재 상태

```
Dstates = { {s0,s1}, {s1,s2}, {s1}, {s1,s3} }
```

| 상태 | 처리 여부 |
|------|----------|
| `{s0,s1}` | ✔ 완료 |
| `{s1,s2}` | ✔ 완료 |
| `{s1}` | ❌ 미처리 |
| `{s1,s3}` | ❌ 미처리 |

---

#### { s1 } is the next unmarked state in Dstates.
`{s1}`이 Dstates에서 다음으로 처리할 **미표시(unmarked) 상태**이다.

subset construction의 흐름:
1. 아직 처리 안 한 상태 하나 고름
2. 그 상태에서 입력 문자 전부에 대해 Move 계산
3. 결과 상태를 추가/기록
4. mark 처리

#### 🔥 핵심

```
다음 처리 대상: T = {s1}
```

---

## 📋 47페이지 — {s1}에서 a 계산

### T = { s1 }  α = a
현재 상태는 `{s1}`, 입력 **a**에 대해 계산한다.

#### 해야 할 계산

```
Move({s1}, a) = ?
```

원소가 하나뿐이므로 사실상 **NFA 상태 s1 하나**에서의 이동만 보면 된다.

#### 🔥 핵심

```
지금부터 계산할 것: δ({s1}, a)
```

---

## 📋 48페이지 — 계산 결과

### U = { s1 , s2 }
다음 상태 U는 **{s1, s2}**이다.

#### 왜 이렇게 되는가? 계산 과정

```
Move({s1}, a):
  s1에서 a → s1 → s1
           → s1 → s2

결과: {s1, s2}
```

#### ε-closure({s1,s2}) = {s1,s2}
추가 ε 이동 없음

---

#### 의미 설명

s1은 원래 "a를 읽으면 자기 자신에 머물 수도 있고, 다음 단계인 s2로도 갈 수 있는" **비결정 상태**였다. DFA에서는 그 두 가능성을 한 번에 담아야 하므로:

```
{s1} --a--> {s1,s2}
```

#### 🔥 핵심

```
δ({s1}, a) = {s1,s2}
```

---

## 📋 49페이지 — 전이표 반영 (기존 상태)

### 현재 δ 전이표

| 상태 | a | b |
|------|---|---|
| `{s0,s1}` | `{s1,s2}` | `{s1}` |
| `{s1,s2}` | `{s1,s2}` | `{s1,s3}` |
| `{s1}` | `{s1,s2}` | |

`{s1}`에서 a를 읽으면 `{s1,s2}`로 간다는 계산 결과를 δ 표에 기록 완료.

---

#### 중요한 포인트

여기서 중요한 점은 `{s1,s2}`가 이미 Dstates 안에 있는 상태라는 점이다.

- 새로운 상태 아님 → **추가는 안 함**
- 전이표만 기록

학생들이 자주 헷갈리는 부분:

> ❌ "결과가 나왔으면 무조건 상태 추가" → 틀림  
> ✅ **없을 때만 추가**, 있으면 전이만 기록

#### 🔥 핵심

```
이 페이지의 핵심:
기존 상태로 가는 전이를 표에 반영
```

---

## 📋 50페이지 — {s1}에서 b 계산 시작

### T = { s1 }  α = b
현재 상태는 `{s1}`, 이번에는 **입력 b**에 대해 계산한다.

#### 해야 할 것

```
Move({s1}, b) = ?
```

`{s1}`에 대한 전이는 두 개를 다 채워야 한다:
- a → 이미 계산함 (= `{s1,s2}`)
- b → **지금부터 계산**

그래야 DFA에서 `{s1}` 행이 완성된다.

#### 🔥 핵심

```
다음 계산: δ({s1}, b)
```

---

## 🔥 46~50페이지 전체 흐름 요약

| 단계 | 내용 |
|------|------|
| 1. 다음 처리 상태 선택 | T = `{s1}` |
| 2. a에 대해 계산 | Move(`{s1}`, a) = `{s1,s2}` |
| 3. ε-closure 적용 | = `{s1,s2}` |
| 4. 전이표 반영 | δ(`{s1}`, a) = `{s1,s2}` (기존 상태 → 추가 없음) |
| 5. b 계산 시작 | δ(`{s1}`, b) 계산 준비 |

#### 현재까지 누적된 DFA 전이표

| DFA 상태 | a | b |
|----------|---|---|
| `{s0,s1}` | `{s1,s2}` | `{s1}` |
| `{s1,s2}` | `{s1,s2}` | `{s1,s3}` |
| `{s1}` | `{s1,s2}` | 아직 계산 중 |
| `{s1,s3}` | 아직 미처리 | 아직 미처리 |

#### 🔥 이 구간에서 꼭 이해해야 할 포인트

1. **원소 하나짜리 집합 상태도 결국 DFA 상태다**  
   `{s1}`도 그냥 하나의 DFA 상태다.

2. **집합 상태에서 계산할 때도 규칙은 같다**  
   Move → ε-closure → 기존 상태인지 확인 → 전이표 기록

3. **기존 상태면 새로 추가하지 않는다**  
   `{s1,s2}`는 이미 있었기 때문에 추가하지 않고 전이만 적는다.
