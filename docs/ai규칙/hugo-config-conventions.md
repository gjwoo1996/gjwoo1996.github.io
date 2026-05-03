# Hugo 설정 규칙 (hugo.toml)

AI 세션이 hugo.toml을 수정할 때 반복되는 실수를 방지하기 위한 문서입니다.

---

## 필수 최상위 설정

아래 항목은 `[params]` 블록 **밖** 최상단에 반드시 위치해야 합니다.
섹션 내부나 params 안에 넣으면 **무시**됩니다.

```toml
baseURL = "https://gjwoo1996.github.io/"
languageCode = "ko-KR"
title = "gjwoo1996's blog"
theme = "PaperMod"
enableRobotsTXT = true   # ← 누락 금지. 없으면 robots.txt가 생성되지 않음
```

> **왜 중요한가**: PaperMod 테마는 robots.txt 생성을 지원하지만, Hugo 레벨에서
> `enableRobotsTXT = true`가 없으면 테마 설정과 무관하게 robots.txt가 만들어지지
> 않아 검색엔진 크롤링에 영향을 줍니다.

---

## [params] 필수 항목

hugo.toml의 `[params]` 섹션을 수정할 때 아래 항목을 유지해야 합니다.

```toml
[params]
  env = "production"       # PaperMod analytics/comment 기능 활성화에 필요
  dateFormat = "2006-01-02"  # 없으면 "Jan 2, 2006" 영문 포맷이 기본값이 됨
  keywords = ["개발", "블로그", "Hugo", "백엔드"]  # SEO meta keywords
```

---

## 검색 기능 설정 ([params.fuseOpts])

검색 관련 코드를 수정할 때 `[params.fuseOpts]` 블록을 삭제하거나 누락하지 마세요.
이 블록이 없으면 Fuse.js 기본값(낮은 검색 정확도)이 사용됩니다.

```toml
[params.fuseOpts]
  isCaseSensitive = false
  shouldSort = true
  location = 0
  distance = 1000
  threshold = 0.4
  minMatchCharLength = 0
  limit = 10
  keys = ["title", "permalink", "summary", "content"]
```

검색 기능이 동작하려면 다음 세 가지가 **모두** 필요합니다.
1. `[outputs]` → `home = ["HTML", "RSS", "JSON"]` (JSON 출력 포함)
2. `content/search/index.md` 파일 존재
3. 위의 `[params.fuseOpts]` 설정

---

## outputs 설정

```toml
[outputs]
  home = ["HTML", "RSS", "JSON"]   # JSON을 빼면 검색 인덱스가 생성되지 않음
```

---

## 코드 하이라이트 설정

```toml
[markup]
  [markup.highlight]
    noClasses = false          # true로 바꾸면 인라인 스타일 강제 적용됨 (불필요한 용량 증가)
    lineNos = true
    lineNumbersInTable = true
```
