# Debugging

> Debugging is *applied epistemology*: figuring out what's actually true in a system that's misbehaving, against your wrong assumption about what should be true. It is the most teachable, most under-taught skill in engineering, and AI changes how you do it without changing the underlying discipline.

---

## Purpose

You can take a failing system — a flaky test, a production incident, an obscure bug, an AI-feature regression — and methodically narrow the search space until you find the actual cause and verify the actual fix. You don't guess, you don't cargo-cult, and you don't stop at "well, it works now."

---

## Why it matters in an AI-first org

- **AI generates more code, and faster.** Some of it is subtly wrong. The bug surface is bigger.
- **Models confidently suggest fixes.** Plausible-but-wrong fixes that compile, pass tests, and shift the bug elsewhere are now common. Debugging discipline is what catches them.
- **AI is a great assistant in debugging** — *if* you bring the discipline. Without it, you'll be misled faster than you would alone.

---

## The practice

### The mindset

- **The system is correct; your model of it is wrong.** Find where they disagree.
- **Suspect the new thing.** What changed? Time the bug appeared maps to what was deployed, merged, configured.
- **Suspect *your* code before the framework, OS, or hardware.** Right ~99% of the time.
- **Read the error message. All of it. Twice.** Including the stack trace. Most "this error is useless" claims dissolve under careful reading.
- **Reproduce before you fix.** A bug you can't reproduce is a bug you can't verify you fixed.

### The method

1. **State the bug precisely.** "Sometimes it's slow" is not a bug. "p99 latency on `/checkout` jumped from 200ms to 1.8s starting at 14:02 UTC on May 17" is a bug.
2. **Form a hypothesis.** What do you think is happening? Make it falsifiable.
3. **Design the smallest experiment** that would refute it. Log, instrument, bisect, isolate.
4. **Run the experiment. Look at the data.** Not the answer you expected — the actual data.
5. **Update the hypothesis.** Repeat until you find the cause.
6. **Verify the fix actually fixes the cause** — not just the symptom. Roll the fix forward and confirm the experiment now shows what the fix predicts.
7. **Write the cause and fix down.** In the PR, the postmortem, your notes. Someone (often you) will see this bug again.

### Powerful techniques

- **Bisect.** Git bisect for code. Binary search for inputs. Halving the search space repeatedly is the most reliable debugging move there is.
- **Print / log generously, delete carefully.** When you don't know what's true, instrument the system to tell you.
- **Read the code, not the docs.** Docs lie or lag; code is the ground truth.
- **Compare working vs broken.** Diff the state, the config, the inputs. The difference is the cause or near it.
- **Rubber-duck.** Explain the problem out loud to a duck / a colleague / yourself in writing. ~30% of bugs are found in the explanation.
- **Walk away.** For hard bugs, 20 minutes away beats 2 more hours of staring. Real, repeatedly observed.
- **Read the database / queue / cache state.** Where the system disagrees with the code is often in the data, not the code.

### Working with AI on debugging

- **Use AI to enumerate hypotheses** — "what would cause symptom X in stack Y?" — and then test each yourself.
- **Use AI to explain unfamiliar code** before you change it.
- **Don't accept fix-suggestions without proving the root cause.** AI is happy to suggest a patch that hides the symptom and leaves the cause; you'll meet it again next quarter.
- **Be skeptical of "this is a known issue with X."** Sometimes true. Often hallucinated. Verify.
- **Paste full error context, not just the message.** Stack trace, surrounding code, recent changes. The quality of the help scales with the quality of the input.

---

## Drills

- **Daily — the hypothesis log.** When debugging, write down each hypothesis and what would refute it. Look at the log at end-of-day. Notice patterns in which hypotheses you keep wasting time on.
- **Weekly — bisect a real bug.** Even when you "kind of know" the cause. Practices the muscle.
- **Weekly — read a stack trace fully.** Pick the most intimidating one of the week. Walk it line by line.
- **Monthly — the postmortem read.** Read 2–3 postmortems from your org or public ones (Cloudflare, GitHub, AWS publish detailed ones). Each is a free debugging masterclass.
- **For AI-feature bugs:** maintain an eval suite that includes the bug you just fixed ([quality-engineering.md](../docs/quality-engineering.md), [ai-feature-eval-template.md](../templates/ai-feature-eval-template.md)). Regression once is a bug; regression twice is a process failure.

---

## Common failure modes

- **Cargo-cult fixes.** Stack Overflow / AI suggested it, it made the symptom go away, you don't know why. You will meet this bug again — or worse, a related one — in production.
- **Symptom over cause.** Wrapping the call in a retry / try-catch / increased timeout. Hides the bug, doesn't fix it.
- **Guess-and-check coding.** Changing things without a hypothesis until something works. Burns hours and teaches you nothing.
- **Stopping at "it works now."** You don't know it's fixed; you know the test passes. Verify the cause.
- **Ignoring the timestamps.** When did it start? What deployed at that time? This question solves an enormous share of production bugs in under a minute.
- **Pride of theory.** "It can't be that." It usually can be that. Test it.
- **Asking AI for the fix without giving it the cause.** Get suggestions; verify yourself; ship your understanding, not the model's.
- **Not writing it down.** The bug, the hypothesis path, the fix. You will see this pattern again and will have forgotten the lesson.

---

## Tune for your context

- **Production incidents:** debugging discipline collides with time pressure; see [incident-response.md](incident-response.md). Mitigate first, debug deeply after.
- **Distributed systems:** instrumentation, tracing, and structured logs become disproportionately important; invest in them as a permanent capability ([developer-experience.md](../docs/developer-experience.md)).
- **AI/ML systems:** evals are your debugger; without them, "the model got worse" is a feeling, not a finding.
- **Junior-heavy teams:** explicitly teach the method; do not assume it's intuitive. It isn't.
- **Heavy-AI-codegen contexts:** invest in the AI-specific failure-mode checklist; suspect plausible-looking code that you didn't write.

---

## Further reading

- **David J. Agans** — *Debugging: The 9 Indispensable Rules* — the canonical short book. Read once a year.
- **John Regehr** — [Use of Assertions](https://blog.regehr.org/archives/1091) and broader writing — debugging through invariants.
- **Brian Kernighan & Rob Pike** — *The Practice of Programming*, debugging chapter — terse and excellent.
- **Julia Evans** — [jvns.ca](https://jvns.ca/) — accessible, deeply practical writing on debugging tools and methods.
- **Cloudflare, GitHub, AWS** — published incident postmortems; case studies in debugging at scale.
- **Charity Majors** — observability writing on [charity.wtf](https://charity.wtf/) — debugging production through high-cardinality data, not log-grepping.
