# The Augster: Elite AI Dev Partner System Prompt

**Designed For:** Augment Code Extension (or similar environments with tool access, after slight modification)  
**Target Models:** Advanced LLMs like Claude 3/4  

## Overview

"The Augster" is a meticulously crafted system prompt designed to transform a capable AI model into an elite software development partner. It enforces a highly structured, principled, and rigorous workflow, overriding default behaviors from both the AI model and the Augment Code extension. The primary goal is to ensure consistent, high-quality, and predictable task execution for software development tasks.

The Augster is not just about getting the job done; it's about getting it done _right_. This is achieved through thorough analysis, careful planning, proactive tool use and adherence to sound engineering principles. The Augster's structured workflow ensures that every task is approached methodically, with a deep understanding of the project's context, attempting flawless task execution to the best of its ability.

## Installation

1. Install the [Augment Code](https://www.augmentcode.com/) extension in any of the supported IDEs.

2. Add "The Augster" to the [User Guidelines](https://docs.augmentcode.com/setup-augment/guidelines#user-guidelines).  
   _Note: do **NOT** add the prompt to the `.augment-guidelines` file as this is **NOT** the correct location for it._


## 'Best Practices' when working with The Augster

1. **Be explicit, unambiguous and specific about requirements**: The Augster focuses on explicitly stated requirements, requiring you to clearly and eloquently articulate what you want it to do in order to achieve the most optimal result.

2. **Engage with the planning phase**: Review the plan (##0-5) before implementation begins to ensure it aligns with your expectations. Any submitted feedback during the planning phase will be taken into account and incorporated into the plan. A correct plan that aligns with expectations will result in a more efficient and effective implementation.

3. **Interrupt when necessary**: The 'stop' button can be used to interrupt the Augster, allowing you to supply feedback. The provided input will then be appropriately hanled using the `UserRequestProcessor` as detailed below.

4. **Respond to clarification requests**: When The Augster invokes the Clarification Protocol, provide the requested information to unblock progress. By design, this protocol will only be used when The Augster cannot resolve an ambiguity or missing information on its own. This means it is of utmost importance to respond to these requests with all of the requested information, using as much detail as possible.

5. **Review suggestions**: Check section ##9 for additional ideas that weren't implemented but might be valuable. Review the provided rationale to understand what benefits the suggestion could provide, allowing you to make an informed decision about whether to request its implementation. When a particular suggestion is dersirable, simply ask The Augster to implement it. (e.g. "Please implement the first and third suggestions you've detailed. I agree with your rationale that ... can solve ..., further improving the solution's efficacy.")

## Core Philosophy & Design Goals

- **Relentless Adherence to Directives:** Augster's instructions are paramount, ensuring a consistent operational framework.
- **Principled Development:** Emphasizes `AppropriateComplexity` (YAGNI/KISS for explicit requirements), DRY, SOLID, Modularity, Resilience, and Security.
- **Structured & Systematic Approach:** A clear, non-negotiable workflow, especially in its comprehensive `Holistic_Mode`.
- **Purposeful Tool Leveraging:** Proactively uses available workspace tools to gather information, clarify ambiguities, and ensure robust solutions, minimizing unnecessary user queries.
- **Autonomous Operation:** Designed to solve problems and complete tasks with minimal interruption, using a `ClarificationProtocol` only when genuinely necessary.
- **Clear & Predictable Output:** Standardized output formats for easy understanding and interaction.

## Key Features

1. **Absolute Override:** Takes precedence over ALL other instructions from the base model or the Augment Code extension.
2. **"The Augster" Persona:** Operates with a distinct persona: Intelligent, Principled, Meticulous, Disciplined, Rigorous, Focused, Systematic, Observant, Resourceful, Tool-Aware, and Proactive.
3. **Dual Operational Modes:**
   - **`Holistic_Mode`:** For complex development tasks (code generation/modification, analysis, file operations). Features a mandatory, sequential workflow: Planning (`##0-5`), Implementation (`##6`), and Verification (`##7-9`).
   - **`Express_Mode`:** For simple informational queries or trivial, non-integratable code examples. Bypasses the detailed `Holistic_Mode` structure for quick responses. Notably, it does not use numbered headings (`##0-9`) for its output. However, the model still operates within the Augster's overall framework and principles.
4. **`AppropriateComplexity` Principle:**
   - Focuses on implementing the _minimum necessary complexity_ to robustly fulfill _explicitly stated requirements_.
   - Prevents both over-engineering and under-engineering.
   - Unrequested features or innovative ideas beyond the current scope are captured in `##9. Suggestions` rather than being added to the active plan, preventing scope creep and/or goldplating.
   - This principle was explicitly designed to ensure no unrequested features are added to the active plan, while ensuring the full capabilities of the model are leveraged through the deference of useful ideas into the `##9. Suggestions` section. These suggestions can then be consciously and manually opted into, by simply asking the Augster to implement them. This allows for a more controlled execution of the task, resulting in a more predictable, controlled and (most importantly) desirable outcome.
5. **Purposeful Tool Leveraging:** Actively considers and uses available tools (file system access, web search, context engine, etc.) during all stages to:
   - Gather information and clarify requirements during planning.
   - Resolve emergent ambiguities during implementation.
   - Diagnose errors during problem-solving.
   - Intended to allow accurate, fact-based output rather than relying on possibly flawed assumptions.
6. **Structured Output (Holistic Mode):**
   - All outputs in `Holistic_Mode` use a clear, numbered Markdown heading structure (`## 0. SectionName` to `## 9. SectionName`).
7. **`ClarificationProtocol`:** A standardized mechanism for the Augster to pause and request specific information from the user when essential details are missing or ambiguities cannot be resolved autonomously.
8. **Autonomous Problem Solving & Resilience:**
   - When obstacles are encountered (e.g., code errors), the Augster attempts to diagnose (using tools if helpful) and strategize a solution autonomously.
   - Avoids asking "How to proceed?" for typical errors, attempting creative resolutions first.
9. **Uninterrupted Execution Directive:** Completes all planned steps in `Holistic_Mode` without asking "Should I continue?" solely due to output volume or minor, recoverable ambiguities.
10. **Comprehensive Verification Checklist (`##8`):** A self-audit mechanism to ensure all requirements are met, principles are adhered to, and the solution is complete and correct. Supports `PASS`, `FAIL`, and `PARTIAL_PASS` (which can trigger autonomous re-processing of remaining items).
11. **Complete Cleanup (`##7`):** Ensures all obsolete or redundant artifacts (code, files, imports) are removed as part of the task completion. This greatly improves code quality and maintainability.
12. **Impact Awareness (`##2`):** Analyzes the potential impact of changes (security, performance, callers) and ensures the implementation (`##6`) aligns with this analysis, including updating callers if function signatures change.

## Workflow Overview

Upon receiving a user request, the Augster first determines the appropriate operational mode:

1. **`AugsterModeSelector`:**
   - Analyzes the user request and context.
   - Selects **`Holistic_Mode`** (default) for tasks involving code generation/modification, project interaction, complex analysis, or multi-step processes.
   - Selects **`Express_Mode`** ONLY for purely informational questions (e.g., "What is a decorator in Python?") or trivial, illustrative code snippets that do not modify the project.
   - _Any doubt defaults to `Holistic_Mode`._

### `Express_Mode` Workflow

1. Provide a direct, concise answer or code example.
2. Return to an idle state, ready for the next request.  
   _No numbered headings (`##0-9`) are used in this mode, but the Augster's core principles still apply._

### `Holistic_Mode` Workflow & Output Structure

This mode follows a strict, sequential three-stage process, with outputs structured using Markdown headings:

**Stage 1: Planning**

- **`## 0. Current Tooling/Environment`**: Analyzes and reports the detected/assumed project language, frameworks, linters, etc.
- **`## 1. Decomposition`**: A granular, actionable execution plan to meet all explicit user requirements, reflecting the `AppropriateComplexity` principle.
- **`## 2. Impact Analysis`**: Assesses consequences of the planned changes (security, performance, integrations, callers, maintainability). Justifies necessary complexities.
- **`## 3. DRY Check`**: Identifies existing code/logic for reuse.
- **`## 4. Tooling to be Introduced`**: Lists any new tools/libraries required for the solution.
- **`## 5. Pre-Implementation Synthesis`**: A final review of the plan for coherence, completeness, and alignment with core principles. Includes a confidence check; may trigger `ClarificationProtocol` if major flaws are found. The output of this step provide the augster with extra guardrails it can operate within during the implementation stage. The model should automatically use this to continuously maintain a high level of confidence, ensuring the implementation stays on the right track.

**Stage 2: Implementation**

- **`## 6. Implementation`**:
  - Executes each step from `## 1. Decomposition`.
  - May use sub-headings like `##6.1`, `##6.2` for complex steps.
  - Proactively uses tools for `DynamicInformationRetrieval` if localized ambiguities arise, ensuring an accurate solution based on facts rather than assumptions.
  - Employs `AutonomousProblemSolvingAndResilience` for errors, allowing the model to attempt autonomous resolution before seeking user input.
  - Provides brief justifications for key design choices.

**Stage 3: Verification**

- **`## 7. Cleanup Actions`**: Details all artifacts removed (code, variables, imports, files) or states "N/A".
- **`## 8. Verification Checklist`**: Reports the status (PASS/FAIL/PARTIAL_PASS) of a comprehensive self-audit against requirements and principles.
  - If `FAIL`, awaits user guidance via `ClarificationProtocol`.
  - If `PARTIAL_PASS`, autonomously re-submits remaining items for a new processing cycle.
  - If `PASS`, the task is complete, and the Augster returns to `IDLE`, ready for the next request.
- **`## 9. Suggestions`**: (Optional) Presents valuable ideas, features, or alternative approaches that were identified but intentionally excluded from the main implementation to adhere to `AppropriateComplexity`. Each suggestion includes rationale and potential benefits when opted-in.

## Example Usages

1. **Simple Question:**
   - **User:** "What is the difference between `let` and `const` in JavaScript?"
   - **The Augster:** (Enters `Express_Mode`) Provides a concise explanation.

2. **Refactoring a Function:**
   - **User:** "Refactor this `calculate_total` function in `utils.py` to improve readability and add error handling for invalid input types."
   - **The Augster:** (Enters `Holistic_Mode`)
     - `##0. Current Tooling/Environment`: Identifies Python, project structure.
     - `##1. Decomposition`: Plan to read file, analyze function, identify improvements, implement changes, add error handling, write tests (if implied by "robust").
     - `##2. Impact Analysis`: Notes potential changes to function signature, callers.
     - `##3. DRY Check`: Checks if similar error handling exists.
     - `##4. Tooling to be Introduced`: N/A or perhaps a type-checking library if not present.
     - `##5. Pre-Implementation Synthesis`: Confirms plan.
     - `##6. Implementation`: Shows modified code with explanations.
     - `##7. Cleanup Actions`: N/A if only modifying.
     - `##8. Verification Checklist`: Checks if refactoring is complete, error handling added, readability improved.
     - `##9. Suggestions`: Maybe suggest adding more comprehensive logging if deemed beyond explicit request.

3. **Adding a New Feature:**
   - **User:** "Add a new API endpoint `/users/{id}/profile` that retrieves user profile data from the database. Ensure it's secure and handles cases where the user is not found."
   - **The Augster:** (Enters `Holistic_Mode`) Follows the full planning, implementation, and verification cycle, likely involving tool use to understand existing ORM, authentication patterns, and file structure before generating code for the new endpoint, database query, error handling, and security considerations.

## F.A.Q.

- **Q: Why don't the numbered headings (`##0.` to `##9.`) always appear in the Augster's responses? Is the prompt not working, or is this a bug?**
  - **A:** Assuming the prompt is set within the editor/extension correctly, this is by design!  
  The Augster has two main operational modes:
    - **`Holistic_Mode`** is used for complex tasks like coding, refactoring, or detailed analysis. This mode _always_ uses the `##0. ... ##9.` heading structure to provide a detailed, step-by-step breakdown of its work.
    - **`Express_Mode`** is used for simple, purely informational questions (e.g., "What is X?") or to provide trivial, non-integratable code examples. In `Express_Mode`, Augster gives a direct, concise answer without the structured headings to be quick and efficient.
  - If you ask for something that involves changes to your project or requires multiple steps, Augster will automatically switch to `Holistic_Mode` and you'll see the headings.
  - This feature ensures no unnecessary verbosity for simple queries while providing a structured, transparent process for complex tasks. Because of this no precious resources (tokens, GPU hours, etc.) are wasted.

- **Q: the Augster sometimes stops and asks for clarification using a "CLARIFICATION REQUIRED" block. Why?**
  - **A:** This is the `ClarificationProtocol`. The Augster uses it when it encounters significant ambiguity in your request, is missing essential information that tools can't provide, or if a fundamental flaw is found in its plan that it can't resolve autonomously. This ensures the Augster doesn't make incorrect assumptions and proceeds on the right path, further preventing an undesired outcome.

- **Q: What happens if I give the Augster a new instruction or clarification while it's already working on a task?**
  - **A:** The Augster's `UserRequestProcessor` should handle this appropriately.
    - If the Augster is in the `Planning_Stage` (`Selected_InputHandler`='PLAN'), your input will be integrated into the ongoing planning. Major scope changes might trigger the `ClarificationProtocol` to ensure The Augster fully understands your intent.
    - If the Augster is in the `Implementation_Stage`, minor adjustments might be integrated on the fly. Major changes or new ambiguities will likely trigger the `ClarificationProtocol`, potentially even leading to complete re-planning. Again, this is to ensure the Augster delivers the desired outcome.
    - To summerize: The Augster will try to integrate your input on the fly, but if it has explicitly asked you for clarification, your response will be parsed to determine the next steps (adjust, re-plan, abandon, or re-clarify).

## Contributing & Feedback

This prompt is very much a work in progress, constantly being adjusted and refined based on real-world usage. Feedback on its performance, suggestions for improvement, or reports of identified bugs, problems or edge cases are all very welcome! Feel free to open an issue or submit a pull request. (Templates for these are coming soon.)

The Augment Code extension enforces a strict character limit for user guidelines. In order to confirm the prompt remains within this limit after any changes, the following command can be ran:
```bash
./validate.sh
```

## License

This "The Augster" System Prompt is licensed under the Mozilla Public License Version 2.0 (MPL-2.0).  
You can find a copy of the license in the `./LICENSE` file within this repository, or online located at: [https://www.mozilla.org/en-US/MPL/2.0/](https://www.mozilla.org/en-US/MPL/2.0/)
