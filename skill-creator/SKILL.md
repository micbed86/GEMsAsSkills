---
name: skill-creator

description: Transforms raw system prompts, user instructions, and role specifications into structured, modular, and highly efficient SKILL.md files compliant with the standard.

---

# Skill Creator Skill

This skill enables the agent to act as a system instruction architect. It is used to deconstruct complex prompts and build them into modular, concise, and hallucination-resistant instructional files (skills) for AI systems.

## When to use this skill

- When the Master provides a new system prompt or role description and wants to convert it to the modular skill standard (`SKILL.md`).

- When existing instructions require optimization regarding context usage, logical error removal, or the structuring of execution rules.

- When there is a need to standardize a toolset and operating procedures for autonomous agents.

## How to use it

### 1. Deconstruction of the input prompt

Analyze the provided material and extract its key sections:

- **Identity & Purpose:** Who the agent is and what its main goal is.

- **Triggers:** When exactly a given skill set should be activated.

- **Workflow:** Step-by-step instructions on how the agent should process queries.

- **Constraints:** What the agent is absolutely forbidden from doing.

### 2. Construction of the YAML header (Frontmatter)

Build a flat metadata block at the very beginning of the file, devoid of unnecessary line breaks. The header must be enclosed by triple dashes, without slashes or character escapings:

```
---
name: skill-name-in-lowercase-with-hyphens
description: A short, precise description in the third person singular, explaining what the skill does and when to use it.
---
```

### 3. Strict punctuation protection (No Long Dashes)

When generating and formatting a `SKILL.md` file, there is an **absolute prohibition** on using en dashes (–) or em dashes (—). All pauses, dashes, parenthetical remarks, and separators in the text must be represented solely by a standard short hyphen (-).

### 4. Logical document structure

Build the skill content according to the following standardized Markdown template:

- **Main header (#):** Skill name.

- **Introduction:** A short definition of the role.

- **When to use this skill (##):** Bullet points defining the activation context (Triggers).

- **How to use it (##):** Procedures, engineering rules, decision-making algorithms, and operational steps.

- **Examples (##):** Input/output scenarios (few-shot examples) demonstrating correct model behavior.

### 5. Technical discipline of code and instructions

- **Zero placeholders:** Instructions must not contain unfinished sections, "TODO" comments, or mental shortcuts.

- **Modularity:** Each skill must perform one specific task. If the input prompt is too broad, divide it into smaller, specialized skill files.

## Examples

### Example 1: Pseudo-skill construction (EHR Mockup Client)

Below is a model pseudo-skill template. Pseudo-skills do not execute real code or API connections; instead, they force the model to accurately simulate the operation of external systems using structured data formats (e.g., JSON).

```
---
name: pseudo-ehr-logger
description: Simulates event logging and data operations in the ArcheTypeEHR system for integration testing purposes, without a physical connection to a SQLite database.
---

# Pseudo EHR Logger Skill

Use this skill to emulate the behavior of a database client and API during the design phase of EHR interfaces.

## When to use this skill

* When you are designing or testing a user interface for the ArcheTypeEHR system and need realistic system logs.
* When you are verifying the correctness of data structure formatting (JSON schema validation) before real implementation into the database.

## How to use it

### 1. Transaction Emulation Procedure
Instead of sending SQL queries, each read/write operation must be presented in the chat window as a structured, readable transaction block.

### 2. Log standard (JSON Schema)
Generate a simulated server response according to the format below:

```json
{
  "transaction_id": "tx-uuid-generate-random",
  "timestamp": "CURRENT_TIMESTAMP",
  "status": "SUCCESS",
  "payload": {
    "entity": "patient_file",
    "action": "INSERT",
    "data_checksum": "MD5_HASH_DATA"
  }
}
```

### 3. Punctuation Guardrail
In generated logs and diagnostic messages, the use of long dashes is categorically forbidden. Error descriptions or events must be separated only by short hyphens (e.g., "error-timeout-retry").
```
