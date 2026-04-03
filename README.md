# Project Starter Instructions

This repository is not an application or runnable project.

It is a suggested documentation-first bootstrap template for starting new software projects in an AI-first workflow, where documentation is treated as the source of truth and code is treated as a derived artifact.

## Why This Exists

AI helps us code faster, but speed without control creates drift.

As AI sessions pile up, the same failure pattern tends to show up:

- summaries lose nuance
- architectural intent fades
- the agent starts introducing patterns that do not belong
- common conventions and styles get broken

If you want GitHub Copilot to respect style, intent, and architecture across multiple sessions, simple prompting is not enough. You need durable project context that survives chat history loss.

This repository exists to provide a strong Day-0 starting point.

## Core Idea

In AI-first development, documentation should be treated as the primary source of truth.

That means:

- implementation should follow the docs
- architectural intent should be captured in files, not in memory
- AI agents should be restarted from project documents, not from prior chats
- consistency should begin at the first commit, not after drift already happened

The primary file in this repository is `project-starter-instructions.md`.

It defines one practical way to bootstrap a new project with:

- an always-on instruction layer for GitHub Copilot
- a documentation hierarchy that preserves architectural intent
- task and design documents that can survive fresh AI sessions
- a repeatable workflow for humans and agents working together

The exact structure does not need to be identical across every repo. Each project can have its own flavor, naming, and level of detail. The important part is preserving the same underlying idea: durable context, explicit architecture, and repeatable instructions that survive fresh AI sessions.

## The Day-0 Strategy

### 1. Always-On Guardrails

Stop repeating your style guide in every prompt.

Use `.github/copilot-instructions.md` as the repository-wide, always-on instruction file. GitHub Copilot loads this automatically and uses it to enforce coding conventions, constraints, and behavioral rules across new tasks.

This is where you define expectations such as:

- what docs must be read before implementation
- what must be updated after implementation
- diff discipline and refactoring boundaries
- architectural constraints that should not be ignored

### 2. Modular Memory Stack

Instructions define the how, but project docs define the why.

The starter structure in this repo uses a simple hierarchy:

- `docs/START_HERE.md` as the knowledge entrypoint
- `docs/tasks.md` as the execution plan
- `docs/design/` as the architectural deep-dive

This gives the agent an explicit path for loading context instead of guessing from scattered files.

### 3. Handshake Protocol

Before the agent writes code, give it the context it deserves.

Example kickoff prompt:

```text
Read docs/START_HERE.md to learn the architecture and constraints before proposing a plan.
```

That small handshake changes the quality of the session. It forces the agent to anchor on project intent before producing code.

## What This Template Suggests

The starter instructions are designed to initialize a documentation-first structure like this:

```text
.github/
	copilot-instructions.md

docs/
	START_HERE.md
	tasks.md
	design/
		design.md
	research/
		research-notes.md
	decisions/
		ADR-0001-initial-architecture.md
	templates/
		TASK-COMPLETION-TEMPLATE.md
		TASK-KICKOFF-TEMPLATE.md
```

Treat this structure as a baseline, not a strict standard. A real project may rename files, split documents differently, or add domain-specific folders. What matters is that the repo gives both humans and AI agents a reliable path to recover intent.

The goal is straightforward: make architectural intent durable enough that a fresh AI session can recover the project correctly.

## How To Verify Copilot Is Really Loading `.github/copilot-instructions.md`

If you are relying on always-on instructions, you should test that they are actually being applied.

One simple technique is to add a temporary, easy-to-detect instruction to `.github/copilot-instructions.md`, for example:

```md
For each response, append the suffix: [copilot-instructions-loaded]
```

Then start a new task in Copilot Chat and see whether the suffix appears consistently.

Other practical verification ideas:

- Add a temporary instruction that says: `Before proposing changes, state which docs you read first.` If Copilot starts by naming the expected docs, the file is likely being honored.
- Add a temporary wording rule such as: `Use the phrase "minimal diff plan" when proposing implementation steps.` This is easy to spot and easy to remove.
- Add a temporary refusal rule for a narrow case, such as: `Do not propose code until you have read docs/START_HERE.md.` Then check whether Copilot follows that sequencing.
- Test in a fresh chat after saving the file. Do not rely on an already-running conversation that may still be carrying earlier context.

Keep these verification markers temporary. They are useful as diagnostics, but you generally do not want permanent noise in normal responses.

## Who This Is For

This template is useful if you want to:

- reduce architectural drift in AI-assisted development
- keep style and intent stable across multiple Copilot sessions
- make project context recoverable without chat history
- onboard new developers and new agents from the same docs
- create cleaner, more reviewable implementation loops

## Use It In Any New Repo

You can copy these starter instructions from `project-starter-instructions.md` into any new repository and adapt them to fit your project's own style, constraints, and operating model.

___
LinkedIn Post: [AI Drift in AI-First Development](https://www.linkedin.com/feed/update/urn:li:activity:7445763394974093312/)

