# FAA A&P 학습 사이트 프로젝트 — 인수인계

> 새 채팅 시작 시 이 문서를 업로드하고 "이어서 작업해줘"라고 말씀하시면 됩니다.

---

## 1. 프로젝트 개요

방인배(inbae)의 FAA A&P 자격 준비용 **이중언어(한/영) 학습 사이트 2개**를 운영·개선 중입니다.

| 사이트 | GitHub | URL |
|---|---|---|
| Airframe | `inbeabang-wq/airframe` | inbeabang-wq.github.io/airframe |
| Powerplant | `inbeabang-wq/powerplant` | inbeabang-wq.github.io/powerplant |

**작업 환경**: Mac (macOS), 모든 파일은 사용자가 직접 GitHub에 업로드
**응답 규칙**: 한국어 존댓말, 영어 용어 병기, 단계별 정리, Mac 기준 안내

---

## 2. 현재 상태 (2026-07-16 갱신) — 두 사이트 모두 완성 단계

### Airframe (18개 챕터)

| 항목 | 상태 |
|---|---|
| 챕터 | ch01~ch18 |
| FAA 도면 갤러리 | **1,193개** (v3 추출, 900px) + ch13 도면 2건 신규(13-131, 13-28) |
| 잘린/플레이스홀더 도면 | **전부 해결** (2-7·2-9·13-55·13-131·13-28) — 2026-07-16 완료 |
| 구술시험 | 406문항 (18챕터 전부) |
| ASA 교재 보강 | **13챕터** — 기존 8(ch02·10·11·13·14·15·16·17) + ch18 + **신규 5(ch01·ch03·ch04·ch09·ch12)** |
| 반응형 CSS / 영어 병기 | 전 챕터 완비 |

### Powerplant (11개 챕터)

| 항목 | 상태 |
|---|---|
| 챕터 | ch01~ch11 |
| FAA 도면 갤러리 | 584개 참조 (얼룩 17개 제거본 반영, 고아 파일 17개는 images 폴더에 잔존·무해) |
| 구술시험 | **295문항** (11챕터 전부, ch05·ch08·ch11 포함 — 업로드 확인 완료) |
| ASA 교재 보강 | 10챕터 (ch01~ch10, ch11 LSA는 대응 교재 없음) |

---

## 3. 이번 세션(2026-07-16) 작업 내역 — 스캔본 ASA 교재 보강 완료

스캔 이미지 PDF 4개를 **tesseract OCR**(dpi 170, lang eng)로 추출 → 기존 챕터와 중복을 피해 교재 고유 내용만 1섹션씩 보강했습니다.

| 교재 PDF | 대상 챕터 | 추가한 섹션(고유 내용) |
|---|---|---|
| 02 METALLIC | ch01 | 금속 재료와 열처리 (알루미늄 4자리 합금·템퍼·용체화/석출 열처리·클래딩·Mg/Ti) |
| 02 METALLIC | ch04 | 리벳 품질 평가·불량 리벳 제거 (성형머리 1.5D×0.5D, 불량 유형, 제거 4단계, NACA법) |
| 03 NONMETALLIC | ch03 | 현대 폴리에스터 외피 시스템 (Poly-Fiber/Ceconite/Superflite, 열수축, STC) |
| 03 NONMETALLIC | ch06·ch07 | **스킵** — 나뭇결 1:15·카세인·레조르시놀(ch06), 진공백·안전(ch07) 이미 완비 |
| 05 HYDRAULIC | ch12 | 유압 펌프의 종류 (정용량 베인/기어/제로터/피스톤 vs 가변용량 컴펜세이터) |
| 07 ELECTRICAL | ch09 | 반도체 회로 제어소자 (다이오드·제너·바이폴라 트랜지스터·SCR) |

**공통 규칙**: 한/영 병기(`en-text`) + `📗 ASA 보강` 배지(`src-badge`, CSS 없으면 추가) + 구술(s-oral) 섹션 앞에 삽입 + TOC 항목 추가. 삽입마다 BeautifulSoup으로 섹션수·TOC앵커·깨진링크·JS 검증.

### 도면 5건 교체 (같은 세션)
- ch02 Figure 2-7(네 가지 힘)·2-9(윙팁보텍스), ch13 Figure 13-55(시미댐퍼): 기존 이미지 양호 확인 후 본문 삽입 → **라이브 반영 완료**
- ch13 Figure 13-131(타이어 구조)·13-28(휠얼라인): 사용자가 핸드북 캡처 제공 → HTML 반영, 이미지는 `images/`에 업로드

---

## 4. 미업로드 / 확인 필요 (사용자 작업 대기)

이번 세션 산출물 중 GitHub 반영 여부를 새 채팅에서 먼저 확인할 것:

```bash
cd /tmp && git clone --depth 1 https://github.com/inbeabang-wq/airframe.git af
```

- ch01·ch04 : 반영 완료(라이브)로 확인됨
- **ch03·ch09·ch12** : 업로드 대기 가능성 → `grep -c 'src-badge' af/ch03_fabric_covering.html` 등으로 확인 (2면 반영됨)
- **ch13 이미지 2건** : `ls af/images/ch13_fig13-131.jpg af/images/ch13_fig13-28.jpg` — 없으면 아직 미반영. HTML은 이 파일을 참조하므로 없으면 깨진 이미지로 뜸. 반드시 `images/` **폴더 안**에 올릴 것(루트 아님)

> ⚠️ 겪었던 이슈: 사용자가 폴더 통째로 GitHub 웹 업로드 시 신규 이미지가 누락되곤 함. 이미지는 저장소의 `images/` 폴더로 들어간 뒤 Add file→Upload files 할 것.

---

## 5. 남은 작업 (선택)

스캔본 교재 보강과 잘린 도면은 **모두 종료**됨. 이후 확장 작업:

1. **학습 도구 추가** — 통합 검색, 북마크, 오답노트 등
2. **@AEROMECHEXPERT 콘텐츠** — 수요일 K-Defense Weekly + MRO 캐러셀 (전용 스킬 보유)
3. Powerplant images 폴더 고아 파일 17개 정리(무해, 선택)

---

## 6. 핵심 자료 위치

### 구글 드라이브
| 자료 | 파일 ID / 폴더 ID |
|---|---|
| ASA Powerplant 교재 (20개 챕터 PDF) | 폴더 `1iGgiwMsr1rOamamsaAJcv3MAaS97uXts` |
| ASA 교재 부모 폴더 | `1J6eAL5LLJ0wi4zJ6dd3y-zMHzpda_RwU` |
| FAA-H-8083-31B (Airframe 핸드북, 112MB) | `1VxeOKXnbkn7Ti4hOuBniL1xiM6INbIp2` |
| amt_powerplant_handbook.pdf (FAA-H-8083-32B, 214MB) | `1SNPUvSkpBoptsPBeW8IgNzjBSpYq71lZ` |

### 스캔본 ASA Airframe 교재 (이번 세션 사용, 사용자 업로드)
- `02 METALLIC AIRCRAFT STRUCTURES.pdf` (110p)
- `03 NONMETALLIC AIRCRAFT STRUCTURES.pdf` (96p)
- `05 HYDRAULIC AND PNEUMATIC POWER SYSTEMS.pdf` (100p)
- `07 AIRCRAFT ELECTRICAL SYSTEMS.pdf` (96p)
- 모두 **텍스트 레이어 없는 스캔본** → OCR 필수. 남은 스캔본 교재(General·기타)가 더 있으면 같은 방식으로 보강 가능

> ⚠️ 10MB 초과 파일은 Claude가 직접 다운로드 불가. 작업 환경 프록시가 drive.google.com·faa.gov 차단(403). 대용량은 사용자 Mac에서 처리.

---

## 7. OCR 파이프라인 (이번 세션 검증 완료)

스캔본 교재 보강 시 표준 절차:

```python
import fitz, pytesseract
from PIL import Image
import io, os
d = fitz.open('교재.pdf')
for pno in range(d.page_count):
    fp = f'/tmp/pages/p{pno:03}.txt'
    if os.path.exists(fp): continue           # 재개 가능(resumable)
    pix = d[pno].get_pixmap(dpi=170)
    img = Image.open(io.BytesIO(pix.tobytes('png')))
    open(fp,'w').write(pytesseract.image_to_string(img, lang='eng'))
```

- `tesseract 4.1.1` 사용 가능, dpi 170이면 품질 양호(리벳/펌프/회로 용어 정확)
- 샌드박스 bash 45초 제한 → **페이지별 파일로 저장하며 배치로 나눠 실행**(한 배치 ~18-24p)
- 필요 라이브러리: `pip3 install pymupdf pytesseract pillow --break-system-packages`

### 고유 내용 선별 원칙 (매우 중요)
기존 챕터는 이미 충실(11~20 섹션). 교재 OCR 후 **핵심 용어를 기존 HTML에 grep**해서 이미 있으면 스킵, 없는 것만 1섹션으로 압축. (예: ch06 나뭇결 1:15·카세인 이미 있어 스킵, ch09 제너·트랜지스터 이론 없어 추가)

---

## 8. HTML 구조 규칙 (수정 시 필수 참고)

### 공통
- 섹션: `<section id="s-xxx" class="comp"><div class="comp-head"><h3>한국어</h3><span class="comp-en">English</span>...</div><div class="comp-body"><div class="comp-text"><p>...</p></div></div></section>`
- 문단 영어 병기: `<p>한국어<span class="en-text">English</span></p>`
- TOC: `<li><a href="#s-xxx" data-target="s-xxx">한국어 <span class="en">English</span></a></li>` — s-oral 항목 앞에 삽입
- 챕터 순서: 본문 섹션들 → `s-oral`(구술) → `s-faa-figures`(도면) → `s-quiz`(기출)
- **파일은 미니파이(긴 한 줄)** → grep 시 과매칭 주의, 파이썬으로 처리 권장

### ASA 보강 배지
```html
<h3>제목 <span class="src-badge">📗 ASA 보강</span></h3>
```
CSS 없으면 `</style>` 앞에 추가:
```css
.src-badge{display:inline-block;margin-left:8px;font-family:'JetBrains Mono',monospace;font-size:10.5px;color:#34D399;background:rgba(52,211,153,.12);border:1px solid rgba(52,211,153,.3);border-radius:5px;padding:2px 7px;vertical-align:middle;}
```

### 도면 (본문 인라인)
```html
<figure class="fig"><img src="images/chXX_figX-Y.jpg" alt="figX-Y" loading="lazy"><figcaption>Figure X-Y. 제목. <span class="figpdf">(FAA-H-8083-31B)</span></figcaption></figure>
```
- 갤러리 컨테이너는 `.figgal`, 출처: airframe=`FAA-H-8083-31B`, powerplant=`FAA-H-8083-32B`

---

## 9. 작업 시 주의사항 (경험칙)

1. **정규식 DOTALL 과매칭 주의** — 미니파이 HTML에서 `<figure ...>.*?특정도면.*?</figure>`를 `re.S`로 돌리면 **앞의 다른 블록까지 삼킴**(이번 세션 실제 발생, ch13 원복 후 리터럴 교체로 해결). 여러 블록 중 하나만 바꿀 땐 **완전한 리터럴 문자열**로 `.replace()` 할 것.
2. **이미지 품질 자동판정 불신** — 통계 말고 `Read`(view)로 눈으로 확인. (이번 세션 2-7·2-9·13-55는 "잘림 의심"이었으나 실제로 양호했음)
3. **기존 챕터 매우 충실** — ASA 보강은 중복 회피, 교재 고유 내용만 압축. 겹치면 과감히 스킵.
4. **명령어 안내 시 주석(`#`) 섞지 말 것** — zsh에서 에러. 한 줄씩 코드블록 분리.
5. **git 이슈** — `~/Downloads/airframe`이 git repo가 아니게 되는 일 있었음(Downloads 자동정리 추정). 깨지면 `mv airframe airframe_old` 후 재클론. 사용자는 GitHub 웹 업로드("Add files via upload")도 병행함 → 로컬 `git status`가 "nothing to commit"이면 이미 웹으로 올라간 것.
6. **파일 전달 후** GitHub 반영 여부를 재클론·grep으로 검증할 것.

---

## 10. 검증 코드 스니펫 (BeautifulSoup 구조 검증)

```python
from bs4 import BeautifulSoup
import os
raw = open(fn).read(); s = BeautifulSoup(raw,'html.parser')
ids = [x.get('id') for x in s.select('section.comp')]
tgt = [a.get('data-target') for a in s.select('a[data-target]')]
missing = [t for t in tgt if t and t not in ids]      # TOC 앵커 누락
broken = [im['src'] for im in s.select('img[src^="images/"]') if not os.path.exists(im['src'])]
print(len(ids),'섹션 | TOC누락',missing,'| 깨진이미지',broken,'| JS', 'orxToggle' in raw)
```
> GitHub Pages·FAA.gov는 봇 차단(403). 라이브 검증 불가 → 로컬 클론 후 검증.

---

## 11. 새 채팅 시작 시 체크리스트

```bash
cd /tmp
git clone --depth 1 https://github.com/inbeabang-wq/airframe.git af
git clone --depth 1 https://github.com/inbeabang-wq/powerplant.git pp
```

먼저 확인:
- `ls af/images/ch13_fig13-131.jpg af/images/ch13_fig13-28.jpg` (도면 2건 반영 여부)
- `grep -c src-badge af/ch03_fabric_covering.html af/ch09_electrical.html af/ch12_hydraulic_pneumatic.html` (ASA 보강 반영 여부, 2면 OK)
