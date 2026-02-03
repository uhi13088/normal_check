# PROJECT_NAME - CLAUDE.md

## 목적
<!-- 1줄로 작성 -->
- 예: 직원 출퇴근/스케줄 관리 웹앱 MVP

## 기술 스택
- Frontend: Next.js 14, TypeScript, TailwindCSS
- Backend: Next.js API Routes, Prisma, PostgreSQL
- 테스트: Vitest

## 작업 규칙 (최우선)
1. **TASK.md 기준으로 작업** - 한 번에 1개 티켓만 진행
2. **Plan → 구현 → 검증** 순서 준수
3. **완료 기준** = AC(Acceptance Criteria) 충족 + 테스트 PASS
4. **작업 완료 시** TASK.md 업데이트 필수

## 코드 규칙
- TypeScript strict 모드, `any` 금지
- API 응답: `{ success: boolean, data?: T, error?: { code, message } }`
- 커밋: `type(scope): message` (feat/fix/docs/refactor/test)

## 금지 사항
- `.env`, `secrets/` 읽기/수정 금지
- 대규모 리팩토링 금지 (필요시 티켓 분리)
- 테스트 없이 완료 처리 금지

## 검증 명령
```bash
pnpm validate   # 전체 (typecheck + lint + test + build)
pnpm test       # 테스트만
pnpm typecheck  # 타입체크만
```

## 참조 문서
- 기술설계: `docs/ARCHITECTURE.md`
- API 스펙: `docs/API.md`
