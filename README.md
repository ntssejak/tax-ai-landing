# Tax AI 랜딩페이지 (GitHub Pages)

세무 AI 업무 플랫폼 **Tax AI**의 진입(랜딩) 페이지입니다.

- **[Tax AI] 버튼 → 로그인 모달 → 지정 서버 분기**: 계정을 Supabase `users` 테이블로 검증한 뒤,
  `users.Server` 컬럼에 지정된 서버(웹서버 app.py `_server_redirect`와 동일 규칙)를 **새 탭**으로 엽니다.
  로그인 창이 뜬 랜딩 탭의 주소표시줄은 끝까지 GitHub 주소를 유지합니다.
- **로그인 1회 인계**: 랜딩은 https, 업무 서버는 http라 브라우저 혼합콘텐츠 정책으로 iframe·직접 fetch가
  차단됩니다. 그래서 검증은 https인 Supabase로 하고, 이동할 서버에는 `#a=<base64url(uid␞pw)>` 해시로
  증명을 넘겨 서버 쪽 index.html(자동로그인 패치)이 같은 출처로 `/api/login`을 호출해 세션까지 만듭니다.
  해시는 서버 쪽이 받자마자 주소창에서 지우고, 패치 전 서버로 보내면 기존 로그인창이 뜹니다(안전 폴백).
- **Server 컬럼 미지정·전체관리자 계정**은 기본 서버①(`http://134.185.114.30/taxai/`)로 연결됩니다.

## 파일
- `index.html` — 페이지 전체(외부 의존성 없음, 다크 모드 지원)
- `.nojekyll` — Jekyll 가공 없이 원본 그대로 서빙

## 관리
- 이 폴더는 배포 마스터(`V:\Tax_AI_Linux_배포`)의 일부 — GitHub Pages 저장소에 그대로 push합니다.
- 업무 서버 쪽 인계(자동로그인) 패치는 `web\index.html`과 `Tax_AI_Windows_배포\web\index.html`에
  적용되어 있고 `sync_web.ps1`로 서버 4곳에 배포합니다.
