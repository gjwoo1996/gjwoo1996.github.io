# GitHub Actions 규칙 (.github/workflows/hugo.yml)

AI 세션이 워크플로우를 수정할 때 반복되는 실수를 방지하기 위한 문서입니다.

---

## concurrency 설정

```yaml
concurrency:
  group: "pages"
  cancel-in-progress: true   # ← 반드시 true
```

> **왜 true인가**: GitHub Actions 공식 문서와 Hugo 공식 예제의 기본값은 `false`입니다.
> 하지만 `false`로 설정하면 빠르게 여러 번 push할 경우 이전 빌드가 취소되지 않고
> 큐에 쌓여 불필요한 Actions 시간이 소비됩니다.
> 개인 블로그에서는 항상 최신 push만 배포되면 충분하므로 `true`가 올바른 설정입니다.

---

## Hugo 버전 고정

```yaml
- name: Setup Hugo
  uses: peaceiris/actions-hugo@v3
  with:
    hugo-version: "0.146.0"   # 버전을 "latest"로 바꾸지 마세요
    extended: true             # extended: true 유지 필수 (Sass/SCSS 처리)
```

> **왜 버전을 고정하는가**: `latest`로 설정하면 Hugo 메이저 업데이트 시 설정 파일
> 호환성이 깨질 수 있습니다. 버전 변경이 필요하면 로컬에서 먼저 검증 후 업데이트하세요.

---

## fetch-depth 설정

```yaml
- name: Checkout
  uses: actions/checkout@v4
  with:
    submodules: recursive
    fetch-depth: 0   # 0으로 유지 — 변경하지 마세요
```

> **왜 0인가**: `fetch-depth: 0`은 전체 git 히스토리를 가져옵니다.
> 이 값이 없으면 Hugo의 `.GitInfo`(포스트 최종 수정일 자동 감지)가 동작하지 않습니다.

---

## 배포 흐름 요약

```
push to main
  └─ build job
       ├─ Checkout (submodules 포함)
       ├─ Setup Hugo (extended, 버전 고정)
       ├─ Configure Pages (base_url 동적 주입)
       ├─ hugo --minify --baseURL "${{ steps.pages.outputs.base_url }}/"
       └─ Upload artifact (./public)
  └─ deploy job (build 완료 후)
       └─ Deploy to GitHub Pages
```

`baseURL`은 hugo.toml의 값을 무시하고 `steps.pages.outputs.base_url`을 사용합니다.
hugo.toml의 `baseURL`은 로컬 빌드 시에만 사용됩니다.
