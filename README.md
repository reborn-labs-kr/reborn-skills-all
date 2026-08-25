# reborn-skills-all

산 스킬팩을 **한 줄로** 설치합니다. 결제 후 받은 주문번호가 필요합니다 → <https://rebornlabs.kr/skillpack>

```bash
npx reborn-skills-all@latest <주문번호>
# 또는
npx reborn-skills-all@latest --token=<주문번호>
```

처음이시라면 그림처럼 적어 둔 안내가 있습니다 → <https://rebornlabs.kr/skillpack-guide>

---

## 어디서 실행하나요

**본인 컴퓨터의 터미널**에서 실행하세요.

| 환경 | 되나요 | 어떻게 |
|---|---|---|
| 윈도우 명령 프롬프트 (`cmd`) | ✅ | 윈도우키 → `cmd` → 엔터 |
| 맥 터미널 | ✅ | `command`+`스페이스` → `터미널` → 엔터 |
| 컴퓨터에 깐 Claude Code | ✅ | 맨 앞에 `!` 를 붙여 `!npx reborn-skills-all@latest …` |
| **폰·브라우저의 Claude 앱** | ❌ | 그 화면은 원격 임시 컨테이너입니다. 설치돼도 **본인 컴퓨터에 남지 않습니다** |

Node.js 18 이상이 필요합니다. `npx` 를 모르는 명령이라고 하면 <https://nodejs.org> 에서 먼저 설치하세요.

---

## 이 프로그램이 하는 일

1. 주문번호를 `https://mobility.rebornlabs.kr/api/skillpack-verify` 로 보내 **결제하신 만큼의 스킬 목록**을 받아옵니다.
2. 목록의 스킬마다 **각 제작자의 공식 설치 명령**을 그대로 실행합니다.
   ```
   npx -y skills@latest add <owner/repo> [--skill <name>] -g -a claude-code -y
   ```
3. 설치 전후로 `~/.claude/skills` 와 `~/.agents/skills` 를 비교해 **실제로 생긴 폴더**로 성공을 판정합니다.
   (종료 코드를 믿지 않습니다. 0을 주고도 아무것도 안 깔리는 설치기가 있습니다.)
4. 하나라도 깔렸으면 `~/.claude/skills/reborn-claudekit/SKILL.md` 에 사용 안내 스킬을 함께 둡니다.
5. 결과 집계(성공·실패 개수, 걸린 시간, Node 버전)를 보고용으로 한 번 보냅니다.

### 스킬 파일을 재배포하지 않습니다

저희는 남의 스킬을 **복사해 두거나 다시 배포하지 않습니다.** 각 제작자의 공식 설치 명령을
대신 실행할 뿐입니다. 만든 곳과 라이선스는 설치된 각 스킬 폴더의 원문에 그대로 남습니다.
저희가 파는 것은 파일이 아니라 **골라 주고 대신 깔아 주는 수고**입니다.

### 무엇을 건드리나요

| 쓰는 곳 | 무엇 |
|---|---|
| `~/.claude/skills/` · `~/.agents/skills/` | 스킬이 설치되는 자리 (설치는 `skills` CLI 가 합니다) |
| `~/.claude/skills/reborn-claudekit/SKILL.md` | 사용 안내 스킬 |

그 밖의 파일은 읽지도 쓰지도 않습니다. 시스템 설정·환경변수·자격증명에 손대지 않습니다.

### 무엇을 보내나요

| 언제 | 어디로 | 무엇 |
|---|---|---|
| 시작할 때 | `/api/skillpack-verify` | 주문번호 (구매 확인용) |
| 끝날 때 | `/api/skillpack-report` | 성공·실패 **개수**, 실패한 스킬 이름, 걸린 시간, Node 버전 |

파일 경로·계정·설치 목록은 보내지 않습니다. 보고가 실패해도 설치에는 영향이 없습니다.

---

## 옵션

| 옵션 | 하는 일 |
|---|---|
| `--check` | 설치하지 않고 지금 상태만 봅니다 |
| `--only <묶음>` | 묶음 하나만 설치합니다 |
| `--self-test` | 내부 자기시험 30건. 네트워크도 설치도 하지 않습니다 |

주문번호는 **30일에 3번**까지 쓸 수 있습니다. PC 를 바꾸셔도 되고, 스킬이 늘어나면 다시 돌리시면 됩니다.

---

## 소스와 검증

- 소스 전문: <https://github.com/reborn-labs-kr/reborn-skills-all> — 의존성 없는 파일 하나입니다.
- npm 에 올라간 판은 GitHub Actions 에서 `--provenance` 로 서명해 냅니다.
  npm 페이지의 provenance 표시를 눌러 **어느 커밋에서 만들어졌는지** 확인하실 수 있습니다.

설치 명령을 돌리기 전에 내용을 보고 싶으시면 이렇게 하셔도 됩니다.

```bash
npm view reborn-skills-all
curl -s https://raw.githubusercontent.com/reborn-labs-kr/reborn-skills-all/main/install.mjs | less
```

막히시면 고객센터로 알려 주세요 → <https://mobility.rebornlabs.kr/cs>

MIT License · REBORN LABS
