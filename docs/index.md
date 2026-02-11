# Introduction

## Overview

Domino provides a **systemic and engine-agnostic gameplay framework**, designed to help build complex mechanics while allowing dynamic behaviors to emerge naturally, without relying on rigid or heavily scripted logic.

Instead of defining hard-coded interactions between actors, the framework is built around **stimuli**, **actions**, and **reactions** that respond to context and state. This approach enables the creation of modular, reusable, and interconnected systems, encouraging emergent gameplay to arise from simple, well-defined rules.

The framework is intentionally **genre-agnostic** and can be used for AI, environmental interactions, puzzles, combat, stealth systems, or experimental gameplay. It is suitable both for rapid prototyping and for integration into more advanced production pipelines.

---

## Philosophy and Goals

The core goals of the plugin are to:

- Reduce tight coupling between gameplay systems
- Minimize bespoke scripting for individual interactions
- Encourage rule-based design over case-by-case logic

The plugin is not meant to replace Unreal Engine’s native systems, but rather to act as a **systemic logic layer** that integrates naturally with existing Unreal workflows.

---

## Systemic Gameplay Use Cases

This framework is well suited for systemic game design, as seen in titles like _Deus Ex_, _Dishonored_, _Prey_, _Thief_, or _Zelda: Breath of the Wild / Tears of the Kingdom_.

In these games, interactions are driven by shared rules rather than hard-coded actor-to-actor logic. For example:

- A burning object emits a **Burning** stimulus → flammable actors accumulate heat.
- A metal object emits a **Conductive** stimulus → reacts to electricity.
- A wet surface modifies how **Electric** stimuli are interpreted.

Instead of scripting specific interactions between actors, systems emit stimuli that other systems interpret and respond to. This rule-based approach enables modular design, cleaner scalability, and naturally emergent gameplay.
