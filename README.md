# Learn Quiz

Learn Quiz is an agent skill for turning explanations into real understanding.

It guides the agent to teach incrementally, ask the user to restate their current understanding, fill gaps, and quiz until the user can explain the topic back clearly.

## What It Does

- Builds an understanding checklist for the topic.
- Starts by asking what the user already understands.
- Teaches one stage at a time instead of dumping a full explanation.
- Uses open-ended or multiple-choice questions to verify comprehension.
- Avoids revealing quiz answers until after the user responds.
- Inspects code, docs, tests, logs, or local artifacts when the answer can be found there.
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

## When To Use It

Use Learn Quiz when the user wants to:

- understand a code change or pull request
- learn why a bug happened
- review a design, plan, or architecture decision
- prepare to explain a topic to someone else
- verify their own understanding after an implementation session
- turn a vague explanation into a concrete mental model

## How It Works

The skill tells the agent to keep a checklist covering the problem, motivation, constraints, decision branches, chosen solution, rejected alternatives, edge cases, and validation steps.

The agent should first ask the user to restate their current understanding, then teach only the missing pieces. It should quiz one concept at a time and move on only after the current concept is understood.

When a question can be answered from the repository or local artifacts, the agent should inspect those sources instead of making the user guess.

## Related Work and Inspiration

Learn Quiz sits in the broader agent-skill ecosystem rather than trying to invent a new category from scratch. Related skills include:

- [mattpocock/skills@teach](https://skills.sh/mattpocock/skills/teach), which focuses on teaching through structured interaction.
- [everyinc/compound-engineering-plugin@coding-tutor](https://skills.sh/everyinc/compound-engineering-plugin/coding-tutor), which explores coding-focused tutoring.
- [readwiseio/readwise-skills@quiz](https://skills.sh/readwiseio/readwise-skills/quiz), which uses quiz behavior as part of a learning workflow.

The learning loop is also influenced by established teaching patterns:

- [Teach-back](https://www.ahrq.gov/teamstepps-program/curriculum/communication/tools/teachback.html): asking the learner to explain their understanding back so gaps become visible.
- [Retrieval practice](https://www.cmu.edu/teaching/resources/instructionalstrategies/activelearningstrategies/retrievalpractice/index.html): using recall and questions as part of learning, not merely as final assessment.

Learn Quiz is shaped for agent-assisted technical work: code changes, debugging sessions, design decisions, PR reviews, and architecture discussions where the goal is not only to get an answer, but to leave with a durable mental model.

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
