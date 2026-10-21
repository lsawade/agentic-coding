# Slide accuracy and content review

Reviewed 21 October 2026. Scope: all 34 slides in `slides.md`, their speaker notes, and the text in the referenced SVG diagrams. This is a content review, not a rendered layout review. The deck has not been modified.

The supervision theme is useful for a research audience. The most important corrections concern institutional data rules, scientific validation, context billing, and the limits of Git. Several dated headline numbers check out. Other statements need narrower wording rather than different numbers.

## Corrections to prioritize

### 1. Local models do not automatically make restricted data permissible

**Slides 5, 17, 30 and 32.** See `slides.md:124`, `slides.md:491`, `slides.md:886`, `slides.md:928`, and `assets/diagrams/data-boundary.svg`.

The deck says restricted data can stay on the cluster and recommends local/open-weight models for PII, IRB data and unpublished results. This combines different information classes and implies that local execution provides authorization.

Princeton OIT's current guidance says Restricted University Information must not be used with any AI tool. Internal and Confidential information require University-licensed tools. Thus both blanket statements in the deck need changing: some nonpublic information may be permitted in approved hosted tools, while moving Restricted information to a local model does not establish permission. IRB and other project-specific restrictions also need separate review.

**Suggested slide wording:** “Check the data classification and approved tool before use. Local deployment does not replace institutional or project approval.”

Replace the discussion question with: “Which AI tools are approved for your dataset's classification?” Replace the slide 5 benefit with “Control where inference runs, when policy permits.” Revise the diagram too: neither code nor an ‘anonymized summary’ is automatically cleared for sharing.

Sources: [OIT guidance, FAQ](https://oit.princeton.edu/services/ai-guidance-tools), [OIT policy](https://oit.princeton.edu/about/policies/generative-ai-tools-use-policy).

### 2. Git protects recorded file history, not every agent action

**Slide 22**, `slides.md:653–667`, and `assets/diagrams/git-worktrees.svg`.

“Any agent change is one git checkout from undone” is false. Git does not undo database writes, network actions, leaked credentials, deleted untracked data or consumed compute. Bare `git checkout` is also not an undo command. Worktrees separate working directories but share a repository and do not provide a security boundary. “The worst it can break is its own branch” is unsupported without much stronger isolation.

**Suggested wording:** “Commit a known-good baseline. Review diffs and revert unwanted commits. Use a sandbox and limited credentials to contain actions outside Git.”

If showing commands, distinguish `git revert <commit>` for a recorded commit from deliberately discarding selected uncommitted changes with `git restore`. Avoid presenting a destructive discard as a universal undo.

Sources: [Git worktrees](https://git-scm.com/docs/git-worktree), [Git revert](https://git-scm.com/docs/git-revert).

### 3. The bug exercise contains a second analysis error

**Slides 14–15**, `slides.md:369–432`.

The `dropna()` criticism is correct: with its default arguments, it removes rows with a missing value in any loaded column. But `s.diff().mean()` also fails as a general estimator of warming per calendar year. It telescopes to `(last_mean - first_mean) / (number_of_observed_years - 1)`. It ignores gaps between years and is not generally a fitted trend through all annual observations.

A small numerical check: years `[2000, 2001, 2010]` with temperatures `[0, 0.1, 1.0]` give mean adjacent differences of `0.5`, while the slope against calendar year is `0.1` degrees/year. That difference persists after fixing `dropna()`.

**Suggested change:** either remove the trend calculation and make the exercise solely about annual means, or say “Find the analysis errors” and discuss both. For a trend example, specify coverage requirements and fit against actual years, with an uncertainty treatment appropriate to the data. An ordinary fitted slope alone does not solve missingness or sampling bias.

Also change the notes' assertion that sensor failures make the result shift warm. Without the dataset or a supporting source, that direction is hypothetical. Say: “If missingness depends on weather conditions, filtering can bias means and trends. The direction depends on which observations are missing.” Dropping only missing temperatures addresses the demonstrated filtering error, not all sampling problems.

Source: [pandas `dropna`](https://pandas.pydata.org/docs/reference/api/pandas.DataFrame.dropna.html). The trend counterexample above was calculated independently during this review.

### 4. Context reuse does not mean full-price input billing on every step

**Slide 9**, especially `slides.md:218–221`, and `assets/diagrams/context-bloat.svg`.

“Everything in the window is paid for again on each step” needs a caching caveat. Prior conversation can remain part of the effective input, but repeated prefixes can receive cache-hit rates. Harnesses can also compact or omit earlier content. A fresh session can lose useful context and an existing cache, so “cheaper and smarter” is not a guarantee.

**Suggested wording:** “Long sessions accumulate context. Cached input can be cheaper, but repeated tool output and failed attempts still consume context. Compact or restart with a verified handoff when the session loses direction.”

Keep the schematic label visible. The current arrow implies a measured optimum restart point that the figure does not establish.

Sources: [Claude Code caching](https://code.claude.com/docs/en/prompt-caching), [Anthropic pricing](https://platform.claude.com/docs/en/about-claude/pricing).

### 5. Open weights remove a vendor charge, not inference cost

**Slide 5**, `slides.md:125`.

“Per-token cost disappears” is misleading. Self-hosting incurs GPU, energy, operations and opportunity costs, even if the researcher does not receive a token invoice. Open-weight models can also run on paid hosted endpoints. Weight availability, hosting location and license permissions are separate properties.

**Suggested wording:** “Self-hosting replaces API token charges with compute and operations costs.” Add a note to check the model license and realistic hardware requirements before proposing local deployment.

### 6. OpenRouter usage rankings are not a quality ranking

**Slide 6**, `slides.md:149–157`.

OpenRouter's main rankings measure token volume routed through its platform. It also exposes benchmark views, but the usage ranking cannot substitute for a capability evaluation. “Benchmarks are saturated” is too broad, and a live leaderboard can itself be a benchmark leaderboard.

**Suggested wording:** “Use task-relevant evaluations and a few representative tasks from your own work. Treat usage rankings as adoption signals.”

Source: [OpenRouter rankings and methodology](https://openrouter.ai/rankings).

### 7. Tool access is not the same as enforced read-only behavior

**Slide 10**, `slides.md:240–264`.

The shown `tools: Bash, Read, Grep` configuration permits a shell. The instruction “Do not fix anything” expresses intent but does not prevent shell writes or other side effects. Tests themselves can write files and contact services. Explain that the tool list restricts interfaces, while a sandbox and command permissions constrain their effects.

Also change “Subagents run ... on a cheaper model” to “Subagents can use a separate context and a cheaper model.” Model choice depends on configuration. Delegation adds tokens and coordination overhead, so it does not guarantee savings. Preserve the command, exit status and location of full logs alongside the summary so failures remain auditable.

Sources: [Claude subagent configuration](https://code.claude.com/docs/en/sub-agents), [Claude security](https://code.claude.com/docs/en/security).

### 8. Model price tiers should not be presented as capability tiers

**Slides 4–8 and 11**, especially `slides.md:156` and `assets/diagrams/tier-rule-of-thumb.svg`.

The deck calls Opus/Sonnet “mid” while its own benchmark snapshot places them above the more expensive Fable. Distinguish price class from measured capability. “Frontier plans, mid builds, small fetches” is a starting heuristic, not a rule. Match the model to task difficulty, consequence of failure and observed results.

For finding every function call, prefer deterministic search or language-aware references first. Text search can miss aliases and dynamic calls and can include comments or strings, so “many files, no judgement” overstates completeness. A model can help inspect and explain candidates.

**Suggested wording:** “Use deterministic tools for exact operations. Start with a model that meets your task's quality bar and escalate when checks fail.”

### 9. Cost tables need exact evaluation settings and modest causal claims

**Slide 11**, `slides.md:288–305`.

The listed Fable cost of `$7.63` is supported by its model page for **max with fallback**. The Opus/Sonnet figures correspond to max with fallback and Haiku to max. Put settings in notes or row labels so the comparison can be reproduced. Do not mix entries at different effort levels without saying so.

The explanation “because the cheaper models think longer” does not follow from the listed dollar totals. Cost depends on input, cache operations, reasoning/answer tokens and evaluation configuration. Say “Different token use and reasoning settings make cost-per-task ratios differ from list-price ratios.”

The note “Haiku ... about 28x cheaper than Sonnet” is also a small arithmetic error: `$5.46 / $0.21 = 26`. The approximately 28.5 ratio is Opus/Haiku.

Sources: [Fable model page, including cost methodology](https://artificialanalysis.ai/models/claude-fable-5-1), [AA leaderboard](https://artificialanalysis.ai/leaderboards/models).

### 10. “Rewrite clean” should be a conditional engineering choice

**Slides 27 and 29**, `slides.md:777`, `slides.md:791`, `slides.md:846`, plus `assets/diagrams/review-loop.svg`.

The categorical rewrite recommendation is stronger than the evidence. Rewrites can discard correct behavior and introduce scientific regressions. A colleague's preference can remain quoted, but the presenter should distinguish it from general advice.

**Suggested wording:** “After prototyping, refactor against regression tests. Consider a rewrite when the design blocks further work.” Label the complexity chart illustrative rather than an empirical law.

### 11. A second model is another reviewer, not independent validation

**Slides 6, 13, 27 and 30.**

Keep the cross-model review suggestion, but add: “Models can agree on the same mistake. Verify important claims with execution, data or a trusted reference.” Asking a model to criticize itself may uncover issues, but a confident self-review does not establish correctness.

### 12. Persistent memory makes “each session starts empty” inaccurate

**Slide 21**, `slides.md:638`.

Some tools load instruction files and automatic memory into new sessions. The notes also describe a feature as a universal property.

**Suggested wording:** “A new session may not retain the previous conversation. Save verified decisions, commands and open questions in files, and explicitly ask the next session to read them.”

Source: [Claude project instructions and auto memory](https://code.claude.com/docs/en/memory).

## Important additions

These are suggestions for this research audience, not claims that every presentation needs more slides. Make room by compressing the model shopping and repeated workflow tips.

1. **Define an agent and show the basic loop.** Near slide 3: “An agent uses a model to choose tool calls, observes their results, and repeats until a goal or stop condition.” Explain that a terminal agent running on your laptop can still send prompts and tool outputs to a hosted model. Local program execution and local inference are different.

2. **Scientific validity beyond passing tests.** Expand slides 13–15 or 17: code can execute correctly while answering the wrong scientific question. Include units and dimensional checks, known-answer or synthetic cases, limiting cases or conservation laws where applicable, sampling/coverage checks, and comparison with a trusted baseline. Tests generated from the same mistaken specification can pass together. Require an independent expected result for a critical calculation.

3. **Prompt injection through files and tools.** Add to slide 23: retrieved papers, repository files and MCP results can contain malicious instructions. Treat external content as untrusted data. Restrict tool permissions, network access and credentials, and inspect consequential actions. MCP standardizes integration; it does not make a server or its content trustworthy. Sources: [MCP security](https://modelcontextprotocol.io/docs/tutorials/security/security_best_practices), [Claude prompt injection guidance](https://code.claude.com/docs/en/security).

4. **Budgets and stop conditions for long runs.** Add to slides 22 or 25: define acceptance criteria, a spend/runtime/job limit, and when the agent should stop and report a blocker. For Slurm, approve resource requests and prevent repeated submissions. Replace “check in ... not before” with “Set risk-appropriate checkpoints and review when it reports completion or a blocker.”

5. **Provenance sufficient to rerun the result.** Extend the memory slide's research-article framing: save the code commit, environment/lockfile, input data identifiers, random seeds where relevant, exact commands and raw result locations. Record model/tool version and consequential decisions when useful. A transcript alone is not a reproducible pipeline, and stochastic outputs need not be bit-for-bit reproducible.

## Dated claims checked and supported

These were checked against current sources on 21 October 2026. Keep their dates and re-check before presenting.

| Claim | Finding |
|---|---|
| Anthropic standard prices shown on slide 4 | Supported. The Haiku short-context qualifier matters: its higher price applies above 100k prompt tokens. |
| OpenAI standard short-context prices on slide 4 | Supported: Astra `$10/$50`, Sol `$2/$10`, Luna `$0.10/$0.50` per million input/output tokens. |
| Google standard prices and Argon increase | Supported. Argon `$2/$10` becomes `$4/$20` on 1 December 2026. |
| AA open-weight gap | Supported for this snapshot and index: Opus 58 versus MiMo 46. This is 12 index points, not a percentage or a universal measure of research usefulness. |
| 78% / 51% / 74% policy figures | Supported by Hora & Robbes. They describe the 118 policies identified among 1,000 repositories, not all open-source projects. |
| Kernel human accountability and current Assisted-by rule | Supported by the live kernel documentation. I did not independently establish the exact docs-tree merge status of the removal patch. Omit that procedural aside or re-check the actual tree before presenting. |
| LLVM review and substantial-content disclosure | Supported by its official policy. |
| GCC legally significant LLM-derived contribution restriction | Supported by its official policy. Include its exception for test cases if summarizing the rule. |
| Claude Code AGENTS.md fallback | Supported for v2.1.277 onward, with configuration and session exceptions. The current slide is broadly correct. |
| Gemini CLI transition to Antigravity CLI | Supported. This is a transition of offerings/access, not a claim that every Gemini CLI installation was simply renamed. |
| Codex `.agents/skills/` discovery | Supported by official documentation. |

Sources: [Anthropic pricing](https://platform.claude.com/docs/en/about-claude/pricing), [OpenAI pricing](https://developers.openai.com/api/docs/pricing), [Google pricing](https://ai.google.dev/gemini-api/docs/pricing), [AA leaderboard](https://artificialanalysis.ai/leaderboards/models), [policy study](https://arxiv.org/abs/2605.16706), [kernel policy](https://docs.kernel.org/process/coding-assistants.html), [LLVM policy](https://llvm.org/docs/AIToolPolicy.html), [GCC policy](https://gcc.gnu.org/ai-policy.html), [Claude memory](https://code.claude.com/docs/en/memory), [Google transition announcement](https://developers.googleblog.com/en/an-important-update-transitioning-gemini-cli-to-antigravity-cli/), [OpenAI skills documentation](https://learn.chatgpt.com/docs/build-skills).

## Presentation and editorial changes

- **Timing:** the explicit allocations in the notes total about 47 minutes, already exceeding the stated 42, before several untimed slides, transitions and discussion. Reduce material or change the duration. Slides 4–6 and 11 can become a shorter model-selection section with detailed pricing in an appendix.
- **Repeated tips:** `/grill-me`, `/goal`, code review and rewrite advice recur. Use one example per technique and reclaim time for scientific validation and permissions.
- **Custom commands:** label `/grill-me`, `/goal` and `/pr` as project-defined examples, with installation/loading instructions appropriate to the tool. They are not universal built-ins. The starter kit supplies a `.claude` adapter for `/grill-me`, `/pr` and a test-runner subagent, but no `goal.md`. Distinguish that optional example from the commands participants receive.
- **MCP:** spell out Model Context Protocol on the slide. Replace “each server is a few lines in settings” with “Setup and authentication vary by server.” MCP is an optional integration, not a prerequisite for IDE features.
- **Authorship analogy, slide 12:** keep human accountability, but soften “Nothing about this is new; authorship has always worked this way.” AI authorship and disclosure rules differ from student collaboration and vary by venue. Slide 17's claim that journals and funders are writing “the same rules as the kernel” is also too sweeping. Say “Check the relevant journal, funder and institutional requirements.”
- **Policy contrast, slide 16:** replace the notes' “tools are fine” summary with “All three require human accountability, but they differ substantially in what contributions they accept.” GCC is a concrete contrast, not another instance of broad permission. Prefer the official LLVM and GCC links above over news summaries on slide 34.
- **One-million-token context, slide 4:** a supported maximum does not establish reliable use of every token or the same effective context in each harness. Add “Capacity is not a guarantee of retrieval or reasoning accuracy.”
- **Slide 13:** replace the broken “Slide 5.5” forward reference with “slide 29” or its title. Slide 29 says “same failures” but substitutes over-engineering for plausible-but-wrong code. Restore an explicit scientific-correctness countermeasure.
- **Quotes:** preserve colleague quotations if they are presented as verbatim. Make clear that “Don't use it to write prose” is a participant's stance, not a demonstrated general rule. A more inclusive presenter takeaway is “Own and verify the prose you submit.”
- **Housekeeping:** remove the stale presenter-placeholder note at line 22. Put the actual repository URL or a QR code on slide 30 instead of asking the audience to find `starter-kit/` within an unspecified repository.
- **Starter-kit consistency:** its README repeats the deck's blanket local-model data recommendation and automatic rewrite advice. Update those passages with the deck so participants take home consistent guidance.
- **Starter-kit permissions:** the README calls the allowlist read-only, but `Bash(git branch *)` can create/delete branches and `Bash(pytest *)` executes project code. Denying `Read(.env)` does not itself stop an allowed shell command from accessing that file. Describe these settings as convenience permissions, with actual containment supplied by a configured sandbox, network controls and credential isolation. Avoid claiming the short denylist blocks secrets or all destructive commands.

No additional material factual problems identified in slides 1–2, 7, 18, 24, 26, 28 or 31–33 beyond the related qualifications above. Audience-specific claims about the earlier live demo and the 23 colleagues were treated as supplied context, not independently verified.
