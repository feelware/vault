---
tags:
  - "#lecture-notes"
src-date: 
src-author:
  - Alan Mackworth
  - David L. Poole
src-link: "[[pdf/ai-foundations-computational-agents.pdf|ai-foundations-computational-agents]]"
---
# Artificial Intelligence: Foundations of Computational Agents

## AI and agents

### What is AI?

> AI is the field that studies the synthesis and analysis of computational agents that act *intelligently*.

### A brief history of AI

Through history, humans have put effort into understanding and modelling human thought through whatever technological paradigm was current.

**Church-Turing thesis**:

> Any effectively computable function can be carried out on a Turing machine (and so also in the lambda calculus or any of the other equivalent formalisms).

- There is no evidence that people can compute functions that are not Turing computable.
- An agent’s actions are a function of its abilities, its history, and its goals or preferences.
- Computation is more than just a metaphor for intelligence; reasoning *is* computation and computation can be carried out by a computer.

AI can be thought of as synthetic epistemology. Instead of just making hypotheses about intelligence, researches craft intelligent models.

"Flying machines", like planes, don't look or behave like flying animals at all, yet they fly. Similarly, "thinking machines" don't have to mimic human thought to work.

> This also offers an approach to the question, “Can computers really think?” by considering the analogous question, “Can airplanes really fly?”

### Agents situated in environments

- Perception + reasoning + acting = **agent**
- Agent + environment = **world**

An agent's actions are a function of its past experiences, observations, abilities and goals, among other factors. These actions affect the agent's environment, which influences the agent back.

![An agent interacting with its environment](../../utilities/attachments/Pasted%20image%2020250215115049.png)

### Knowledge representation

Knowledge is used to solve problems, it must be represented in a way a computer can understand.

- Representation scheme: The way an agent's knowledge is organized
- Knowledge base: The representation of everything the agent "knows"

#### Defining a solution

- The problem must be understood by the agent, even when some details are not specified
- Very often the solution doesn't need to be optimal, but close to optimal, or even just acceptable based on a threshold

#### Representations


