---
name: learn-quiz
description: Use when the user wants to deeply understand a session, implementation, bug, design, code change, or technical topic through incremental teaching, restatement, and quizzes until mastery is demonstrated.
---

# Learn Quiz

Help the user genuinely understand the topic, not just receive an explanation.

Use this skill when the user asks to learn, review, quiz, drill, explain, teach back, check understanding, or make sure they understand a session, plan, code change, bug, design, or implementation.

## Core Workflow

1. Build an understanding checklist for the topic.
2. Ask the user to restate what they currently understand before teaching.
3. Fill gaps incrementally, one stage at a time.
4. Verify each stage before moving on.
5. Use open-ended or multiple-choice questions to test understanding.
6. Do not reveal quiz answers until after the user responds.
7. Continue until the user has demonstrated understanding of the checklist, or until remaining items are explicitly deferred.

## Understanding Checklist

Maintain a running checklist in the conversation or, when useful for a long session, in a short Markdown note.

Include high-level and low-level items:

- what the problem or topic is
- why it matters
- why the problem existed
- relevant context and constraints
- branches of the decision tree
- the chosen solution
- why that solution was chosen
- alternatives rejected
- business logic or domain rules
- edge cases and failure modes
- what changed and what the change impacts
- validation, debugging, or verification steps

## Teaching Style

Start by asking the user to explain their current understanding. Use that answer to decide where to teach next.

When teaching:

- explain why before what and how
- drill into more why questions when the motivation is fuzzy
- move from concept to concrete examples
- use code, docs, logs, tests, or debugger steps when they would make the topic clearer
- keep each stage small enough to verify before continuing
- adapt depth if the user asks for ELI5, ELI14, or intern-level explanations

## Quiz Rules

Ask one quiz question at a time unless the user explicitly asks for a full quiz.

For each quiz question:

- use open-ended questions when reasoning matters
- use multiple choice when distinctions are crisp
- vary the position of the correct answer
- do not reveal the answer before the user responds
- after the response, explain what was correct, what was missing, and what to fix
- only move on when the current concept is understood

If the environment provides a user-question tool, use it when it improves the quiz flow. Otherwise, ask inline in chat.

## Repository-Aware Rule

If a question can be answered by inspecting the codebase, docs, tests, existing artifacts, or local runtime output, inspect those first instead of asking the user to guess.

Show the relevant code or evidence when it helps the user understand the reasoning.

## Stop Rule

Do not end the learning session merely because the explanation is complete.

End only when the user has demonstrated understanding of the checklist, or when the remaining unknowns are intentionally deferred with clear follow-up items.
