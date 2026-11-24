# SDL4 Digital Integration Plan

Version 1.2, 2026-11-24

**Goal:** SDL4 has various disconnected modules. They will need both physical and digital integration in the Lash Miller expansion. For digital integration to go smoothly, we need two things from each module owner: information about the module, and code brought in line with reasonable standards. This information will also help us pass knowledge on to future users.

Some words, such as *module*, *state*, *unit operation* and *flow*, have a specific meaning here. They are defined in [Definitions](definitions.md).

## What's in this repository

| File | What it is |
|---|---|
| [requirements/information-required.md](requirements/information-required.md) | What to write about your module |
| [requirements/up-to-date-code.md](requirements/up-to-date-code.md) | The standards your code should meet, as a checklist |
| [definitions.md](definitions.md) | What the key words mean |
| [template/MODULE_INFO.md](template/MODULE_INFO.md) | A blank file to copy into your repository and fill in |
| [examples/lash-e/MODULE_INFO.md](examples/lash-e/MODULE_INFO.md) | A worked example for one module, Lash-E. It is an example, not a requirement. |

## What to hand in (by December 11, 2026)

1. **Your module's information:** copy [template/MODULE_INFO.md](template/MODULE_INFO.md) into your repository as `docs/MODULE_INFO.md` and fill it in, laid out like the [Lash-E example](examples/lash-e/MODULE_INFO.md).
2. **Your repository:** brought up to the [Up-to-Date Code](requirements/up-to-date-code.md) standards.

Both live in your own repository, so you hand in one thing: a link to its main branch. Send the link, and any questions, by opening an issue in this repository or messaging Owen on Slack.

## How to do this

Work through these steps in order. Each one keeps your working code safe while you change it.

**Who does what:** the AI reads your code, drafts text and makes changes when you ask. You decide what to keep, test everything, and are responsible for what you hand in.

| Step | You | The AI |
|---|---|---|
| 1. Save a working version | Commit the code that runs today | Nothing |
| 2. Make a branch | Make all changes on a branch | Nothing |
| 3. Check your code | Paste the prompt; check its answer | Checks your code against the standards and lists the changes |
| 4. Draft your module's information | Paste the prompt; fill in and correct the draft | Drafts it from your code, marking guesses |
| 5. Make the changes | One item at a time: read, test, commit | Makes the changes for one item |
| 6. Test on hardware, then merge | Run a real workflow with someone watching | Nothing on the hardware |
| 7. Hand in | Send your repository link | Nothing |

### The steps in detail

1. **Save a working version.** If your code isn't in GitHub yet, put all of it in one repository. Then commit the version that runs on your module today. This is your safe point: you can always go back to it.

2. **Make a branch.** A branch is a separate copy of your code where you can make changes without touching the version you saved in step 1. Make all the changes below on this branch. The lab keeps running from your main version until you've tested the branch and merged it back.

3. **Ask AI to check your code.** Open your repository in an AI coding tool that can read your files, such as Claude Code, and paste:

   > Read the standards in https://github.com/AC-SDL4/integration/blob/main/requirements/up-to-date-code.md and check my repository against each one. For each one, say met, partly met or not met, and point to the files. Then list the smallest changes that would meet each one, in the order of the checklist. Don't change anything yet.

   Read the answer and check it against what you know about your module. This list is your plan for making the changes.

4. **Draft your module's information.** In the same tool, paste:

   > Copy https://github.com/AC-SDL4/integration/blob/main/template/MODULE_INFO.md into my repository as docs/MODULE_INFO.md, and fill it in from my code, following https://github.com/AC-SDL4/integration/blob/main/requirements/information-required.md and laid out like https://github.com/AC-SDL4/integration/blob/main/examples/lash-e/MODULE_INFO.md. Mark anything you guessed or couldn't find.

   Then go through it yourself. The code can't tell the AI about maintenance, known issues or where you buy supplies, so fill those in and correct anything it got wrong.

5. **Make the changes one at a time.** On your branch, work through the [checklist](requirements/up-to-date-code.md) in order. For each item, paste:

   > Make the changes for [item name] only. This code runs real hardware, so don't change what the hardware does (moves, positions, speeds, order of steps) without asking me.

   Read what it changed before you keep it. Test the change without hardware, then commit it with a short note saying what changed. If something breaks, you can go back to your last commit.

6. **Test on the hardware, then merge.** When the checklist is done, run a short, real workflow from your branch, with someone watching who can stop the module. Start with steps that are easy to recover from, such as a single move or a dispense of water. If it all works, merge the branch into main. If not, fix it on the branch, or go back to the version you saved in step 1.

7. **Hand in.** Send a link to your repository's main branch, as described in [What to hand in](#what-to-hand-in-by-december-11-2026).

If your AI tool can't open links, download this repository and give it the files instead.
