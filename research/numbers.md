# Numbers for "Agentic AI for Research" (Princeton, 2026-10-20)

As of: 2026-10-20 (all pages opened that day; prices USD per 1M tokens, standard tier, short context). Things marked UNVERIFIED were not confirmed on a page I opened.

## 1. Model ladders and API prices

### OpenAI (outline's "Sol / Terra / Luna" is OUT OF DATE: current line is GPT-6 Astra / Sol / Luna; Terra exists only in the older GPT-5.6 line)

| Model (API id) | Role | Input | Output | Context | Reasoning |
|---|---|---|---|---|---|
| GPT-6 Astra (`gpt-6-astra`) | flagship | $10.00 | $50.00 | 1.05M | effort: low/medium/high/xhigh/max (no "none") |
| GPT-6.1 Sol (`gpt-6.1-sol`) | mid ("near-Astra at lower cost") | $2.00 | $10.00 | 1.05M | same |
| GPT-6 Luna (`gpt-6-luna`) | efficient | $0.10 | $0.50 | 1.05M | none/low/.../max |
| (older) gpt-5.6-sol / -terra / -luna | previous gen | $4 / $2 / $0.20 | $20 / $12 / $1.20 | not shown | Terra is not on the models page |

Ratios: Astra/Luna = 100x input, 100x output. Sol/Luna = 20x both. Older 5.6 line: Sol/Luna = 20x in, 16.7x out.
Flagship: Astra is a configurable-effort reasoning model (effort levels, not a binary toggle; "none" only on Luna). Whether Astra's thinking can be fully switched off: not stated on the page (UNVERIFIED).
Sources: https://developers.openai.com/api/docs/pricing ; https://developers.openai.com/api/docs/models (both opened). openai.com/api/pricing returned 403.

### Anthropic (names confirmed: Fable / Opus / Sonnet / Haiku, 5.x generation)

| Model (API id) | Input | Output | Context | Thinking |
|---|---|---|---|---|
| Claude Fable 5.1 (`claude-fable-5-1`) | $10 | $50 | 1M | adaptive, always on; `disabled` returns 400 |
| Claude Opus 5.5 (`claude-opus-5-5`) | $4 | $20 | 1M | adaptive, always on; `disabled` returns 400 |
| Claude Sonnet 5.5 (`claude-sonnet-5-5`) | $2 | $10 | 1M | adaptive; `disabled` rejected, `between_tools` is the lowest setting |
| Claude Haiku 5.5 (`claude-haiku-5-5`) | $0.10 (prompts <=100k); $0.50 (>100k) | $0.50 (<=100k); $2.50 (>100k) | 1M listed on overview (pricing page says Haiku 5.5 is excluded from the flat-rate 1M context) | adaptive; `disabled` accepted at effort <= high |

Ratios: Fable/Haiku = 100x in and out (Haiku <=100k); 20x vs Haiku >100k. Opus/Haiku = 40x. Sonnet/Haiku = 20x. Fable/Opus = 2.5x.
Flagship Fable 5.1: not a toggleable hybrid; thinking is adaptive and cannot be turned off (steered by effort, default `high`). Also listed: Mythos 5.1 (limited availability, $10/$50).
Sources: https://platform.claude.com/docs/en/about-claude/pricing ; https://platform.claude.com/docs/en/models/overview ; https://platform.claude.com/docs/en/build-with-claude/thinking

### Google

| Model (id) | Input | Output | Notes |
|---|---|---|---|
| Gemini 4 Argon (`gemini-4-argon`) | $2.00 through 30 Nov 2026; $4.00 from 1 Dec 2026 | $10.00 -> $20.00 (incl. thinking) | single flagship, 1,048,576-token window shared by input+output; thinking levels low/medium/high; GA 13 Oct 2026 (per secondary sources) |
| Gemini 3.1 Pro Preview (`gemini-3.1-pro-preview`) | $2.00 (<=200k) / $4.00 | $12.00 / $18.00 | the last model actually named "Pro" |
| Gemini 3.8 Flash (`gemini-3.8-flash`) | $0.75 (-> $1.50 from 1 Jan 2027) | $3.75 (-> $7.50) | |
| Gemini 3.5 Flash-Lite (`gemini-3.5-flash-lite`) | $0.30 | $2.50 | cheapest current 3.x text model |

Ratios (Argon / 3.5 Flash-Lite): now 6.7x in, 4.0x out; from 1 Dec 2026 13.3x in, 8.0x out. (Gemini 3.1 Pro / Flash-Lite: 6.7x in, 4.8x out.) Argon is not labelled Pro or Flash; the "Pro/Flash" naming is only partly current. Whether Argon's thinking can be disabled: page does not say (UNVERIFIED).
Outline claim "roughly 5-10x": holds only for Google. OpenAI and Anthropic top/bottom ratios are 100x (20-40x if comparing the middle tier to the bottom).
Sources: https://ai.google.dev/gemini-api/docs/pricing ; https://ai.google.dev/gemini-api/docs/models ; https://ai.google.dev/gemini-api/docs/models/gemini-4-argon ; release date from search results only (UNVERIFIED on primary page).

## 2. Open-weight gap (Artificial Analysis Intelligence Index v4.3.2)

| Item | Value |
|---|---|
| Top proprietary | Claude Opus 5.5 (max with fallback): 58 |
| Next proprietary | Sonnet 5.5 56; Muse Wonder Full (max) 56; Fable 5.1 53; GPT-6 Astra (max) 53; Gemini 4 Argon (high) 53 |
| Top open weights | MiMo-V2.6-Pro (Xiaomi): 46 |
| Next open | DeepSeek V4.1 Flash 1017 45; GLM-5.3 45; Step 5 Preview 44; Kimi K3 44; Muse Spark Open (Meta) 39; Qwen3.8 27B 34 |
| Gap | 58 - 46 = **12 points** (outline says ~11; roughly consistent, the site shows 12) |

US open weights (fetched 21 Oct 2026, v4.3.2): Muse Spark Open (Meta, xhigh) 39; Beam 1.0 (Reflection) 30; Nemotron 3.5 Super VL (NVIDIA) 26, released 15 Oct 2026, 120B total / 12B active, OpenMDW-1.1 licence; Inkling Small 26, Inkling xhigh 25 (Thinking Machines; launch headline of 41 was on an earlier index version); Nemotron 3 Ultra 23; Nemotron 3.5 Bolt 74B-A9B 21; Gemma 4 31B (Google) 15, released 2 Apr 2026, Apache 2.0, 30.7B; Gemma 4 26B A4B 17 (asterisked on the leaderboard, meaning not explained; not used); gpt-oss-120b (high) 12.
Sources (accessed 21 Oct 2026): https://artificialanalysis.ai/leaderboards/models ; https://artificialanalysis.ai/models/open-source ; https://artificialanalysis.ai/models/nemotron-3-5-super-vl ; https://artificialanalysis.ai/models/gemma-4-31b ; https://artificialanalysis.ai/models/inkling ; https://techcrunch.com/2026/10/19/nvidia-launches-new-open-models-to-run-agents-in-the-enterprise-and-on-pcs/

Caveat: the leaderboard fetch did not label licences; open-weights list came from the /models/open-source page. The leaderboard is dynamic, re-check on the day.

Latest open-weight releases (dates from secondary/aggregator sources; treat as UNVERIFIED against lab pages):
- DeepSeek: V4.1-Flash 10 Sep 2026; V4.1-Flash-1017 mid-Oct 2026 (qz.com 403, snippet only).
- Qwen: Qwen3.8-27B, 5 Aug 2026 (single aggregator).
- Kimi K3: weights 27 Jul 2026.
- GLM-5.3: late Aug 2026 (26 or 28 Aug, sources disagree).
- Mistral: Mistral Large 4, 6-7 Oct 2026 (aggregator only); Mistral Medium 3.5, May 2026 (hidekazu-konishi.com, opened).
- Meta: Muse Spark Open, 15 Oct 2026 (816B total / 42B active; Muse Model License; Llama no longer the current line; Llama 4 was Apr 2025). Muse Glimmer (Apache 2.0) 10 Aug 2026 per one aggregator.
Sources opened: https://artificialanalysis.ai/leaderboards/models ; https://artificialanalysis.ai/models/open-source ; https://hidekazu-konishi.com/entry/open_weights_llm_release_history_and_timeline.html . Others via search results only.

## 3. ICSME 2026 study (arXiv 2605.16706)

| Item | Value |
|---|---|
| Title | AI Policy, Disclosure, and Human in the Loop: How Are Contribution Guidelines Adapting to GenAI? |
| Authors | Andre Hora, Romain Robbes |
| Data | 1,000 popular GitHub repositories -> 118 AI policies |
| Allow AI-assisted contributions | 78% (22% explicitly discourage) |
| Require disclosure | 51% |
| Require human in the loop | 74% |
| Status | v1 15 May 2026, v2 13 Jul 2026; accepted to ICSME 2026 |

All three headline numbers confirmed.
Source: https://arxiv.org/abs/2605.16706

## 4. Linux kernel "Assisted-by"

| Item | Status as of 2026-10-20 |
|---|---|
| Maintainers Summit, Prague | 8 Oct 2026; majority of ~30 invited devs supported dropping the tag (heise) |
| Patch | Sasha Levin; v1 9 Oct, withdrawn after objections, v2 13 Oct with Lorenzo Stoakes ack (fosslinux) |
| Phoronix article | 13 Oct 2026, confirmed: patch removes Assisted-by docs, mixed LKML opinion |
| Merge | Applied to Jonathan Corbet's docs tree 14 Oct 2026 (fosslinux; heise says docs-next). NOT in mainline: fosslinux re-checked 19 Oct and the rule was still present. Linux 7.3 released 18 Oct without it; expected in 7.4 merge window (that last point from a search summary, UNVERIFIED). Not rejected. |
| Context | Only ~10% of commits in 7.3 carried the tag; replacement idea: note AI use in cover letter |
| Slashdot headline (17 Oct) "no longer need" overstates; it is merged to docs-next only |
| Rules still on docs.kernel.org (live page, tag still listed) | "AI agents MUST NOT add Signed-off-by tags"; only humans certify the DCO; human reviews all AI code, ensures licence compliance and "takes full responsibility"; `Assisted-by: LLM [TOOL1] [TOOL2]` tag (the part being removed) |

Sources: https://phoronix.com/news/Linux-Dropping-Assisted-By-Req (opened via www.phoronix.com) ; https://www.heise.de/en/news/Linux-may-drop-AI-code-labels-Torvalds-uses-LLMs-too-11490773.html ; https://www.fosslinux.com/162933/ai-assisted-kernel-linux-7-3.htm ; https://linux.slashdot.org/story/26/10/17/0723207/linux-maintainers-can-now-submit-ai-generated-code-without-declaring-it ; https://docs.kernel.org/process/coding-assistants.html

## 5. LLVM and GCC

| Project | Date | Substance |
|---|---|---|
| LLVM "AI tool policy: human in the loop" | Adopted Jan 2026 (It's FOSS 22 Jan 2026; devclass 21 Jan 2026) | Any tools allowed, but a human must review all LLM output and answer questions about it; disclose substantial tool-generated content (e.g. Assisted-by trailer); bans agents acting in project spaces without human approval. Drafted by Reid Kleckner. |
| GCC Steering Committee | Announced 29 Jul 2026 by David Edelsohn (LWN; It's FOSS 30 Jul) | Declines "legally significant" contributions (~15 lines of code/text) that include or derive from LLM output; test cases exempt; smaller AI-assisted changes must carry Assisted-by; LLMs allowed for research/review if not submitted; review early 2027. |

Primary gcc.gnu.org post: archive index shows thread "GCC AI Policy Announcement" by David Edelsohn (248628.html) but I did not open the message itself; text above is from LWN. Primary llvm.org page opened.
Sources: https://llvm.org/docs/AIToolPolicy.html ; https://itsfoss.com/news/llvm-ai-policy/ ; https://lwn.net/Articles/1086041/ ; https://itsfoss.com/news/gcc-bans-ai-code/ ; https://gcc.gnu.org/pipermail/gcc/2026-July/

## 6. Cost-per-task anchor (Artificial Analysis, "cost per Intelligence Index task", weighted average)

| Model | Index score | $/task |
|---|---|---|
| Claude Fable 5.1 | 53 | $7.63 |
| Claude Opus 5.5 | 58 | $5.98 |
| Claude Sonnet 5.5 | 56 | $5.46 |
| Claude Haiku 5.5 | 43 | $0.21 |

Note: this is a benchmark-suite task, not an agentic-coding session; no official Anthropic/OpenAI per-session cost page found. Sonnet is ~92% of Opus's cost and Haiku ~28x cheaper, so list-price ratios overstate real-cost gaps among the top three (thinking-token usage differs).
Sources: https://artificialanalysis.ai/models/claude-opus-5-5 ; .../claude-sonnet-5-5 ; .../claude-haiku-5-5 ; .../claude-fable-5-1

## 7. Agent instruction files and harness status (accessed 2026-10-21)

- Claude Code reads `AGENTS.md` directly from v2.1.277 (Sep 2026), and by default only when there is no `CLAUDE.md`, `.claude/CLAUDE.md` or `CLAUDE.local.md` in the working directory or above; if one exists, only the CLAUDE.md files load. `@AGENTS.md` import or the /config "Project instructions" setting loads both. Not read: `AGENTS.local.md`, `AGENTS.override.md`, `.agents/`. Release month (Sep 2026) from secondary coverage only. Sources: https://code.claude.com/docs/en/memory ; https://devops.com/claude-code-adds-agents-md-fallback-cutting-instruction-file-sprawl
- Gemini CLI -> Antigravity CLI (`agy`): announced 19 May 2026. On 18 Jun 2026 Gemini CLI stopped serving Google AI Pro/Ultra and free Gemini Code Assist for individuals. Still works with Code Assist Standard/Enterprise licenses and paid Gemini / Gemini Enterprise Agent Platform API keys. Google's post does not use the word "deprecated". Antigravity CLI reads `AGENTS.md` (legacy `GEMINI.md` still supported). Sources: https://developers.googleblog.com/en/an-important-update-transitioning-gemini-cli-to-antigravity-cli/ ; https://docs.flutter.dev/ai/antigravity-cli.md
