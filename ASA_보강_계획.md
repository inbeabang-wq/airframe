# ASA AMT 교재로 기존 사이트 보강 계획

## 교재 정보
- **ASA Aviation Maintenance Technician Series Vol.2 (Airframe Systems)**
- 기존 FAA-H-8083-31B와 다른 책 → 더 상세한 실무 설명·회로 동작·정비 절차 포함
- 텍스트 추출 정상 확인 (구글 드라이브 챕터별 PDF)

## 보강 원칙
- **중복 제외**: 기존 사이트에 이미 있는 개념은 건너뜀
- **신규 보강**: 교재에만 있는 상세 내용을 별도 섹션으로 추가
- 추가 섹션에는 "📗 ASA AMT Vol.2 보강" 배지 표시로 출처 구분
- 기존 한/영 병기 형식(.comp 섹션) 그대로 유지

## 파일 ↔ 사이트 챕터 매핑
| ASA 교재 PDF | 사이트 챕터 |
|---|---|
| 01 BASIC AERODYNAMICS | ch02 공력·리깅 |
| 02 METALLIC STRUCTURES | ch01 구조, ch04 금속수리 |
| 03 NONMETALLIC STRUCTURES | ch03 우포, ch06 목재, ch07 복합재 |
| 04 ASSEMBLY & RIGGING | ch02 리깅 |
| 05 HYDRAULIC/PNEUMATIC | ch12 유압·공압 |
| 06 LANDING GEAR | ch13 착륙장치 |
| 07 ELECTRICAL | ch09 전기 |
| 08 FUEL SYSTEMS | ch14 연료 |
| 09 CABIN ATMOSPHERE | ch16 객실환경 |
| 10 INSTRUMENTS | ch10 계기 |
| 11 COMM/NAV | ch11 통신·항법 |
| 12 ICE/RAIN | ch15 방빙 |
| 13 FIRE PROTECTION | ch17 화재방지 ✅ 완료 |
| 14 INSPECTION | (신규 챕터 또는 실기·검사) |

## 진행 상황
- ✅ **ch17 화재방지 완료** — 3개 섹션 보강:
  1. 완전한 화재 방지 계통 (엔진/APU/화물칸/휠웰/라바토리)
  2. 탐지기 정비·서비싱 (검사 5항목)
  3. 소화 계통 정비 (압력/온도 보간 계산, HRD 카트리지)

## 다음
- ch17 검토 후, 나머지 13개 챕터를 같은 방식으로 순차 보강
- 챕터당 교재 정독 → 기존 대조 → 신규 섹션 2~4개 추가

---
## 이미지 추가 (2026-07-12 업데이트)
ASA 교재 PDF에서 도면을 직접 추출해 보강 섹션에 삽입하는 워크플로 확립:
1. 구글드라이브 PDF 다운로드 → PyMuPDF로 페이지 렌더링(dpi 170~200)
2. OCR(tesseract)로 Figure 캡션 y좌표 특정 → 도면 영역 크롭
3. JPEG 압축(quality 82) → base64 임베드 → `<figure class="fig">`로 삽입

### ch17 삽입 도면 3개
- Figure 13-14 HRD 소화병 단면 (완전한 계통 섹션)
- Figure 13-20 그로밋 설치 (탐지기 정비 섹션)
- Figure 13-22 압력/온도 차트 (소화 계통 정비 섹션)

각 도면 캡션에 "📗 ASA AMT Vol.2" 출처 표기.
