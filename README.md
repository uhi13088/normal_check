# Claude Code 프로젝트 템플릿 (단일 세션용)

> 🎯 **목표**: Claude Code가 TASK.md 기반으로 자동으로 작업을 진행하게 만드는 템플릿

---

## 📁 파일 구조

```
your-project/
├── CLAUDE.md                    # 프로젝트 규칙 (30줄)
├── TASK.md                      # 작업 큐 (상태 관리)
└── .claude/
    ├── settings.json            # 권한/자동화 설정
    └── commands/                # 커스텀 명령어
        ├── validate.md          # /validate - 전체 검증
        ├── pr.md                # /pr - PR 작성
        ├── next.md              # /next - 다음 작업 진행
        └── status.md            # /status - 상태 확인
```

---

## 🚀 사용법

### 1. 파일 복사
```bash
# 템플릿 파일들을 프로젝트 루트에 복사
cp CLAUDE.md TASK.md your-project/
cp -r .claude your-project/
```

### 2. 프로젝트에 맞게 수정

**CLAUDE.md**
```markdown
## 목적
- 여기에 프로젝트 1줄 설명

## 기술 스택
- 실제 사용하는 기술로 수정
```

**TASK.md**
```markdown
## 📋 QUEUE
- [ ] **T1: 실제 첫 번째 작업**
  - AC: 완료 기준 1
  - AC: 완료 기준 2
```

### 3. Claude Code 실행
```bash
cd your-project
claude  # 또는 본인 환경의 실행 명령어
```

### 4. 세션 시작 프롬프트 (1회만)
```
이 프로젝트의 개발자야.
CLAUDE.md 규칙을 따르고, TASK.md 기준으로 작업해.
작업 시작 전 항상 TASK.md 확인하고, 완료 시 업데이트해.
지금 TASK.md 확인하고 다음 작업 시작해.
```

---

## ⌨️ 명령어

| 명령어 | 설명 |
|--------|------|
| `/next` | 다음 작업 진행 (QUEUE → IN_PROGRESS → DONE) |
| `/status` | 현재 프로젝트 상태 요약 |
| `/validate` | 전체 검증 (typecheck + lint + test + build) |
| `/pr` | PR 설명 자동 생성 |

---

## 🔄 작업 흐름

```
┌─────────┐     ┌──────────────┐     ┌──────┐
│  QUEUE  │ ──► │ IN_PROGRESS  │ ──► │ DONE │
└─────────┘     └──────────────┘     └──────┘
                       │
                       ▼ (실패/불명확)
                ┌─────────┐
                │ BLOCKED │ ← 사람 개입 필요
                └─────────┘
```

### 자동 진행 조건
- ✅ AC 명확
- ✅ 테스트 PASS
- ✅ 빌드 성공

### 멈추는 조건 (BLOCKED)
- ❌ 테스트 FAIL
- ❌ AC 불명확
- ❌ 권한 필요 (배포 등)

---

## 🔒 권한 설정 (settings.json)

| 구분 | 내용 |
|------|------|
| **deny** | `.env` 읽기, `rm -rf`, `curl`, `wget` |
| **ask** | `git push`, `deploy` (확인 필요) |
| **allow** | 테스트, 빌드, git 기본 명령어 |

### 자동 훅
- 파일 수정 후 → 자동 포맷팅 실행

---

## 📝 티켓 작성 팁

### 좋은 티켓 ✅
```markdown
- [ ] **T1: 사용자 로그인 API**
  - AC: POST /api/auth/login 엔드포인트 구현
  - AC: 이메일/비밀번호 검증, JWT 반환
  - AC: 유닛 테스트 3개 이상
```

### 나쁜 티켓 ❌
```markdown
- [ ] **T1: 로그인 만들기**
  - AC: 로그인 되게
```

### AC 작성 규칙
- **구체적**: "로그인 구현" ❌ → "POST /api/auth/login 엔드포인트" ✅
- **검증 가능**: "잘 동작" ❌ → "테스트 PASS" ✅
- **작게**: 2시간 내 완료 가능한 크기

---

## ❓ 언제 개입해야 하나?

| 상황 | 대응 |
|------|------|
| BLOCKED 발생 | 원인 확인 → AC 수정 또는 답변 |
| 배포/푸시 요청 | 승인 또는 거부 |
| 스펙 변경 | TASK.md 티켓 수정 |

**그 외에는 `/next` 또는 `/status`로 진행 상황만 확인하면 됩니다.**

---

## 🔧 커스터마이징

### 검증 명령어 변경
`CLAUDE.md`의 검증 명령 섹션 수정:
```markdown
## 검증 명령
pnpm validate   # 또는 yarn, npm
```

### 새 명령어 추가
`.claude/commands/새명령어.md` 파일 생성

### 권한 수정
`.claude/settings.json`의 deny/ask/allow 수정
