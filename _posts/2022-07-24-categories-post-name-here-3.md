---
title: "공부"
excerpt: "알아둬야할 것"

categories:
  - Categories3
tags:
  - [tag1, tag2]

permalink: /categories3/post-name-here-3/

toc: true
toc_sticky: true

date: 2025-07-31
last_modified_at: 2025-07-31

# sitemap :
#   changefreq : daily
#   priority : 1.0
---


<div class="jekyll-overview">

  <h2>1. Jekyll의 동작 구조 (정적 사이트 생성기)</h2>
  <ul>
    <li><code>.md</code> 파일(= Markdown 문서) → <code>.html</code>로 빌드해서 정적 웹사이트로 변환함</li>
    <li><code>_config.yml</code>: 사이트 전체 설정 파일</li>
    <li><code>_posts/</code>, <code>_pages/</code>, <code>_layouts/</code>, <code>_includes/</code> 등의 폴더가 의미 있는 역할을 함</li>
    <li>Liquid 템플릿 문법 (<code>{% if %}</code>, <code>{{ 변수 }}</code>)을 통해 페이지 내용을 동적으로 구성</li>
  </ul>
  <p><strong>📌 핵심 이해 포인트:</strong><br>
    <code>site.categories["운영체제"]</code> → 해당 카테고리에 속한 글 목록<br>
    <code>_pages/categories/...md</code> → 각 카테고리별 아카이브 페이지를 자동 생성하는 트리거
  </p>

  <h2>2. Minimal Mistakes 테마 작동 방식</h2>
  <ul>
    <li><code>_layouts/</code>, <code>_includes/</code>에 미리 만들어둔 HTML+Liquid 조각들을 조합</li>
    <li><code>layout: category</code>, <code>layout: home</code>, <code>layout: archive</code> 같은 설정이 전체 레이아웃을 결정</li>
    <li><code>taxonomy:</code>는 특정 레이아웃에서 글을 필터링할 때 쓰는 키워드</li>
  </ul>
  <p><strong>📌 핵심 이해 포인트:</strong><br>
    <code>_data/navigation.yml</code> → 사이드바와 상단 메뉴 구성 정의<br>
    <code>taxonomy:</code>와 <code>categories:</code>는 카테고리 글 모음 페이지를 자동 생성할 때 연결고리 역할
  </p>

  <h2>3. GitHub Pages를 통한 웹 호스팅</h2>
  <ul>
    <li>GitHub에 <code>.md</code>, <code>.yml</code>, <code>.html</code> 파일들을 업로드하면</li>
    <li>GitHub이 Jekyll을 자동으로 실행해서 정적 사이트로 빌드 + 호스팅</li>
    <li><code>_config.yml</code>이 바뀌거나, 새 <code>.md</code> 파일이 생기면 GitHub이 자동으로 rebuild함</li>
  </ul>

  <h2>📚 추천 학습 순서</h2>
  <ol>
    <li>Markdown 문법 → <code>.md</code> 문서 작성 자유자재</li>
    <li>Jekyll 기본 구조 → <code>_posts</code>, <code>_layouts</code>, <code>_includes</code> 이해</li>
    <li>Liquid 문법 → <code>{{ }}</code>, <code>{% %}</code> 문법으로 동적 처리 방식 익히기</li>
    <li>Minimal Mistakes 구조 분석 → <code>config.yml</code>, <code>_data/navigation.yml</code>, <code>_pages/</code>, <code>_layouts/</code></li>
    <li>GitHub Pages 동작 원리 → 브라우저에서 자동으로 빌드/배포되는 원리</li>
  </ol>

</div>
