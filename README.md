1. 프로젝트 목적
본 프로젝트의 목적은 Gmail로 수신되는 이메일을 자동으로 분류하고, 그 결과를 Trello에 업
무 카드로 생성하는 자동화 워크플로우를 구현하는 것이다. 이를 통해 사용자가 메일을 직접
확인하고 Trello에 수동으로 업무를 등록하는 과정을 줄이고자 하였다. 2. 전체 자동화 흐름
Gmail에서 메일 수신 → 메일 제목 기준으로 HIGH/NORMAL 판단 → 조건에 따라 분기 →
Trello의 HIGH 또는 NORMAL 리스트에 카드 자동 생성
제목에 high 포함 → HIGH 리스트에 카드 생성
제목에 normal 포함 → NORMAL 리스트에 카드 생성
3. 도구별 구현 과정
3-1. Zapier 구현
Gmail(Email by Zapier)을 트리거로 설정하여 새 이메일 도착 시 자동화 시작
Paths 기능으로 조건 분기 구성
Path A: 제목에 high 포함 → Trello HIGH 리스트에 카드 생성
Path B: 제목에 normal 포함 → Trello NORMAL 리스트에 카드 생성
Zap 활성화 (즉시 실행 방식)
3-2. Make 구현
Gmail 모듈을 트리거로 설정하여 새 이메일 감시
Router로 흐름을 두 갈래로 분기
각 경로에 Filter 조건 설정
제목에 high 포함 → Trello HIGH 리스트에 카드 생성
제목에 normal 포함 → Trello NORMAL 리스트에 카드 생성
시나리오 활성화 (15분 주기 자동 실행)
4. 테스트 결과
테스트를 위해 제목에 high와 normal이 포함된 이메일을 각각 발송하였다. 그 결과 high가
포함된 이메일은 Trello의 HIGH 리스트에, normal이 포함된 이메일은 NORMAL 리스트에
카드로 생성되었다. 이를 통해 두 도구 모두 자동화가 의도한 대로 정상 작동함을 확인하였
다. 5. Zapier vs Make 비교분석
구분 Zapier Make
자동화 단위 Zap Scenario
시작 조건 Trigger Trigger Module
분기 방식 Paths Router + Filter
실행 방식 즉시 자동 실행 예약 실행 (15분 주기)
구조 단계별 나열형, 단순 흐름도 기반, 시각적
6. 사용 소감 및 평가
두 도구 모두 동일한 목표를 달성할 수 있었으나, 개인적으로는 Make가 제작 과정이 더 쉬웠
다. Make는 전체 워크플로우가 흐름도 형태로 화면에 시각적으로 표시되어, 데이터가 어디서
어디로 흘러가는지 한눈에 파악할 수 있었다. Router와 Filter로 분기를 구성하는 과정도 직
관적이었다. 반면 Zapier는 단계가 세로로 나열되는 구조라 설정 자체는 단순했지만, 분기가 많아질수록
전체 구조를 파악하기 어렵다고 느꼈다. 7. 결론
이번 실습을 통해 트리거 → 조건 분기 → 액션으로 이어지는 자동화의 기본 구조를 이해하
고, Zapier와 Make 두 도구로 동일한 워크플로우를 구현하였다. 두 도구 모두 Gmail과
Trello를 연결한 업무 분류 자동화를 성공적으로 구현했으며, 시각적 편집 환경 측면에서는
Make가 더 사용하기 쉬웠다는 결론을 얻었다. 세부과정
이메일이 도착하면 내용을 확인해서
중요한 메일은 HIGH 업무로, 일반 메일은 NORMAL 업무로 분류한 뒤
Trello에 자동으로 카드가 생성되게 하는 것
즉, 사람이 직접 메일을 보고 Trello에 업무 카드를 만드는 과정을 자동화한 것입니다. 2. 자동화 흐름 요약
전체 흐름은 이렇게 됩니다. Gmail에서 메일 수신
↓
메일 제목이나 라벨을 기준으로 HIGH / NORMAL 판단
↓
조건에 따라 분기
↓
Trello의 HIGH 리스트 또는 NORMAL 리스트에 카드 생성
예를 들면, 메일 제목: high 서버 오류 발생
→ HIGH로 판단
→ Trello HIGH 리스트에 카드 생성
메일 제목: normal 회의 자료 요청
→ NORMAL로 판단
→ Trello NORMAL 리스트에 카드 생성
3. 왜 mail을 사용했는가?
이번 작업에서는 이메일이 들어오는 순간부터 업무가 시작된다고 가정했습니다. 그래서 mail을 트리거로 사용했습니다. 트리거란?
트리거는 자동화를 시작하게 만드는 조건입니다. 이번 경우에는:
새로운 이메일이 도착함
이 트리거
즉,mail에 새 메일이 오면 자동화가 시작됩니다. 4. 왜 HIGH / NORMAL로 나누었는가?
모든 메일의 중요도가 같지는 않습니다. 그래서 업무를 두 종류로 나누었습니다. HIGH: 중요하거나 긴급한 메일
NORMAL: 일반적인 메일
이렇게 나누면 Trello에서 업무 우선순위를 쉽게 볼 수 있습니다. 5. 왜 Trello를 사용했는가?
Trello는 업무를 카드 형태로 관리하는 도구입니다. 1. 해야 할 일을 한눈에 볼 수 있다. 2. HIGH / NORMAL로 우선순위를 구분할 수 있다. 3. 메일을 놓치지 않고 업무로 관리할 수 있다. 4. 팀원들과 공유하기 쉽다. 즉, Gmail은 메일을 받는 곳이고, Trello는 업무를 관리하는 곳입니다. 6. Trello에서 리스트를 만든 이유
Trello 보드 안에 두 개의 리스트를 만들었습니다. HIGH
NORMAL
이유는 자동화가 분류한 결과를 눈에 보이게 정리하기 위해서입니다. 중요 메일 → HIGH 리스트
일반 메일 → NORMAL 리스트
그래서 사용자는 Trello만 봐도 어떤 업무가 중요한지 바로 알 수 있습니다. 7. Zapier에서는 어떤 과정을 했는가?
Zapier에서는 하나의 Zap 안에서 자동화를 만들었습니다. 흐름은 다음과 같습니다. Gmail에서 새 이메일 감지
↓
Paths 기능으로 조건 분기
↓
HIGH 조건이면 Trello HIGH 리스트에 카드 생성
↓
NORMAL 조건이면 Trello NORMAL 리스트에 카드 생성
Zapier의 핵심 기능: Paths
Zapier에서 사용한 핵심은 Paths입니다. Paths는 조건에 따라 작업 흐름을 나누는 기능입니다. 메일 제목에 high가 있으면 Path A 실행
메일 제목에 normal이 있으면 Path B 실행
즉, Zapier에서는 Paths를 이용해서 HIGH와 NORMAL을 구분했습니다. 8. Make에서는 어떤 과정을 했는가?
Make에서도 비슷한 자동화를 만들었습니다. 흐름은 다음과 같습니다. Gmail 모듈에서 새 이메일 감시
↓
Router로 흐름을 두 갈래로 나눔
↓
각 경로에 Filter 조건 설정
↓
HIGH 조건이면 Trello HIGH 리스트에 카드 생성
↓
NORMAL 조건이면 Trello NORMAL 리스트에 카드 생성
Make의 핵심 기능: Router와 Filter
Make에서는 Router와 Filter가 핵심입니다. Router
Router는 흐름을 여러 방향으로 나누는 장치입니다.
하나의 이메일
↓
HIGH 경로
NORMAL 경로
이렇게 갈라주는 역할을 합니다. Filter
Filter는 각 경로로 갈 조건을 정하는 기능입니다. 즉, Router가 길을 나누고, Filter가 어떤 길로 갈지 판단합니다. 9. Zapier와 Make의 차이
두 도구 모두 같은 목표를 달성했습니다. 하지만 구현 방식이 조금 다릅니다. 구분 Zapier Make
자동화 이름 Zap Scenario
시작 조건 Trigger Trigger Module
분기 방식 Paths Router + Filter
실행 방식 자동 실행 중심 예약 실행 또는 Run once
구조 단계별로 단순함 흐름도가 시각적으로 보임
쉽게 말하면:
Zapier는 Paths로 분기한다. Make는 Router와 Filter로 분기한다. 목표는 같지만, 도구에서 사용하는 방식이 다릅니다. 10. 테스트 메일을 보내서 자동화가 제대로 작동하는지 확인해
그래서 제목에 high, normal이 들어간 메일을 보냈습니다.  복사
high urgent test
normal test
이 메일들이 Trello에 각각 들어가는지 확인했습니다. 결과는 다음과 같았습니다. high 메일 → Trello HIGH 리스트에 카드 생성
normal 메일 → Trello NORMAL 리스트에 카드 생성
따라서 자동화가 정상적으로 작동한다고 판단할 수 있었습니다.
make는 15분마다 Gmail 확인
하도록 설정했습니다. 12. 최종 결과
최종적으로 다음 기능이 완성되었습니다. Gmail에 메일이 도착하면
메일의 제목을 기준으로 HIGH 또는 NORMAL로 분류하고
Trello의 해당 리스트에 자동으로 카드가 생성된다. 즉, 이메일 기반 업무 분류와 Trello 카드 생성이 자동화되었습니다. 프로젝트 목적
이 프로젝트의 목적은 Gmail로 수신되는 이메일을 자동으로 분류하고, 그 결과를 Trello에 업
무 카드로 생성하는 자동화 워크플로우를 구현하는 것이다. 이를 통해 사용자가 메일을 직접
확인하고 Trello에 수동으로 업무를 등록하는 과정을 줄이고자 하였다. 구현 과정
먼저 Gmail을 트리거로 설정하여 새로운 이메일이 도착하면 자동화가 시작되도록 하였다. 이
후 메일 제목에 포함된 키워드를 기준으로 HIGH와 NORMAL로 분류하였다. Zapier에서는
Paths 기능을 사용하여 조건 분기를 구현하였고, Make에서는 Router와 Filter를 사용하여
같은 분기 구조를 구현하였다. 분기된 결과에 따라 Trello의 HIGH 또는 NORMAL 리스트에
카드가 자동으로 생성되도록 설정하였다. 테스트 결과
테스트를 위해 제목에 high와 normal이 포함된 이메일을 각각 발송하였다. 그 결과 high가
포함된 이메일은 Trello의 HIGH 리스트에 카드로 생성되었고, normal이 포함된 이메일은
NORMAL 리스트에 카드로 생성되었다. 이를 통해 자동화가 의도한 대로 정상 작동함을 확인
하였다. 결론
이번 실습을 통해 이메일 수신, 조건 분기, 업무 카드 생성으로 이어지는 자동화 워크플로우
를 구축하였다. Zapier와 Make는 모두 자동화를 구현할 수 있지만, Zapier는 Paths를 사용
하여 비교적 단순하게 분기하고, Make는 Router와 Filter를 사용하여 시각적으로 흐름을 구
성한다는 차이가 있었다. 최종적으로 두 도구 모두 Gmail과 Trello를 연결하여 업무 분류 자
동화를 성공적으로 구현하였다. 한계 및 개선 방안
본 실습에서는 자동화 구조를 검증하기 위해 메일 제목의 키워드(high/normal)를 분류 기준
으로 사용하였다. 그러나 실제 환경에서는 발신자가 이러한 키워드를 포함해 메일을 보내지
않으므로, 이 기준을 그대로 사용하기는 어렵다.
이를 개선하기 위해서는 분기 조건을 다음과 같이 변경할 수 있다.발신자 주소를 기준으로 상
사나 주요 거래처의 메일을 HIGH로 분류하는 방법 또는 워크플로우 중간에 AI(ChatGPT) 모
듈을 추가하여 메일 내용을 분석해 중요도를 판단하게 하는 방법이있다
중요한 점은 이러한 개선 시에도 본 실습에서 구축한 트리거 → 조건 분기 → 액션 구조는 그
대로 유지되며, 분기 조건만 교체하면 된다는 것이다. 즉, 본 실습은 실무 자동화로 확장 가능
한 기본 구조를 구현했다는 데 의의가 있다.
1. UI/UX 개념
UI (User Interface, 사용자 인터페이스)
→ 화면에 "보이는 것" : 버튼, 메뉴, 색상, 배치
UX (User Experience, 사용자 경험)
→ 사용하면서 "느끼는 것" : 편리함, 직관성, 배우기 쉬운 정도
쉬운 비유: UI는 식당의 인테리어, UX는 그 식당에서의 식사 경험 전체예요. 2. Zapier vs Make — UI/UX 비교
화면 구성 위→아래 목록형 (설문지 채우듯) 시각적 다이어그램 (원과 선으로 연결)
워크플로우 파악 단계를 펼쳐봐야 앎 전체 흐름이 한눈에 보임
분기 표현 Paths (목록 안에서 갈라짐) Router (선이 실제로 갈라져 보임)
학습 난이도 쉬움 (초보자 친화적) 처음엔 낯설지만 익숙해지면 강력
테스트/디버깅 단계별 테스트 각 모듈 위에 데이터 말풍선 표시
보고서에 쓸 핵심 문장 예시:
Zapier는 순차적 목록형 UI로 진입장벽이 낮고, Make는 시각적 플로우차트형 UI로 복잡한
분기 구조를 직관적으로 파악할 수 있다. 실제로 HIGH/NORMAL 분기 구현 시 Make의
Router는 흐름이 시각적으로 갈라져 이해가 쉬웠던 반면, Zapier의 Paths는 단계를 클릭해
들어가야 구조를 확인할 수 있었다. Zapier : 약 7,000개 이상의 앱 연동 (업계 최다) 
Make : 약 1,500~2,000개 앱 연동
Zapier가 더 넓어요. 특히 마이너한 서비스, 최신 SaaS 툴까지 지원하는 폭이 넓습니다. Make는 개수는 적지만, HTTP 모듈로 API를 직접 호출할 수 있어서 지원 목록에 없는 서비
스도 연동 가능해요 (단, 기술 지식 필요).
⚠주의: 앱 개수는 계속 변하니까, 보고서 제출 전에 각 공식 홈페이지에서 최신 숫자를 확
인하고 "2024년 기준, 공식 홈페이지 참조" 식으로 출처를 달아주세요!
4. 무료 플랜 비교
항목 Zapier 무료 Make 무료
월 실행 한도 100 tasks 1,000 operations
워크플로우 단계 2단계만 가능 (트리거+액션 1개) 제한 없음 (멀티스텝 OK)
분기(Paths/Router) ❌ 유료 ✅ 무료 가능
실행 주기 15분 폴링 15분 폴링
중요한 포인트 :
숫자만 보면 Make가 10배 넉넉해 보이지만, 단위가 달라요. Zapier의 1 task = 액션 1번 실
행, Make의 1 operation = 모듈 1개 실행(트리거, 필터 통과 등도 카운트)이라 단순 비교는
어려워요. 그래도 실질적으로 Make 무료 플랜이 훨씬 관대하다는 평가가 일반적이에요. 5. 총정리 — 장단점 & 적합한 상황
Zapier
장점 ✅
- 연동 앱 수 압도적 (7,000+) - UI가 쉬워 비개발자도 바로 사용
- 문서/커뮤니티 자료 풍부
단점 ❌
- 무료 플랜 제약 큼 (2단계, 분기 유료) - 유료 요금이 상대적으로 비쌈
- 복잡한 워크플로우 표현에 한계
적합한 상황: 코딩을 모르는 비개발자, 단순한 자동화(A하면 B해라), 마이너한 앱까지 연동해
야 할 때, 빠르게 구축하고 싶을 때
Make
장점 ✅
- 무료 플랜이 관대 (분기, 멀티스텝 가능) - 시각적 UI로 복잡한 흐름 설계에 강함
- 데이터 변환, 반복 처리 등 고급 기능
- 유료 플랜도 저렴한 편
단점 ❌
- 연동 앱 수가 Zapier보다 적음
- 초기 학습 곡선이 있음
- Operation 카운트 방식이 헷갈릴 수 있음
적합한 상황: 분기·조건이 많은 복잡한 자동화, 예산이 적은 개인/스타트업, 기술적 이해가 있
는 사용자, 이번 과제처럼 Router 분기가 필요한 경우

2번과제
1. IFTTT 자동화 — 과정과 결과
구현 과정
① IFTTT 가입 및 로그인
② [Create] 버튼 클릭 → 새 Applet 만들기
③ If This (트리거) 설정
 → "Date & Time" 서비스 선택
 → "Every day at" 선택
 → 원하는 시간 지정 (예: 오전 9시)
④ Then That (액션) 설정
 → "Email" 서비스 선택
 → "Send me an email" 선택
 → 메일 제목/본문 작성
⑤ Applet 저장 및 활성화
결과
- 매일 지정한 시간에 등록된 이메일 주소로 자동 메일 발송 확인
- 별도의 조작 없이 예약된 시간마다 반복 실행됨
- Applet 활성화 상태에서 지속적으로 작동
IFTTT의 Date & Time 트리거와 Email 액션을 연결하여, 매일 지정한 시각에 자동으로 이메
일이 발송되는 Applet을 구현하였다. 테스트 결과 설정한 시간에 메일이 정상 수신되었으며, 별도의 조작 없이 매일 반복 실행됨을 확인함
2. 왜 IFTTT를 사용했나
① 가장 쉬운 구조
 → "If This, Then That" 단 두 단계만 존재
 → 트리거 1개 + 액션 1개, 3분이면 완성
② 시간 기반 트리거가 무료
 → Date & Time 트리거를 무료 플랜에서 제공
 → "매일 특정 시간" 같은 예약 실행에 최적
③ 세 도구의 성격 비교가 가능
 → Zapier/Make: 조건 분기가 있는 복잡한 자동화
 → IFTTT: 단순 반복 자동화
 → 도구별 적합한 용도의 차이를 보여주기 좋음
(단,IFTTT플랜은 Applet 개수 제한(2~3개)이 있음)
Zapier와 Make로는 "조건에 따라 분기하는 복잡한 자동화"를, IFTTT로는 "단순하고 규칙적인
반복 자동화"를 구현함으로써, 자동화 도구마다 적합한 영역이 다르다.
Cancel Edit Applet
Want to publish this Applet so anyone can use it? Click here
If Every day at
+
Then Send me an email
Pro +
Update
Edit Delete
Edit Delete
If Every day at
11:00 AM, then
Send me an email at
jmyd051027@nave
r.com
by jmyd051027
Connected
IFTTT Daily Test
보낸사람 Date & Time via IFTTT <action@ifttt.com>
받는사람 jmyd051027@naver.com
2026년 7월 14일 (화) 오후 12:31
영어 한국어 번역하기
This email is automatically sent every day using IFTTT.
Manage
Unsubscribe from these notifications or sign in to manage your Email service.
Connected
How this automation works
If
Then
Every day at
Polling trigger This Trigger
fires every single day at a specific
time set by you.
Trigger ingredients
CheckTime
Send me an email
Action This Action will send
you an HTML based email.
Images and links are supported.
Action fields
subject body
