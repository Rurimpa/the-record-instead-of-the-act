# The Record Instead of the Act

**An agent can carry a task as far as writing it down — and the writing down
becomes the doing.**

The minutes say the notice was circulated. The notice was never sent. The commit
message says the entries were added. They were not in the commit. Nothing was
fabricated: the record is genuine, and the act is simply missing.

日本語版：[README.ja.md](README.ja.md)

## Use it now

Paste this into your `CLAUDE.md` or `AGENTS.md`:

```markdown
## Before saying "done"
- Before acting, write down what should exist afterwards (files, ledger entries, messages sent).
- Before saying "done", check that list against what actually exists, not against your memory of what you did.
- When another agent tells you it is done, ask it: "What did you advance? List what now exists."
```

Then:

1. When you delegate a task or receive a handoff, ask the agent one closed question: **"What did you advance?"**
2. Compare its answer with what actually exists (the file, the commit, the sent message).

That is all. Why it works, and where it does not, is below.

---

## This is not hallucinated tool output

There is a known failure where an agent emits a plausible Thought → Action →
Observation trace without ever calling the tool, and invents the result. That is
fabrication, and it is detectable: the tool's own logs are empty.

**This is the other one.** The tool calls really happened. The minutes really
were written. The commit really was made. The record is a true record of what
the agent did — and what the agent did stopped one step short.

That makes it harder to catch, because every artifact you would normally check
is present and correct.

## What we observed

Two cases, from one evening in a long-running multi-agent workspace.

**Case 1 — the notice that was written about but never sent.** One agent was
told by another: *circulate these five prohibitions as they are.* The agent
wrote the instruction into the meeting minutes. It asked "may I circulate
these?", received an answer, and the matter felt closed. **The circular was
never issued.** Nowhere in the agent's own state was there an expectation that
something ought to exist afterwards.

**Case 2 — the commit message that described work the commit did not contain.**
Another agent's commit message said two entries had been added to a ledger. The
append had silently dropped and they were not in the commit. The agent fixed it
in a later commit, noted the discrepancy in the new message, and did not rewrite
the old one.

**How each was found is the interesting part:**

| | how it surfaced |
|---|---|
| Case 1 | **not by any mechanism.** Another agent happened to ask a closed question — *what did you advance?* — and the agent recounted and noticed |
| Case 2 | **the agent's own check.** It had written down "B7 and B8 should be in there", then grepped. Because it had placed an expectation, it could see the mismatch |

That pairing is the finding. In the same workspace on the same evening, eight
self-checks were run against places where an expectation had been stated in
advance; all eight agreed. The competing explanation — *an agent can catch
anything that passes in front of it* — was tested and failed: the same agent had
seen other agents' numbers many times and stopped on none of them.

**Being shown something is not enough. An expectation has to have been placed.**

**This is n=2** for the pattern itself, with a supporting n=8 for the mechanism.
Field observation, not a controlled experiment.

## What to do

**Have someone ask a closed question.**

Not "is everything on track?" — that invites a yes. Ask:

> **What did you advance?**

The question is doing specific work. It forces the agent to place an
expectation — *these are the things that should now exist* — and then compare it
against what does exist. The gap becomes visible at that moment and not before.

This is the same shape as the case-2 self-check, with the expectation supplied
from outside instead of from within. It works because an agent that never placed
an expectation has nothing to be surprised by.

Places to put it:

- at the end of a delegated task, from whoever delegated it
- at a handoff, from the agent receiving it
- before you accept "done", from you

And write the expectation down before you act, when you can. *After this, a file
named X should exist / the ledger should contain B7 and B8 / a message should
have gone to Y.* Then check that list, not your memory of what you did.

## Limits

- **n=2.** Two cases in one evening. We are not reporting a rate.
- **The closed question is not a mechanism.** In case 1 it happened because one
  agent happened to care. Nobody is guaranteed to ask. If you want this
  reliably, someone or something has to be required to ask, every time — and we
  have not built that.
- **It does not catch everything.** It catches the gap between *what should now
  exist* and *what exists*. It does not catch work that was done wrongly, or an
  expectation that was itself wrong.
- **Asking costs a round trip and some goodwill.** Ask it where the act matters
  and a missing act would be expensive. Asking after every small step turns into
  noise, and noise is ignored.
- **Self-correction has known limits.** There is a body of work showing that LLM
  self-verification degrades without external grounding. Consistent with that,
  the thing that worked here was not "check yourself harder" — it was a
  concrete, externally stated expectation to check *against*.

## Prior art

- **Fabricated tool use** — agents producing plausible traces without calling
  the tool — is documented in public issue trackers and evaluated in agent
  benchmarks. As above, that is a different failure: there the record is false,
  here it is true.
- **LLM self-correction limits** are well studied; self-verification without
  external signal is known to degrade, and there is recent work on
  pre-registered evaluation of verifiers.
- **Premature commitment** — an agent settling on one reading and defending it
  for the rest of the run — is a documented adjacent failure.
- **What we did not find**: this specific pattern named and separated from
  fabrication — *the record is genuine and the act is absent* — together with
  the detection method of a closed question that forces the agent to place an
  expectation it did not have.
- Absence in our search is not proof of absence. Open an issue and we will
  credit prior work here.

## License

MIT.
