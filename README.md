# 우선심사 신청 길라잡이 웹앱 (2026.11.1 기준)

지식재산처 발행 「누구나 따라하는 우선심사 신청 길라잡이」(2026. 11. 1. 기준) 내용을 담은
반응형 PWA 웹앱입니다. GitHub Pages에 그대로 올려 사용할 수 있습니다.

## GitHub Pages 배포 방법

1. GitHub에 새 저장소(Repository)를 만듭니다. (예: `priority-review-guide`)
2. 이 폴더의 **모든 파일과 폴더 구조 그대로**를 업로드합니다.
   - 웹에서 올리기: 저장소 → **Add file → Upload files** → `index.html`, `manifest.json`,
     `sw.js`, `README.md`, `icons/` 폴더 전체를 드래그 → **Commit changes**
   - 또는 명령어:
     ```bash
     git init
     git add .
     git commit -m "우선심사 신청 길라잡이 웹앱 최초 배포"
     git branch -M main
     git remote add origin https://github.com/<아이디>/<저장소명>.git
     git push -u origin main
     ```
3. 저장소 → **Settings → Pages** → *Build and deployment* →
   **Source: Deploy from a branch**, **Branch: main / (root)** 선택 → **Save**
4. 1~2분 후 `https://<아이디>.github.io/<저장소명>/` 로 접속합니다.
   - 첫 접속 후 "앱 설치" 버튼(또는 모바일 브라우저 메뉴 → *홈 화면에 추가 / 앱 설치*)으로
     홈 화면에 앱처럼 추가할 수 있습니다.
   - 서비스 워커가 첫 방문 이후 **오프라인에서도 동작**합니다.
   - GitHub Pages는 HTTPS를 기본 제공하므로 PWA 설치·오프라인 기능이 정상 동작합니다.

## 파일 구성

| 파일 | 설명 |
|------|------|
| `index.html` | 앱 본체 (콘텐츠·스타일·스크립트 전부 포함) |
| `manifest.json` | PWA 설치 정보 (아이콘·이름·시작 URL) |
| `sw.js` | 서비스 워커 (오프라인 캐시) |
| `icons/` | 앱 아이콘 (192 / 512 / 마스커블 / 파비콘) |

## 주요 기능

- 반응형 레이아웃 (데스크톱 사이드바 / 모바일 하단 탭·드로어)
- 테마 3종 (흰색·아이보리·검은색) + 글자 크기 조절 — 선택 저장
- 전체 검색, FAQ 91건 카테고리 필터·아코디언
- 신청 전 체크리스트 (체크 상태 저장)
- 심사 착수 기한 계산기
- PWA: 홈 화면 설치, 오프라인 사용, iOS 홈 화면 추가 안내
- 이 앱 공유(Web Share API), 인쇄/PDF 저장

## 안내

본 웹앱은 지식재산처 발행 자료(참고용 길라잡이)를 재구성한 것으로,
자세한 사항은 우선심사 고시와 관련 공고(www.moip.go.kr)를 확인하시기 바랍니다.

## 고시·공고 변경 알림 (GitHub Actions) 사용법

앱은 방문 시 `version.json`을 읽어 헤더에 버전 배지를 표시하고, 이전 방문 때와
버전이 바뀌었으면 홈 화면에 "새 버전 안내" 배너를 띄웁니다.

`version.json`은 저장소의 `.github/workflows/update-version.yml`이 자동 갱신합니다.

1. 저장소 **Settings → Actions → General → Workflow permissions**에서
   *"Read and write permissions"*를 허용해 두세요 (기본값이 허용인 경우 그대로 사용).
2. 워크플로우는 **매주 월요일**(한국시간 12시)에 지식재산처 고시공고 목록 페이지를
   가져와 정규화 해시를 비교하고, 내용이 바뀌었으면 `version.json`의
   확인일·안내 문구를 갱신해 자동 커밋합니다 → GitHub Pages가 재배포됩니다.
3. 페이지 주소가 바뀌면 워크플로우 안의 `MOIP_URL` 값을 수정하세요.
   Actions 탭의 *"고시·공고 변경 확인"*에서 **Run workflow**로 수동 실행할 수도 있습니다.
4. 실제 내용 반영(판본 번호 올리기)은 사람이 확인합니다: 고시공고 원문을 읽고
   `version.json`의 `version`(예: `2026.11.1` → `2027.1.1`)과 본문을 업데이트하면
   방문자에게 갱신 배너가 표시됩니다.

> 참고: 지식재산처 누리집은 RSS를 제공하지 않아(2026. 11. 기준 확인) 목록 페이지
> 해시 비교 방식을 사용합니다. 페이지 구조가 바뀌면 감지가 조용히 실패할 수 있으니
> 가끔 Actions 실행 기록을 확인하세요.
