---
title: "공부"
excerpt: "알아둬야할 것"

categories:
  - Categories1
tags:
  - tag1
  - tag2

permalink: /categories1/post-name-here-3/

toc: true
toc_sticky: true

date: 2025-07-31
last_modified_at: 2025-07-31



---


## 1. Jekyll의 동작 구조 (정적 사이트 생성기)

- `.md` 파일(= Markdown 문서) → `.html`로 빌드해서 정적 웹사이트로 변환함  
- `_config.yml`: 사이트 전체 설정 파일  
- `_posts/`, `_pages/`, `_layouts/`, `_includes/` 등의 폴더가 의미 있는 역할을 함  
- Liquid 템플릿 문법 (`{% if %}`, `{{ 변수 }}`)을 통해 페이지 내용을 동적으로 구성  

**📌 핵심 이해 포인트:**  
`site.categories["운영체제"]` → 해당 카테고리에 속한 글 목록  
`_pages/categories/...md` → 각 카테고리별 아카이브 페이지를 자동 생성하는 트리거  

---

## 2. Minimal Mistakes 테마 작동 방식

- `_layouts/`, `_includes/`에 미리 만들어둔 HTML+Liquid 조각들을 조합  
- `layout: category`, `layout: home`, `layout: archive` 같은 설정이 전체 레이아웃을 결정  
- `taxonomy:`는 특정 레이아웃에서 글을 필터링할 때 쓰는 키워드  

**📌 핵심 이해 포인트:**  
`_data/navigation.yml` → 사이드바와 상단 메뉴 구성 정의  
`taxonomy:`와 `categories:`는 카테고리 글 모음 페이지를 자동 생성할 때 연결고리 역할  

---

## 3. GitHub Pages를 통한 웹 호스팅

- GitHub에 `.md`, `.yml`, `.html` 파일들을 업로드하면  
- GitHub이 Jekyll을 자동으로 실행해서 정적 사이트로 빌드 + 호스팅  
- `_config.yml`이 바뀌거나, 새 `.md` 파일이 생기면 GitHub이 자동으로 rebuild함  

---

## 📚 추천 학습 순서

1. Markdown 문법 → `.md` 문서 작성 자유자재  
2. Jekyll 기본 구조 → `_posts`, `_layouts`, `_includes` 이해  
3. Liquid 문법 → `{{ }}`, `{% %}` 문법으로 동적 처리 방식 익히기  
4. Minimal Mistakes 구조 분석 → `config.yml`, `_data/navigation.yml`, `_pages/`, `_layouts/`  
5. GitHub Pages 동작 원리 → 브라우저에서 자동으로 빌드/배포되는 원리  

