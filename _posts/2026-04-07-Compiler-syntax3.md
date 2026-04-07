---
title: "Syntax Analysis Part 3"
excerpt: ""

categories:
  - Compiler
tags:
  - tag1
  - tag2

permalink: /Compiler/syntax3/

toc: true
toc_sticky: true

date: 2026-04-07
last_modified_at: 2026-04-07



---
# COMP321 Compiler — Syntax Analysis Part 3
**Kyungpook National University | Hwisoo So | Spring 2026**

---

## 📋 1페이지 — 제목

### Syntax Analysis – 3

> **구문 분석 – 3**

이번 강의는 **Syntax Analysis (구문 분석)**의 세 번째 파트다.  
즉 지금부터는 컴파일러에서 Lexical Analysis(토큰화) 다음 단계, 문장 구조를 이해하는 단계를 다루는 내용이다.

- **Hwisoo So** → 소휘수 (강의 담당 교수)
- **Kyungpook National University** → 경북대학교
- **COMP321 Compiler Spring 2026** → 컴파일러 과목, 2026년 봄학기

#### 🖼 그림 설명
- 가운데: "Syntax Analysis – 3"
- 아래: 교수 이름 + 학교 로고
- 오른쪽 위: 과목 정보

이 페이지는 완전한 표지(slide cover)다. 내용 없음, 단순히 강의 시작 알림 역할.

---

## 📋 2페이지 — Outlook (전체 개요)

### Syntax Analysis COMP321@KNU

### Outlook
**전체 개요 / 진행 내용**

| 항목 | 상태 |
|------|------|
| Syntax and Semantics of Programming Languages | ✔ 완료 |
| Specifying the Syntax of a programming language | ✔ 완료 |
| CFGs, BNF and EBNF | ✔ 완료 — CFG, BNF, EBNF (문법 정의 형식들) |
| Grammar transformations | ✔ 완료 — Left factoring, left recursion 제거 등 |
| Top-down parsing (LL) | ✔ 완료 |
| **Recursive descent (LL) parser construction** | **← 지금 여기** |
| LL Grammars | 예정 |
| AST Construction | 예정 |
| Parse trees vs. ASTs | 예정 |
| Chomsky's Hierarchy | 예정 |

#### 지금 위치
👉 Parsing 중에서도 **Recursive Descent Parser** 부분 시작

---

## 📋 3페이지 — Recursive Descent Parsing

### Recursive Descent Parsing
**재귀 하강 파싱**

#### Recursive descent parsing is a straightforward LL (top-down) parsing method.
재귀 하강 파싱은 단순한 LL(하향식) 파싱 방법이다.

- LL = Left to right + Leftmost derivation
- top-down 방식
- 구현 쉬움 / 함수 호출 구조로 만든다

#### We will now look at how to develop a recursive descent parser from an EBNF specification.
이제 EBNF 명세로부터 재귀 하강 파서를 만드는 방법을 살펴본다.

핵심: **문법 → 코드로 변환**

#### Key idea: the parse tree structure corresponds to the caller–callee relationship of parsing procedures that call each other at runtime.
핵심 아이디어: 파스트리 구조는 실행 시 서로 호출하는 파싱 함수들의 호출 관계와 대응된다.

✔ 핵심 개념: **파스트리 구조 = 함수 호출 구조**

```
Sentence
 ├── Subject
 ├── Verb
 └── Object
→ 실제 코드:
parseSentence()
  -> parseSubject()
  -> parseVerb()
  -> parseObject()
```

즉 트리 = 함수 호출 트리

---

## 📋 4페이지 — Recursive Descent Parser Construction Example

### Recursive Descent Parser Construction Example
**재귀 하강 파서 구성 예제**

#### 문법 정의

```
Sentence ::= Subject Verb Object .
Subject  ::= I | a Noun | the Noun
Object   ::= me | a Noun | the Noun
Noun     ::= cat | mat | rat
Verb     ::= like | is | see | sees
```

| 규칙 | 의미 |
|------|------|
| Sentence | 주어 + 동사 + 목적어 + "." |
| Subject | I / a+명사 / the+명사 |
| Object | me / a+명사 / the+명사 |
| Noun | cat / mat / rat |
| Verb | like / is / see / sees |

#### Define a procedure parseN for each non-terminal N
각 non-terminal N마다 parseN 함수를 정의한다.

```python
parseSentence()
parseSubject()
parseObject()
parseNoun()
parseVerb()
```

✔ 핵심 규칙: 문법 → 함수 **1:1 매핑**

| 문법 | 함수 |
|------|------|
| Sentence | parseSentence |
| Subject | parseSubject |
| Object | parseObject |
| Noun | parseNoun |
| Verb | parseVerb |

#### 🖼 그림 설명
- 슬라이드 상단: 문법
- 하단: 함수 리스트
- 의미: 문법을 코드로 그대로 옮긴다

---

## 📋 5페이지 — Recursive Descent Parser Construction Example (클래스 구조)

### Recursive Descent Parser Construction Example
**파서 클래스 뼈대**

```python
class MicroEnglishParser:

    def __init__(self):
        self.currentToken = None  # 현재 토큰을 저장하는 변수

        # Auxiliary methods will go here (보조 함수들이 여기에 들어간다)

        # Parsing methods will go here (파싱 함수들이 여기에 들어간다)
```

✔ parser는 항상 현재 토큰을 하나 보고 판단한다.

전체 구조:

```
Parser 클래스
 ├── currentToken
 ├── auxiliary methods (accept 등)
 └── parsing methods (parseX)
```

#### 🖼 그림 설명
- 슬라이드 박스 안: 클래스 구조
- 주석으로 영역 나눔
- 의미: 실제 구현 뼈대

---

## 🔥 1~5페이지 핵심 정리

1. **Recursive Descent Parser 정의** — LL(top-down) 방식 / 함수 호출 기반 파싱
2. **가장 중요한 개념** → 파스트리 = 함수 호출 구조
3. **구현 원리** — Non-terminal → 함수 / Terminal → accept()
4. **코드 구조**
```
Parser
 ├── currentToken
 ├── accept()
 └── parseX()
```

---

## 📋 6페이지 — Recursive Descent Parser Construction: Auxiliary Methods

### Recursive Descent Parser Construction: Auxiliary Methods
**재귀 하강 파서 구성: 보조 메서드**

```python
class MicroEnglishParser:

    def __init__(self, scanner):
        self.scanner = scanner          # scanner를 저장한다
        self.currentToken = None        # 현재 토큰 초기화

    def accept(self, expectedToken):
        if self.currentToken == expectedToken:
            # get next token from scanner
            self.currentToken = self.scanner.scan()  # 다음 토큰으로 이동
        else:
            report a syntax error  # 문법 오류 발생
```

✔ 이제 parser는 scanner와 연결된다: `input → scanner → parser`

#### accept 함수의 역할 (핵심 중요)

| 동작 | 설명 |
|------|------|
| 현재 토큰 검사 | expectedToken과 일치 여부 확인 |
| 맞으면 | 다음 토큰으로 이동 |
| 틀리면 | 에러 발생 |

```python
accept("if")
→ "if"가 아니면 바로 에러
```

👉 **accept 함수 = parser의 핵심 primitive**

#### 🖼 그림 설명
- 슬라이드: 클래스 + accept 함수 코드
- 의미: parser 동작의 최소 단위 정의

---

## 📋 7페이지 — Recursive Descent Parser Construction: Parsing Methods

### Recursive Descent Parser Construction: Parsing Methods
**파싱 메서드**

```
Sentence ::= Subject Verb Object .
```

문장 → 주어 + 동사 + 목적어 + "."

```python
def parseSentence(self):
    parseSubject()   # 주어 파싱
    parseVerb()      # 동사 파싱
    parseObject()    # 목적어 파싱
    self.accept('.')  # "."을 기대하고 소비한다
```

✔ **문법 그대로 코드화됨**

```
Sentence ::= A B C .
→
parseA()
parseB()
parseC()
accept('.')
```

👉 완전히 기계적 변환

#### 🖼 그림 설명
- 위: 문법
- 아래: 코드
- 1:1 대응 강조

---

## 📋 8페이지 — Recursive Descent Parser: Parsing Methods (Subject)

### Recursive Descent Parser: Parsing Methods
**parseSubject 구현**

```
Subject ::= I | a Noun | the Noun
```

주어는: I / a + 명사 / the + 명사

```python
def parseSubject(self):
    if self.currentToken == 'I':
        self.accept('I')
    elif self.currentToken == 'a':
        self.accept('a')
        parseNoun()
    elif self.currentToken == 'the':
        self.accept('the')
        parseNoun()
    else:
        report a syntax error
```

✔ **선택 구조 ( | ) 처리 방식:**

```
A ::= X | Y | Z
→
if token == X:
elif token == Y:
elif token == Z:
else error
```

👉 FIRST set 기반 선택

#### 🖼 그림 설명
- 위: 문법
- 아래: if-elif 코드
- "선택문 = 조건문" 변환

---

## 📋 9페이지 — Recursive Descent Parser: Parsing Methods (Noun)

### Recursive Descent Parser: Parsing Methods
**parseNoun 구현**

```
Noun ::= cat | mat | rat
```

명사는: cat / mat / rat

```python
def parseNoun(self):
    if self.currentToken == 'cat':
        self.accept('cat')
    elif self.currentToken == 'mat':
        self.accept('mat')
    elif self.currentToken == 'rat':
        self.accept('rat')
    else:
        report a syntax error
```

✔ 완전 동일 패턴: 선택문 → if-elif

---

## 📋 10페이지 — Recursive Descent Parser: Parsing Methods (Object, Verb — 빈칸)

### Recursive Descent Parser: Parsing Methods
**parseObject / parseVerb (미완성 상태)**

```
Object ::= me | a Noun | the Noun
Verb   ::= like | is | see | sees
```

```python
def parseObject(self):
    ? (미완성)

def parseVerb(self):
    ? (미완성)
```

✔ 이 페이지는 일부러 비워둠 → 학생이 직접 구현해보게 함

#### 어떻게 채워야 하는지 (핵심)

**parseObject:**
```python
if token == 'me':
elif token == 'a':
elif token == 'the':
```

**parseVerb:**
```python
if token in ('like', 'is', 'see', 'sees'):
```

#### 🖼 그림 설명
- 위: 문법
- 아래: 빈 코드
- "이걸 너가 채워라" 구조

---

## 🔥 6~10페이지 핵심 요약

1. **accept 함수** — 토큰 검사 + 다음 토큰 이동 / 틀리면 에러

2. **변환 규칙 (핵심 암기)**

| 문법 | 코드 |
|------|------|
| A ::= B C | parseB(); parseC(); |
| A ::= x | accept(x) |
| A ::= X \| Y | if-elif |

3. **핵심 구조** → parser는 결국 `if / 함수호출 / accept` 이 3개로 끝남

---

## 📋 11페이지 — Recursive Descent Parser: Parsing Methods (Object, Verb — 완성)

### Recursive Descent Parser: Parsing Methods
**parseObject / parseVerb 완성본**

```
Object ::= me | a Noun | the Noun
Verb   ::= like | is | see | sees
```

```python
def parseObject(self):
    if self.currentToken == 'me':
        self.accept('me')
    elif self.currentToken == 'a':
        self.accept('a')
        parseNoun()
    elif self.currentToken == 'the':
        self.accept('the')
        parseNoun()

def parseVerb(self):
    if self.currentToken in ('like', 'is', 'see', 'sees'):
        self.acceptIt()  # 현재 토큰을 그대로 소비한다
```

✔ **acceptIt() vs accept(token)**

| 함수 | 의미 |
|------|------|
| accept(x) | 특정 토큰 x 기대 |
| acceptIt() | 그냥 현재 토큰 소비 |

👉 parseVerb는: "어떤 동사든 상관없고, 그냥 하나 소비"

#### 🖼 그림 설명
- 슬라이드: Object, Verb 문법 + 완성 코드
- 이전 페이지(빈칸)를 채운 완성본

---

## 📋 12페이지 — Systematic Development of a RD Parser

### Systematic Development of a RD Parser
**재귀 하강 파서의 체계적인 개발 방법**

#### (1) Express grammar in EBNF
문법을 EBNF로 표현한다.

#### (2) Grammar Transformations:
문법 변환 수행

- **Left factorization and left recursion elimination**
- 좌측 인수분해와 좌측 재귀 제거

#### (3) Create a parser class with
parser 클래스를 만든다.

- `private variable currentToken`
- `methods to call the scanner: accept and acceptIt`

#### (4) Convert EBNF into a RD parser
EBNF를 RD parser로 변환한다.

- **Implement private parsing methods** — 파싱 메서드 구현
- **add private parseN method for each nonterminal N** — 각 non-terminal마다 parseN 함수 추가
- **public parse method that:**
  - gets the first token from the scanner (첫 토큰을 scanner에서 가져옴)
  - calls parseS (S is the start symbol of the grammar)
  - ensure that all tokens are consumed upon return from parseS()

✔ **RD parser 만드는 절차 = 시험 핵심**

```
① 문법 작성
② 문법 변환
③ parser 구조 생성
④ 코드로 변환
```

---

## 📋 13페이지 — MiniC: Systematic Development of an RD Parser (1 & 2)

### MiniC: Systematic Development of an RD Parser (1 & 2)

#### Common prefixes require left-factorization:
공통 접두어가 있으면 left-factorization 필요

**기존 문법:**
```
program ::= ( function-def | variable-def )*
```

프로그램은 함수 정의 또는 변수 정의 반복

❌ 문제:
```
typespec ID ...
typespec ID ...
```
둘 다 같은 시작 → LL parser에서 선택 불가

**변환 후:**
```
program ::= ( typespec ID (VarPart | FuncPart) )*
```

공통 부분(typespec ID)을 먼저 빼고 분기

✔ **left factoring:**
```
A ::= X Y | X Z
→
A ::= X (Y | Z)
```
👉 LL parser에서 필수

#### 🖼 그림 설명
- 위: 원래 문법
- 아래: 변환된 문법
- 공통 prefix 제거 과정 시각화

---

## 📋 14페이지 — Left Recursion Elimination

### Left recursion elimination
**좌측 재귀 제거**

**기존 문법 (left recursion):**
```
add-expr ::= mult-expr
           | add-expr "+" mult-expr
           | add-expr "-" mult-expr
```

덧셈 표현식 정의

❌ 문제: left recursion → `add-expr → add-expr ...` → RD parser에서 무한 재귀 발생

**변환 후:**
```
add-expr ::= mult-expr ( ("+" | "-") mult-expr )*
```

mult-expr 뒤에 +,- 반복 구조

✔ **left recursion 제거 공식:**
```
A → A α | β
→
A → β α*
```

👉 재귀 → while문으로 바뀜

#### 🖼 그림 설명
- 위: 재귀 구조
- 아래: 반복 구조

---

## 📋 15페이지 — Developing a RD Parser for MiniC

### Developing a RD Parser for MiniC
**MiniC.py의 컴파일러 실행 코드**

```python
def compileProgram(self, sourceName):
    self.scanner = Scanner(source)           # scanner 생성
    self.reporter = ErrorReporter()          # 에러 리포터 생성
    self.parser = Parser(scanner, reporter)  # parser 생성
    self.parser.parse()                      # 파싱 실행

    boolean successful = (self.reporter.numErrors == 0)  # 에러 0이면 성공

    if successful:
        print("Compilation was successful.")
    else:
        print("Compilation was unsuccessful.")
```

✔ **컴파일러 전체 흐름:**
```
source
 → scanner
 → parser
 → errorReporter
 → 결과 출력
```

👉 parser는 전체 pipeline의 일부

---

## 🔥 11~15페이지 핵심 요약

1. **parseObject / parseVerb 완성** — 선택문 처리 구조 완성
2. **RD parser 만드는 절차 (시험 핵심)**
   - EBNF 작성 → left factoring → left recursion 제거 → 코드 변환
3. **문법 변환 이유** — LL parser에서 선택 가능하게 만들기
4. **컴파일러 전체 구조** — scanner → parser → error 처리

---

## 📋 16페이지 — The Error Reporter (ErrorReport.py)

### The Error Reporter (ErrorReport.py)
**에러 리포터**

```python
class ErrorReporter:

    def __init__(self):
        self.numErrors = 0  # 에러 개수를 0으로 초기화

    def reportError(self, m, tok, pos):
        print("ERROR: ", end="")
        for c in m:
            if c == "%":
                print(tok, end="")  # % 자리에 토큰 삽입
            else:
                print(c, end="")
        print(" " + str(pos.StartCol) + ".." + str(pos.EndCol)
              + ", line" + str(pos.StartLine) + ".")  # 에러 위치 출력
        self.numErrors += 1  # 에러 개수 증가
```

#### 예시
```
reportError("Type specifier instead of % expected", ...)
→ 출력: ERROR: Type specifier instead of IF expected 9..10, line 22.
```

✔ **"%"의 역할:** 메시지 템플릿의 % 자리에 토큰 삽입

👉 출력 형식: **메시지 템플릿 + 토큰 + 위치**

---

## 📋 17페이지 — MiniC Parser: Reporting Errors and Throwing Exceptions

### MiniC Parser: Reporting errors and throwing exceptions
**에러 처리 및 예외 발생**

```python
def syntaxError(self, messageTemplate, tokenQuoted):
    pos = self.currentToken.GetSourcePos()  # 현재 토큰 위치 가져오기
    self.errorReporter.reportError(messageTemplate, tokQuoted, pos)  # 에러 출력
    raise SyntaxError()  # 예외 발생

class SyntaxError(Exception):
    def __init__(self, message=""):
        super().__init__(message)  # 부모 클래스(Exception) 초기화
```

#### 예시
```
syntaxError("Type specifier instead of % expected", ...)
→ ERROR: Type specifier instead of IF expected ...
```

✔ **흐름:**
```
syntaxError()
 → reportError()
 → raise exception
```

👉 exception을 쓰는 이유: 파싱 중단 + 상위로 에러 전달

---

## 📋 18페이지 — Exception Handling in the MiniC Parser

### Exception Handling in the MiniC Parser
**MiniC 파서에서 예외 처리**

```python
def parse(self):
    self.currentToken = self.scanner.scan()  # 첫 토큰 읽기
    try:
        self.parseProgram()  # 프로그램 파싱
        if currentToken.kind != Token.EOF:
            self.syntaxError("% not expected after end of program", ...)
            # 프로그램 끝 뒤에 이상한 토큰 → 에러
    except SyntaxError as s:
        return None  # 실패 시 None 반환
```

✔ **전체 구조:**
```
try:
    parseProgram()
except:
    에러 처리
```

👉 의미: 에러 발생 → exception → 여기서 catch

#### 🖼 그림 설명
- 슬라이드: try-except 구조 강조
- parser의 "최상위 안전장치"

---

## 📋 19페이지 — Algorithm to Convert EBNF into a RD Parser

### Algorithm to convert EBNF into a RD parser
**EBNF → RD parser 변환 알고리즘**

```
def parseN(self) { parse X() }
```

N ::= X → parseN은 parseX 호출

#### The conversion ... is so "mechanical" that it can easily be automated!
이 변환은 매우 기계적이라 자동화 가능하다.

We can describe the algorithm by a set of mechanical rewrite rules.  
기계적 변환 규칙으로 설명 가능하다.

✔ 진짜 중요: **문법 → 코드 변환은 규칙 기반**

#### 🖼 그림 설명
- 슬라이드: 문법 → 함수 변환 화살표

---

## 📋 20페이지 — Algorithm to Convert EBNF into a RD Parser (규칙)

### Algorithm to convert EBNF into a RD parser
**변환 규칙 상세**

| 문법 요소 | 변환 코드 | 설명 |
|----------|----------|------|
| terminal `t` | `self.accept(t)` | t를 기대하고 소비 |
| non-terminal `N` | `self.parseN()` | parseN 호출 |
| ε (빈 문자열) | `# do nothing` | 아무것도 하지 않음 |
| `X Y` (순서) | `self.parseX(); self.parseY()` | X 파싱 후 Y 파싱 |

✔ **변환 규칙 정리 (시험 핵심):**

```
terminal t   → accept(t)
non-terminal N → parseN()
ε             → 아무것도 안 함
X Y           → 순서대로 호출
```

#### 🖼 그림 설명
- 슬라이드: 각 규칙 → 코드 변환
- "완전 기계적 변환 규칙"

---

## 🔥 16~20페이지 핵심 요약

1. **에러 처리 구조** — reportError → 메시지 출력 / syntaxError → exception 발생
2. **parser 전체 흐름** — scan → parse → error handling
3. **EBNF → 코드 변환 규칙 (핵심 암기)**
   - `t` → `accept(t)`
   - `N` → `parseN()`
   - ε → nothing
   - `XY` → 순차 호출

👉 여기까지 이해하면 RD parser 구현 80% 끝난 상태다.

---

## 📋 21페이지 — Algorithm to Convert EBNF into a RD Parser (선택/반복)

### Algorithm to convert EBNF into a RD parser
**선택 ( | ) 과 반복 ( * ) 변환**

#### parsing X | Y

```python
match self.currentToken.kind:
    cases in FIRST[X]:
        parse X
    cases in FIRST[Y]:
        parse Y
    case _:
        report syntax error
```

**FIRST[X]**: X로부터 시작할 수 있는 terminal들의 집합  
`FIRST [X] denotes the set of terminal symbols that start sentences derived from X.`

#### parsing X*

```python
while self.currentToken.kind is in FIRST[X]:
    parse X()
```

✔ **핵심 변환 규칙 (매우 중요):**

**1. 선택 ( | )**
```
X | Y
→
if token ∈ FIRST[X]:
    parseX()
elif token ∈ FIRST[Y]:
    parseY()
else:
    error
```

**2. 반복 ( \* )**
```
X*
→
while token ∈ FIRST[X]:
    parseX()
```

👉 이 두 개가 RD parser 핵심이다.

#### 🖼 그림 설명
- 위: 선택 구조
- 아래: 반복 구조
- FIRST 집합 기반 분기

---

## 📋 22페이지 — Example: parseExpr

### Example: parseExpr

```
Expr ::= AndExpr ( "||" AndExpr )*
```

Expr는 AndExpr 뒤에 ("||" AndExpr)가 0번 이상 반복

```python
def parseExpr(self):
    self.parseAndExpr()                           # 먼저 AndExpr 파싱
    while self.currentToken.kind == Token.OR:     # 현재 토큰이 OR(||)이면 반복
        self.acceptIt()                           # "||" 소비
        self.parseAndExpr()                       # 다음 AndExpr 파싱
```

✔ 21페이지 규칙 적용:

```
( X )*
→
while condition:
    X
```

👉 의미:
```
a || b || c
→
parseAndExpr()
while '||':
    parseAndExpr()
```

#### 🖼 그림 설명
- 위: 문법
- 아래: 코드
- 반복 구조 → while문

---

## 📋 23페이지 — Example: parseProgram

### Example: parseProgram

```
program ::= ( (VOID|INT|BOOL|FLOAT) ID ( FunPart | VarPart ) )*
```

프로그램은: 타입 + ID + (함수 or 변수), 이 구조가 반복됨

```python
def parseProgram(self):
    while self.isTypeSpecifier(self.currentToken.kind):  # 현재 토큰이 타입이면 반복
        self.acceptIt()             # 타입 소비
        self.accept(Token.ID)       # ID 소비
        if self.currentToken.kind == Token.LEFTPAREN:  # "("이면
            self.parseFunPart()     # 함수 파싱
        else:
            self.parseVarPart()     # 변수 파싱
```

`isTypeSpecifier is true iff the current Token is either Token.VOID, Token.INT, Token.BOOL or Token.FLOAT.`  
→ isTypeSpecifier는 토큰이 void/int/bool/float일 때 true

✔ **구조:**
```
while 타입:
    타입
    ID
    if '(':
        함수
    else:
        변수
```

👉 **선택 ( | )** 과 **반복 ( \* )** 둘 다 포함된 완전한 예제

#### 🖼 그림 설명
- 슬라이드: 문법 → 코드
- 실제 컴파일러 수준 코드

---

## 📋 24페이지 — Outlook (전체 정리)

### Outlook
**전체 정리**

| 항목 | 상태 |
|------|------|
| Syntax and Semantics of Programming Languages | ✔ 완료 |
| Specifying the Syntax | ✔ 완료 |
| Top-down parsing (LL) | ✔ 완료 |
| **Recursive descent (LL) parser construction** | **✔ 완료** |
| LL Grammars | 예정 |
| AST Construction | 예정 |
| Parse trees vs. ASTs | 예정 |
| Chomsky's Hierarchy | 예정 |

✔ **지금까지:** RD parser 구현 완료  
✔ **다음:** AST / LL grammar

---

## 🔥 21~24페이지 핵심 요약 (진짜 중요)

**1. 선택문 ( | )**
```python
if token ∈ FIRST[X]:
    parseX()
elif token ∈ FIRST[Y]:
    parseY()
```

**2. 반복문 ( \* )**
```python
while token ∈ FIRST[X]:
    parseX()
```

**3. RD parser 핵심 구조 4개**

| 요소 | 코드 |
|------|------|
| terminal | accept() |
| non-terminal | parseN() |
| 선택 | if / elif |
| 반복 | while |

**4. 전체 흐름**
```
EBNF
 → 문법 변환
 → FIRST 기반 분기
 → 함수 코드 생성
```

---

## 🔥 전체 강의 핵심 요약 (1~24페이지)

### RD parser 만드는 절차

```
① EBNF 문법 작성
② Grammar Transformations (left factoring, left recursion 제거)
③ Parser 클래스 생성 (currentToken, accept, acceptIt)
④ EBNF → 코드 변환
```

### EBNF → 코드 변환 규칙 완전 정리

| 문법 | 코드 |
|------|------|
| terminal `t` | `accept(t)` |
| non-terminal `N` | `parseN()` |
| ε | nothing |
| `X Y` | `parseX(); parseY();` |
| `X \| Y` | `if FIRST[X]... elif FIRST[Y]...` |
| `X*` | `while FIRST[X]: parseX()` |

### 핵심 함수 정리

| 함수 | 역할 |
|------|------|
| `accept(t)` | 특정 토큰 t 기대하고 소비, 틀리면 에러 |
| `acceptIt()` | 현재 토큰 그냥 소비 |
| `syntaxError()` | 에러 출력 + exception 발생 |
| `parseN()` | non-terminal N 파싱 |
