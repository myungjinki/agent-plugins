# agent-plugins

이 프로젝트의 작업 기준이다. 모든 저장소의 공통 작업 기준은 '공통 규칙' 구역의 방법으로 읽는다.

## 공통 규칙

- 일을 시작하기 전에 공통 규칙을 읽는다. 시작 훅이 보인 공통 규칙 문서가 없으면 `python3 scripts/tasks.py rules`를 실행해 끝까지 읽는다. 읽지 못하면 첫 응답에서 알린다.

## 완료 기준

- 동작이나 사용법을 바꿨으면 `README.md`와 해당 플러그인의 `README.md`, 관련 문서를 같은 커밋에서 고쳤다.

## 검증

- 플러그인·마켓플레이스를 고친 뒤 `claude plugin validate .`를 실행한다. 오류 없이 끝나야 한다.
- 플러그인을 고쳤으면 해당 플러그인의 `.claude-plugin/plugin.json`과 `.codex-plugin/plugin.json`의 `version`이 같고, `.claude-plugin/marketplace.json`·`.agents/plugins/marketplace.json`·`README.md`의 플러그인 목록이 일치하는지 대조한다.
- 문서를 고쳤으면 `eval-all`(Claude `/jk-template:eval-all`, Codex `$eval-all`)로 점검해 깨진 링크·고아 문서·문서 간 어긋남이 없어야 한다.

## 문서

- README가 길어지면 나눈 문서와 이 저장소의 목표·계획은 `docs/`에 적는다. 문서를 더하면 `README.md`의 '문서' 목록에서 가리킨다.

## 함정

- Claude 마켓플레이스(`.claude-plugin/marketplace.json`)와 Codex 마켓플레이스(`.agents/plugins/marketplace.json`)는 경로와 스키마가 다르다. 플러그인을 더하거나 고칠 때 한쪽만 수정하지 않는다.
- 플러그인 폴더(`plugins/<플러그인>/`)마다 `.claude-plugin/plugin.json`과 `.codex-plugin/plugin.json`이 따로 있다. 둘 중 하나만 버전을 올리면 도구별 버전이 어긋난다.
- 플러그인을 고칠 때는 그 폴더의 `AGENTS.md`도 함께 따른다.

## 정해 둔 것

- 일 하나를 끝낼 때마다 검증을 통과한 뒤 관련 파일만 명시해서 스테이징해 커밋한다.
- 공개 라이선스는 MIT로 한다([agent-plugins#9](https://github.com/myungjinki/agent-plugins/issues/9), 2026-11-23 사용자 답). 이유: 남이 고쳐 다시 배포하는 것을 허용한다. 이미 배포된 사본에는 적용을 거둘 수 없다. `LICENSE`와 `README.md` '라이선스' 구역에 적었다.
- 일을 끝내 커밋했거나 푸시·PR·머지를 요청받으면 `ship`이나 `ship-all`로 묻지 않고 한다.

## 프로젝트 작업 기준

- `STATE.md` '지금'에는 현재 달성 수준과 진행 단계를 적는다.
- 구현 규칙: 플러그인을 더하면 두 마켓플레이스와 `README.md` 목록에 함께 적고, 플러그인을 고치면 두 `plugin.json`의 `version`을 같은 값으로 올린다.
- 공개 저장소다. 키·토큰·인증 파일과 개인정보를 커밋하지 않는다.
- 스스로 정하는 일: 기존 플러그인의 버그·문서 수정, 이 저장소 문서·할 일 갱신과 커밋. 사용자에게 확인받는 일: 플러그인·마켓플레이스 이름 바꾸기, 플러그인 지우기, 라이선스 정하기.
