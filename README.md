# Argus Daily Site Prestart

현장 Daily Site Prestart를 폰이나 PC에서 작성하고, 서명하고, 원본 양식과 똑같은 PDF로 보내는 단일 페이지 앱이에요.

## 파일 구성

| 파일 | 설명 |
|---|---|
| `index.html` | 앱 전체. pdf-lib 라이브러리와 원본 PDF 양식이 파일 안에 들어 있어 서버나 빌드가 필요 없음 |
| `.nojekyll` | GitHub Pages가 Jekyll 처리를 건너뛰도록 하는 빈 파일 |
| `THIRD_PARTY_NOTICES.md` | pdf-lib (MIT) 라이선스 |

## GitHub Pages에 올리기

1. GitHub에서 새 저장소를 만든다 (예: `argus-prestart`).
2. 이 폴더의 파일을 전부 올린다.
   ```bash
   cd argus-prestart
   git init
   git add .
   git commit -m "Daily site prestart"
   git branch -M main
   git remote add origin git@github.com:<계정>/argus-prestart.git
   git push -u origin main
   ```
3. 저장소 **Settings → Pages**에서 Source를 **Deploy from a branch**, Branch를 `main` / `/ (root)`로 선택하고 저장한다.
4. 1~2분 뒤 `https://<계정>.github.io/argus-prestart/` 에서 열린다.
5. 크루 폰에서 이 주소를 열고 브라우저 메뉴의 "홈 화면에 추가"를 하면 앱처럼 쓸 수 있다.

## 공개 범위 주의

- GitHub Free 계정에서는 **공개 저장소**만 Pages로 배포된다. 이 경우 `index.html` 안의 직원 이메일 주소와 회사 양식이 누구나 볼 수 있는 상태가 된다.
- Pro / Team 요금제에서는 저장소를 비공개로 둘 수 있지만, **Pages 사이트 주소 자체는 공개**다. 사이트 접근 제한은 GitHub Enterprise Cloud에서만 가능하다.

## 이메일 목록 수정

`index.html`에서 `DEFAULT_CONTACTS`를 찾아 이름과 이메일을 고치면 모든 사용자에게 반영된다. 앱에서 "+ Add new person…"으로 추가한 사람은 그 기기(브라우저)에만 저장된다.

## 보내기 동작

| 버튼 | 폰 (https로 열었을 때) | PC 또는 공유가 안 될 때 |
|---|---|---|
| Save PDF | PDF 저장 | PDF 저장 |
| Email PDF | 공유 시트로 메일 앱에 PDF 첨부 | PDF 저장 후, 주소·제목·본문이 채워진 메일 창을 연다 (첨부는 직접) |
| WhatsApp | 공유 시트에서 WhatsApp을 고르면 PDF 첨부 (단체방 가능) | PDF 저장 후, 요약이 채워진 WhatsApp을 연다 (첨부는 직접) |

브라우저만으로는 PDF를 첨부해 자동으로 보낼 수 없다. 자동 발송이 필요하면 별도 서버가 있어야 한다.

## 알려진 제한

- PDF는 Helvetica 폰트를 쓰기 때문에 영어만 출력된다. 한글은 `?`로 찍힌다.
- 작성 중인 내용은 같은 탭을 새로고침할 때만 유지된다. 새 창을 열면 항상 빈 양식으로 시작한다.
- 코멘트가 항목 줄에 다 들어가지 않으면 PDF 2페이지에 전체 내용이 출력된다.
- 양식 문구나 레이아웃을 바꾸면 PDF 좌표(`fillPrestart` 함수)도 함께 맞춰야 한다.
