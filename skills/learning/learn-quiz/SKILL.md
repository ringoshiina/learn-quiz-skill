---
name: learn-quiz
description: Use when the user wants to deeply understand source material already present in context, available in the workspace, or supplied or pointed to by the user, such as a session, implementation, bug, design decision, code change, PR, generated artifact, or prior handoff, through incremental teaching, source-grounded explanation, restatement, quizzes, misconception correction, and continuation handoff until mastery is demonstrated.
---

# Learn Quiz

Help the user genuinely understand context-backed source material, not just receive an explanation. Treat learning as a feedback loop: establish the goal, ground the explanation in evidence, teach one chunk, test retrieval or transfer, update mastery state, then continue or hand off.

Use this skill when the user asks to learn, review, quiz, drill, explain, teach back, check understanding, or make sure they understand a session, plan, code change, bug, design decision, implementation, PR, generated artifact, or prior handoff.

Keep this skill lightweight. Do not turn it into a course workspace, long reading plan, HTML lesson generator, or general teaching system unless the user explicitly asks for reusable study material. The main product is demonstrated understanding in the current conversation.

## Do Not Use

Do not use this skill when:

- the user only wants a direct answer, quick fix, or one-shot output without teaching or verification
- the user is asking for pure execution work, such as "just implement this", "run this command", or "apply this patch"
- the user explicitly declines quizzes, restatement, or stepwise understanding checks
- the user wants broad from-scratch instruction without current context, workspace-accessible source material, or a supplied source pointer

## Operating Modes

Choose the lightest mode that preserves learning quality:

- **Chat-native mode**: Default. Maintain the learning goal, checklist, evidence map, and rubric in the conversation.
- **Session-state mode**: For long or complex sessions, maintain a short Markdown note with checklist state, evidence, misconceptions, and next questions. Create it only when useful, and keep it terse.
- **Continuation mode**: When context is getting long, the user is switching sessions, or the user asks for a handoff, produce a handoff that preserves learning state rather than only summarizing topic content.

This skill is context-first. Existing sessions are best when the relevant code, discussion, debug trace, PR, or artifact is already in context. New sessions work if the user provides or points to source material, or when the relevant material is available in the workspace, such as a diff, PR description, design doc, bug report, code snippet, transcript, local artifact, module path, or prior handoff.

## Core Workflow

1. Define the learning goal and scope.
2. Build an evidence map from available source material.
3. Build an understanding checklist for the topic.
4. Ask the user to restate what they currently understand before teaching.
5. Fill gaps incrementally, one stage at a time.
6. Verify each stage with retrieval, application, or transfer questions.
7. Update the mastery rubric and misconception log.
8. Continue until the user demonstrates understanding, or defer remaining items explicitly.

## Learning Goal

Before teaching, clarify what the user must be able to do. Keep it concrete:

- what they should be able to explain
- what they should be able to diagnose, judge, reproduce, or implement
- which source material or real-world situation the learning is grounded in
- what is out of scope for this session

If the goal is vague, ask one focused question before proceeding. Prefer goals like "explain why this bug happened and why the fix works" over "understand the PR".

## Evidence Map

When the topic is about code, a bug, a design, a PR, a document, or a previous session, inspect available evidence before teaching. Do not ask the user to guess facts that can be checked.

Useful evidence includes:

- code paths, diffs, tests, logs, stack traces, runtime output, browser behavior, or debugger findings
- PR descriptions, issues, design docs, ADRs, comments, user reports, or prior handoffs
- generated artifacts, screenshots, exported files, or validation results

Use evidence in the explanation when it clarifies causality. If evidence is missing, say what is missing and teach from stated assumptions only when the risk is low.

## Understanding Checklist

Maintain a running checklist in the conversation or, for long sessions, in a short note. Include high-level and low-level items:

- the problem, topic, or change
- why it matters
- why the problem existed or why the design pressure exists
- relevant context and constraints
- the source evidence that supports the explanation
- the decision tree and rejected alternatives
- the chosen solution or current behavior
- domain rules, business logic, or terminology
- edge cases, failure modes, and regressions to watch for
- validation, debugging, or verification steps
- what the user should be able to transfer to a new situation

## Mastery Rubric

Track mastery per checklist item using three states:

- **not-yet**: cannot correctly explain the why, gives a mostly incorrect or memorized answer, or cannot connect the idea to evidence
- **partial**: can explain the core what/how with some gaps, weak causal reasoning, or inconsistent application
- **mastered**: can explain why -> what/how, cite or reason from evidence, answer a transfer question, and avoid prior mistakes

Only mark an item **mastered** after the user gives evidence of understanding. Material that was merely covered is not learned. Critical checklist items should be **mastered** before treating the session as complete; non-critical items can be **partial** or explicitly deferred.

## Misconception Log

Track important misunderstandings as they appear. Use them to adapt teaching rather than simply correcting and moving on.

Record or summarize:

- the mistaken belief or fuzzy distinction
- the evidence or example that corrected it
- the simpler concept or concrete code path to revisit if confusion returns

If the user gets consecutive questions wrong on the same concept, downgrade one level of abstraction, give a tighter hint or mini-example, and re-check with a simpler why or what question before retrying transfer-level prompts. If misses continue, switch to ELI14 or ELI5 depth before asking again.

## Teaching Style

Start by asking the user to explain their current understanding. Use that answer to decide where to teach next.

When teaching:

- explain why before what and how
- keep each chunk small enough to verify immediately
- move from concept to concrete examples
- use code, docs, logs, tests, or debugger steps when they make the topic clearer
- sharpen overloaded terms and align with the language used by the repo, docs, or domain
- slow down and narrow scope when confusion increases
- compress and advance when answers are consistently strong
- adapt depth if the user asks for ELI5, ELI14, intern-level, or expert-level explanations

## Quiz Strategy

Ask one quiz question at a time unless the user explicitly asks for a full quiz.

Sequence questions from easier retrieval to stronger transfer:

1. **Recall**: "What is the core problem in your own words?"
2. **Why**: "Why did this happen, or why does this design pressure exist?"
3. **Path tracing**: "Walk me through the code/data/control flow."
4. **Contrast**: "Why this solution instead of that alternative?"
5. **Transfer**: "What would happen in this similar but different scenario?"
6. **Failure mode**: "Where would this explanation break, or what regression would reveal a bad understanding?"

For each quiz question:

- use open-ended questions when reasoning matters
- use multiple choice when distinctions are crisp
- do not reveal the answer before the user responds
- after the response, explain what was correct, what was missing, and what to fix
- update the rubric immediately for the touched checklist item
- only move on when the current concept is understood
- keep each round to 1-2 questions

For multiple-choice questions, enforce answer-position balance:

- maintain a rolling window of the latest 5 multiple-choice questions and keep correct options as evenly distributed as possible
- avoid placing the correct answer in the same option slot for 3 or more consecutive questions
- if reliable state tracking is unavailable, randomize answer positions and run a quick repetition check before sending

For multiple-choice questions, enforce distractor quality:

- keep distractors in the same semantic domain and granularity as the correct answer
- make distractors plausible-but-wrong rather than obviously absurd
- avoid leaking the answer by mirroring stem keywords only in the correct option
- avoid obvious clues such as a uniquely long or uniquely specific correct option

Default difficulty for multiple-choice questions is medium discrimination:

- at least two distractors should share core concepts with the correct option but fail on causality, boundary conditions, or applicability
- only reduce distractor strength when the user explicitly asks for easy mode

Run a quick quality self-check before sending a multiple-choice question:

- check whether correct-answer positions are becoming concentrated in recent questions
- check whether every distractor is reasonably confusable with the correct option
- check whether wording length or tone accidentally reveals the answer
- if any check fails, rewrite options first, then ask the question

## Retention Guardrails

Distinguish short-term fluency from durable understanding. A smooth answer right after an explanation may only prove immediate fluency.

Build stronger understanding with:

- retrieval before re-reading: ask the user to recall first, then fill gaps
- spacing inside the session: revisit important ideas after a few intervening chunks
- interleaving when appropriate: mix related concepts so the user must choose which rule applies
- transfer questions: require the user to apply the idea in a changed scenario

Use these sparingly in short sessions, but prefer them for complex bugs, architecture, and PR reviews.

## Pacing Guardrails

- keep turns short and checkpoint frequently instead of giving long lectures
- verify one concept chunk at a time, then adapt based on the user's response
- periodically summarize progress against the checklist and call out what remains

If the environment provides a user-question tool, use it when it improves the quiz flow. Otherwise, ask inline in chat.

## Repository-Aware Rule

If a question can be answered by inspecting the codebase, docs, tests, existing artifacts, or local runtime output, inspect those first instead of asking the user to guess.

Show the relevant code or evidence when it helps the user understand the reasoning. If the code contradicts the user's stated understanding, surface the contradiction directly and resolve it before continuing.

## Handoff Format

When context is getting long or the user may continue elsewhere, produce a concise handoff with learning state:

```md
# Learn Quiz Handoff: {topic}

## Goal
- {what the user is trying to be able to explain, judge, or do}

## Evidence Used
- {files, docs, diffs, logs, commands, artifacts, or links inspected}

## Checklist State
- mastered: {items with evidence}
- partial: {items that need one more check}
- not-yet: {items not covered or still shaky}
- deferred: {intentional out-of-scope items}

## Misconceptions / Corrections
- {misunderstanding -> correction -> evidence or example}

## Last Good Answer
- {short note on the user's strongest demonstrated understanding}

## Next Question
- {the exact next quiz question to ask}
```

Do not rely on a fresh session remembering chat history. If continuing in a new session, tell the user to provide the handoff and ask to continue from the next question.

## Lightweight Session Template

Use this loop for most sessions:

1. **Goal + scope**: confirm what they want to understand and what success looks like.
2. **Evidence map**: inspect or list the source material.
3. **Initial restatement**: ask what they currently believe.
4. **Teach one chunk**: explain why first, then what/how.
5. **Quiz one question**: check understanding before moving on.
6. **Rubric update**: mark not-yet, partial, or mastered with evidence.
7. **Next step**: continue, slow down, defer, or hand off.

## Stop Rule

Do not end the learning session merely because the explanation is complete.

End only when the user has demonstrated understanding of the checklist, or when the remaining unknowns are intentionally deferred with clear follow-up items. If the session must stop early, leave the next quiz question and the current rubric state.
