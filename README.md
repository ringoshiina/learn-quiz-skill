# Learn Quiz

Learn Quiz is an agent skill for turning context-backed explanations into real understanding.

It guides the agent to teach incrementally from current session context, workspace-accessible source material, or supplied source material, ask the user to restate their current understanding, fill gaps, and quiz until the user can explain the material back clearly.

## What It Does

- Builds an understanding checklist for the topic.
- Clarifies a concrete learning goal and scope.
- Grounds teaching in source evidence such as code, diffs, tests, logs, docs, PRs, or prior handoffs.
- Starts by asking what the user already understands.
- Teaches one stage at a time instead of dumping a full explanation.
- Uses open-ended or multiple-choice questions to verify retrieval, causality, path tracing, contrast, transfer, and failure modes.
- Avoids revealing quiz answers until after the user responds.
- Tracks mastery state and important misconceptions.
- Inspects code, docs, tests, logs, or local artifacts when the answer can be found there.
- Requires source material or a workspace pointer for new sessions instead of acting as a generic from-scratch tutor.
- Produces a learning-state handoff when the session needs to continue elsewhere.
- Ends only when the user has demonstrated understanding or explicitly deferred remaining items.

## Install

Install globally:

```bash
npx skills add ringoshiina/learn-quiz-skill --skill learn-quiz -g -y
```

Install interactively, without auto-confirming:

```bash
npx skills add ringoshiina/learn-quiz-skill --skill learn-quiz -g
```

Install for the current project only:

```bash
npx skills add ringoshiina/learn-quiz-skill --skill learn-quiz
```

## Usage

```text
[$learn-quiz] Help me understand this code change step by step and quiz me until I can explain it.
```

```text
[$learn-quiz] Teach me why this bug happened, then quiz me on the edge cases.
```

```text
[$learn-quiz] Review this architecture decision with me and check whether I really understand the tradeoffs.
```

```text
[$learn-quiz] Continue from this handoff and ask me the next question.
```

## When To Use It

Use Learn Quiz when the user wants to:

- understand a code change or pull request
- learn why a bug happened
- review a design, plan, or architecture decision
- prepare to explain a specific change, decision, or artifact to someone else
- verify their own understanding after an implementation session
- turn a vague context-backed explanation into a concrete mental model

## How It Works

The skill tells the agent to keep a checklist covering the problem, motivation, constraints, source evidence, decision branches, chosen solution, rejected alternatives, edge cases, validation steps, and transfer targets.

The agent should first ask the user to restate their current understanding, then teach only the missing pieces. It should quiz one concept at a time, log important misconceptions, and move on only after the current concept is understood.

When a question can be answered from the repository or local artifacts, the agent should inspect those sources instead of making the user guess.

When starting in a fresh session, the user should provide or point to the source material first, such as a diff, PR description, design doc, bug report, code snippet, transcript, local artifact, module path, or prior handoff.

For long sessions, the skill can preserve a lightweight learning state or produce a handoff containing the goal, evidence used, checklist status, misconceptions, the last good answer, and the next quiz question.

## Inspiration

Learn Quiz was inspired by [ThariqS's Learn Quiz gist](https://gist.github.com/ThariqS/1389dcdff9eba4789887a2211370f06b), which frames the core loop: teach incrementally, ask the learner to restate their understanding, keep a checklist, and quiz until mastery is demonstrated.

This repository packages that learning loop as an installable agent skill and adapts it for technical work such as code changes, debugging sessions, design decisions, PR reviews, and architecture discussions.

## Skill Path

```text
skills/learning/learn-quiz/SKILL.md
```

## Repository Structure

```text
skills/
  learning/
    learn-quiz/
      SKILL.md
      agents/
        openai.yaml
```

## License

MIT
