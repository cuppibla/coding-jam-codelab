# TA Training — Speaker Notes (v7.1)

**Format:** Conversational script. Read or paraphrase. Stage directions in *italics*. Demo clip cues in **bold boxes**.

**Through-line to hammer:** *"Ask the next question. Don't answer it."* — Setup is the only exception.

**What's new in v7.1:** TDD is now a dedicated stage (Stage 5) between Implement and Verify. Tests are the gate before human verification. The `test-driven-dev` skill provides methodology; `engineering.md`'s Testing strategy section provides the project-specific plan.

**Target length:** 60+ min with live demo clips played inline.

---

## Slide 1 — Title

*[Open slide. Pause for a beat. Let people settle in.]*

> Hey everyone, welcome. Glad you're all here.
>
> If you're new — this is the TA training for Coding Jam, our weekly workshop where complete beginners walk in and ship working AI apps in 75 minutes. If you're returning — welcome back, there are a few tweaks since last cohort that I want to walk you through. The biggest one: we've added a dedicated testing stage. We'll get there.
>
> The next hour is going to do two things. First, I'm going to walk you through the full development lifecycle that participants go through — every stage they hit, in order. Second, at each stage, I'm going to play a clip from a demo I recorded so you can see exactly what the participant experience looks like, and exactly what your job is.
>
> Before we start, one sentence. If you remember nothing else from today, remember this:
>
> **"Ask the next question. Don't answer it."**
>
> That's the entire job, summarized. We'll come back to it a lot. There's one exception, and we'll get to that too.
>
> Let's go.

*[Advance to slide 2.]*

---

## Slide 2 — The Full Development Lifecycle

*[This slide is the spine of the whole training. Spend 4-5 minutes here. Walk through the diagram with your finger or laser pointer.]*

> OK, this is the map. Hold this in your head — everything we do today maps to this diagram.
>
> A participant walks in with an idea. *[Point to "Requirement" box.]* That's where they start.
>
> Stage one — they have a 2-minute conversation with AI called a **Spec Talk**. *[Point.]* No code yet. They're just answering a few questions so AI understands what to build.
>
> Stage two — AI generates **three design artifacts**. *[Point to the red box with the three file chips.]* A product doc, a UI doc, an engineering doc. These get saved as markdown files on the participant's disk. That matters. We'll come back to why.
>
> Notice the engineering doc has a little subline — *[point to the "+ Testing strategy" tag]* — "Testing strategy." That's new in v7.1. The engineering doc now includes a section saying what tests need to exist for this app. We'll use it in Stage 5.
>
> Stage three — **Review and iterate**. *[Point to the yellow box and the bidirectional arrows.]* The participant reads the docs, leaves comments, asks AI to fix the plan. Notice the arrows go both ways — that's the "oops loop." They might bounce between Artifacts and Review a few times before approving.
>
> Once they approve, stage four — **Implement**. *[Point.]* This is where AI actually writes code. But first, there's a setup step that involves Vertex AI, API keys, configuration. We'll talk about that — it's the scariest part of the whole session.
>
> Now — *[point firmly to the new green Stage 5 box]* — **this is new.** Stage five — **Write & Run Tests.** Before a human verifies anything, tests run. AI writes tests based on the testing strategy in `engineering.md`. AI runs them. If they fail, AI fixes the code and re-runs, up to three times. That's the auto-fix loop you see on the side. Tests pass — *[trace the green arrow down]* — gate cleared, hand off to human. Tests fail past three tries, AI stops and we troubleshoot.
>
> Stage six — **Verify**, by the human. *[Point to the blue box.]* Tests caught the dumb stuff. The human catches the UX stuff — things tests missed. And when the human catches a bug, the discipline is to write a test for it. So bugs found in Stage 6 become new tests in Stage 5. *[Trace the small upward arrow.]*
>
> Once MMV works, stage seven — **Pivot or Expand**. *[Point to the pivot box, then trace the red dashed arrow back up to Design Artifacts.]* This is the most important arrow on this whole diagram. When a participant pivots, they don't go back to the start. They don't start over. They go back to the *design docs* and regenerate them. Including the testing strategy. Then they re-apply the skill, and new tests get written. The spec is the lever. Not the code.
>
> Stage eight — **Polish**. *[Point.]* Apply a design skill, iterate on color and text. Notice this one also loops on itself — polish is never done.
>
> Now — *[point to the Skills cloud on the right]* — see this floating box on the side? **Skills.** These apply at any stage. But look — *[point to the green ★ row at the top of the Skills cloud]* — there's one skill that's REQUIRED, not optional. The `test-driven-dev` skill. That's the methodology that drives Stage 5. Everything else in the Skills cloud is optional — apply it when useful. The TDD skill is the one you can't skip.
>
> Last thing before we move on — *[trace the flow one more time, fast]* — Requirement, Spec Talk, Three Artifacts, Review, Implement, Tests, Verify, Pivot, Polish. That's the whole map. Every clip I play is one of these stages. Every TA intervention happens at one of these stages.
>
> Questions about the map before we get into the details?

*[Pause for questions. Then advance.]*

---

## Slide 3 — Pre-Session Floor: Environment Check

*[Practical slide. Move briskly — 2-3 minutes max.]*

> Before every session, you have homework. I'm going to be quick about this because it's logistical, but it matters.
>
> Run the demo path yourself, on a fresh machine, before every session. Whatever breaks for you will break for participants. Guaranteed.
>
> On the **tooling side** *[point to blue panel]* — Antigravity installed, signed in, CLI authenticated, an API key you've tested with at least one prompt, and the codelab open in a browser tab. Not bookmarked — actually open. You will reference it during the session.
>
> Two new things in v7.1 on the tooling list. First, **the test runner has to actually work on your machine.** That's pytest for Python or Jest/Vitest for Node. Install it, then run one dummy test that passes, just to confirm it executes. If the runner isn't installed properly, Stage 5 will fail in a confusing way — and it'll look like AI is wrong when it's actually your environment.
>
> Second, **bookmark the GitHub URL of the `test-driven-dev` skill.** You'll be pasting this link to every participant in Stage 5. Have it ready in your clipboard or pinned in a tab.
>
> On the **environment side** *[point to green panel]* — Python installed at the version the codelab says, same for Node, and Git available. Check the versions match the codelab. They've bitten me before.
>
> And know the **OS gotchas**. *[Gesture to the row at top.]* Every session has at least one of each — Mac, Windows, ChromeOS. The pain points are different on each. Macs throw permission prompts on first run. Windows is the worst — PowerShell vs. Command Prompt confusion, antivirus blocking installs. ChromeOS, the Linux container has to be enabled in settings or nothing works.
>
> Returning TAs — quick reminder, we now require you to have actually run the demo, *including the testing stage*, not just installed the tools. Catching a real bug yourself is worth more than reading docs.
>
> One sentence I want you to internalize: "Let me check the docs" works *once* before participants stop trusting you. So do the homework.

*[Advance.]*

---

## Slide 4 — Stage 1: The Spec Talk

*[Now the real content starts. Spend ~5 minutes on this slide including the clip.]*

> OK, Stage 1. The Spec Talk.
>
> Here's the framing I want you to use with participants: a Spec Talk is a 2-minute conversation. One required question. The rest shape the result.
>
> The required question — *[point to the big red card]* — is "What goes in, what comes out?" This is the I/O contract. Without this, AI literally cannot build. With *only* this, AI can build something. It might not be the right thing, but it can build.
>
> Everything else *[gesture to the three optional questions below]* — magical moment, what you're NOT building, personality — those *shape the result*. They make the output better. They're not required.
>
> Why does this matter for you as a TA? Because first-timers freeze on the optional questions. They especially freeze on "What's the magical moment?" — they don't know what to say. And what you'll be tempted to do is help them brainstorm a magical moment.
>
> **Don't.**
>
> If they freeze on the optional questions, skip them. Make sure they nail Q1, and move on. They can come back and shape the result later.
>
> Now let me show you what this looks like in practice.

*[**PLAY CLIP 1 — Spec Talk conversation.** Roughly 2-3 minutes of demo.]*

> Did you notice what happened there? I didn't tell AI what to build. *AI asked me*, and I answered. That's the whole pattern.
>
> Notice also — I answered Q1 carefully and I was kind of lazy on Q3. That's fine. The contract was clear, AI knew what to build.
>
> Now — *[point to the "Who runs it" panel on the right]* — quick note on facilitation. In weeks 1 through 3, you facilitate the Spec Talk *for the room*. Everyone does the same Spec Talk together, you ask AI the questions. Weeks 4 through 7, participants do it solo. Week 8, they do it on their own original idea.
>
> If you have a drop-in who shows up for the first time in week 8 — treat them like week 1. Don't throw them into the deep end.
>
> And here's the rule that gets violated the most — *[point to the green TA Role panel at bottom]* — **TAs never run the Spec Talk for a participant.** Even if they're stuck. Even if they're frustrated. Even if you've got an idea that would be perfect for them.
>
> Your job is to ask the next question. Not answer it.
>
> If they freeze on Q1, try: "Close your eyes — when you imagine showing this to one person, who is that person?" That's a question, not an answer. They have to fill in the blank.
>
> This is the move that separates the workshop from a tutorial. We're teaching them how to talk to AI. The Spec Talk is the practice; the apps are just the side effect.

*[Pause. Ask: "Questions on the Spec Talk?" Then advance.]*

---

## Slide 5 — Stage 2: Three Design Artifacts

*[~5 minutes including clip. Slightly longer than v7 because the testing strategy section is a new thing to flag.]*

> Stage 2. After the Spec Talk, AI generates three saved files.
>
> *[Point to each in turn.]* `product.md` — what we're building and why. `ui.md` — how it looks and feels. `engineering.md` — how it's built. And inside `engineering.md`, a section called **"Testing strategy."**
>
> Let me explain the mental model first, then I'll explain why the testing strategy section matters.
>
> The model: **treat it like a team.** AI is your PM, AI is your designer, AI is your engineer, AI is your QA. You are the boss. You don't write the docs yourself — you have your team write them, then you review.
>
> This framing changes everything. Suddenly it's not "I'm using AI to write code." It's "I have a team and I'm directing them." That's a much more empowering posture.
>
> Now — about the testing strategy section. *[Point to the green sub-line on the engineering.md chip.]* This is new in v7.1. When AI generates `engineering.md`, it now includes a section that says, for *this specific app*, what needs to be tested. Which functions get unit tests. Which user flow gets a simple integration test. What's deliberately not being tested.
>
> Here's the important thing — this is **half the testing setup.** The other half lives in a reusable skill on GitHub called `test-driven-dev`. The skill defines *how* to test — the auto-loop, the retry cap, the stack defaults. The doc defines *what* to test for this project. The skill is universal; the plan is specific. We'll see them combine in Stage 5.
>
> For now, what matters: the testing strategy section has to actually exist in `engineering.md`. If it's missing, Stage 5 has nothing to execute on.
>
> Let me show you the generation.

*[**PLAY CLIP 2 — Three artifacts generated.** Show AI producing all three docs, with the testing strategy section visible in engineering.md.]*

> OK — your job here is to verify three things.
>
> First — *[point to the green TA Role panel]* — coach them to actually save the files. The prompt I use is: *"Save the product, UI, and engineering designs as three separate markdown files."* Then you walk over to their machine and **verify the files appear in the file explorer.**
>
> If the files aren't there, the AI didn't actually save them. Re-prompt. No files means no foundation for the rest of the session — they have nothing to come back to when they pivot.
>
> Second — and this is new — **check that `engineering.md` has a Testing strategy section.** Just open it, scroll, look for the heading. If it's missing or thin — like one vague sentence — coach them to prompt: *"Add a Testing strategy section to engineering.md. List what needs unit tests, what needs one integration test, and what's not worth testing."*
>
> Third thing to convey: these files are **portable**. They work in Antigravity. They work in Gemini CLI. They work in Claude Code. The chat history doesn't transfer between tools. The saved docs do.
>
> So if a participant switches tools mid-session, or wants to keep building at home with a different tool, the spec travels with them. The conversation doesn't.
>
> This is one of those small things that turns a one-night workshop into a forever skill. Make sure they save the files. Make sure the testing strategy section is there.

*[Advance.]*

---

## Slide 6 — Stage 3: Review & Iterate

*[~3 minutes including clip.]*

> Stage 3. Before AI writes any code, the boss reviews the plan.
>
> Participants read each of the three docs and leave comments on them — like reviewing a pull request, if you're familiar with that. If they're not familiar with PR review, the framing is "you're the editor, AI wrote the draft, your job is to mark it up."
>
> Now here's where the most important habit in the whole workshop shows up. I call it the **"oops" loop.**
>
> *[Point to the yellow quote.]* When the plan needs updating — and it will — participants will instinctively want to ask AI to fix the code. Or worse, they'll wait until AI has built something they don't like, and *then* try to fix the code.
>
> Stop them. Coach them to update the doc first.
>
> The prompt is something like: *"We just changed our minds. Update product.md to reflect the new plan, then rebuild from that."*
>
> See the difference? They're not asking AI to change the code. They're asking AI to change the *plan*, and then build from the new plan. The doc is the source of truth.
>
> Why does this matter? Because without spec discipline, by minute 35 they're going to have an AI that's confused. They've piled prompts on top of prompts, the code is a mess, and they don't remember what they originally wanted. The doc keeps them anchored.
>
> One thing to flag — this rule applies to the testing strategy section too. If, during review, the participant looks at the testing strategy and thinks "those tests don't make sense for what I'm building" — same move. Update the doc, then move on. Don't try to fight with the test plan downstream.

*[**PLAY CLIP 3 — Reviewing and commenting on docs.**]*

> Did you notice? I'm not editing the code in that clip. I'm not even looking at the code. I'm reading the plan, finding things I want to change, and asking AI to update the plan.
>
> Once the plan is right, the code follows.
>
> Your TA role here — *[point to green panel]* — when AI builds something that looks wrong, pull them back to the doc. Don't help them debug the code. Ask: "Does the doc match what you actually want? Fix that first."
>
> That's the move that separates vibe coders from real builders. Code comes from a plan. Plan changes first.

*[Advance.]*

---

## Slide 7 — Stage 4: Implement (Setup + Build)

*[~6 minutes including clip. This is where most of your TA work happens, so spend time.]*

> OK, Stage 4. Implement. This is where AI actually writes code.
>
> But first — and this is the part you need to be ready for — there's the scariest 10 minutes of the entire session. **Vertex AI setup.**
>
> Setting up the AI account, getting an API key, configuring the project ID and region — for first-timers, this is terrifying. They see a Google Cloud console, they see fields asking for things they've never heard of, and they think they're going to break something.
>
> They're not. But they don't know that.
>
> Here's your setup protocol. *[Walk through the numbered list.]*
>
> Step 1, walk them through the tool install. Step 2, create the API key — and *verify it works* with one test prompt before moving on. Don't trust that it's set up just because they got through the menu. Step 3, configure Vertex AI — Project ID, region, model. Step 4 — and this is the important one — **if they're truly stuck past 10 minutes, take the keyboard.**
>
> This is the **one exception** to the rule I told you about at the start. Everywhere else in the workshop, you don't type for them. Here, you do. Setup is the one place.
>
> Here's the phrase I want you to actually say out loud, to the participant, when you take the keyboard:
>
> *"I know this looks scary — we're just copying numbers over so the AI can do the real work for you."*
>
> Say that. It frames the setup as not-the-real-work. It tells the participant the magical part is still ahead. And it lets you do the boring config without making them feel like they failed.
>
> Let me show you the setup.

*[**PLAY CLIP 4 — Vertex AI setup and AI building.**]*

> A couple of things to watch for during setup. *[Read tip at bottom of left panel.]* Participants who are stuck on setup go silent. They don't ask for help. They just close their laptop lid a little, or they're scrolling around the site looking lost, or they're frowning at a config screen.
>
> **Setup eats build time silently.** Someone who loses 15 minutes to setup has 30 minutes to build instead of 45. Walk the room aggressively in the first 20 minutes.
>
> Now — once setup is done, AI starts building. **The rules flip.**
>
> *[Point to the green TA panel on the right.]* This is where the rule from the start of training comes back. Build phase, you don't type for them.
>
> When someone says "Can you just type this for me?" — the response is: *"I'd love to, but it'd rob you of the part you'll be most proud of. What do you want to tell the AI?"*
>
> When you don't know the tech they're working with — and you won't sometimes — the move is: *"I don't know. Let's ask Claude. What would you type?"*
>
> Notice both responses. They're both questions. Not answers.
>
> Setup phase: you can type for them if stuck. Build phase: you ask the next question. Different rules, same session. The rule flip happens the moment they've got a working environment.

*[Pause. "Questions on Implement?" Then advance.]*

---

## Slide 8 — Stage 5: Write & Run Tests (THE NEW STAGE)

*[~7 minutes including clip. This is the brand-new stage — spend extra time on it. Returning TAs especially need to hear this since it didn't exist in v6.]*

> OK. Stage 5. This is the new one. **Write and run tests.**
>
> Returning TAs — this is the biggest change since last cohort. So pay attention even if the other stages feel familiar.
>
> Here's the principle, in one sentence: **tests are the gate.** Before a human verifies anything visually, tests run first. If tests pass, the human takes over. If tests fail and AI can't fix them in three tries, we stop and figure out why.
>
> Now — this stage uses two halves that combine. *[Point to the left panel.]*
>
> **Half 1 — the methodology.** This lives in the `test-driven-dev` skill on GitHub. The skill defines: how to write tests, the auto-loop where AI runs them and fixes failures, the maximum of three iterations before stopping, the stack defaults — pytest for Python, Jest or Vitest for Node and React — and the regression rule, which we'll come back to in Stage 6.
>
> The skill is universal. Every project applies the same methodology.
>
> **Half 2 — the plan.** This lives in `engineering.md`, in the "Testing strategy" section AI wrote back in Stage 2. The plan is project-specific: which functions in *this* app need unit tests, which user flow needs an integration test, what's deliberately not being tested.
>
> The plan is specific. Every project has its own.
>
> The skill executes the plan. *[Point to the prompt.]* Participants prompt AI:
>
> *"Apply the test-driven-dev skill from [GitHub link]. Use the Testing strategy in engineering.md as the plan."*
>
> AI loads the skill, reads the plan, writes tests, runs them. If they pass — *[trace the down-arrow]* — gate cleared, hand off to human verification in Stage 6. If they fail, AI fixes the code and re-runs. Up to three times. After three failed iterations, AI stops and reports what's broken.
>
> Why three? Because if AI can't fix it in three tries, the problem usually isn't the code — it's the spec. The testing strategy is asking for something the implementation can't reasonably provide, or the spec itself is unclear. So we stop and update the doc, not the code.
>
> Let me show you what this looks like.

*[**PLAY CLIP 5 — TDD stage. AI applying the skill, writing tests, running them, fixing one failure, succeeding.**]*

> Did you see the loop? AI wrote a few tests. Ran them. One failed. AI looked at the failure, fixed the code, re-ran. All green. Then it told me what passed and what didn't, and handed it off for visual checking.
>
> That whole thing happened without me touching the code. I just applied the skill and let AI work the loop.
>
> Now — *[point to the right TA Role panel]* — here's your job at this stage.
>
> First, **make sure the skill is applied.** Quick check: walk by and ask, "Have you pasted the test-driven-dev skill link to AI yet?" If they haven't, the GitHub URL you bookmarked in pre-session — paste it now.
>
> Second, **watch for generic tests.** If AI is testing every random function with no priorities, that's a sign the engineering doc is missing a real testing strategy. Send them back to update `engineering.md` first, then re-apply the skill.
>
> Third — and this is the big one — **when the cap is hit, send them back to the spec.** If AI tried three times and tests are still failing, don't help them debug the code. The coaching prompt is: *"AI stopped after three tries. Pull up engineering.md — is the testing strategy realistic for what got built? Update the doc, then re-apply the skill."*
>
> Notice the move — same as the "oops" loop from Stage 3. When something downstream isn't working, you fix the doc, not the artifact.
>
> Fourth — *[emphasize]* — **don't let them skip tests "to save time."** Some participants will push back. "I just want to see if my app works, can I skip the tests?" The answer is no. Tests are saving them time — they catch the dumb stuff in 30 seconds. If they skip tests, the dumb stuff hits them in Stage 6 and we spend three minutes troubleshooting instead.
>
> Gently say: *"Let's run the tests first — it'll catch the obvious stuff in 30 seconds."* If they still resist, say: *"Trust me on this one."* Then move on. Don't argue.
>
> The big point — *[point to the "Tests are the gate" line on the right]* — **human verification doesn't begin until tests pass.** That's the discipline. AI catches the dumb stuff so humans only have to catch the interesting stuff.

*[Pause. "Questions on the TDD stage? This is the big new thing — happy to slow down." Then advance.]*

---

## Slide 9 — Stage 6: Verify (the Human Pass)

*[~5 minutes including clip. The methodology here was Stage 5 in v6 — same content, just bumped one number because of TDD insertion.]*

> Stage 6. Verify — by the human.
>
> The setup: tests passed. App is running. AI has handed off the build. Now the human pulls up the app and checks the UI.
>
> Here's what humans catch that tests miss. Tests catch: wrong return values, broken function calls, missing imports, off-by-one errors. The dumb stuff. Humans catch: "this color is ugly," "this button is in the wrong place," "this animation is annoying," "the copy doesn't sound right." The taste stuff. The UX stuff.
>
> So this stage is about catching what tests can't see.
>
> The methodology is the same as troubleshooting in v6 — observe, expect, fix. *[Point to the green numbered list.]*
>
> One — **what you observed.** Paste the actual log. Screenshot the actual UI. Don't summarize.
>
> Two — **what you expected.** Describe what should have happened.
>
> Three — **ask for the fix.** Let AI propose. Then verify it actually works before moving on.
>
> The script — *[read the green quote]* — *"Here's the error I got. Here's what I expected. What's wrong?"*
>
> Observe, expect, ask. Then verify. Same loop.

*[**PLAY CLIP 6 — Human verification. Catching a visual bug, applying the loop.**]*

> Now — *[point firmly to the regression rule callout]* — here's where Stage 6 connects back to Stage 5. **The regression rule.** This comes from the test-driven-dev skill.
>
> When the human catches a bug here — a real bug that tests missed — the next move is **not** to just fix the code. Coach them like this:
>
> *"That bug suggests we're missing a test. Write a test that catches this case — it should fail right now — then fix the code so the test passes."*
>
> This turns every human-caught bug into a regression test. The test suite gets stronger over time. Next time AI builds something similar, that test catches the same class of bug automatically.
>
> The pattern is: bugs found here flow *back* to Stage 5. *[Trace the arrow.]* Every human-caught bug becomes a new test.
>
> Why does this matter? Because if you just fix the code without writing a test, the bug can come back. Next session, next pivot, AI regenerates code, same bug returns. With a regression test, the bug literally cannot return — the test will fail.
>
> This is real engineering. We're not just shipping a working app — we're shipping a working app *with a test suite that defends it*. That's what real teams do.
>
> Talk to AI like a teammate. Share the evidence, share the intent. And when you catch something — write a test for it.

*[Pause briefly. Advance.]*

---

## Slide 10 — Troubleshooting Toolkit

*[~5 minutes. No clip. Reference material. Walk through the table.]*

> Same Stage 6, but now the practical toolkit. This slide is the specific patterns you'll see every session.
>
> First — *[point to top panel]* — when you start the app, **run it manually in the terminal.** Don't let the tool auto-run it. Why? Because when you run it manually, the logs are visible. Logs visible equals troubleshooting input.
>
> Tell your participants to open a terminal, paste the run command, and run it themselves. They might not understand what they're doing the first time. Doesn't matter. They'll see logs.
>
> Now — *[point to the evidence panel]* — what counts as "evidence" for the loop. AI handles these well: terminal logs (paste the whole thing, not a summary), screenshots of the broken UI, network tab errors from browser dev tools, and the exact prompt-and-response pair that came back wrong.
>
> If they screenshot the UI, AI can read the screenshot. If they paste a stack trace, AI can read the stack trace. The more evidence, the better the fix.
>
> Now the patterns. *[Walk down the symptom/prompt table.]*
>
> **Port conflict.** This happens every session. Multiple participants, all on port 3000, conflict. Don't explain network ports — coach them to ask AI: *"Port 3000 is in use. Change the config to 3001."* AI fixes it. Done.
>
> **Module not found.** Paste the error, ask AI what package they need to install.
>
> **Auth failure.** Walk through the API key setup again, step by step. Usually they missed a step.
>
> **UI doesn't match the spec.** Pull up `ui.md`, ask AI: "Does the rendered UI match this doc?" That's a great moment because it teaches them the docs are *checkable*.
>
> Two new rows in v7.1 — *[point to the green rows at the bottom of the table]* — and these are TDD-specific.
>
> **Test failure past three tries.** AI's auto-loop hit the cap. Don't just keep trying. Coach: *"Pull up engineering.md. Ask AI: 'Why might my testing strategy be unrealistic for the current code? Suggest updates.'"* Send them back to the spec.
>
> **AI wrote tests but didn't run them.** This means the skill wasn't loaded properly. The skill explicitly requires running, not just writing. Coach: *"Re-apply the test-driven-dev skill — paste the GitHub link again. The skill requires running the tests."*
>
> Memorize these. Port conflict especially. Test cap hits — those will happen too once participants get into harder builds.
>
> Last thing — *[point to README reminder on the right]* — once the app works, **before any polishing**, coach them to write a README. The prompt is: *"The app is working. Create a README.md that explains how I install and run this next time."*
>
> Verify the file exists.
>
> Why does this matter? Because the participant might want to come back to this on Tuesday night, three weeks from now, and they'll have forgotten everything. A spec plus tests plus a README means they have a real project they can return to.
>
> Three files — `engineering.md` (with testing strategy), the test suite itself, and `README.md` — equals a real project. That's the takeaway.

*[Pause. "Anything on troubleshooting?" Advance.]*

---

## Slide 11 — Stage 7: Pivot or Expand

*[~5 minutes including clip. Same as v6 Stage 6, with TDD integration.]*

> Stage 7. Pivot or expand. This is what fast finishers do — or what someone does when they don't like what they built.
>
> Two paths, same methodology. *[Point to the two cards.]*
>
> **Path A — Expand.** They have a good foundation, they want to add a feature. Brainstorm with AI, pick one feature, expand. They regenerate `product.md` and `ui.md`, and they update the **Testing strategy section** of `engineering.md` so it includes tests for the new feature. They usually keep the rest of `engineering.md` because the underlying structure is fine.
>
> Then — and this is critical — they **re-apply the test-driven-dev skill.** AI generates new tests for the new feature, runs them, auto-fixes if needed.
>
> **Path B — Pivot.** They don't like the prototype. They want to change direction. Same flow, but expect more of `engineering.md` to change — including bigger changes to the testing strategy. Old tests get deleted, new ones replace them, because the underlying behavior is changing.
>
> Re-apply the skill — same prompt as Stage 5. The skill generates fresh tests against the new strategy.
>
> Here's the sentence on this slide I want to land — *[point to the blue quote]* — **pivot from code is pain. Pivot from spec plus tests plus skill is clean.**
>
> If a participant has been building for 45 minutes and they decide they don't like what they have, and they try to pivot by editing code — they're going to hate their life. The code's a mess, they're going to keep finding little pieces of the old direction sticking out. And their tests still test the *old* behavior, which makes everything noisier.
>
> But if they pivot by regenerating the design docs first — including testing strategy — and then re-applying the skill so tests regenerate, then asking AI to rebuild — it's clean. AI starts fresh from the updated plan, new tests defend the new behavior.
>
> This is the payoff for everything we set up back in Stages 2 and 5. Three saved docs, one applied skill — together, that's a reusable pivot machine. We told them in Stage 2 these would matter when they pivot. This is when we come back to them.

*[**PLAY CLIP 7 — Pivot flow with test regeneration.**]*

> Notice the order in the clip. I brainstormed features with AI first. I picked one. I regenerated `product.md` and `ui.md`. I updated the testing strategy in `engineering.md`. I reviewed the new plan. I approved it. *Then* I re-applied the test-driven-dev skill — AI generated new tests. *Then* AI rebuilt. Tests passed. *Then* I verified.
>
> Same sequence as Stage 2 through 6, just with regenerated content. The lifecycle is fractal — pivot is just running the whole thing again from the docs.
>
> Your TA role here — *[point to green panel]* — when fast finishers go idle and start draining the room's energy, point them at this stage immediately. The coaching prompt is: *"What feature do you want next? Update the design docs first."*
>
> Then immediately after they update the docs, the follow-up: *"Did you re-apply the test-driven-dev skill? The plan changed, so the tests need to change too."*
>
> Notice — both questions. Not answers. You're not suggesting a feature. You're not writing tests for them. You're asking them what they want, then reminding them of the discipline.
>
> Ask the next question. Don't answer it.

*[Advance.]*

---

## Slide 12 — Stage 8: Polish (and Skills Apply Anywhere)

*[~5 minutes including clip.]*

> Stage 8. Polish. And while we're here, we're going to talk about skills more broadly.
>
> First the polish part. **Polish is iterative, not terminal.** It's not a finish line. It's a loop. Change a color, see what it looks like, change it again. Adjust some text, regenerate, adjust again.
>
> Tell participants this explicitly — polish is never done. Set a timer if you have to.
>
> Now the trick. *[Point to the red panel on the left.]* The way you polish is you point AI at a skill repo on GitHub. Just like we did in Stage 5 — but for design instead of tests.
>
> A "skill" is a reusable set of instructions stored on GitHub. The prompt is something like: *"Read this skill from [GitHub link] and apply it to my UI."* AI fetches the skill, reads it, applies it to your code.
>
> Then you iterate the same way as troubleshooting. *"Change this color to teal."* *"The hero text should be bigger."* Same observe-expect-fix loop, just applied to design instead of bugs.

*[**PLAY CLIP 8 — Applying a design skill from GitHub.**]*

> Did you notice — same loop. I observed something I didn't like. I told AI what I expected instead. AI proposed the change. I verified. If I still didn't like it, I went around again.
>
> The methodology you taught them in Stage 6 just got reused for design. That's the lesson.
>
> Now the bigger point. *[Point to the rainbow panel on the right.]* **Skills aren't just for polish.** That table shows skills applied at every stage.
>
> Look at the right column — "REQUIRED?" — most rows say "—" (optional). Only one row says **★ REQUIRED**. That's `test-driven-dev`. Every other skill in this table — prompting, doc-template, code-style, debugging, design system — those are all *optional*. Apply them when they help. Skip them when they don't.
>
> The TDD skill is different. It's required for every build, because it's not about *this* app — it's about the *discipline*. Without the TDD skill, Stage 5 doesn't happen. Tests don't run. The gate doesn't exist.
>
> So when you talk to participants about skills, here's the message: "Skills are a cross-cutting tool. You can apply one at any stage if it helps. There's one you have to apply — `test-driven-dev` — because it's the gate. The rest are tools you reach for when useful."
>
> The TA role here — *[brief gesture]* — late finishers who are panicking, MMV is the win, skip polish. Fast finishers who are bored, polish and skills are for them. Either way, TDD is non-negotiable.

*[Pause. Advance.]*

---

## Slide 13 — Scout the Share-Out

*[~2 minutes. No clip. Set the emotional close.]*

> OK, last five minutes of build phase. This is share-out scouting. This is the easiest job in the workshop and the most important one.
>
> Walk the room and look for delightful results. Even messy ones. Especially messy ones.
>
> *[Point to the quote.]* The line is: *"Yours is so good — would you share?"*
>
> Some participants will share without prompting. Most won't. Some are scared to share, especially in their first session. Some don't realize what they built is impressive.
>
> Your job is to scout, to find the moments worth sharing, and to nudge the quiet ones.
>
> A shy participant sharing their messy-but-magical app is a workshop-defining moment. People remember those. They tell their friends. They come back. They bring their coworkers.
>
> So scout actively. Find at least two or three people you'd want to share before the build phase ends. Tell them gently, individually, before the share-out — "I'd love it if you'd share yours, would that be OK?"
>
> Don't surprise them. Ask. They'll usually say yes.

*[Advance.]*

---

## Slide 14 — The Whole Lifecycle, One More Time

*[~3 minutes. Closing recap. Bring it home.]*

> OK, we're at the end. Let me bring it together.
>
> *[Point to the cheat sheet on the left.]* One stage, one move. That's the whole job.
>
> **Spec Talk** — make sure they nail Q1. Skip optional questions if they freeze. Never run the Spec Talk for them.
>
> **Artifacts** — verify the three files actually saved to disk. **Check `engineering.md` has a Testing strategy section.**
>
> **Review** — fix the doc first, not the code.
>
> **Implement** — setup is the one place you type for them if they're stuck past 10 minutes. Build, you never type.
>
> **Tests** — *[emphasize]* — **make them apply the `test-driven-dev` skill. Don't let them skip it.** This is the one new discipline since last cohort.
>
> **Verify** — observe, expect, fix, taught out loud while you walk the room. **Human-caught bugs become new tests.**
>
> **Troubleshoot** — memorize the symptom-prompt table on slide 10. Port conflict happens every session. Test cap hits — send back to the spec.
>
> **Pivot** — regenerate the design docs including testing strategy, re-apply the skill, then rebuild. Not the code.
>
> **Polish** — iterate. Don't treat it as done.
>
> **Skills** — most are optional. **TDD is the one required skill.**
>
> *[Pause. Point to the right panel.]* And one sentence to take home.
>
> **Remove friction. Don't fix code.**
>
> If you're typing on their keyboard, you're stealing the moment they'll be most proud of. The one exception is setup. Everywhere else — you ask the next question. You don't answer it.
>
> That sentence — *"ask the next question, don't answer it"* — is the entire job. Everything else on this cheat sheet is a special case of that.
>
> You're not here to be the expert. You're here to model how a builder thinks with AI in front of a beginner. When you don't know something, you turn to AI. When they're stuck, you ask them what they want, you don't tell them. When tests fail, you point them at the spec, not the code.
>
> Welcome to the team. Let's go make some builders.

*[Pause. Open for final questions.]*

---

## Final Q&A (5-10 min)

**Likely questions and quick answers:**

> **"What if a participant gets really frustrated and wants to quit?"**
>
> Reframe to MMV. Help them land one working output — even uglier is fine — with tests passing. Shipping beats perfecting. If they ship anything with green tests, they win.

> **"What if I genuinely don't know an answer?"**
>
> Turn to AI in front of them. That's actually the *best* moment in the workshop — they get to see you do exactly what we're teaching them. "I don't know. Let's ask Claude. What would you type?"

> **"What about participants way ahead of everyone else?"**
>
> Stage 7. Pivot or expand. Point them there immediately. Don't let fast finishers go idle — idle fast finishers drain the room's energy faster than late builders do. Remind them to regenerate tests, not just code.

> **"What if I disagree with a participant's idea?"**
>
> Doesn't matter. Their idea, their app. Even if you think it's a bad idea. The workshop teaches the methodology — the idea is just the vehicle. If their bad idea gets them through the loop, they learned the loop.

> **"How do I handle multiple stuck participants at once?"**
>
> Triage by stage. Setup-stuck people get priority — they're hemorrhaging build time. Build-stuck and test-stuck people are still working. Verify-stuck people are usually one observe-expect-fix loop away from working. Test-cap-hit people need to go back to the spec — that's the easiest redirect.

> **"What if a participant insists on skipping the TDD stage?"**
>
> Push back once gently: *"Tests catch the dumb stuff in 30 seconds — let's run them."* If they still resist, escalate to: *"Trust me on this one — we built the workshop around this for a reason."* Then move on; don't argue further. If they truly refuse, let them — but don't be surprised when they hit weird bugs in Stage 6 that tests would have caught.

> **"What if AI keeps failing the auto-loop at three tries?"**
>
> Almost always means the spec is wrong, not the code. Pull up `engineering.md`, look at the testing strategy section, ask: "Is what we're asking AI to test something the implementation can reasonably support?" Usually the answer is no — the strategy assumed behavior that isn't actually there. Update the doc, re-apply the skill.
