---
name: oz-assignment-feedback
description: Run assignment feedback for OZ Coding School 1인 창업가 개발부트캠프 6기 by checking Notion submissions and optionally replying to OZ LMS challenges.
---

# OZ Assignment Feedback - 6기

Use this skill when the user asks to check, write, continue, or automate OZ Coding School assignment feedback for `1인 창업가 개발부트캠프 6기` or `창업가 6기`.

## Fixed 6기 Context

This skill is intentionally fixed to 6기. Do not ask the user to configure or select a cohort unless they explicitly want to change the skill.

Default 6기 context:

- Cohort: `1인 창업가 개발부트캠프 6기`
- Notion daily assignment page: `https://app.notion.com/p/7cccaf5650aa8376a7d40136b14b7372`
- Notion assignment data source: `collection://441caf56-50aa-8215-b986-87d71735dd25`
- Known OZ web basics class: `https://ozcodingschool.com/classes/view?order_id=50102&lecture_id=56501`
- Feedback authors for duplicate checks: `강지훈`, `지훈_조교`

## Required Run Context

Before writing anything, identify the target from the user's request:

- Target Day(s), or the rule for choosing them, for example yesterday plus earlier missing submissions.
- Whether to write Notion feedback only or also reply in OZ LMS.

Use the fixed 6기 context above for Notion lookup. If OZ LMS replies are requested and the target Day belongs to a course/challenge that cannot be found from the known class URL or currently logged-in LMS account, ask the user for the correct LMS class or challenge link instead of guessing.

## Operating Rules

For an actual feedback run, read and follow [references/workflow.md](references/workflow.md). The workflow contains duplicate checks, submission reading requirements, attachment handling, comment tone, and LMS reply rules.

Keep the user-facing report short for this workflow: report completed items, skipped items, failures, unreadable submissions, and login/link/limit blockers only. Do not narrate intermediate browsing or file-reading steps unless the user asks.
