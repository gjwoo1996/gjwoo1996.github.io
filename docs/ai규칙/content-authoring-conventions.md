# 콘텐츠 작성 규칙

AI 세션이 콘텐츠 파일을 생성하거나 수정할 때 참고해야 하는 문서입니다.

---

## 포스트 frontmatter 표준

`content/posts/` 아래 모든 포스트는 아래 형식을 따릅니다.

```yaml
---
title: "포스트 제목"
date: 2026-01-01T12:00:00+09:00   # 타임존 +09:00 (KST) 명시
draft: false
tags: ["태그1", "태그2"]
categories: ["카테고리"]
description: "검색 결과와 OG 태그에 표시되는 설명 (1~2문장)"
summary: "포스트 목록에 표시되는 요약 (없으면 본문 앞 70단어 자동 추출)"
---
```

> **summary vs description**
> - `description`: SEO meta description, OG 태그에 사용
> - `summary`: 포스트 목록 카드에 표시되는 미리보기 텍스트
> 두 값이 다를 수 있으니 각각 명시적으로 작성하는 것을 권장합니다.

---

## 특수 콘텐츠 페이지 (수정 주의)

아래 파일은 기능 페이지로, 임의로 수정하면 해당 기능이 깨집니다.

### content/search/index.md

```yaml
---
title: "Search"
layout: "search"        # ← "search" 레이아웃 고정. 변경 금지
summary: "블로그 검색"  # 의미 없는 플레이스홀더 금지 (SEO에 노출됨)
placeholder: "검색어를 입력하세요"
---
```

- `layout: "search"` 값을 바꾸면 검색 페이지가 일반 페이지로 렌더링됩니다.
- 이 파일에 본문 내용을 추가하지 마세요.

---

## .gitignore 유지 항목

아래 항목은 항상 `.gitignore`에 포함되어야 합니다.

```gitignore
public/           # Hugo 빌드 결과물 (CI에서 생성)
.hugo_build.lock  # Hugo 빌드 잠금 파일
resources/_gen/   # Hugo 자동 생성 리소스
node_modules/
.DS_Store
*.swp
```

`public/`을 커밋하면 GitHub Actions 배포와 충돌합니다.
