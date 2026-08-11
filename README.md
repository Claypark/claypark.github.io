# claypark.github.io

**⚠️ 이 레포를 삭제하거나 GitHub Pages를 끄지 말 것.**

과거 Jekyll 블로그("Doodle")였으나 2026-08-11에 걷어냈다.
지금 이 레포의 존재 이유는 단 하나다.

## 1. `app-ads.txt`를 도메인 루트에 서빙한다 (필수)

AdMob은 스토어 등록정보의 **개발자 웹사이트(마케팅 URL) 도메인**에서
`/app-ads.txt`를 **도메인 루트로만** 크롤링한다. 서브패스는 보지 않는다.

| 경로 | 인증 |
|------|------|
| `https://claypark.github.io/app-ads.txt` | ✅ 크롤링 대상 (이 레포) |
| `https://claypark.github.io/dev-page/app-ads.txt` | ❌ 안 봄 (소스 사본일 뿐) |

GitHub Pages에서 `claypark.github.io` 도메인 루트를 잡을 수 있는 건
user-site 레포인 **이 레포뿐**이다. 이 레포가 죽으면 루트 `app-ads.txt`가
404가 되고 Google AdMob / Meta Audience Network / Unity Ads 인증이
전부 깨져 광고 fill이 0이 된다.

**`app-ads.txt`를 수정할 때는 `Claypark/dev-page` 레포의 사본
(`dev-page/app-ads.txt`)도 반드시 같이 갱신할 것.**

## 2. 루트 접속을 앱 소개 페이지로 넘긴다

`index.html`과 `404.html`은 `/dev-page/`로 보내는 리다이렉트 문서다.
쿼리스트링(`?lang=ja`, `?utm_source=...`)은 `index.html`에서 보존해 넘긴다.

실제 콘텐츠는 전부 별도 레포에 있다:

- 앱 소개 페이지 · 각 앱 개인정보처리방침 → `Claypark/dev-page` (`/dev-page/`)
- Amen(Selah) 방침·약관 → `Claypark/selah-pages`
- 오운완 방침·약관 → `Claypark/ounwan-pages`
- 대나무숲 방침·약관 → `Claypark/juk-forest-pages`

## 구성

```
index.html    → /dev-page/ 리다이렉트 (쿼리스트링 보존)
404.html      → /dev-page/ 리다이렉트 (도메인 전체 404 폴백)
app-ads.txt   → ★ 광고 인증 본체. 함부로 지우지 말 것
.nojekyll     → Jekyll 빌드 비활성화 (정적 파일 그대로 서빙)
```

상세 배경: mi-app 레포 `docs/refs/rf-02-admob-config.md`
