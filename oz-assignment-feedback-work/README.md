# 창업가 6기 과제 피드백 자동화 Skill 안내

안녕하세요. 조교님들의 과제 피드백 반복 업무를 줄이고, 제출물 누락 없이 더 안정적으로 수강생을 케어할 수 있도록 `창업가 6기 과제 피드백 자동화 Skill`을 준비했습니다.

이 Skill은 `1인 창업가 개발부트캠프 6기` 전용으로 설정되어 있어 별도 기수 설정 없이 설치 후 바로 사용할 수 있습니다.

## 준비물

- [Codex Desktop](https://openai.com/ko-KR/codex/)
- Codex Notion 연결
- GitHub 접근 권한 또는 공개 GitHub 제출물 접근
- OZ Coding School 계정

## 설치방법

Codex 채팅창에 아래 명령어를 그대로 입력하면 Skill이 설치됩니다.

```bash
python3 ~/.codex/skills/.system/skill-installer/scripts/install-skill-from-github.py \
  --repo agrade1/oz-assignment-feedback-skill \
  --path oz-assignment-feedback-work \
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
- 레포 링크, 코드, 파일 첨부, 댓글 첨부, 압축파일, 사진 캡쳐 확인
- 제출물을 실제로 확인한 경우에만 Notion 피드백 댓글 작성
- OZ Coding School LMS 챌린지 답글 등록
- 처리 완료/실패/스킵 결과 요약

## 참고

- OZ 로그인이 필요하면 Skill이 로그인 화면을 요청합니다.
- JavaScript 등 추가 강의의 LMS 챌린지 링크를 찾지 못하면 임의로 추측하지 않고 링크를 요청합니다.
- 이 Skill에는 6기 Notion/OZ 링크가 포함되어 있으므로 내부 공유용으로 사용하는 것을 권장합니다.

사용해보시고 피드백 부탁드립니다. 감사합니다.
