# docs/

이 디렉토리는 두 가지 용도의 문서를 담고 있습니다.

```
docs/
├── ai규칙/        ← AI 세션 간 일관성 유지를 위한 규칙 문서
└── 블로그가이드/  ← 블로그 운영 방법을 설명하는 한글 문서
```

---

## ai규칙/

AI가 코드를 수정하기 전에 참고하는 규칙 문서입니다.

| 파일 | 내용 |
|------|------|
| [hugo-config-conventions.md](ai규칙/hugo-config-conventions.md) | hugo.toml 필수 설정 및 주의사항 |
| [github-actions-conventions.md](ai규칙/github-actions-conventions.md) | CI/CD 워크플로우 규칙 |
| [content-authoring-conventions.md](ai규칙/content-authoring-conventions.md) | 포스트 frontmatter 형식 및 특수 페이지 주의사항 |

### 수정 전 체크리스트

- [ ] `hugo.toml` 수정 시 → `ai규칙/hugo-config-conventions.md` 확인
- [ ] `.github/workflows/hugo.yml` 수정 시 → `ai규칙/github-actions-conventions.md` 확인
- [ ] `content/` 파일 생성·수정 시 → `ai규칙/content-authoring-conventions.md` 확인

---

## 블로그가이드/

블로그를 처음 접하는 사람을 위한 운영 설명 문서입니다.  
자세한 목록은 [블로그가이드/블로그운영가이드.md](블로그가이드/블로그운영가이드.md)를 참고하세요.

```
블로그가이드/
├── 시작하기/    전체개요, 핵심개념, 폴더구조
├── 글쓰기/      글작성방법, 글배포워크플로우, 이미지삽입
├── 설정/        설정파일, 검색기능, 배포자동화, 테마커스터마이징
└── 참고/        주의사항및자주하는실수
```
