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

> AI is the *field* that studies the synthesis and analysis of computational agents that act intelligently.

### A brief history of AI

Through history, humans have put effort into understanding and modelling human thought through whatever technological paradigm was current.

> [!quote] Church-Turing thesis 
> Any effectively computable function can be carried out on a Turing machine (and so also in the lambda calculus or any of the other equivalent formalisms).

Computation is more than just a metaphor for intelligence; **reasoning is computation** and computation can be carried out by a computer.

"Flying machines", like planes, don't look like flying animals at all, yet they fly. Similarly, "thinking machines" don't have to perfectly emulate human thought to work.

AI can be thought of as **synthetic epistemology**, AI researchers craft intelligent models instead of just making hypotheses about intelligence.

### Agents situated in environments

- Perception + reasoning + acting = **agent**
- Agent + environment = **world**

An agent's actions are a function of its past experiences, observations, abilities and goals, among other factors. These actions affect the agent's environment, which influences the agent back.

![An agent interacting with its environment](../../utilities/attachments/Pasted%20image%2020250215115049.png)

### Knowledge representation

Knowledge is used to solve problems, it must be represented in a way a computer can understand.

- Knowledge base: Everything the agent knows
- Representation scheme: The way an agent's knowledge is organized

#### Defining a solution

- Agents must "use common sense" to fill in unspecified details about the problem
- Often times, a solution doesn't need to be optimal, but close to optimal, or even just acceptable based on a threshold

#### Representations

Computers and human minds are **physical symbol systems**.

> [!quote] Physical symbol system hypothesis
> A physical symbol system has the necessary and sufficient means for general intelligent action.

- Symbol: Meaningful pattern that can be manipulated
- Symbol system: Creates, copies, modifies, and destroys symbols

A symbol system is physical when its symbols exist in the physical world.

Agents use these systems to model the world. Not all models of reality have the same level of detail, it depends on what's relevant and what isn't. Often, multiple levels of abstraction are used at once.

> [...] you do not have to emulate every level of a human to build an AI agent, but rather you can **emulate the higher levels** and **build them on the foundation of modern computers**.

There are two main levels of abstraction:

1. [Knowledge level](https://www.wikiwand.com/en/articles/Knowledge_level): What an agent knows and what its goals are.
2. [Symbol level](https://www.wikiwand.com/en/articles/Symbol_level): **Reasoning**. The way an agent transforms symbols to arrive to a solution. 

#### Reasoning and acting

> One way that AI representations differ from computer programs in traditional languages is that an AI representation typically specifies **what** needs to be computed, **not how** it is to be computed.

Three stages of reasoning can be distinguished:

1. Design time reasoning: Done by the designer when creating the agent
2. Offline computation: Done by the agent to build background knowledge before acting
3. Online computation: Done by the agent while acting as a result of observing its environment

Some agents, like thermostats, need a lot of design time but little online computation to work.

To build agents that adapt to changing environments, there are two main strategies:

1. Simplify the environment
2. Increase the agent's reasoning abilities

### Dimensions of complexity

An agent's complexity can be measured in multiple dimensions:

#### Modularity

The degree to which an agent can be decomposed into smaller, interconnected components.

An agent's structure can be:

- Flat: Indivisible
- Modular: Multiple modules 
- Hierarchical: Multiple modules where each one be further decomposed into simpler modules 

> [...] to explore the other dimensions, we initially ignore the hierarchical structure and assume a flat representation.

#### Representation scheme

The way the world (agent + environment) is described

There are multiple, often infinite, **states** the world can be in. An useful way of describing states as a combination of **features**.

> [!example]
> A thermostat for a heater may have two belief states: *off* and *heating*. The environment may have three states: *cold*, *comfortable*, and *hot*. There are thus six states corresponding to the different combinations of belief and environment states.

- **Proposition**: feature that evaluates to either true or false



### Prototypical applications

> AI applications are widespread and diverse [...] Rather than treating each application separately, we **abstract the essential features** of such applications to allow us to **study the principles** behind intelligent reasoning and action. 

#wip


