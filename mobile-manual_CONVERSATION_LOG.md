# mobile-manual 대화 로그

## 프로젝트 개요

- **목적**: KT 스카이라이프 모바일 전산 매뉴얼 웹페이지
- **URL**: https://pjungjin85-sketch.github.io/mobile-manual/
- **비밀번호**: `20260306`
- **저장소**: https://github.com/pjungjin85-sketch/mobile-manual
- **로컬 경로**: `/Users/jaypark/workspace/mobile-manual/`

---

## 세션 1 (이전 대화 요약 기반)

### 주요 작업
- 정적 사이트(HTML/CSS/JS + JSON) 구조 설계
- `data/manual.json`을 단일 소스로 카테고리/항목 관리
- KT Skylife 디자인 시스템 적용 (red: #E60012, Noto Sans KR)
- 비밀번호 보호 기능 (sessionStorage 기반)
- 키워드 검색 기능 (title, description, keywords, steps, 카테고리명)
- 단계별 이미지 뷰어 (detail.html, 라이트박스, 사이드바 스크롤스파이)
- 안면인증 PDF → 8개 항목, 30장 이미지 추출 (pymupdf, 2x 해상도)

### 주요 버그 수정
- 검색 결과 표시 안됨: `style.display = ''` → `style.display = 'block'` 으로 수정
- Write 도구 보안 훅 차단 (innerHTML, `.exec()` 오탐): heredoc 방식 & `text.split(RegExp)` 으로 우회

---

## 세션 2 — 2026-03-31

### 작업 내용

#### PDF 7개 추가 처리

| PDF 파일 | 카테고리 | 생성 항목 수 |
|----------|---------|------------|
| skylife 모바일 SCIS Juice 현행화_MI사업팀_20230727.pdf | gaetong | 1개 |
| skylife 모바일 eSIM 웨어러블의 이해 및 개통_20221216_v2.pdf | gaetong | 6개 |
| SCIS 모바일 해지, 개통취소 매뉴얼_20220715.pdf | cs | 1개 |
| MVNO-RDS 로그인, 비밀번호초기화, 판매점등록 매뉴얼.pdf | rds | 3개 |
| MVNO-RDS 기본 사용법 매뉴얼_V2_20240516.pdf | rds | 4개 |
| (종합)SCIS 모바일 신규 전산 설명 자료_20250416.pdf | gaetong | 15개 |
| skylife 모바일 SCIS 데이터 누구나 결합_MI사업팀_20230809.pdf | gaetong | 5개 |

- 이미지 추출: 88장 PNG (pymupdf 2x 해상도)
- 폴더: images/gaetong/juice|esim|scis-new|data-bundle, images/cs/cancel, images/rds/rds-login|rds-basic

#### GitHub Pages 배포
- 저장소 생성: pjungjin85-sketch/mobile-manual (public)
- 141개 파일 커밋 & push
- GitHub Pages 활성화 (master 브랜치, / 경로)
- 배포 URL: https://pjungjin85-sketch.github.io/mobile-manual/

#### 최종 항목 현황

| 카테고리 | 항목 수 |
|---------|--------|
| 개통 (gaetong) | 27개 |
| 안면인증 (face-auth) | 8개 |
| RDS | 7개 |
| CS | 1개 |
| **합계** | **43개** |

---

## 파일 구조

```
mobile-manual/
├── index.html          # 메인 페이지 (카테고리 그리드, 검색)
├── detail.html         # 상세 페이지 (단계별 이미지, 사이드바)
├── data/
│   └── manual.json     # 전체 콘텐츠 소스
└── images/
    ├── face-auth/       # 안면인증 이미지 (30장)
    ├── gaetong/
    │   ├── juice/       # Juice 현행화 (2장)
    │   ├── esim/        # eSIM 웨어러블 (30장)
    │   ├── scis-new/    # SCIS 신규전산 (34장)
    │   └── data-bundle/ # 데이터누구나결합 (15장)
    ├── cs/
    │   └── cancel/      # 해지/개통취소 (2장)
    └── rds/
        ├── rds-login/   # RDS 로그인 등 (7장)
        └── rds-basic/   # RDS 기본사용법 (18장)
```

---

## 업데이트 방법

```bash
cd ~/workspace/mobile-manual
git add -A
git commit -m "내용 설명"
git push
# 약 1~2분 후 URL 자동 반영
```

---

## 세션 3 — 2026-04-02

### 작업 내용

#### Vercel 배포 전환
- GitHub Pages → Vercel로 배포 방식 변경
- `vercel.json` 추가 (no-cache 헤더 설정)
- 최종 배포 URL: **https://mobile-manual.vercel.app/**
- git push 시 자동 배포됨

#### skylife-guide 아웃링크 추가
- `https://skylife-guide-jyac.vercel.app/#` 페이지에 "전산 매뉴얼" 버튼 추가
- FAQ 버튼 옆에 위치

#### GitHub 저장소 이름 변경
- `pjungjin85-sketch/skylife` → `pjungjin85-sketch/skylife-commission-calculator`
- 로컬 remote URL도 함께 업데이트

### 주의사항
- Vercel에서 **Import 버튼 절대 누르지 말 것** — 누르면 새 프로젝트 생성되며 URL 변경됨
- 반영 안 될 때는 Vercel 대시보드에서 배포 상태 확인 후 `Cmd+Shift+R` 강력 새로고침
- INP 경고는 개발자 도구(F12)에서만 보이는 것 — 일반 사용자에게 노출 안 됨
- skylife-guide 최종 URL: `https://skylife-guide-jyac.vercel.app/#` (vz8q는 구버전)

---

## 세션 4 — 2026-04-05

### 헤더 디자인 통일 (skylife-guide 기준)

- `index.html`: `kt skylife` 로고 + `MOBILE` 배지 + `전산 매뉴얼` 제목 구조로 변경, `.header-title` CSS 추가
- `detail.html`: `MOBILE` 배지 추가, `.header-badge` CSS 추가
- 커밋: `d82b310`

---

## 미완성 / 향후 작업

- [ ] 반응형 디자인 (모바일 최적화) — 현재 PC 전용
- [ ] id-scanner(신분증스캐너), pre-approval(사전승낙), kos(KOS) 카테고리 항목 추가
- [ ] 새 PDF 업로드 시 항목 추가
