# HANDOFF — Airframe ASA 기출문제 이식 프로젝트

> 최종 업데이트: 2026-07-10 5차 (토론토) · 상태: **실물 책 페이지 64~137p 전체 이식 완료 ✅ (도면 문항 제외)**

## 1. 프로젝트 개요
- 사이트: FAA Airframe 학습 웹사이트 (GitHub Pages)
- 리포: `inbeabang-wq/airframe` · 로컬 클론: `/home/claude/airframe`
- 목표: ASA/FAA Airframe 기출문제를 챕터별 퀴즈 섹션 + 모의고사(mock_exam.html) QB에 이식
- 반영 방법: push 자격증명 없음 → 사용자가 GitHub 웹 업로드로 수정 파일 교체

## 2. 진행 현황 (완료표)

| 챕터 | 파일 | 총 카드 | ASA 문항 | ASA 번호대 |
|---|---|---|---|---|
| ch01 구조 | ch01_aircraft_structures.html | 34 | 16 | 8259–8304 |
| ch02 공력·리깅 | ch02_aerodynamics_rigging.html | 40 | 30 | 8212–8228(회전익), 8216–8659 |
| ch03 패브릭 | ch03_fabric_covering.html | 18 | 10 | 8015–8024, 8096 |
| ch04 판금 | ch04_metal_repair.html | 40 | 25 | 8044–8173 |
| ch05 용접 | ch05_welding.html | 24 | 12 | 8179–8211 |
| ch06 목재 | ch06_wood_structure.html | 20 | 10 | 8002–8099 |
| ch07 복합재 | ch07_composites.html | 30 | 20 | 8052–8098 |
| ch08 도장·마감 | ch08_painting.html | 24 | 12 | 8026–8040 |
| ch09 전기 | ch09_electrical.html | 139 | 133 | 8803–8933, 8963–8968, 8912-1/2 (도면 8909/8910 제외) — 전기 챕터 완결 |
| ch10 계기 | ch10_instruments.html | 76 | 66 | 8586–8646, 8940, 8941, 8948–8950, 8938, 8939, 8842, 8874, 8599, 8600, 8610-1, 8601-1 |
| ch11 통신·항법 | ch11_comm_nav.html | 64 | 54 | 8618–8697, 8870, 9036–9038 (도면 8693/8694 시리즈 제외, 8659는 ch02) |
| ch12 유압·공압 | ch12_hydraulic_pneumatic.html | 44 | 34 | 8386–8401, 8434–8487 |
| ch13 착륙장치 | ch13_landing_gear.html | 30 | 16 | 8316–8375, 8951–8962, 9039 |
| ch14 연료 | ch14_fuel_systems.html | 120 | 110 | 8698–8802, 8707-1~8710-6, 8746-1/2 (도면 8706, 정답불일치 8710-7 제외) — 연료 챕터 완결 |
| ch15 방빙·제우 | ch15_ice_rain.html | 39 | 27 | 8969–8996 — 방빙 챕터 완결 |
| ch16 객실 환경 | ch16_cabin_environment.html | 102 | 88 | 8497–8585, 9029/9030(물·폐수) |
| ch17 화재 방지 | ch17_fire_protection.html | 40 | 30 | 8997–9028 (도면 9020/9021 제외) — 화재 챕터 완결 |

- **mock_exam.html QB: 총 884문항** (전 챕터 동기화 완료)
- 근거 자료: 사용자가 업로드한 실물 ASA Airframe Test Guide 페이지 64–103 (유압 후반·환경·계기·통신항법·연료 전체). 미이식(도면 필요): 8542(Fig.13), 8572(Fig.14), 9020/9021(Fig.21), 8706(Fig.17), 8693/8694+8694-1~13(Fig.16/22~34), 8688/8689는 공식만으로 풀이 가능해 이식함. 8710-7은 책 정답표[C]와 해설(B 지지)이 불일치하여 보류.

## 3. 구조·규칙 (변경 금지)
- 각 챕터 `<section id="s-quiz">` 내 `iqcard` 카드: 문제 KO + `<span class="en-text">`EN, 보기 3개 A/B/C `iqPick(this,'정답문자')`, `iqToggle` 해설, 해설 끝 `(ASA NNNN)` 표기. ASA 카드에는 oral 섹션 없음.
- 새 카드는 s-quiz의 `</section>` 직전 삽입, 라벨 `기출문제 <span class="iq-n">NN문항</span>` 갱신.
- mock_exam.html: `var QB=[...];` JSON. 필드: id(cXqN)/ch/chko/ko/en/ok/oe/ans/xk/xe/fg(null 또는 base64 도면).
- chko 명칭 확정: ch8 도장·마감 / ch9 항공기 전기 계통 / ch10 항공기 계기 계통 / ch11 통신·항법 / ch12 유압·공압 계통 / ch14 항공기 연료 계통 / ch15 방빙·제우 계통 / ch16 객실 환경 제어 / ch17 화재 방지 계통.
- **ASA 번호는 절대 임의 생성 금지.** web_search로 원문·정답이 검증된 번호만 사용.
- 빌드 도구: `/home/claude/work/asa_common.py` → `build(chfile, chnum, chko, Q, start_idx, old_label)`. 실행은 반드시 `cd /home/claude/airframe` 후 (상대경로 사용). Q 항목: `(asa, ko질문, en질문, [(ko보기,en보기)×3], 정답인덱스, ko해설, en해설)`.

## 3.5 practical_acs.html 이중언어화 (2026-07-10 완료)
- 구술 92문항 + 실기 프로젝트 연계(DME) 26문항 전체에 영어 질문·Model Answer 병기 완료.
- 구조: 질문 뒤 `<span class="en-q">`, 답안 뒤 `<span class="en-a">` 삽입. CSS는 </style> 직전에 .en-q/.en-a 추가됨.

## 3.9 전기계통 이식 (2026-07-10 완료)
- ch09에 신규 123문항 이식 완료(16→139). 도면 문항 8909(Fig.18)/8910(Fig.19)만 제외.

## 3.95 ASA 공식 구술 기출 이식 (2026-07-11 완료 ✅)
- 근거: 책 p.139~167 (Oral & Practical Study Guide). practical_acs.html에 "ASA 공식 구술 기출" 섹션 신설, 이중언어 카드로 이식.
- 빌더: /home/claude/work/oral_common.py (add_orals) — 카드 id 자동 연번, 진행 카운터 총계 자동 갱신.
- 완료(전체): ACS 샘플 17, 금속 35, 목재 13, 패브릭 19, 비행조종 17, 기체검사 13, 착륙장치 23, 유압 22, 환경 27, 계기 29, 통신항법 22, 연료 22, 전기 19, 방빙 15, 화재 17, 회전익 4 = 314문항. **구술 카드 총 406문항** (기존 92 + 신규 314). 책 p.139~167 구술 파트 완결.
- 선택 잔여: 각 주제의 Typical Practical Projects 목록(수행 과제) — 필요 시 실기 프로젝트 섹션에 요약 이식 가능.
- 2026-07-11: 실기 프로젝트 13개의 DESCRIPTION/GIVEN/PERFORMANCE STANDARD 본문 39건 영어 병기 완료(<span class="en-q"> 삽입). 페이지 소개문을 "실기 13개 + 구술 406문항"으로 갱신.
- Typical Practical Projects 목록(각 주제별)은 선택 작업 — 필요 시 프로젝트 섹션에 요약 이식.

## 4. 남은/선택 작업
1. (선택) 도면(Figure) 필요 문항 추가: ch17 9020/9021 (Fig.21 압력-온도 차트), 기타 챕터 도면 문제 — fg 필드에 base64 이미지 넣는 방식은 검증 완료.
2. (선택) ch11 오토파일럿 vs ch02 요댐퍼(8659) 주제 배분 검토.
3. 사용자 GitHub 웹 업로드 반영 확인 후 사이트(inbeabang-wq.github.io) 동작 점검.

## 5. 검증 방법 (세션 시작 시)
```bash
cd /home/claude/airframe
python3 - <<'EOF'
import re, json
qb = json.loads(re.search(r'var QB=(\[.*?\]);', open('mock_exam.html').read(), re.S).group(1))
print('QB:', len(qb))
from collections import Counter; print(Counter(q['ch'] for q in qb))
EOF
```
