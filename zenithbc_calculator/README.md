# 두산위브더제니스 부천 자금계획 계산기

입주자모집공고 제2026000382호(2026.08.12. 부천시청 주거정비과 승인)를 토대로 만든
**참고용** 계산기입니다. 세부 일정·옵션 금액·중도금 금리 및 이자는 실제와 다를 수 있으며,
판단은 반드시 공급계약서 원문과 금융기관·사업주체의 공식 안내로 확인하십시오.

공개 주소: https://ghjeon.github.io/zenithbc_calculator/

## 파일

| 파일 | 설명 |
|---|---|
| `index.html` | 배포본. React를 포함해 전부 인라인된 단일 파일이라 외부 의존성이 없습니다. |
| `app.jsx` | 원본 소스. 수정은 이 파일에서 하고 아래 명령으로 다시 빌드합니다. |

이 저장소 루트에 `.nojekyll`이 있어 GitHub Pages가 Jekyll 처리 없이 파일을 그대로
서빙합니다. 따라서 `index.html`에는 front matter를 넣지 마십시오.

## 다시 빌드하기

```bash
cd zenithbc_calculator
npm i --no-save esbuild@0.24.0 react@18.3.1 react-dom@18.3.1

cat > entry.jsx <<'ENTRY'
import React from "react";
import { createRoot } from "react-dom/client";
import App from "./app.jsx";
createRoot(document.getElementById("root")).render(<App />);
ENTRY

npx esbuild entry.jsx --bundle --minify --format=iife --target=es2019 \
  --define:process.env.NODE_ENV='"production"' --outfile=bundle.js
```

그 다음 `index.html`의 `<script>` ... `</script>` 사이 내용을 `bundle.js`로 교체합니다.
`entry.jsx`, `bundle.js`, `node_modules`는 커밋하지 않습니다.

## 계산 근거

- 분양가·층별 세대수·납부일정·주택형별 옵션가 — 입주자모집공고 제2026000382호 원문
- 계약금 2차 일자 차이 — 무순위(사후) 공고 제2026910241호(2026.09.16.)
- 인지세 — 공고문에 실린 기재금액별 표, 사업주체(또는 은행)와 계약자 각 50%
- 중도금 대출 보증료 — HUG 주택구입자금보증 연 0.130% 단일요율
  (`보증금액 × 요율 × 보증기간/365`)
- 취득세 — 전용 85㎡ 이하 현행 세율, 지방교육세 포함

중도상환수수료는 기본 0%로 두었습니다. 대환이 아닌 자기자금 상환은 통상 면제이나
반드시 대출 약정서에서 확인해야 합니다.
