# RIEN 서버 가이드

## 파일 구성

| 파일 | 역할 |
|---|---|
| `index.html` | 화면과 기능. 디자인을 바꿀 때만 건드립니다. |
| `data.json` | 모든 수치와 문구. **내용 수정은 여기서만 합니다.** |

## 깃허브 배포

1. 깃허브에서 새 저장소를 만듭니다. (Public)
2. `index.html` 과 `data.json` 두 파일을 올립니다.
3. 저장소 **Settings → Pages** 로 들어가 Branch 를 `main`, 폴더를 `/ (root)` 로 지정하고 저장합니다.
4. 1~2분 뒤 `아이디.github.io/저장소명` 으로 접속됩니다.

## 내용 수정

깃허브 저장소에서 `data.json` 을 열고 연필 아이콘을 눌러 고친 뒤 커밋하면 됩니다.
1분 이내에 사이트에 반영됩니다. `index.html` 은 다시 올릴 필요가 없습니다.

### 자주 쓰는 수정 위치

- **강화 재료·확률** → `enhance`
  - `costStone`, `costMeso` 를 바꾸면 계산기도 같이 바뀝니다.
  - 증폭 확률표는 `enhance.amp.table` 의 `["결과","확률","수치 변동"]` 형식입니다.
- **영혼석 재료** → `soul` 의 `fragPerUnit` / `purifyPerUnit` / `mesoPerUnit`
- **히든 스킬** → `hiddenSkills` 에 `{ "name", "category", "meso", "desc" }` 추가
- **연금술 아이템** → `alchemy.items` 에 `["분류","이름", 경험치, "하위 재료"]` 추가
  - 새 분류를 넣으면 탭이 자동으로 생깁니다.
  - 하위 재료 열을 쓰는 분류는 `alchemy.upgradeCategories` 에 이름을 넣어주세요.
- **아이템 정보** → `items.list` 에 아이템 추가
  - `rows` 는 위쪽 요약 항목, `stats` 는 확률표입니다.
  - `stats` 의 각 줄은 `{"name":"힘","tiers":[["+0","90%"],["+1~+3","5%"], …]}` 형식이고, 칸 수는 `items.tierHeaders` 와 맞춰주세요.
  - 아이템을 추가하면 상단 탭이 자동으로 늘어납니다.
- **스킬** → `skills`
  - 궁극기는 `skills.ultimates` 에 `{"group":"전사","job":"히어로","name":"스킬명","type":"궁극기","rows":[["항목","값"], …]}` 형식으로 추가합니다.
  - 패치 내역은 `skills.patches` 에 `{"group":"전사","job":"히어로","changes":["스킬명 — 변경 내용", …]}` 형식입니다.
  - `group` 은 상단 필터 버튼이 되고, 새 값을 쓰면 버튼이 자동으로 생깁니다.
- **일일퀘스트 등급** → `quest.dailyGrades`
- **요일별 재료** → `quest.weekday.rows` 에 `["금요일","아이템 1개"]` 추가하고, 다 채우면 `note` 를 지웁니다.
- **필드보스** → `quest.bosses` 에 `["이름", 개수, 경험치, 메소]` 추가
- **퀘스트** → `quest.quests` 에 `{ "name", "mat", "effect", "reward" }` 추가
  - `reward` 는 숫자만 씁니다. 초반루트 순서가 이 값 기준으로 자동 정렬됩니다.
- **홍포 상점** → `shop.items` 에 아이템을 넣고, `shop.order` 에서 묶음을 구성합니다.
  - `numbered: true` 면 번호가 붙고, `false` 면 점 없는 목록으로 나옵니다.
  - `pre` 에 선행 아이템 이름을 적으면 포인트 계산에 자동 반영됩니다.
- **추천 초반루트** → `route.stages`. 단계 수를 늘리거나 줄이면 퀘스트가 자동으로 나눠집니다.
- **오늘의 팁** → `dailyTips`
- **기본 팁** → `basicTips`
- **메뉴 제목·설명** → `sections`, 홈 카드는 `home`

## 주의

- `data.json` 은 쉼표 하나만 빠져도 사이트가 안 열립니다. 수정 후 <https://jsonlint.com> 에 붙여넣어 확인하면 안전합니다.
- 파일을 더블클릭해서 여는 방식은 브라우저 보안 정책 때문에 `data.json` 을 못 읽습니다. 웹 주소로 접속해서 확인하세요.
