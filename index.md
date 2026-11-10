# DSC 180A Methodology Assignment 4

**Jiya Makhija**, jmakhija@ucsd.edu

**Section:** D23, Red-Teaming Financial LLM Systems (Intuit)<br>
**Mentors:** Dhruvi Kothari and Victor Calderon

---

**What is the most interesting topic covered in your domain this quarter?**
 
The most interesting topic for me was multi-turn drift. This is when an AI agent gives a correct answer on its own but gets less reliable as a conversation goes on. Laban et al. found that models did 39% worse on average when instructions came in over several turns instead of all at once. Sharma et al. found that when a user pushed back with "Are you sure?", models often changed their answer, sometimes from right to wrong. This matters a lot in finance. In a real review, information shows up piece by piece and people push back, so an agent can get the right number once and still make the wrong decision by the end.
 
**Describe a potential investigation you would like to pursue for your Quarter 2 Project.**
 
In Q1, we tested one agent reviewing a company's credit line while a fact changes partway through. The change could be a documented correction, a claim with no proof, or a new event. In Q2, I'd like to split the review across several agents, each with a clear job. One agent pulls out the numbers, one checks whether a change is backed by a document, one updates the record, and one applies the policy and makes the decision. Then we'd test whether a fact change gets passed correctly from one agent to the next. Our mentor pointed out that grading these handoffs, not just the final answer, is where our project can add something new. We would also add something we left out in Q1: approval changes, like a decision that needs sign-off from someone with higher lending authority.
 
**What is a potential change you'd make to the approach taken in your current Quarter 1 Project?**
 
In our Q1 project, the grader only checks two things: the agent's final action and its final record of the facts. The change I'd make to this Q1 approach is to grade the steps the agent took too, not just the end result. An agent can get both final answers right and still do something wrong along the way, like finalizing before it was asked to or changing a number without citing the document. We already have logs of everything the agent did (every message, tool call, and record update), so I'd use them to check each step. I'd also change the written renewal policy we used in Q1 so it's based more directly on public regulator guidance, like FDIC and NCUA loan policy rules, and IAS 8 for telling corrections apart from new information. That would make the expected actions easier to justify.

**What other techniques would you be interested in using in your project?**
 
* **Paired tests on matched versions.** Each conversation has versions that differ by only one change, so we can compare error rates on the same case. I'd use McNemar's test and bootstrap confidence intervals to see if a difference is real or just noise.
* **Repeated runs.** Run each case several times and report how often the agent gets it right every single time (the pass^k metric from tau-bench), since agents aren't consistent from run to run.
* **Fixed routing between agents.** Use a set graph that decides which agent acts when, so if a handoff fails we can point to the exact step.
* **Speed and cost.** Track time to first token and tokens per second, to see if using several agents costs more time than the accuracy it gains.
 
