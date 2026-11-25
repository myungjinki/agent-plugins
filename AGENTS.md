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

- 일회성 할 일의 원본은 이 저장소의 GitHub Issues이고, `TASKS.md` '일회성' 표·`STATE.md` '진행 중' 표·`LANDED.md`는 주 폴더의 `python3 scripts/tasks.py sync`만 쓰는 사본이다. 흐름은 할 일 기록 흐름, 명령은 `TASKS.md` '일회성' 머리말을 따른다.
- 세션 시작 훅(`.claude/settings.json`)이 `python3 scripts/tasks.py hook` 출력(열린 이슈의 번호·제목·구분·등급·차례 요약표, 진행 중, 막지 않은 실패, 밀린 주기적 항목, 날짜가 지난 대기 항목)을 보여 준다. 할 일 본문과 끝 조건은 출력에 없으니 일을 잡기 전에 `tasks.py show <번호>`로 읽는다. 훅이 없으면 그 명령을 직접 실행한다. 시작 전에 `STATE.md`도 읽는다. 출력이 '사본을 보인다'고 하거나 막지 않은 실패·밀린 항목이 있으면 첫 응답에서 알린다.
- 세션을 끝내기 전에 잡은 일의 '멈춘 곳'과 '다음 걸음'을 `tasks.py note`로 남기고, 주 폴더에서 `tasks.py sync`로 사본을 맞춰 바뀐 사본을 커밋한다. 주 폴더가 기본 브랜치가 아니거나 `origin`보다 뒤처졌으면 sync가 멈추므로, 기본 브랜치로 돌아가 `git pull --ff-only`(또는 `sync --pull`) 뒤 다시 한다.
- worktree에서는 `TASKS.md`·`STATE.md`·`LANDED.md`를 고치지 않는다.
- 명령이 틀렸거나 도구가 예상과 다르게 동작해 다시 해야 했으면 `tasks.py fail`로 그 이슈에 남기고, 막으면 `tasks.py fixed`로 막은 방법을 남긴다.
- 일을 잡을 때 항목의 `등급`과 지금 세션 모델의 등급을 비교해 AI 사용 전략의 '맡기는 법'을 따른다.

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
- 공개 라이선스는 MIT로 한다([agent-plugins#9](https://github.com/myungjinki/agent-plugins/issues/9), 2026-11-23 사용자 답). 이유: 남이 고쳐 다시 배포하는 것을 허용한다. 이미 배포된 사본에는 적용을 거둘 수 없다. `LICENSE`와 `README.md` '라이선스' 구역에 적었다.
- 일을 끝내 커밋했거나 푸시·PR·머지를 요청받으면 `ship`이나 `ship-all`로 묻지 않고 한다.
- ship은 `scripts/check-task-files.py`가 있으면 그 검사를 자동으로 하므로 검사 명령에 따로 넣지 않는다. ship은 worktree에서 할 일 파일을 고쳤거나 아직 푸시하지 않은 브랜치가 최신 `origin/main` 위에 있지 않으면 멈춘다. 뒤의 경우 커밋한 뒤 `git rebase origin/main`으로 올리고 다시 ship한다. 이슈의 할 일을 끝낼 때는 ship에 `--task <번호> --model "<모델>" --summary "<완료 내용>"`을 준다. ship이 PR 본문에 닫을 이슈를 넣고 머지 뒤 완료 댓글을 남긴다. 주 폴더의 기본 브랜치가 깨끗하면 사본을 동기화하고 바뀐 사본을 직접 푸시한다.
- 커밋 메시지는 영어, 동사 원형으로 시작하고 첫 글자는 대문자, 마침표 없이 50자 안팎. 필요하면 한 줄 띄우고 본문. 할 일을 끝낸 커밋은 메시지 끝에 끝낸 할 일의 번호를 괄호로 붙인다.

## 프로젝트 작업 기준

- 목적과 사용 대상은 `README.md`, 목표·범위·완료 기준은 `docs/plan.md`를 따른다.
- 요청이 목표나 범위를 바꾸면 변경 이유와 새 완료 기준을 `docs/plan.md`에 기록한다.
- `STATE.md` '지금'에는 현재 달성 수준과 진행 단계를 적는다.
- 구현 규칙: 플러그인을 더하면 두 마켓플레이스와 `README.md` 목록에 함께 적고, 플러그인을 고치면 두 `plugin.json`의 `version`을 같은 값으로 올린다.
- 공개 저장소다. 키·토큰·인증 파일과 개인정보를 커밋하지 않는다.
- 스스로 정하는 일: 기존 플러그인의 버그·문서 수정, 이 저장소 문서·할 일 갱신과 커밋. 사용자에게 확인받는 일: 플러그인·마켓플레이스 이름 바꾸기, 플러그인 지우기, 라이선스 정하기.
