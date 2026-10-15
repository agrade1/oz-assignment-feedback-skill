# 창업가 6기 과제 피드백 자동화 Skill 안내

안녕하세요. 조교님들의 과제 피드백 반복 업무를 줄이고, 제출물 누락 없이 더 안정적으로 수강생을 케어할 수 있도록 `창업가 6기 과제 피드백 자동화 Skill`을 준비했습니다.

이 Skill은 `1인 창업가 개발부트캠프 6기` 전용으로 설정되어 있어 별도 기수 설정 없이 설치 후 바로 사용할 수 있습니다.

## 준비물

- [Codex Desktop](https://openai.com/ko-KR/codex/)
- Codex Notion 연결
- GitHub 접근 권한 또는 공개 GitHub 제출물 접근
- OZ Coding School 계정

## 모델 설정

기본 권장 모델은 **GPT-6 Sol (`gpt-6-sol`)**입니다. **GPT-6 Luna (`gpt-6-luna`)**로도 사용할 수 있습니다.

### 기존 사용자가 GPT-5.5 선택 때문에 실행되지 않을 때

다음 오류는 스킬 본문이 아니라 Codex의 대화 요약(compact) 요청에서 지원되지 않는 모델을 호출한 경우입니다.

```text
Error running remote compact task:
The 'gpt-5.5' model is not supported when using Codex with a ChatGPT account.
```

1. Codex 대화의 모델 선택에서 **GPT-6 Sol** 또는 **GPT-6 Luna**를 선택합니다.
2. 예약 자동화로 실행 중이면 해당 자동화의 실행 모델도 같은 모델로 변경합니다. 대화 모델과 자동화 모델은 각각 확인해 주세요.
3. 모델 변경 후에도 기존 대화에서 같은 요약 오류가 이어지면, 선택한 모델로 새 대화를 열고 같은 스킬을 호출해 미처리 과제부터 이어서 진행합니다. 기존 피드백 댓글은 중복 확인 후 건너뜁니다.

모델이 목록에 나타나지 않으면 사용하는 Codex를 업데이트하고, 해당 계정에서 선택 가능한 모델을 확인해 주세요. 저장소에는 GPT-5.5를 고정한 설정이 없으며, 스킬을 다시 설치하는 것만으로 기존 대화나 자동화의 모델이 바뀌지는 않습니다.

### 저장소를 Codex 프로젝트로 열어 실행할 때

저장소의 `.codex/config.toml`에 다음 프로젝트 기본값이 포함되어 있습니다.

```toml
model = "gpt-6-sol"
```

Luna를 사용하려면 이 프로젝트 설정의 모델을 `gpt-6-luna`로 변경할 수 있습니다. 프로젝트 설정은 신뢰한 프로젝트에서만 적용되며, 대화나 실행 명령에서 모델을 명시했다면 그 선택을 별도로 확인해야 합니다.

CLI에서 한 번 실행할 때 모델을 직접 선택할 수도 있습니다.

```bash
codex -m gpt-6-sol
```

스킬만 설치한 경우에는 위 프로젝트 설정이 작업 중인 다른 프로젝트에 자동 적용되지 않습니다. Codex의 모델 선택 또는 사용 중인 프로젝트의 설정에서 모델을 지정해 주세요.

공식 문서: [Codex 설정](https://learn.chatgpt.com/docs/config-file/config-basic), [GPT-6 Sol](https://developers.openai.com/api/docs/models/gpt-6-sol), [GPT-6 Luna](https://developers.openai.com/api/docs/models/gpt-6-luna).

## 설치방법

Codex 채팅창에 아래 명령어를 그대로 입력하면 Skill이 설치됩니다.

```bash
python3 ~/.codex/skills/.system/skill-installer/scripts/install-skill-from-github.py \
  --repo agrade1/oz-assignment-feedback-skill \
  --path . \
  --ref main \
  --method auto \
  --name oz-assignment-feedback
```

설치 후 Codex를 재시작하거나 새 채팅에서 사용해 주세요.

## 사용방법

오늘 기준 전날 과제와 이전 미피드백 제출까지 확인하려면 아래처럼 입력합니다.

```text
$oz-assignment-feedback 오늘 기준 과제 피드백 진행해
```

특정 Day만 진행할 때는 아래처럼 입력합니다.

```text
$oz-assignment-feedback Day11 과제 피드백 진행해
```

Notion 피드백 작성 후 OZ Coding School 챌린지 답글까지 진행하려면 아래처럼 입력합니다.

```text
$oz-assignment-feedback Day11 피드백하고 챌린지 답글까지 진행해
```

## 처리 범위

- 6기 Notion 데일리 과제 페이지와 명단 DB 확인
- 기존 조교 피드백 중복 체크
- Notion URL 속성, 게시글 본문 링크/북마크, GitHub 레포 링크 확인
- 게시글 본문에 직접 작성한 코드/설명/회고 확인
- `파일과 미디어` 속성, 게시글 파일/이미지 블록, 댓글 첨부파일 확인
- ZIP 압축파일은 다운로드/해제 후 HTML/CSS/JS 등 실제 코드 확인
- 사진 캡쳐는 가능한 범위에서 화면을 시각적으로 확인
- 제출물을 실제로 확인한 경우에만 Notion 피드백 댓글 작성
- OZ Coding School LMS 챌린지 답글 등록
- 읽을 수 없는 파일/링크 유형은 실행 결과에 기록
- 반복적으로 막히는 파일 유형은 요청 시 GitHub 이슈 등록용으로 정리
- 처리 완료/실패/스킵 결과 요약

## 참고

- OZ 로그인이 필요하면 Skill이 로그인 화면을 요청합니다.
- JavaScript 등 추가 강의의 LMS 챌린지 링크를 찾지 못하면 임의로 추측하지 않고 링크를 요청합니다.
- GitHub 이슈는 공개 레포에 등록되므로 수강생 이름, 비공개 Notion 링크, signed file URL 같은 민감 정보는 기본적으로 제외합니다.
- 이 Skill에는 6기 Notion/OZ 링크가 포함되어 있으므로 내부 공유용으로 사용하는 것을 권장합니다.

사용해보시고 피드백 부탁드립니다. 감사합니다.
