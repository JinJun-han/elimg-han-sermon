# 새 설교 추가 가이드

분기마다 1편씩 정선된 설교를 추가합니다. 매주 업데이트가 목표가 아닙니다.

## 1. 설교 HTML 파일 생성

`sermons/001-luke-1-5-7.html`을 복사하여 새 파일을 만듭니다.

```
sermons/002-{book}-{chapter}-{verse}.html
```

예: `sermons/002-matthew-5-3-12.html` (마태복음 5:3-12, 팔복)

파일 내용은 기존 001 구조를 따릅니다 — 9개 언어 탭, 오디오 플레이어, YouTube 임베드, 공유 버튼.

## 2. index.html SERMONS 배열에 추가

`index.html` 약 353번째 줄의 `const SERMONS = [...]` 배열에 객체 추가:

```javascript
{
  id: '002',
  date: '2026.MM.DD',
  title: '설교 제목',
  subtitle: '부제목',
  reference: '성경 구절',
  category: 'gospel' | 'ot' | 'epistle' | 'special',
  desc: '설교 요약 (1~2문장)',
  tags: ['태그1', '태그2', '태그3'],
  langs: '🇰🇷🇺🇸🇻🇳... (n개 언어)',
  url: 'sermons/002-filename.html'
}
```

카테고리:
- `gospel` — 복음서 (마태·마가·누가·요한)
- `ot` — 구약
- `epistle` — 서신서
- `special` — 절기·기념일 설교

## 3. sitemap.xml 업데이트

```xml
<url>
  <loc>https://elimg-han-sermon.netlify.app/sermons/002-filename.html</loc>
  <lastmod>2026-MM-DD</lastmod>
  <changefreq>yearly</changefreq>
  <priority>0.8</priority>
</url>
```

## 4. 통계 업데이트 (선택)

`index.html`의 hero-stats에서:
- 설교 편 수: `<div class="hs-num" id="sermonCount">1</div>` → 자동 카운트 (JS가 SERMONS.length로 갱신)
- 언어 수: 누적 9개 언어가 줄지는 않음

## 5. 커밋·푸시

```powershell
cd D:\Dev\projects\elimg-han-sermon
git add sermons/002-* index.html sitemap.xml
git commit -m "content: 설교 #002 추가 — {제목}"
git push
```

Netlify가 1~2분 내 자동 배포합니다. **Cloudflare 아닙니다 — wrangler 불필요**.

## 다국어 번역 워크플로

1. 한국어 설교 원문 작성 (목사님 직접 또는 luke 에이전트 협력)
2. GPT-4 / Gemini Pro로 각 언어 번역 (영어 → 베트남어 → 인도네시아어 등 1차)
3. 모국어 화자 검토 (가능한 경우)
4. 설교 HTML 9개 언어 탭에 붙여넣기
5. 오디오 녹음 → `.m4a`로 sermons/ 폴더에 배치
6. (선택) Google TTS API로 각 언어 음성 생성

## 분기 갱신 페이스

- 1분기: 002 추가
- 2분기: 003 추가
- 3분기: 004 추가
- 4분기: 005 추가 + 연간 회고

연 4편 = 5년 후 20편 아카이브. 양보다 깊이가 자산입니다.
