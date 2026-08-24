# OZ Assignment Feedback Workflow

This workflow covers Notion assignment feedback and OZ Coding School LMS challenge replies for OZ Coding School `1인 창업가 개발부트캠프 6기`.

## 1. Configure The Run

Use the fixed 6기 context from `SKILL.md` and collect only the missing execution target from the user:

- `days`: explicit Day numbers/pages or a rule such as yesterday plus earlier unreviewed submissions.
- whether Notion feedback only or OZ LMS replies too.

Use the fixed Notion daily assignment page and assignment data source from `SKILL.md`. If the target Day's LMS course/challenge is not visible from the known OZ web basics class or the logged-in OZ account, ask the user for the correct LMS class or challenge link.

## 2. Find Submission Targets In Notion

Prefer the Notion connector for Notion reads/writes.

- Start from the assignment data source when available.
- Find target Day pages and each Day page's roster/list database, commonly named `📋 명단`.
- Query each roster for student rows with actual submission signals: checked code/screenshot fields, URL fields, file/media fields, page body content, or page/comment attachments.
- If SQL/data-source querying hits a plan/usage limit, fall back to Notion search/fetch only when Day, student, submission state, submission page, and existing feedback status can still be verified confidently.
- If lookup confidence is incomplete, do not write comments. Report `Notion 조회 한도/확인 필요`.

For each candidate submission page, fetch page content with discussions/comments before writing. Skip rows that already have tutor feedback by any configured feedback author.

## 3. Read The Actual Submission

Do not write feedback unless the submitted work was actually read or visually inspected.

Check all possible submission forms:

- Repository links: inspect the relevant branch/folder/file contents. Prefer official GitHub connector/API for public GitHub links.
- Inline code or page body: read the submitted content directly.
- Notion file/media attachments: download when needed, inspect, and delete local downloaded copies after the comment is completed.
- Comment attachments: check Notion discussions/comments and download files from student comments when those are the submitted work.
- ZIP archives: extract to a temporary directory, inspect source files such as HTML/CSS/JS/README/assets, then delete the archive and extracted files after processing.
- Images/screenshots: visually inspect when possible. Use screenshot evidence only for what is visible; do not claim to have read code from an image unless it is legible.

If a file/image/archive cannot be opened because of permissions, tool limits, broken links, unsupported format, or missing data, do not leave a Notion feedback comment. Report the student, Day, and unreadable reason.

Never quote or expose secrets, API keys, tokens, or personal data in public comments. If visible, advise the student to hide/remove them without reproducing the value.

## 4. Write Notion Feedback

Before creating a comment, re-check comments/discussions for duplicate tutor feedback.

Feedback style:

- Korean TA tone: short, warm, specific, and praise-first.
- Usually 1-3 sentences.
- Include `!` naturally when it fits.
- Mention concrete things observed in the submission.
- Keep improvement suggestions to one gentle point when needed.
- Avoid stiff labels such as `자동 확인 결과`, `검사 리포트`, `세부 확인이 어렵습니다`.
- Do not use headings, lists, excessive emoji, or long rubric-style reports.

Examples of acceptable tone:

- `변수 선언부터 콘솔 출력까지 요구사항을 잘 채워주셨고, 화면에 값이 보이도록 연결한 점도 좋습니다! 다음에는 변수명만 과제 기준과 한 번 더 맞춰보면 더 좋아요.`
- `화면 구성이 깔끔하고 제출 흐름도 잘 정리되어 있어요! 링크 연결까지 자연스럽게 확인됩니다.`
- `압축파일 안의 코드까지 확인했습니다! 단계별 주석이 잘 나뉘어 있어 흐름을 따라가기 좋았어요.`

After all safe comments for a Day are complete, update the Day feedback status only when the local workflow and schema make that property clear.

## 5. Reply In OZ Coding School LMS

Use the browser for OZ LMS because login/session and challenge comments are UI-dependent.

Before replying:

- Confirm the user is logged in. If login is required, open the login page and ask the user to sign in.
- Locate the correct 6기 class/course for the subject. Do not assume all Days live in one class; JavaScript, frontend, database, etc. can be separate courses.
- Match the challenge by Day/subject name, then match each LMS submission comment by both student name and Notion submission page link.
- If name and link do not both match, skip and report `확인 필요`.
- If an existing `지훈_조교` or configured tutor reply exists under that LMS comment, skip to prevent duplicates.

Default LMS reply:

```text
과제 제출 확인되었습니다!

피드백은 아래 문서에 남겨두었어요.
확인해보시고, 궁금한 점 있으면 편하게 댓글 주세요.

데일리 과제 피드백:
[Notion submission page link]
```

Minor natural variation is allowed, but the reply must include the confirmation, feedback-location notice, and exact Notion submission page link.

OZ replies are representational comments to a third-party site. If the browser safety policy requires action-time confirmation, summarize the exact target count/names and ask for approval immediately before registering.

## 6. Final Report

Keep the final user report concise:

- Overall completion status.
- Day(s) processed.
- Students with Notion feedback created.
- Students with OZ replies created.
- Skipped items with short reason, for example existing feedback, no submission, unreadable file, LMS challenge link missing, login required, or matching uncertain.
- Downloaded attachment cleanup status when files were downloaded.

Do not include detailed intermediate logs unless requested.
