# 조직도 생성기 PWA

텍스트 입력으로 조직도를 만들고 SmartArt, Excel, 이미지, PNG로 내보낼 수 있는 정적 웹 앱입니다. GitHub Pages에서 바로 배포할 수 있도록 PWA 파일과 Pages Actions 워크플로를 포함합니다.

## 파일 구성

- `index.html`: 앱 본문과 PWA 메타 태그
- `manifest.json`: 앱 이름, 시작 URL, 아이콘, 설치 정보
- `service-worker.js`: 오프라인 실행을 위한 앱 셸 캐시
- `404.html`: GitHub Pages 진입 경로 보정
- `.nojekyll`: GitHub Pages 정적 파일 처리
- `.github/workflows/deploy-pages.yml`: `main` 브랜치 push 시 Pages 자동 배포
- `example-state.json`: 예시 파일 데이터
- `icons/`: PWA 및 홈 화면 아이콘

## GitHub Pages 배포

1. 이 폴더의 파일을 GitHub 저장소 `main` 브랜치에 올립니다.
2. GitHub 저장소에서 `Settings > Pages`로 이동합니다.
3. `Build and deployment`의 `Source`를 `GitHub Actions`로 설정합니다.
4. `Actions` 탭에서 `Deploy PWA to GitHub Pages`가 성공하면 배포 URL이 생성됩니다.

GitHub Pages는 HTTPS를 제공하므로 서비스 워커와 PWA 설치 조건을 만족합니다.

## 로컬 확인

```powershell
python -m http.server 32123
```

브라우저에서 `http://127.0.0.1:32123/index.html`로 접속합니다. 로컬호스트도 PWA 테스트에 허용됩니다.

## 배포 후 캐시 갱신

앱 파일을 수정했는데 사용자의 화면이 오래된 버전으로 남으면 `service-worker.js`의 `CACHE_NAME` 값을 올린 뒤 다시 배포합니다.
