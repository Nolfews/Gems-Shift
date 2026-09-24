# Development Guidelines

This document defines the development conventions used throughout **Gems Shift**.
The goal is to keep the project consistent, readable, and easy to maintain, especially when working with Unreal Engine Blueprints.

---

## 1. Commit Convention

We use a simplified version of **Conventional Commits**.

### Format

```text
<type>: <short description>
```

### Commit Types

| Type       | Usage                                                          |
| ---------- | -------------------------------------------------------------- |
| `feat`     | Add a new feature or gameplay mechanic                         |
| `fix`      | Fix a bug                                                      |
| `refactor` | Improve or reorganize existing logic without changing behavior |
| `art`      | Add or modify visual assets, animations, VFX, materials, etc.  |
| `audio`    | Add or modify sounds or music                                  |
| `level`    | Add or modify level design                                     |
| `ui`       | Add or modify UI elements                                      |
| `docs`     | Add or modify documentation                                    |
| `chore`    | Project maintenance or configuration                           |
| `test`     | Add or modify tests or test-related content                    |

### Commit Guidelines

* Keep commits focused on a single purpose.
* Use the imperative form.
* Keep the description short and clear.
* Avoid mixing unrelated changes in the same commit.
* Do not use commits such as `update`, `stuff`, `changes`, or `final`.

---

# 2. Unreal Engine Blueprint Conventions

Gems Shift uses **Blueprints exclusively** for gameplay programming.

Blueprints must therefore be organized consistently to remain readable and maintainable.

The following conventions apply to all gameplay Blueprints.

---

## 2.1 Blueprint Organization

Blueprint logic must be separated into clearly identifiable sections.

Each major system should have its own **Comment Box**.

Example:

```text
[Initialization]

[Input]

[Movement]

[Interaction]

[Animation]

[Abilities]

[Elemental Logic]

[UI]

[Debug]
```

Do not place unrelated logic inside the same section.

---

## 2.2 Comment Box Color Convention

Each Blueprint section uses a predefined color.

| Section         | Color              | Code HexsRGB |Purpose                                                 |
| ----------------| ------------------ | ------------ | ------------------------------------------------------ |
| Initialization  | Blue               |   0000FFBF   | Begin Play, initialization and setup                   |
| Input           | Purple             |   C400FFBF   | Player input and input events                          |
| Movement        | Orange             |   FF8100BF   | Movement, jumping and locomotion                       |
| Interaction     | Red                |   FF0000BF   | Interactions with objects, NPCs and environment        |
| Animation       | Green              |   00FF00BF   | Animation logic, montages and animation state handling |
| Abilities       | Yellow             |   FFF800BF   | Player abilities and special actions                   |
| Elemental Logic | Pink               |   FF81C3BF   | Element transformations and elemental-specific logic   |
| UI              | White / Light Gray |   D7D7D7BF   | UI communication and HUD logic                         |
| Audio           | Brown              |   C97F00BF   | Sound effects and audio triggers                       |
| Debug           | Dark Gray          |   3A3A3ABF   | Debugging and development-only logic                   |

> **Important:** Colors are used for organization only. The section title must always clearly describe the purpose of the logic.

---

## 2.3 Blueprint Layout

Blueprint execution flow should generally move from **left to right**.

Organize nodes so that:

```text
Event → Logic → Result
```

is easy to follow.

Avoid excessive wire crossings whenever possible.

### Example

```text
Event
  ↓
Validation
  ↓
Gameplay Logic
  ↓
Animation / VFX
  ↓
Result
```

When a Blueprint becomes too large, separate the logic into:

* Functions
* Macros when appropriate
* Custom Events
* Child Blueprints
* Actor Components

Do not keep adding nodes to an already difficult-to-read graph.

---

## 2.4 Comments

Comments should explain **why** something is done when the logic is not immediately obvious.

Avoid comments that simply repeat the node name.

Comments should be:

* Short
* Specific
* Written in English
* Focused on intent rather than describing every node

---

## 2.5 Variables and Functions

Use descriptive English names.

Good:

```text
CurrentElement
FireGem
IsTransforming
CanInteract
InteractionTarget
TransformationDuration
```

Avoid:

```text
Thing
Temp
Test
NewVar
MyVariable
```

Boolean variables should generally use a clear prefix:

```text
IsTransforming
IsGrounded
CanInteract
HasFireGem
```

Functions should describe an action:

```text
TransformToElement
ActivateFireAbility
CheckInteraction
UpdateElementUI
ResetTransformation
```

---

## 2.7 Element System

Because elemental transformation is a core mechanic of **Gems Shift**, elemental logic should remain clearly separated from generic player logic.

Whenever possible, structure it around the five available elements:

```text
Fire
Water
Wind
Electricity
Earth
```

Example:

```text
[Elemental Logic]
    ├── Get Current Element
    ├── Transform
    ├── Remove Element
    └── Element Validation

[Fire]
    ├── Fire Ability
    ├── Fire Interaction
    └── Fire VFX

[Water]
    ├── Water Ability
    ├── Water Interaction
    └── Water VFX
```

This makes it easier to add or modify elements without affecting unrelated systems.

---

## 2.8 General Rule

> **If a developer opens a Blueprint they have never seen before, they should be able to understand its structure without asking another developer.**

When adding new logic, always ask:

1. Which system does this belong to?
2. Which Comment Box should contain it?
3. Is the logic easy to follow from left to right?
4. Does the variable/function name explain its purpose?
5. Should this logic be extracted into a function or component?

Consistency is more important than personal preference.
