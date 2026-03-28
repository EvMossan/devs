---
title: "From Writing Code to Programming the Process"
subtitle: "A Working Thesis on AI-Native Software Engineering"
date: "March 2026"
lang: en
---

**Core thesis**

> I did not stop programming. I stopped programming the product line by line and started programming the process by which the product is created. Code did not disappear. It became an intermediate executable layer inside a conveyor of architecture, specifications, handoffs, and verification.

## Abstract

This document is a working thesis, not a universal proof. It is my attempt to describe what has changed in my own engineering practice while building a complex iPhone application with AI agents, despite having no prior iOS development background. My claim is not that code has become irrelevant. My claim is that code is no longer the only, or even the main, human control surface in software creation. In an AI-native workflow, a substantial share of engineering value can shift upward: into architecture, specification, decomposition, orchestration, acceptance criteria, and verification.

This claim is grounded in two things. First, it is grounded in my own project: a local-first iPhone application developed through a structured repository workflow built around architecture contracts, technical specifications, role-separated agents, shared handoffs, and runtime verification. Second, it is grounded in a broader pattern visible in current research and industry practice. Recent work from Anthropic, OpenAI, and Microsoft suggests that AI changes the distribution of engineering labor more than it simply “automates coding away.” Low-level code writing becomes less central; debugging, code reading, conceptual understanding, prompt/spec design, and validation become more central (Anthropic, 2026a; Lee et al., 2025; OpenAI, 2025a, 2026a).

The strongest version of my thesis is not “code no longer matters.” That overstates the case. The stronger and more defensible version is this: **code remains the executable reality of the system, but it no longer has to remain the primary interface through which the human engineer steers the system**.

## 1. The claim I am actually making

The easiest way to misunderstand my position is to hear it as a shallow anti-code statement. That is not what I mean.

I am not claiming that software can exist without code. I am not claiming that understanding code never matters. I am not claiming that a high-stakes production system should be shipped without serious verification. I am not even claiming that my own current workflow generalizes cleanly to every domain.

What I am claiming is more specific:

1. Software engineering has always involved much more than typing code.
2. AI systems are now capable enough that line-by-line code production can be delegated much more aggressively than before.
3. Once code production becomes partially delegable, the human engineer’s center of gravity shifts upward.
4. The new high-value human work is not “doing nothing.” It is designing and governing the system that produces the code.
5. In my own project, this is not a theoretical claim. It is how the product was actually built.

A useful way to frame this is as a **control-plane / execution-plane split**.

- The **control plane** consists of problem framing, architecture, contracts, specifications, agent instructions, handoff rules, acceptance criteria, and evaluation logic.
- The **execution plane** consists of generated code, tests, command runs, build artifacts, runtime behavior, and the system’s observable outputs.

In a traditional workflow, a single person often occupies both layers at once and experiences “programming” mainly as direct code authorship. In my current workflow, I spend much more of my time authoring the control plane. The execution plane still exists, but it is increasingly mediated by agents and by formalized repository process.

That is why the sentence above matters to me. It captures the actual shift:

> I did not stop programming. I started programming the process that creates the product.

## 2. Why natural language and voice are not “anti-engineering”

A second misunderstanding is to treat language as somehow inferior to “real engineering.” That objection confuses the medium with the work.

Engineering is not defined by whether an idea is written as a diagram, a formula, a checklist, code, or a spoken instruction. Engineering is defined by whether a person can transform an intention into a system that works under constraints in reality. Language becomes an engineering medium when it carries structure, scope, priorities, invariants, interfaces, and tests.

This matters for my workflow because I often work by speaking large prompts out loud. Voice is not just an input method for me. It is part of the thinking process itself. When I verbalize a design, I usually notice contradictions, missing assumptions, hidden scope creep, and unclear constraints earlier than when I merely “have the idea in my head.”

There is real cognitive science behind this intuition, even if no paper proves my exact workflow. Research on **self-explanation** shows that prompting learners to explain material to themselves can improve understanding relative to rereading alone (Chi et al., 1994). A major review of learning techniques rated self-explanation as having “moderate utility” across multiple domains and outcomes (Dunlosky et al., 2013). More recent work on **private speech** found that, in a visual-spatial working-memory task, young adults performed better on trials where they produced more speech to themselves (Guo & Dobkins, 2023). These findings do not mean “talking always makes you smarter.” But they do support a narrower claim: **verbalization can be a real cognitive tool for structuring thought, not just a delivery channel for thoughts that already exist**.

This gives me a better way to describe what happens when I work with agents by voice. I am not merely “asking the model for code.” I am using language as a mechanism for decomposition, clarification, and self-explanation. In that sense, my spoken prompt is partly an instruction to the model and partly an instrument for my own cognition.

## 3. What current research suggests about the shift in engineering work

No single paper says exactly what I am saying. But several current lines of evidence point in the same direction.

First, Anthropic’s 2026 study on coding skill formation makes an important distinction between different kinds of coding competence. The paper explicitly argues that low-level code writing, such as remembering syntax, is becoming less important than debugging, code reading, and conceptual understanding for the oversight of AI-generated code (Anthropic, 2026a). In their randomized study of 52 mostly junior software engineers learning an unfamiliar Python library, the AI-assisted group scored lower on a follow-up quiz than the hand-coding group on average, with the largest gap on debugging. But the qualitative patterns are more interesting than the headline. Heavy delegation and AI-led debugging were associated with low scores, while conceptual inquiry and explanation-seeking patterns were associated with higher scores (Anthropic, 2026a). The practical lesson is not “AI makes engineers stupid.” The lesson is that **how** one uses AI matters.

Second, Microsoft’s survey of 319 knowledge workers found that GenAI does not simply erase critical thinking. Instead, people described critical thinking in AI-assisted work as setting goals, refining prompts, assessing outputs against criteria, and verifying results against external sources (Lee et al., 2025). The paper is based on self-report, so it should not be inflated into a civilizational claim. But it supports the idea that cognition is being **reallocated**, not simply removed.

Third, current official guidance from OpenAI now describes a build process in which coding agents can draft whole feature implementations, tests, and documentation from written specifications, while engineers shift toward clarifying product behavior, reviewing architectural implications, refining business logic, and defining guardrails and conventions (OpenAI, 2025a). In the same guide, OpenAI is explicit that critical decisions still stay with engineers, especially for sensitive production changes or low-confidence situations (OpenAI, 2025a). That is almost exactly the shape of the world I see.

Fourth, Anthropic’s own internal research and 2026 trends reporting point to the same broad movement. Anthropic reports that its engineers often use Claude for debugging, code understanding, and implementing features, while fully delegating only a small fraction of work end to end (Anthropic, 2025a). Their 2026 report explicitly describes the role transformation as a shift from writing code toward orchestrating agents, evaluating output, providing strategic direction, and ensuring the system solves the right problems (Anthropic, 2026b). That report is not peer-reviewed science; it is an industry signal. But it is a very relevant one.

Taken together, these sources do not prove that code is irrelevant. They do suggest that the profession’s center of gravity is moving from **manual production** toward **orchestration, evaluation, and governance**.

## 4. My project as a case study

My own project is a local-first iPhone application with AI-assisted behavior. I did not come into it as an iOS engineer. My background is in data science, data engineering, and algorithmic trading. I had never built an iOS application of this complexity before. Nevertheless, the application now exists and works.

That fact, by itself, does not prove a new law of software development. It does, however, provide a serious case study. It shows that a person without prior domain-specific implementation background can still build a non-trivial product if the human work is moved upward into architecture, decomposition, and process design, while low-level implementation is delegated to capable agents inside a disciplined workflow.

The project’s runtime architecture is already formalized in internal documentation. The iOS app owns user interaction, local rendering, and consent gating. On-device SQLite is treated as the sole source of truth for user data and runtime state. The gateway is stateless and exists to proxy model calls while keeping API keys backend-only. OpenAI is treated as execution infrastructure rather than durable application state (Internal Project, 2026d). This is important because it reduces both architectural ambiguity and blast radius. The product is explicitly local-first rather than cloud-state-first.

I also have an explicit orchestration contract for the agent runtime. That contract exists to reduce unnecessary model round trips, reduce repeated context replay, and preserve the existing product UX while simplifying the flow (Internal Project, 2026e). In parallel, I maintain a more specific runtime architecture for the Apple Health goal subsystem, including data ownership, persistence, service surfaces, and refresh paths (Internal Project, 2026f). In other words, I did not “skip engineering.” I externalized and formalized it.

## 5. The workflow I actually built

The most important part of my method is not the model itself. It is the workflow I built around it.

At the repository level, my workflow document establishes a strict source-of-truth order, a change-request protocol, a stage contract, test-first implementation, self-review, verification, a runtime reality gate, and a three-pass completion sweep before a stage can be treated as closed (Internal Project, 2026a). The same repository also contains a technical specification authoring standard that forces every technical spec to include a problem statement, scope boundaries, implementation plan, testing and verification plan, requirement traceability set, definition of done, clarifying questions, and a user decisions log (Internal Project, 2026c). The visual workflow map then turns this into a clear multi-role conveyor: `spec-author -> runtime-implementer -> runtime-verifier`, with a shared active handoff carrying the baton until the verifier records `PASS` (Internal Project, 2026b).

The result is that the “program” I write is no longer just Swift or backend code. It is a larger operational program composed of contracts, roles, transitions, and evidence.

### Table 1. How I currently divide the work

| Layer | Primary question | Main owner in my workflow | Main artifact |
|---|---|---|---|
| Intent | What problem am I solving and why? | Human | Problem statement, user request |
| Architecture | What owns what? What are the invariants? | Human | Architecture contracts |
| Specification | What is in scope, out of scope, and done? | Human + spec-author agent | Technical specs, DoD, traceability |
| Implementation | How is the spec translated into code and tests? | Runtime-implementer agent | Code, tests, diffs, self-review |
| Verification | Did it actually work on the real runtime path? | Runtime-verifier agent + runtime/test system + human when needed | Evidence, handoff, PASS/BLOCKED verdict |

Several parts of this workflow matter more than they may first appear.

### 5.1 Source-of-truth discipline

The workflow begins by resolving which documents outrank which others and explicitly forbids guessing under conflict; instead, it requires a recorded change request (Internal Project, 2026a). This is not bureaucracy for its own sake. In agentic systems, context drift is one of the main hidden failure modes. A source-of-truth hierarchy is a way of preventing plausible nonsense from silently becoming implementation.

### 5.2 Specifications as contracts, not as notes

The technical specification standard forces every spec to contain scope boundaries, testing and verification, requirement traceability, definition of done, clarifying questions, and a user decisions log (Internal Project, 2026c). This changes the role of a spec. It is no longer a loose planning note. It becomes a contract that can be checked against implementation and against evidence.

### 5.3 Role separation

The visual map and repository process separate spec writing, implementation, and verification into distinct sessions and roles (Internal Project, 2026a, 2026b). This matters because the same context that generates a solution is often too forgiving when reviewing it. Anthropic’s guidance for Claude Code explicitly recommends multi-session or writer/reviewer patterns because a fresh context improves review quality (Anthropic, 2026c). My process arrived at a very similar structure independently.

### 5.4 Runtime reality, not plausible-looking output

One of the strongest parts of my repository workflow is the **Runtime Reality Gate**. For runtime-impacting changes, the system requires live end-to-end verification on the real running stack rather than mocks or stubs. Without this, the workflow explicitly states, agents cannot reliably distinguish working code from plausible-looking code (Internal Project, 2026a). This is close in spirit to OpenAI’s current framing of evals as captured runs with artifacts and checks, rather than “does this feel right?” judgments (OpenAI, 2026a).

### 5.5 Requirement traceability and closure discipline

My spec standard requires an explicit requirement traceability set with acceptance evidence (Internal Project, 2026c). My stage workflow then requires a three-pass completion sweep that re-reads the source of truth and checks requirement-by-requirement whether anything is missing, partial, or only superficially addressed (Internal Project, 2026a). This is a way of turning completion into an evidentiary claim instead of an intuition.

### 5.6 Anti-shortcut rules

The workflow forbids silent deviations from scope, runtime fallbacks that hide failure, and test doubles that simulate success instead of verifying real behavior (Internal Project, 2026a). Those rules exist precisely because agents are good at producing believable but weak artifacts. The process is designed around the fact that “looks complete” and “is complete” are not the same thing.

## 6. A useful conceptual lens: distributed code cognition

One of the most useful ways I now understand my own method is through the idea of **distributed code cognition**.

I often do not personally inspect every generated code file. From a traditional perspective, that seems like abdication. But that is not actually what is happening. The code is still being read, edited, tested, and checked. What has changed is **who** or **what** performs each part of that cognition.

- I hold the product intent, architecture, priorities, and acceptance logic.
- The implementer agent reads and edits the relevant code surfaces.
- The verifier agent re-reads changed surfaces and re-runs checks.
- The test harness checks executable behavior.
- The runtime reality gate checks the live stack.
- The handoff and traceability artifacts preserve what happened across sessions.

In other words, code cognition has not disappeared. It has been distributed across a socio-technical system. My role is less “single-threaded author of every line” and more “designer and governor of the process by which code is produced, checked, and accepted.”

This is why I do not think the right question is “But who read the code?” The better question is: **where in the system is code being read, checked, and falsified, and how trustworthy are those checks?**

That question is much more operational, and much more modern.

## 7. What I already have, and what I still do not have

The strongest way to present this thesis is to separate present capability from unresolved problems.

### 7.1 What I already have

In my current project, I already have:

1. **A clear architectural ownership model.** The local-first runtime contract establishes that the app and on-device database, not the model provider, own user state (Internal Project, 2026d).
2. **A structured specification layer.** Every feature is expected to pass through problem framing, scope, verification planning, and definition of done (Internal Project, 2026c).
3. **A multi-role agent conveyor.** Specification, implementation, and verification are treated as distinct functions rather than one undifferentiated chat (Internal Project, 2026b).
4. **A hard verification culture.** The workflow requires red-before-green testing, runtime reality checks, evidence capture, and a three-pass completion sweep (Internal Project, 2026a).
5. **A relatively low blast radius.** My current product is real, but it is not a nuclear reactor, a trading exchange, or a safety-critical medical device. That matters.

### 7.2 What I do not yet have

I do **not** yet have:

1. **A universal proof.** This is still an N=1 case study, even if it is a meaningful one.
2. **A high-stakes-grade oracle layer.** For serious financial, security-critical, or life-critical systems, the central unsolved problem is still trustworthy verification.
3. **Complete formal enforcement.** Some of my strongest rules are process rules written in documents. They are powerful, but they are not yet fully turned into deterministic enforcement everywhere.

One obvious next step is to translate more of this governance out of markdown-only rules and into deterministic enforcement. Current vendor guidance points in that direction: Anthropic’s hooks are explicitly designed to ensure that certain actions always happen instead of relying on the model to remember them, and OpenAI’s current eval guidance treats an agent skill as something that should be measured through captured runs, artifacts, and explicit checks (Anthropic, 2026d; OpenAI, 2026a).

4. **A solved answer to document drift.** Once the control plane is distributed across multiple contracts, specs, handoffs, and architecture documents, keeping them synchronized becomes a new engineering problem.
5. **A proven large-team operating model.** My workflow works for me in my current project. It is not yet proven that it scales cleanly to large multi-team organizations without new failure modes.

These limitations do not invalidate the thesis. They tell me where the thesis is strongest and where it is still vulnerable.

## 8. What this thesis does **not** mean

To keep the claim honest, I need to say clearly what it does not mean.

### 8.1 It does not mean code is irrelevant

Even Anthropic’s work that most strongly supports a shift away from low-level code authorship still emphasizes debugging, code reading, and conceptual understanding as central skills for supervising AI-generated code (Anthropic, 2026a). My own workflow also depends on code being read by the implementer and verifier roles. The truth is not “no code.” The truth is “less direct human line-by-line authorship, more indirect governance of code through process.”

### 8.2 It does not mean pure delegation is safe

The most important learning studies in this area do not support naive delegation. Bastani and colleagues showed that unguarded GPT access improved performance during practice but hurt later unassisted performance, while a more constrained tutor design mitigated the damage (Bastani et al., 2025). Anthropic’s coding skills study found that heavy delegation and AI-led debugging were associated with weak conceptual mastery, while explanation-seeking modes looked better (Anthropic, 2026a). The lesson is that AI use can be **complementary** to learning or **substitutive** for learning, depending on how the workflow is designed.

My own workflow is explicitly trying to bias the system toward the complementary side: architecture first, specification first, verification first, evidence first.

### 8.3 It does not mean human judgment disappears in high-stakes systems

OpenAI’s current guidance is explicit that critical decisions remain with engineers for novel incidents, sensitive production changes, and low-confidence situations (OpenAI, 2025a). That is the right default. The real frontier is not “remove humans from the loop at all costs.” The real frontier is to make human attention more selective, more evidence-based, and more focused on genuinely high-risk points.

## 9. Educational and professional implications

If my thesis is even partly right, then the educational implication is not “stop teaching programming.” It is “stop equating programming with syntax recall and line-by-line authorship.”

The skill stack that seems to matter more in an AI-native workflow includes:

- problem framing;
- architecture and ownership design;
- task decomposition;
- spec writing;
- scope control;
- testing and evaluation design;
- debugging and code reading;
- verification and evidence review;
- agent orchestration;
- judgment under uncertainty.

This does not make conceptual knowledge obsolete. On the contrary, it makes conceptual knowledge more important, because without it, oversight becomes fake. A person who cannot reason about the system cannot meaningfully validate it. But the relative value of manually typing every line of implementation code appears to be decreasing.

OpenAI’s own guidance describes engineers increasingly as reviewers, editors, and sources of direction rather than purely as translators of specs into code (OpenAI, 2025a). Anthropic’s reports describe a similar move toward orchestration and broader “full-stack” capability expansion with active human oversight rather than full replacement (Anthropic, 2025a, 2026b). That matches what I see in practice.

## 10. My current synthesis

The best short version of my position is now this:

> Software engineering is moving from direct artifact authorship toward control-plane design.

That is the angle I had not fully articulated at the beginning. I had been describing my process operationally, but the deeper conceptual shift is that I am increasingly authoring the **control system** that produces, constrains, and validates software.

In older workflows, programming mainly meant writing code that the machine would execute.
In my current workflow, programming increasingly means writing:

- architecture contracts the system must obey,
- specifications that define scope and acceptance,
- role instructions that shape how agents work,
- handoff structures that preserve state across sessions,
- tests and checks that constrain implementation,
- and verification logic that determines whether a change is real or only plausible.

The code still matters. It is still what runs. But my engineering work is less and less about touching each line personally, and more and more about building a process in which code is generated, challenged, and accepted under explicit rules.

That is why the original sentence still feels right to me:

> I did not stop programming. I stopped programming the product line by line and started programming the process by which the product is created.

## 11. Conclusion

I do not claim that this is the final form of software engineering, or that the hard problems are solved. In fact, I think the hardest unresolved problem has now become clearer: not code generation, but trustworthy verification. For low-blast-radius products, a process like mine can already be extremely effective. For high-stakes systems, the question is how to scale verification, evidence, escalation, and human judgment without re-creating the old bottlenecks in a new costume.

Still, I think the shift itself is real.

The human engineer is not disappearing. The human engineer is being pushed upward.

Less effort goes into manually producing every line.
More effort goes into defining the right system, constraining it, interrogating it, and deciding whether the result deserves to exist.

That is not the end of programming.

It is a new layer of programming.

## References

Anthropic. (2025a, December 2). *How AI is transforming work at Anthropic*. Anthropic Research. https://www.anthropic.com/research/how-ai-is-transforming-work-at-anthropic

Anthropic. (2026a, January 29). *How AI assistance impacts the formation of coding skills*. Anthropic Research. https://www.anthropic.com/research/AI-assistance-coding-skills

Anthropic. (2026b, January 21). *2026 agentic coding trends report*. Anthropic. https://resources.anthropic.com/hubfs/2026%20Agentic%20Coding%20Trends%20Report.pdf

Anthropic. (2026c). *Best practices for Claude Code*. Claude Code Docs. https://code.claude.com/docs/en/best-practices

Anthropic. (2026d). *Automate workflows with hooks*. Claude Code Docs. https://code.claude.com/docs/en/hooks-guide

Bastani, H., Bastani, O., Sungu, A., Ge, H., Kabakcı, Ö., & Mariman, R. (2025). *Generative AI without guardrails can harm learning: Evidence from high school mathematics*. *Proceedings of the National Academy of Sciences*. https://hamsabastani.github.io/education_llm.pdf

Chi, M. T. H., de Leeuw, N., Chiu, M.-H., & LaVancher, C. (1994). Eliciting self-explanations improves understanding. *Cognitive Science, 18*, 439–477. https://doi.org/10.1207/s15516709cog1803_3

Dunlosky, J., Rawson, K. A., Marsh, E. J., Nathan, M. J., & Willingham, D. T. (2013). Improving students’ learning with effective learning techniques: Promising directions from cognitive and educational psychology. *Psychological Science in the Public Interest, 14*(1), 4–58. https://pubmed.ncbi.nlm.nih.gov/26173288/

Guo, X., & Dobkins, K. (2023). Private speech amount positively predicts memory performance in young adults. *Consciousness and Cognition, 113*, 103534. https://doi.org/10.1016/j.concog.2023.103534

Internal Project. (2026a). *Agent workflow for iOS MVP repository*.

Internal Project. (2026b). *Agent workflow visual map*.

Internal Project. (2026c). *Technical specification authoring standard*.

Internal Project. (2026d). *Runtime architecture contract*.

Internal Project. (2026e). *Agent orchestration architecture contract*.

Internal Project. (2026f). *Apple Health goal runtime architecture*.

Lee, H. P., Rintel, S., Banks, R., Wilson, N., et al. (2025). *The impact of generative AI on critical thinking: Self-reported reductions in cognitive effort and confidence effects from a survey of knowledge workers*. CHI 2025. https://www.microsoft.com/en-us/research/publication/the-impact-of-generative-ai-on-critical-thinking-self-reported-reductions-in-cognitive-effort-and-confidence-effects-from-a-survey-of-knowledge-workers/

OpenAI. (2025a, November 20). *Building an AI-native engineering team*. OpenAI / Codex. https://developers.openai.com/codex/guides/build-ai-native-engineering-team

OpenAI. (2026a, January 22). *Testing agent skills systematically with evals*. OpenAI Developers. https://developers.openai.com/blog/eval-skills/
