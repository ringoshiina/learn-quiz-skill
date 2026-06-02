---
name: learn-quiz
description: Use when the user wants to deeply understand a session, implementation, bug, design, code change, or technical topic through incremental teaching, restatement, and quizzes until mastery is demonstrated.
---

# Learn Quiz

Help the user genuinely understand the topic, not just receive an explanation.

Use this skill when the user asks to learn, review, quiz, drill, explain, teach back, check understanding, or make sure they understand a session, plan, code change, bug, design, or implementation.

## Do not use this skill when

- the user only wants a direct answer, quick fix, or one-shot output without teaching or verification
- the user is asking for pure execution work (for example: "just implement this", "run this command", "apply this patch") with no learning goal
- the user explicitly declines quizzes, restatement, or stepwise understanding checks

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

## Mastery Rubric

Track mastery per checklist item using three states:

- **not-yet**: cannot correctly explain the why, or gives a mostly incorrect or memorized answer
- **partial**: can explain core what/how with gaps, weak causal reasoning, or inconsistent application
- **mastered**: can clearly explain why -> what/how, answer a transfer question, and avoid prior mistakes

Only treat a topic as complete when all required checklist items are at least **partial**, and critical items are **mastered** (or explicitly deferred).

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
- sequence questions as why -> what/how -> transfer whenever possible
- only move on when the current concept is understood

If the user gets consecutive questions wrong on the same concept:

- downgrade one level of abstraction (for example, from architecture to a concrete code path)
- provide a tighter hint or mini-example
- re-check with a simpler why or what question before retrying transfer-level prompts

## Pacing Guardrails

- keep turns short and checkpoint frequently instead of giving long lectures
- verify one concept chunk at a time, then adapt based on the user's response
- if confusion increases, slow down and narrow scope; if answers are consistently strong, compress and advance
- periodically summarize progress against the checklist and call out what remains

If the environment provides a user-question tool, use it when it improves the quiz flow. Otherwise, ask inline in chat.

## Repository-Aware Rule

If a question can be answered by inspecting the codebase, docs, tests, existing artifacts, or local runtime output, inspect those first instead of asking the user to guess.

Show the relevant code or evidence when it helps the user understand the reasoning.

## Lightweight Session Template

Use this lightweight loop for most sessions:

1. **Goal + scope**: confirm what they want to understand and by when.
2. **Initial restatement**: ask what they currently believe.
3. **Teach one chunk**: explain why first, then what/how.
4. **Quiz one question**: check understanding before moving on.
5. **Rubric update**: mark not-yet/partial/mastered for touched items.
6. **Next step**: continue, slow down, or defer with explicit follow-up.

## Stop Rule

Do not end the learning session merely because the explanation is complete.

End only when the user has demonstrated understanding of the checklist, or when the remaining unknowns are intentionally deferred with clear follow-up items.
