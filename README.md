# 🦊 콤부차의 오르내림

휴대폰 중심의 개인 등산 기록 웹사이트입니다. GitHub Pages에서 무료로 정적 웹페이지를 공개하고, Firebase Authentication / Firestore / Storage로 관리자 로그인과 사진 저장을 처리합니다.

## 먼저 미리보기

`index.html`을 GitHub Pages에 올리면 지도를 볼 수 있습니다. Firebase 설정 전에는 기록 등록과 로그인 기능이 비활성화됩니다. 지도에 보이는 회색 산은 예시로 수록한 주요 산 약 20곳이며, 전체 산 목록이 아닙니다. 좌표는 대략적인 참고 위치이므로 공식 산행 안내나 내비게이션 용도로 사용하지 마세요.

## Firebase 설정 (필수)

1. https://console.firebase.google.com 에서 프로젝트를 만듭니다.
2. Authentication → Sign-in method → **이메일/비밀번호**를 활성화하고, Authentication → Users에서 본인 관리자 계정을 생성합니다. 해당 사용자의 **UID**를 복사합니다. 공개 회원가입 화면은 제공하지 않습니다.
3. Firestore Database를 만들고 Storage도 활성화합니다. **Storage는 요금제/지역에 따라 Blaze 결제 계정 연결이 필요할 수 있습니다.** 사용량과 과금 정책을 Firebase 콘솔에서 확인하세요.
4. 프로젝트 설정 → 웹 앱 등록 후 나온 구성값을 `firebase-config.js`에 입력합니다. `ADMIN_UID`에도 2번에서 복사한 UID를 입력합니다. Firebase 웹 앱 구성값은 공개되어도 되지만 **비밀번호나 서비스 계정 비밀키는 절대 저장소에 올리지 마세요.**
5. `firestore.rules`와 `storage.rules`의 `REPLACE_WITH_ADMIN_UID`를 같은 UID로 교체하고, Firebase 콘솔의 각 서비스 **Rules** 탭에 붙여넣어 게시합니다. 관리자 UID 제한을 적용하지 않고 테스트 모드로 공개하지 마세요.
6. Authentication → Settings → Authorized domains에서 GitHub Pages 도메인(`계정명.github.io`)을 승인합니다. 이메일/비밀번호 로그인은 브라우저에서 작동합니다.
7. 관리자로 로그인한 뒤 산 이름을 검색하고 검색 결과에서 위치를 선택하여 기록을 저장합니다. 사진은 최대 10장, 각 10MB 이하이며 브라우저에서 JPEG로 축소·압축됩니다.

## GitHub Pages 게시

1. GitHub에서 새 **public repository**를 만들고 이 폴더의 파일과 `assets` 폴더를 그대로 업로드합니다.
2. Settings → Pages → Build and deployment → Deploy from a branch → `main` / `(root)` → Save.
3. 몇 분 후 `https://계정명.github.io/저장소명/` 주소로 접속합니다. 사진은 Firebase Storage에 저장되고 GitHub 저장소에 업로드되지 않습니다.

## 참고

- 사이트는 누구나 읽을 수 있고, 기록의 쓰기 권한은 관리자 UID로 제한됩니다.
- 공개 사이트이므로 사진·벙주 이름 등 공개 동의를 확인하세요.
- 지도는 OpenStreetMap 타일과 Leaflet을 사용합니다. 검색은 OpenStreetMap Nominatim 공개 서비스를 사용하므로 과도한 자동 검색은 피하세요. 검색 결과는 확인 후 선택해야 합니다.
- 저장소/Firestore/Storage 사용량에 따라 비용이 발생할 수 있습니다.
- 이 버전의 통계는 **등록된 본인 참여 산행**만 집계합니다. 같은 산을 여러 번 가면 다녀온 산은 1개, 산행 횟수는 방문 횟수만큼 증가합니다.
