# agent-plugins

모든 저장소에 적용하는 공통 기준과 이 프로젝트의 작업 기준이다.

## 완료 기준

- 아래 '검증'을 통과한다. 검증 명령이 없으면 바꾼 부분을 직접 실행해 확인한다.
- 동작이나 사용법을 바꿨으면 `README.md`와 해당 플러그인의 `README.md`, 관련 문서를 같은 커밋에서 고쳤다.
- 요청한 동작을 확인하고, 실행한 검증과 남은 제약을 보고한다.

## 검증

- 플러그인·마켓플레이스를 고친 뒤 `claude plugin validate .`를 실행한다. 오류 없이 끝나야 한다.
- 플러그인을 고쳤으면 해당 플러그인의 `.claude-plugin/plugin.json`과 `.codex-plugin/plugin.json`의 `version`이 같고, `.claude-plugin/marketplace.json`·`.agents/plugins/marketplace.json`·`README.md`의 플러그인 목록이 일치하는지 대조한다.
- 문서를 고쳤으면 `eval-all`(Claude `/jk-template:eval-all`, Codex `$eval-all`)로 점검해 깨진 링크·고아 문서·문서 간 어긋남이 없어야 한다.

## 할 일

- 작업을 시작하기 전에 `TASKS.md`와 `STATE.md`를 읽는다.
- 일을 잡을 때 항목의 `등급`과 지금 세션 모델의 등급을 비교해 [AI 사용 전략](https://github.com/myungjinki/role-ai-engineer/blob/main/docs/ai-strategy.md#맡기는-법)의 '맡기는 법'을 따른다.
- 세션을 끝내기 전에 `STATE.md` '진행 중'을 지금과 맞춘다.
- 번호·차례·잡은 일·끝내거나 취소한 일의 기록은 `TASKS.md`, `STATE.md`, `LANDED.md`의 머리말을 따른다.

## 문서

- README가 길어지면 나눈 문서와 이 저장소의 목표·계획은 `docs/`에 적는다. 문서를 더하면 `README.md`의 '문서' 목록에서 가리킨다.
- 파일·구역·표 이름을 바꾸면 저장소 안에서 기존 이름을 검색하고, 그 이름을 가리키는 링크와 안내를 함께 고친다.

## 함정

- Claude 마켓플레이스(`.claude-plugin/marketplace.json`)와 Codex 마켓플레이스(`.agents/plugins/marketplace.json`)는 경로와 스키마가 다르다. 플러그인을 더하거나 고칠 때 한쪽만 수정하지 않는다.
- 플러그인 폴더(`plugins/<플러그인>/`)마다 `.claude-plugin/plugin.json`과 `.codex-plugin/plugin.json`이 따로 있다. 둘 중 하나만 버전을 올리면 도구별 버전이 어긋난다.
- 플러그인을 고칠 때는 그 폴더의 `AGENTS.md`도 함께 따른다.

## 정해 둔 것

- 일 하나를 끝낼 때마다 검증을 통과한 뒤 관련 파일만 명시해서 스테이징해 커밋한다.
- 기존 사용자 변경을 덮어쓰거나 되돌리지 않는다.
- 되돌리기 어려운 결정은 이유와 함께 이 구역에 적는다.
- 푸시·PR·머지는 `ship`이나 `ship-all`로 한다.
- 커밋 메시지는 영어, 동사 원형으로 시작하고 첫 글자는 대문자, 마침표 없이 50자 안팎. 필요하면 한 줄 띄우고 본문. 할 일을 끝낸 커밋은 메시지 끝에 끝낸 할 일의 번호를 괄호로 붙인다.

## 프로젝트 작업 기준

- 목적과 사용 대상은 `README.md`, 목표·범위·완료 기준은 `docs/plan.md`를 따른다.
- 요청이 목표나 범위를 바꾸면 변경 이유와 새 완료 기준을 `docs/plan.md`에 기록한다.
- `STATE.md` '지금'에는 현재 달성 수준과 진행 단계를 적는다.
- 구현 규칙: 플러그인을 더하면 두 마켓플레이스와 `README.md` 목록에 함께 적고, 플러그인을 고치면 두 `plugin.json`의 `version`을 같은 값으로 올린다.
- 공개 저장소다. 키·토큰·인증 파일과 개인정보를 커밋하지 않는다.
- 스스로 정하는 일: 기존 플러그인의 버그·문서 수정, 이 저장소 문서·할 일 갱신과 커밋. 사용자에게 확인받는 일: 플러그인·마켓플레이스 이름 바꾸기, 플러그인 지우기, 라이선스 정하기.
