전체 검증을 실행하고 결과를 요약해줘.

## 실행 순서
1. `pnpm typecheck` (또는 npm run typecheck)
2. `pnpm lint` (또는 npm run lint)
3. `pnpm test` (또는 npm test)
4. `pnpm build` (또는 npm run build)

## 출력 형식
```
## 검증 결과

| 항목 | 결과 | 상세 |
|------|------|------|
| TypeScript | PASS/FAIL | 에러 수 |
| ESLint | PASS/FAIL | 경고/에러 수 |
| 테스트 | PASS/FAIL | 통과/전체 |
| 빌드 | PASS/FAIL | - |

### 실패 항목 (있으면)
- 에러 메시지
- 수정 제안
```

## 실패 시
- TASK.md의 현재 티켓을 BLOCKED로 옮길지 제안
- 수정 방법 제시
