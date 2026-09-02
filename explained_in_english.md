# Preparing Human-Authored Code for AI

How do you handle editing existing repositories with tools like Codex?

There are times when documentation is insufficient for an AI to grasp the entire project, or test cases are lacking for an AI to perform automated edits and execute TDD (Test-Driven Development). Handing over a repository that humans have nurtured over time to an AI can feel daunting.

In such cases, using something like `@codex-ready` might make your life easier.

https://github.com/reiwa-ai/codex-ready-skill


# What is this?

AI coding agents like Codex and Cloud Code are incredibly useful for building applications from scratch.

However, real-world software development isn't always a clean, straightforward process.

In fact, a far more common scenario is:

**"Handing over an existing repository—developed by humans over many years—to an AI."**

This presents challenges distinct from greenfield development: documentation is often insufficient for the AI ​​to understand the project scope, and test cases are lacking for the AI ​​to perform automated edits or run TDD loops.

**Ultimately, the extra work required to prepare the project for AI handover becomes so burdensome that using AI agents isn't feasible.**

It is easy to simply attribute this to a lack of documentation or test cases—implying that the humans involved were lazy—but that isn't the whole story.

The real issue is that **"differences in cognitive mechanisms between humans and AI mean that more information is required for a successful handover."**

## Handing Over Existing Repositories to AI is Surprisingly Difficult

Imagine, for instance, a repository that humans have maintained for years.

The code itself is stored in Git.

However, the information necessary to modify that code isn't always explicitly written within the code itself. "This logic looks odd, but it's kept there to maintain backward compatibility."

"Do not add files directly to this directory."

"In the production environment, services start up in this specific order."

"Unit testing this function alone fails, but the system works correctly as a whole."

"It’s not in the README, but this configuration value has a specific meaning."

Human developers gradually learn this kind of information through code reviews, past incidents, Slack conversations, verbal explanations, Git history, and so on.

In other words, the reason humans can edit existing code isn't just because they can read the source code.

**It is because they possess "contextual knowledge" about the repository.**

AI coding agents face the same issue.

If you open a repository in Codex and ask it to:

"Add this feature,"

it will, of course, examine the code and make the changes.

However, without knowledge of the repository's specific nuances, the following issues can arise:

*   It might decide that working code is "unnecessary" and remove it.
*   It might violate implicit design rules.
*   It might modify areas that didn't need changing.
*   It might fail to verify the validity of changes because it doesn't know how to run the tests.
*   It might re-investigate the same things every time the session changes.

I don't believe the solution here is simply writing longer prompts.

What is needed is:

**Transforming repositories originally built for humans into repositories that AI can also handle effectively over the long term.**

## Creating an "AI-Ready Repository"

`codex-ready` is a Skill that tasks Codex itself with performing the preparatory work to achieve this.

Its defining characteristic is that it doesn't jump straight into implementation.

First, it analyzes the target repository.

It checks the language, framework, package manager, build process, test environment, entry points, deployment configuration, and existing documentation to categorize the type of software the repository contains. For example, categories include:

* Python API
* Node.js / TypeScript backend
* React / Next.js / Vue frontend
* CLI
* Monorepo
* Data processing / Machine learning
* Infrastructure
* Mobile / Desktop apps

The key is not to force a single repository into just one category.

In real-world projects, it is common to have a combination of characteristics—such as "Python API + React UI + ML + Docker."

`codex-ready` classifies repositories across multiple axes and constructs the AI-specific information needed for them.

## A README Isn't Enough

As a result of this preparation process, `codex-ready` primarily sets up the following files:

### README.md

This is intended for humans, just as it has always been.

It covers the project overview, architecture, setup instructions, key workflows, and so on.

### KNOWLEDGE.md

This file contains knowledge specifically for AI agents.

It stores information that is difficult to glean from reading the code alone, such as:

* Points of caution
* Implicit assumptions
* Invariants
* Common pitfalls
* Repository-specific rules

In short, the roles are divided as follows:

**The README explains "what this software is," while KNOWLEDGE explains "what to watch out for when working with this software."**

Personally, I consider this separation to be crucial.

If you bloat the README with AI-specific details, it becomes difficult for humans to read.

Conversely, a human-oriented README alone cannot adequately capture the fine-grained precautions an agent needs.

That is why the information is separated based on the intended audience.

## Don't Fix Bugs Without Permission

Another file that is prepared is:

`KNOWN_BUGS.md`

When you have an AI thoroughly analyze an existing repository, it may discover issues unrelated to the task you originally requested.

To an AI agent, the action of saying, "I found a problem, so I fixed it," might seem helpful.

However, in an existing system, this can be dangerous.

Behavior that appears to be a bug might actually be there to maintain compatibility with past versions. Other systems might rely on that specific behavior.

Therefore, the policy for `codex-ready` is that if an issue is discovered during investigation,

**it must first be recorded in `KNOWN_BUGS.md`**

Fixing the issue comes later.

This is an engineering rule for safely handling existing systems, rather than something specific to AI.

## Creating "Handover Documentation" for AI

Another crucial component is `AGENT.md`.

This file outlines operational guidelines for AI agents that might edit the repository in the future.

For example, it includes instructions such as:

* Check the repository before making edits
* Read the guide relevant to the project type
* Review `KNOWLEDGE.md`
* Record any issues found during investigation in `KNOWN_BUGS.md`
* Perform unit tests on critical functions
* Run E2E tests after a series of changes
* Respect existing code and minimize the scope of changes
* Do not make major changes based on assumptions if the intent is unclear

In essence, this is similar to what human developers would call

**"handover documentation for a new team member."**

The only difference is that the intended reader is an AI.

## Retaining Project-Specific Expertise Locally

For instance, a project mixing Python and React requires attention to different details for each language.

To address this, `codex-ready` avoids cramming all instructions into a single massive file; instead,

```text
.codex-ready/
└── project-types/
├── python.md
├── web-ui.md
└── ...
```

it generates specific guides tailored to the types of components found in the repository.

`codex-ready` itself also includes built-in reference material for:

* Python
* JavaScript / TypeScript
* Go / Rust / Java / .NET
* C / C++ / Ruby / PHP
* Web UI
* Mobile / Desktop
* Data / ML / Infrastructure The design ensures that the system references only what is necessary based on an analysis of the repository.

This prevents the AI ​​from having to derive development methods from general principles every time;

instead, it translates information into—and retains—local knowledge specific to the question:

**"How do we handle things in *this* repository?"**

## Another crucial factor: "Testability"

In AI coding, attention often focuses solely on the ability to generate code.

However, when it comes to continuously editing existing code, something even more important is:

**the AI's ability to verify the results of its own changes.**

In a repository lacking tests,

if the AI ​​says, "I fixed this function,"

it has no way to verify whether the fix actually worked.

That is why `codex-ready` emphasizes preparing the following—even when existing test coverage is insufficient:

*   Lightweight execution paths to verify critical functions
*   A framework for E2E tests or a defined testing strategy

For instance, in Python, you don't necessarily need to build a massive test suite from scratch.

Simply being able to execute key processes directly and verify inputs and outputs makes a significant difference for the agent.

It is not just about the ability to read code;

it is about enabling the AI ​​to execute the **Change → Execute → Verify** loop on its own.

This, too, is part of making a project "AI-Ready."

## "AI-oriented documentation" isn't a one-time task

Even after creating `KNOWLEDGE.md`, it won't be perfect from the start.

In fact, as the AI ​​performs tasks, it should accumulate new knowledge, such as:

"This API must not be called under these conditions."

"This test requires a Docker environment."

"This process looks unnecessary at first glance, but it must not be deleted."

`codex-ready` is designed to capture these insights in `KNOWLEDGE.md` and reuse them in future editing sessions.

This eliminates the need for the AI ​​to research the same information repeatedly across different sessions.

It is essentially the same process used by human teams to:

**"convert individual-specific knowledge into organizational knowledge through documentation,"**

but applied here to AI agents. ## Use this before having Codex write code

`codex-ready` is not a code-generation skill itself.

Rather, it serves as a preparatory step that comes right before that.

When you are about to work on an existing repository using Codex, the intended workflow is as follows:

```text
Existing repository
↓
codex-ready
↓
README / KNOWLEDGE / KNOWN_BUGS
AGENT / project-types / tests
↓
Development with Codex
↓
Accumulate gained knowledge
↓
Used by Codex next time
```

Once this preparation is complete, it becomes much easier to make ongoing modifications using Codex.


## In the Era of AI Coding, More Than Just Code Becomes Part of the Repository

Until now, the focal point of software repositories has naturally been the source code.

README files and design documents were generally viewed as supplementary materials to help humans understand the code.

However, the situation changes somewhat when AI coding agents begin to continuously edit software.

For an AI, information regarding:

*   the structure,
*   how changes should be made,
*   what must not be changed,
*   how to conduct testing, and
*   past issues encountered

is just as important as the code itself.

In other words, I believe that moving forward:

**Not only source code but also "knowledge for the AI ​​to handle the source code" will become a repository asset.**

OpenAI's "Skills" feature itself is a mechanism that allows work procedures to be reused via `SKILL.md` files. OpenAI positions Skills as workflows where the method for executing a specific task is defined once and then applied repeatedly.

`codex-ready` takes this concept a step further by embedding it directly into the repository.

It does not involve packing all knowledge into the Skill itself.

Instead, it uses the Skill to:

**Create AI-oriented knowledge specific to that repository *within* the repository itself.**

Only after establishing this state do we entrust full-scale editing to Codex.

Such preparation is likely essential if we are to carry not only newly created "AI-native code" but also code developed by humans over many years into the AI ​​era.

Please give it a try as the first Skill you use when you start editing an existing repository with Codex.

**codex-ready**

[View on GitHub](https://github.com/reiwa-ai/codex-ready-skill?utm_source=chatgpt.com)