# Seongwon Kim — 개인 학술 홈페이지

[al-folio](https://github.com/alshedivat/al-folio) 테마(Jekyll)를 기반으로 구축된 개인 학술 홈페이지입니다.

---

## 목차

1. [로컬 미리보기 실행](#1-로컬-미리보기-실행)
2. [GitHub Pages 배포 체크리스트](#2-github-pages-배포-체크리스트)
3. [논문 추가 방법](#3-논문-추가-방법)
4. [뉴스 추가 방법](#4-뉴스-추가-방법)
5. [프로젝트 추가 방법](#5-프로젝트-추가-방법)
6. [프로필 사진 교체](#6-프로필-사진-교체)
7. [CV 업데이트](#7-cv-업데이트)
8. [페이지 구조](#8-페이지-구조)

---

## 1. 로컬 미리보기 실행

Docker를 사용하므로 Ruby나 Jekyll을 별도로 설치할 필요 없습니다.

### 사전 조건

- [Docker Desktop](https://www.docker.com/products/docker-desktop) 설치 완료

### 실행 방법

```bash
# 프로젝트 디렉토리로 이동
cd /home/seongwon/homepage

# 최초 1회: 이미지 빌드 (약 3~5분 소요)
docker compose pull

# 서버 실행 (http://localhost:8080 에서 미리보기)
docker compose up
```

브라우저에서 `http://localhost:8080` 을 열면 사이트를 확인할 수 있습니다.
파일을 수정하면 자동으로 새로고침됩니다.

### 종료

```bash
# Ctrl+C 로 중지하거나:
docker compose down
```

---

## 2. GitHub Pages 배포 체크리스트

아래 단계를 순서대로 진행하면 `https://SeongwonKim0111.github.io` 에 사이트가 배포됩니다.

- [ ] **레포지토리 생성**: GitHub에서 `SeongwonKim0111.github.io` 라는 이름의 **public** 레포지토리를 생성합니다.
- [ ] **레포지토리 Push**:
  ```bash
  cd /home/seongwon/homepage
  git remote set-url origin https://github.com/SeongwonKim0111/SeongwonKim0111.github.io.git
  git checkout -b main
  git add -A
  git commit -m "Initial homepage setup based on al-folio"
  git push -u origin main
  ```
- [ ] **GitHub Pages 설정**: 레포지토리 → Settings → Pages → Source: **Deploy from a branch** → Branch: **gh-pages** → Save
- [ ] **Actions 권한 설정**: Settings → Actions → General → Workflow permissions → **Read and write permissions** 체크
- [ ] **첫 배포 확인**: Actions 탭에서 "Deploy site" 워크플로우가 성공적으로 실행되는지 확인 (약 3~5분 소요)
- [ ] **프로필 사진 업로드**: `assets/img/prof_pic.jpg` 로 교체 (아래 [섹션 6](#6-프로필-사진-교체) 참고)
- [ ] **CV 업로드**: `assets/pdf/cv_seongwon_kim.pdf` 파일을 추가 (아래 [섹션 7](#7-cv-업데이트) 참고)

---

## 3. 논문 추가 방법

논문은 `_bibliography/papers.bib` 파일에 BibTeX 형식으로 추가합니다.

### 기본 예시 (최소 필드)

```bibtex
@article{kim2025myslam,
  abbr={IROS},
  bibtex_show={true},
  title={Robust LiDAR-Visual SLAM for Dynamic Environments},
  author={Kim, Seongwon and Kim, Pyojin},
  journal={IEEE/RSJ International Conference on Intelligent Robots and Systems},
  year={2025},
  selected={true},
}
```

### 전체 필드 예시 (PDF, arXiv, 코드, 동영상, 썸네일 포함)

```bibtex
@article{kim2025myslam,
  abbr={IROS},
  bibtex_show={true},
  title={Robust LiDAR-Visual SLAM for Dynamic Environments},
  author={Kim, Seongwon and Kim, Pyojin},
  journal={IEEE/RSJ International Conference on Intelligent Robots and Systems (IROS)},
  year={2025},
  abstract={We propose a novel LiDAR-visual SLAM system...},
  preview={myslam_thumbnail.png},
  pdf={myslam_2025.pdf},
  arxiv={2501.12345},
  code={https://github.com/SeongwonKim0111/myslam},
  website={https://seongwonkim0111.github.io/projects/myslam},
  video={https://www.youtube-nocookie.com/embed/YOUR_VIDEO_ID},
  selected={true},
}
```

### 썸네일 이미지 추가

`preview` 필드에 지정한 이미지 파일을 `assets/img/publication_preview/` 에 저장합니다.

```
assets/img/publication_preview/myslam_thumbnail.png  ← 여기에 저장
```

### PDF 파일 추가

로컬 PDF는 `assets/pdf/` 폴더에 저장하고 `pdf={파일명.pdf}` 로 참조합니다.

```
assets/pdf/myslam_2025.pdf  ← 여기에 저장
```

### 내 이름 자동 볼드 처리

`_config.yml` 의 `scholar` 섹션에 이름이 등록되어 있습니다:

```yaml
scholar:
  last_name: [Kim]
  first_name: [Seongwon, S.]
```

`author` 필드에 `Kim, Seongwon` 또는 `Kim, S.` 형식으로 쓰면 자동으로 **볼드** 처리됩니다.

---

## 4. 뉴스 추가 방법

뉴스 항목은 `_news/` 폴더에 마크다운 파일로 추가합니다.

### 인라인 뉴스 (짧은 한 줄 공지)

파일명 형식: `YYYY_짧은설명.md`

```markdown
---
layout: post
date: 2026-09-01 09:00:00+0900
inline: true
related_posts: false
---

Paper accepted to IROS 2026!
```

### 상세 뉴스 (클릭 가능한 긴 글)

```markdown
---
layout: post
date: 2026-09-01 09:00:00+0900
title: "Paper Accepted at IROS 2026"
inline: false
related_posts: false
---

Our paper "Robust LiDAR-Visual SLAM" has been accepted to IROS 2026.
The paper will be presented in ...
```

뉴스는 날짜 기준으로 최신순 자동 정렬됩니다.

---

## 5. 프로젝트 추가 방법

프로젝트는 `_projects/` 폴더에 마크다운 파일로 추가합니다. `importance` 값이 낮을수록 먼저 표시됩니다.

### 파일 예시: `_projects/2_depth_estimation.md`

```markdown
---
layout: page
title: Depth Estimation
description: Monocular depth estimation for robot navigation using deep learning.
img: assets/img/projects/depth_preview.gif
importance: 2
category: research
related_publications: false
---

### Overview

프로젝트 설명을 여기에 작성하세요.

### Demo

<div class="row">
    <div class="col-sm mt-3 mt-md-0">
        {% include figure.liquid path="assets/img/projects/depth_result.png" title="Depth result" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
```

### 카드 이미지 (GIF/PNG)

카드에 표시할 이미지/GIF는 `assets/img/projects/` 에 저장하고, 프론트매터의 `img:` 필드에 경로를 지정합니다.

```
assets/img/projects/depth_preview.gif  ← 여기에 저장
```

---

## 6. 프로필 사진 교체

1. 사진 파일을 `prof_pic.jpg` 로 이름 변경 (권장 크기: 400×400px 이상, 정방형)
2. `assets/img/prof_pic.jpg` 로 덮어쓰기

---

## 7. CV 업데이트

1. PDF 파일을 `cv_seongwon_kim.pdf` 로 준비
2. `assets/pdf/cv_seongwon_kim.pdf` 에 저장

---

## 8. 페이지 구조

| 페이지 | 파일 | URL | 내비게이션 |
|--------|------|-----|----------|
| About (메인) | `_pages/about.md` | `/` | 자동 (홈) |
| News | `_pages/news.md` | `/news/` | ✅ |
| Publications | `_pages/publications.md` | `/publications/` | ✅ |
| Projects | `_pages/projects.md` | `/projects/` | ✅ |
| CV | `_pages/cv.md` | `/cv/` | ✅ |
| Blog | `_pages/blog.md` | `/blog/` | 숨김 |
| Teaching | `_pages/teaching.md` | `/teaching/` | 숨김 |

내비게이션에 페이지를 추가하려면 해당 파일의 프론트매터에서 `nav: true` 로 변경하면 됩니다.

---

## 주요 파일 위치

```
homepage/
├── _config.yml              ← 사이트 전체 설정 (이름, 이메일, 링크 등)
├── _bibliography/
│   └── papers.bib           ← 논문 목록 (BibTeX)
├── _news/                   ← 뉴스 항목
├── _projects/               ← 프로젝트 카드
├── _pages/
│   ├── about.md             ← 메인 페이지 (바이오)
│   ├── publications.md      ← 논문 목록 페이지
│   ├── projects.md          ← 프로젝트 페이지
│   ├── cv.md                ← CV 페이지
│   └── news.md              ← 뉴스 페이지
├── assets/
│   ├── img/
│   │   ├── prof_pic.jpg             ← 프로필 사진
│   │   ├── publication_preview/     ← 논문 썸네일
│   │   └── projects/                ← 프로젝트 이미지/GIF
│   └── pdf/
│       └── cv_seongwon_kim.pdf      ← CV PDF
└── .github/
    └── workflows/
        └── deploy.yml       ← 자동 배포 설정
```
