# agent-plugins

Claude Code와 Codex 사용자가 마켓플레이스(`plugins`) 하나로 받아 쓰는 공개 플러그인 저장소.

지금 상태는 [STATE.md](STATE.md), 할 일은 [TASKS.md](TASKS.md)에 있다.

| 플러그인 | 소개 |
| --- | --- |
| [`codyssey-final-check`](plugins/codyssey-final-check/README.md) | 코디세이 AI 네이티브 파이널 프로젝트 저장소를 평가기준표에 맞춰 자가 점검한다 |

## 시작하기

- 필요한 도구와 접근 권한: Claude Code 또는 Codex CLI, `git`

1. 저장소를 받고 폴더로 들어간다.

```bash
git clone https://github.com/myungjinki/agent-plugins.git
```

```bash
cd agent-plugins
```

2. Claude Code에 마켓플레이스를 등록하고 플러그인을 설치한다. Codex 설치와 제거 명령은 [`codyssey-final-check` 설치·제거](plugins/codyssey-final-check/README.md#설치)에 있다.

```bash
claude plugin marketplace add .
```

```bash
claude plugin install codyssey-final-check@plugins
```

3. 점검할 프로젝트 저장소 폴더에서 `/codyssey-final-check:evaluate`(Codex `$evaluate`)를 인자 없이 실행한다. [점검 순서 안내](plugins/codyssey-final-check/skills/evaluate/references/order.md)가 출력되고 파일이 바뀌지 않으면 정상이다.

## 사용법

1. 점검할 프로젝트 저장소에서 전체 점검(`/codyssey-final-check:evaluate all`) 또는 일부 요건(`/codyssey-final-check:evaluate G3`)을 실행한다(Codex는 `$evaluate all`, `$evaluate G3`).
2. 터미널에 필수요건(G1~G7) 항목별 표와 6개 영역 100점 채점 결과가 출력되고, 같은 내용이 대상 프로젝트의 `docs/evaluate-result/<YYYYMMDD-HHMMSS>.md`에 저장된다(자동 커밋하지 않음).
3. 결과 파일의 미충족 항목을 보완한 뒤 다시 실행해 확인한다. `서비스 검증`을 포함한 입력별 동작과 제약은 [`codyssey-final-check` 사용법](plugins/codyssey-final-check/README.md#사용법)에 있다.

## 확인 방법

플러그인을 고친 뒤 확인하는 명령과 통과 기준은 [AGENTS.md 검증](AGENTS.md#검증)에 있다.

## 문서

`docs/`에는 README가 길어지면 나눈 문서와 이 저장소의 목표·계획을 둔다.

- [목표와 계획](docs/plan.md): 해결할 문제, 목표, 범위, 단계
- [docs](docs/README.md): `docs/` 폴더의 용도
- [작업 지침](AGENTS.md): 에이전트가 따르는 저장소 규칙
- [변경 기록](LANDED.md): 끝나거나 취소한 할 일
- [흐름 보고](docs/reports/): `docs/reports/<모드>/<기간>/report.md` (최근: [2026-11-18 일간](docs/reports/daily/2026-11-18/report.md)). 과거 보고는 지금의 `STATE.md`와 다를 수 있다
