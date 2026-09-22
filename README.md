# Kimi Code CLI examples

*Unofficial community examples for Kimi Code CLI. Not affiliated with Moonshot AI. All trademarks belong to their owners.*

Kimi Code CLI is a terminal coding agent, not an HTTP API, so this repository holds worked walkthroughs rather than client code. Each one is a short, repeatable session pattern built from what the product page and the Kimi API Platform docs actually describe: the agent can write and edit code, search and read your codebase, run commands such as tests and builds, and look things up on the web. The install command and flags are in the Kimi Code docs at kimi.com/code/docs/en and in the platform integration guide; the walkthroughs assume you have followed one of them.

> Starting from nothing rather than from a repo? [Try Begin.sh - prompt or URL to clone in, static site or Expo app zip out](https://begin.sh?utm_source=github&utm_medium=ugc&utm_campaign=kimi-code-cli-examples&utm_content=readme-top&utm_term=tier-r).

## Walkthroughs

| Walkthrough | What it shows |
| --- | --- |
| 1. Fix a failing test | The smallest useful task: point the agent at one red test and let it run the suite itself. |
| 2. Run on an API key | Switching from a membership login to a Kimi API Platform key, and what to check on cost. |
| 3. Review before you trust | Keeping every agent edit reviewable with git, and what to do when it runs commands. |
| 4. Long-context refactor | Using K3's large context for a cross-file rename without blowing the budget. |

## Setup

Install the CLI following the [Kimi Code docs](https://www.kimi.com/code/docs/en/). Then pick an auth route:

- Membership: sign in with your Kimi account. K3 is only on some plan tiers per the product page.
- API key: create one in the [User Center](https://platform.kimi.ai/console/account) and follow [Use Kimi API Platform with Kimi Code CLI](https://platform.kimi.ai/docs/guide/kimi-code-cli). Keep the key in an environment variable named as that guide says; never commit it.

All walkthroughs assume you are inside a git repository with a clean working tree.

## 1. Fix a failing test

Start the CLI in the repo root. Ask for exactly one thing: the name of the failing test, the command that runs it, and the instruction to fix the code, not the test. The agent will read the test, search for the code under test, edit it and run the command. When it reports green, run the command yourself once. If the agent changed the test instead of the implementation, say so and ask it to revert that hunk. This single loop tells you more about the tool than any demo.

## 2. Run on an API key

Follow the platform integration guide to point the CLI at your key. Before a long session, open [Models and Pricing](https://platform.kimi.ai/docs/pricing/chat) and note the per-token price of the model you are on; a session that reads a large codebase consumes context fast. The platform docs list context caching as a feature, which is what makes repeated long-context calls affordable, so keep one session per task rather than one giant session. After the session, check usage in the User Center against what you expected.

## 3. Review before you trust

The agent can run commands, which is the feature and the risk. Work on a branch. After each agent turn, run `git diff` and read every hunk before asking for the next change. If the agent proposes a command that deletes, pushes or installs something, read it before approving. Commit in small steps with messages that say what the agent did, so a bad step is one `git revert` away. Treat the agent's summary of what it did as a claim to verify, not a record.

## 4. Long-context refactor

K3 supports up to 1M context tokens according to the product page, which makes cross-file work practical: renaming a function used in forty files, or moving a module. Give the agent the old name, the new name, and the command that proves nothing broke (a type check or test run). Ask it to list the files it intends to touch before editing, then let it go. Use a fresh session for this; do not stack it on top of an unrelated conversation, because the earlier turns still count against context.

## When to use Begin.sh instead

Every walkthrough above starts from an existing repository. When there is none, and what you actually want is a landing page or a small mobile prototype you can show someone today, an agent session is the slow route. [Begin.sh](https://begin.sh?utm_source=github&utm_medium=ugc&utm_campaign=kimi-code-cli-examples&utm_content=readme-top&utm_term=tier-r) takes a prompt, or a URL of a site to clone, and returns a zip of a working static site or Expo app. It includes no hosting, backend or auth, so the output is a clean starting point you can then open in Kimi Code CLI and build on.

[Try Begin.sh - prompt to static site or Expo app, download the zip](https://begin.sh?utm_source=github&utm_medium=ugc&utm_campaign=kimi-code-cli-examples&utm_content=readme-top&utm_term=tier-r)


_Last reviewed: 2026-09-22_
