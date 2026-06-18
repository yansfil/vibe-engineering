# vibe-engineering

Claude Code 등 AI 코딩 에이전트를 위한 **개발 프로세스 스킬 모음**입니다.
아이디어를 명확히 하고(`clarify`) → 요구사항을 정의하고(`prd`) → 구현하고(`implement`)
→ 검증하고(`verify`) → PR로 정리하고(`pr`) → 배운 것을 남기는(`learn`)
end-to-end 워크플로우를 다룹니다.

> **바이브 엔지니어링(Vibe Engineering)** 온라인 강의 자료의 일부로 사용됩니다.
> 강의에서 다루는 AI 페어 개발 워크플로우를 실제 스킬로 옮겨, 수강생이
> `npx skills add yansfil/vibe-engineering`으로 바로 설치해 실습할 수 있도록 만든 것입니다.

[skills.sh](https://www.skills.sh/) / [Vercel `skills` CLI](https://github.com/vercel-labs/skills)로 설치할 수 있습니다.

## 설치

```bash
npx skills add yansfil/vibe-engineering -a claude-code -y
```

특정 스킬만 설치하려면:

```bash
npx skills add yansfil/vibe-engineering/clarify
npx skills add yansfil/vibe-engineering/prd
```

Claude Code, Cursor, Copilot, Gemini, Cline, Zed 등 20여 종의 에이전트를 지원합니다.

## 스킬 목록

| 스킬 | 언제 쓰나 |
| --- | --- |
| [`clarify`](skills/clarify/SKILL.md) | 아이디어/요청이 아직 모호할 때. PRD·구현 전에 핵심 질문으로 모호함을 줄이고 핸드오프 요약을 만든다. |
| [`prd`](skills/prd/SKILL.md) | 구현 가능한 요구사항 문서가 필요할 때. 요구사항·수용 기준·태스크·검증을 담은 PRD를 `.dev/<slug>/`에 작성한다. |
| [`implement`](skills/implement/SKILL.md) | 승인된 PRD/스코프를 실제로 구현할 때. `.dev/<slug>/` 아티팩트(prd·checklist·context-notes)를 이어받아 가장 작은 안전한 변경을 만들고, 구현을 마친 뒤 마지막에 독립 검증(`verify`) subagent를 한 번 띄워 수용 기준을 판정한다(실패 시 고치고 한 번 재확인). |
| [`verify`](skills/verify/SKILL.md) | 완료 판정이 필요할 때. "어떻게 검증하나"의 단일 출처 — Static/Behavior/Runtime/Adversarial 검증으로 판정만 하고 코드는 고치지 않는다. `implement`의 완료 게이트로도, 단독 감사로도 쓰인다. |
| [`pr`](skills/pr/SKILL.md) | 변경을 PR로 정리할 때. git status/diff 점검, 무관한 변경 배제, 검증 증거 정리, PR 제목·본문 초안 작성. |
| [`learn`](skills/learn/SKILL.md) | 세션 끝에서 반복 실수·유용한 명령·프로젝트 규칙을 다음 세션을 위해 남길 때. |

## 권장 워크플로우

```
clarify ─▶ prd ─▶ implement ─▶ verify ─▶ pr ─▶ learn
(모호함 해소)  (요구사항)  (구현+마지막 독립검증) (독립 감사)  (PR 정리)  (학습 보존)
```

- `implement`는 구현을 **먼저 끝낸 뒤**, 마지막에 독립 verifier를 한 번 띄워 `verify`에 판정을 **위임**합니다. 직접 검증을 재구현하지 않고, 실패하면 지적된 부분을 고친 뒤 한 번 재확인합니다(과한 매-라운드 루프 없음).
- `verify`는 "어떻게 검증하나"의 **단일 출처**이자 **판정기**입니다. 코드를 고치지 않고 증거 기반 판정만 합니다. `implement`의 완료 게이트로도, 끝난 변경에 대한 단독 감사로도 동일하게 쓰입니다.
- 즉 *검증하는 법*은 `verify` 한 곳에만 살고, `implement`는 그 판정기를 호출해 done에 도달합니다. 각 스킬은 자기 단계의 책임만 수행합니다.

## 저장소 구조

```
skills/
  clarify/SKILL.md
  prd/SKILL.md
  implement/SKILL.md
  verify/SKILL.md
  pr/SKILL.md
  learn/SKILL.md
```

`skills/<name>/SKILL.md` 평면 레이아웃은 `skills` CLI가 자동 탐색하는 표준 구조입니다.
각 `SKILL.md`는 `name`, `description` frontmatter를 가집니다.

## 라이선스

[MIT](LICENSE)
