# Ensue: The Shared Memory Layer for Agents

![Agent Swarms](./images/agent_swarms.gif)

Instead of one siloed, stateless agent or LLM, imagine a world where you have access to the shared memory of millions - all connected through a single, cohesive system.

## Introducing Ensue

The first _shared_ memory layer for agents. It will be a distributed protocol and memory marketplace where

- Memory is portable across tools, agents, and models.
- Agent builders tap into rich, shared memory streams from other actors.
- Triggers and access rules for the memory snippets (per-agent, per-field) will shape and secure interactions.

## How Ensue will change your agent-building

- Build smarter systems powered by collective intelligence.
- Create dynamic, programmatic workflows that reason across shared memory.
- Move beyond rigid, pre-scripted tasks toward adaptive, autonomous coordination at scale.

## Problems Ensue solves

- **Scaling multi-agent coordination** – Tired of message-passing hacks and database boilerplate? Tools like A2A are great - until you scale. ensue gives agents a shared memory space to collaborate.
- **Porting context across tools** – Pick up a conversation in Claude Code that started in ChatGPT or Gemini. Or pass context from an n8n workflow into another custom agent.
- **Controlling what agents can access** – With agent permissions, you can give each agent exactly what they need - and nothing more.

## Ensue in action

Imagine a multi-actor system of specialized agents and users (app-users, legal-counsel, feature-developer, etc.) using unique models (Gemini, Claude, GPT, etc.) dynamically interacting with the same Ensue shared memory layer.

```typescript
import { AgentMemory, Fq } from "ensue";

// Gemini powered PM agent that takes user inputs and develops feature specs
async function main() {
  const geminiKey = Fq.random();
  // loads existing memory from `address` config file
  const memory = await AgentMemory.create(geminiKey);
  const codeBase = await memory.read("code-base");

  // user agents constantly append feedback
  const userAppFeedback = await memory.read("user-app-feedback");

  // ensure critical data is authenticated
  const managerAppFeedback = await memory.readVerified("manager-app-feedback");
  const lawyerAppFeedback = await memory.readVerified("lawyer-app-feedback");

  const memories = [
    codeBase,
    userAppFeedback,
    managerAppFeedback,
    lawyerAppFeedback,
    // prompt:
    "write me a feature spec that addresses all the feedback above",
  ];

  const instructions = await executeGemini(memories);
  await memory.update_or_create_key("gemini-instructions", instructions);
}
```

```typescript
// Claude powered feature development agent
async function main() {
  const claudeKey = Fq.random();
  // loads same memory from `address` config file
  const memory = await AgentMemory.create(claudeKey);
  const featureSpec = await memory.read("gemini-instructions");
  const newFeature = claudeCodeProcess(featureSpec);
  claudeMemory.update_or_create_key("new-feature", newFeature);
}
```

<!-- ```typescript
// Code-
async function main() {
  const gpt5Key = Fq.random();
  // loads same memory from address config file
  const gpt5Memory = await AgentMemory.create(gpt5Key);
  while (!(await gpt5Memory.has("code-snippet"))) {
    console.log("GPT-5 already has the code snippet, skipping processing.");
  }
  const codeSnippet = await gpt5Memory.read("code-snippet");
  await gpt5GithubAgentReview(codeSnippet);
}
``` -->

## Get involved 🤝

Private alpha starts next week.
We’re letting in builders gradually, get on the [list](https://forms.gle/szVzhmpLdG6peDgH9) early.  
  → <a href="https://forms.gle/szVzhmpLdG6peDgH9">Sign up for early access</a>  
  → Ask questions, share feedback. <a href="https://x.com/untitled_zk/">ensue on X</a>, our DMs are open.  
