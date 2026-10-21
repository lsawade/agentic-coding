# Grill me: interrogate an idea or plan until the foggy parts are explicit

The user gives an idea or plan. If they give none, use the most recent plan file in `plans/`. Read it fully before asking anything.

Ask the five hardest questions about it, one at a time, in this order:
1. Assumptions: which claims does the plan take for granted?
2. Data: does the data it needs exist, is it accessible, and is it clean enough?
3. Falsification: what result would show the idea is wrong?
4. Feasibility: what is the smallest test that could run this week?
5. Scope: what is explicitly out of scope?

Ask one question, then wait for the answer. If an answer is vague, ask a follow-up on that point before moving on.

When all five are answered, write the clarified plan to `plans/<slug>.md`, where `<slug>` is a short lowercase name for the idea. Use these sections: Goal, Assumptions, Data, Falsification, Smallest test, Out of scope, Still foggy.

The "Still foggy" section lists every point that is still unresolved, including anything you could not get a clear answer on. Do not hide open questions there, and do not mark them resolved.

Do not start implementing. This command only clarifies the plan.
