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

Notion attachment handling details:

- Notion database `FILES` properties can appear in connector output as encoded `file://{...}` references, for example a `파일과 미디어` value with `source: attachment:...:filename.zip`. These are Notion attachment metadata references, not local file paths and not direct download URLs.
- Do not try to download a `file://{...}` Notion attachment reference with shell tools or generic URL fetchers. Decode it only to identify the filename, source, and permission record.
- If a submission has a `file://{...}` attachment reference, first check whether the same actual work is also available through a URL property, page body link, bookmark, repository link, inline code, image block, or comment attachment. If that alternate source is enough to inspect the work, use it and do not block feedback on the unavailable duplicate attachment.
- If the attachment is the only submitted work, open the Notion page in the browser with the user's logged-in session and click the attachment in the Notion UI to obtain a temporary `https://file.notion.com/...` signed download URL or trigger a browser download. Inspect the downloaded file, then delete the archive and extracted files after the comment is completed.
- If the browser cannot expose/download the file because of login, permission, expired signed URL, UI limitation, or missing browser tooling, do not write feedback. Report the exact reason as `Notion 파일 속성 첨부 다운로드 필요/불가` with the student and Day.

If a file/image/archive cannot be opened because of permissions, tool limits, broken links, unsupported format, or missing data, do not leave a Notion feedback comment. Report the student, Day, and unreadable reason.

Unreadable submission tracking:

- Keep a compact internal list for every unreadable submission encountered during the run.
- For each item, record the Day, student name for the user-facing report, submission surface, file name/extension if visible, source form, attempted access path, and short failure reason.
- Submission surface examples: `Notion 파일과 미디어 속성`, `Notion 본문 파일 블록`, `Notion 댓글 첨부`, `OZ LMS 댓글 첨부`, `GitHub 링크`, `외부 URL`, `이미지 캡쳐`.
- Source form examples: `file:// Notion attachment metadata`, `https://file.notion.com signed URL`, `.zip`, `.html`, `.css`, `.js`, `.png`, `.jpg`, `GitHub repository`, `broken/expired URL`.
- If the same unreadable pattern looks like a skill/tooling gap rather than a one-off login or permission problem, offer to register a GitHub issue in `agrade1/oz-assignment-feedback-skill`.
- Create the GitHub issue only when the user asks for issue registration or approves it after the run. Creating an issue is an external write.
- Because the repository is public, do not include student names, private Notion URLs, signed file URLs, tokens, or personal data in the GitHub issue unless the user explicitly approves that disclosure. Prefer anonymized details such as Day, file extension, source surface, and redacted error category.
- Suggested issue title: `Unreadable submission: <source surface> <file type or URL type>`.
- Suggested issue body:

```markdown
## Case
- Cohort: 1인 창업가 개발부트캠프 6기
- Day:
- Source surface:
- File/link type:
- Failure category:

## What happened

## Expected behavior

## Notes
- Private student/page/file details omitted by default.
```

Never quote or expose secrets, API keys, tokens, or personal data in public comments. If visible, advise the student to hide/remove them without reproducing the value.

## 4. Write Notion Feedback

Before creating a comment, re-check comments/discussions for duplicate tutor feedback.

Feedback style:

- Write much more praise-first than a grading or inspection note.
- Start with a bright, clear compliment that the student can receive positively.
- Use a Korean TA tone with one spoon of excited "praising a child" energy, while staying respectful and not childish, sarcastic, or patronizing.
- Use `!!` naturally in praise or encouragement, usually 1-3 times per comment.
- Usually 2-5 short sentences. If the comment gets longer, split it with line breaks so it is easy to read.
- Always praise at least one concrete point actually observed in the submitted work.
- Keep improvement suggestions to one gentle point only when needed, phrased like `다음에는 이렇게 해보면 더 좋아요`.
- Avoid stiff expressions such as `검사 결과`, `자동 확인`, `정답/오답`, `검사 리포트`, or `세부 확인이 어렵습니다`.
- Do not use headings, lists, excessive emoji, or long rubric-style reports.
- Never include full feedback comment text in the final user report.

Examples of acceptable tone:

- `와 과제 너무 잘해주셨어요!! 변수 선언부터 콘솔 출력까지 요구사항을 차근차근 잘 채운 게 보여요. 화면에 값이 보이도록 연결한 부분도 아주 좋았습니다!! 다음에는 변수명만 과제 기준과 한 번 더 맞춰보면 더 깔끔해질 것 같아요.`
- `화면 구성이 깔끔해서 보기 좋았어요!! 제출 흐름도 자연스럽게 이어지고, 링크 연결까지 잘 확인됩니다. 이 정도면 오늘 과제 흐름 잘 잡고 가고 있어요!!`
- `압축파일 안의 코드까지 확인했습니다!! 단계별 주석이 나뉘어 있어서 흐름 따라가기가 좋았어요. 이렇게 정리해두면 나중에 다시 볼 때도 훨씬 편합니다!!`

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
- Unreadable submission patterns and whether a GitHub issue was created, offered, or not requested.
- Downloaded attachment cleanup status when files were downloaded.

Do not include detailed intermediate logs unless requested.
