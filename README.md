# dev-process skills

Claude Code 등 AI 코딩 에이전트를 위한 **개발 프로세스 스킬 모음**입니다.
아이디어를 명확히 하고(`clarify`) → 요구사항을 정의하고(`prd`) → 구현하고(`implement`)
→ 검증하고(`verify`) → PR로 정리하고(`pr`) → 배운 것을 남기는(`learn`)
end-to-end 워크플로우를 다룹니다.

[skills.sh](https://www.skills.sh/) / [Vercel `skills` CLI](https://github.com/vercel-labs/skills)로 설치할 수 있습니다.

## 설치

```bash
npx skills add yansfil/vibe-engineering
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
| [`implement`](skills/implement/SKILL.md) | 승인된 PRD/스코프를 실제로 구현할 때. 라이브 체크리스트로 가장 작은 안전한 변경을 만들고 수용 기준 증거를 추적한다. |
| [`verify`](skills/verify/SKILL.md) | 완료 선언 전, 변경 후 "진짜 동작하는지" 증거 기반으로 확인할 때. Static/Behavior/Runtime 3단계 검증. |
| [`pr`](skills/pr/SKILL.md) | 변경을 PR로 정리할 때. git status/diff 점검, 무관한 변경 배제, 검증 증거 정리, PR 제목·본문 초안 작성. |
| [`learn`](skills/learn/SKILL.md) | 세션 끝에서 반복 실수·유용한 명령·프로젝트 규칙을 다음 세션을 위해 남길 때. |

## 권장 워크플로우

```
clarify ─▶ prd ─▶ implement ─▶ verify ─▶ pr ─▶ learn
(모호함 해소)  (요구사항)   (구현+검증)   (독립 검증)  (PR 정리)  (학습 보존)
```

- `implement`는 PRD가 약속한 검증을 자체적으로 포함합니다. `verify`는 그 위에 독립적인 완료 감사가 필요할 때 별도로 돌립니다.
- 각 스킬은 코드를 함부로 바꾸지 않고, 자기 단계의 책임만 수행하도록 설계되어 있습니다.

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
