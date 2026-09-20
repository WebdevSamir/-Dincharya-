# Dincharya — An Adaptive, Context-Aware and Personalized Personal Planning Framework

> **Research prototype / experimental framework for adaptive personal planning, constraint-aware scheduling, behavioral duration learning, and explainable replanning.**

Dincharya (दिनचर्या) is being developed as a research-oriented personal planning framework rather than only a conventional productivity application. The project investigates how a planning system can combine task constraints, contextual information, user preferences, historical execution behavior, and adaptive replanning to produce realistic daily schedules while preserving user control and explainability.

**Repository:** https://github.com/WebdevSamir/-Dincharya-

---

## 1. Vision

Most digital planners are effective at recording tasks but comparatively limited at understanding whether a plan is realistic for a particular person.

Dincharya explores a different direction:

**Plan → Execute → Observe → Learn → Adapt → Replan**

The long-term objective is to develop a framework that can learn from a user's actual execution behavior and improve future planning without turning the system into an opaque autonomous decision-maker.

---

## 2. Central Research Problem

The central research question is:

> **How can an adaptive personal planning framework use task constraints, contextual information, user preferences, and historical execution behavior to generate realistic daily plans and continuously adapt them while preserving user control and explainability?**

The project therefore treats planning as a combination of:

- Task representation
- Constraint satisfaction
- Scheduling and optimization
- Personalization
- Behavioral learning
- Context awareness
- Dynamic replanning
- Human-computer interaction
- Explainability and user control

---

## 3. Research Questions

### RQ1 — Planning
How can personal tasks be represented and scheduled while respecting time, priority, dependency, availability, and deadline constraints?

### RQ2 — Realism
How accurately can historical execution data improve task-duration estimation for an individual user?

### RQ3 — Personalization
How can individual preferences and behavioral patterns influence planning without compromising hard constraints?

### RQ4 — Adaptation
How should a planner respond when actual execution deviates from the original schedule?

### RQ5 — Explainability
How can schedule changes and recommendations be explained in a way that users can understand and control?

### RQ6 — Evaluation
Which objective and human-centered metrics are appropriate for evaluating adaptive personal planning systems?

---

## 4. Research Objectives

### Primary Objective

Design and evaluate an adaptive personal planning framework that combines constraint-aware scheduling with behavioral duration learning and context-aware replanning.

### Specific Objectives

1. Develop a structured task model.
2. Represent hard and soft scheduling constraints.
3. Implement a rule-based planning baseline.
4. Implement a constraint-aware scheduling baseline.
5. Model individual task-duration behavior.
6. Compare estimated and actual execution duration.
7. Incorporate historical behavior into future estimates.
8. Detect schedule deviations during execution.
9. Generate alternative recovery plans after disruptions.
10. Provide explanations for important planning decisions.
11. Preserve user override and manual control.
12. Establish reproducible evaluation procedures.
13. Measure planning, execution, adaptation, and human-centered outcomes.
14. Produce research artifacts suitable for academic publication.

---

## 5. Research Positioning

Dincharya should be evaluated as a progression of increasingly capable planners:

1. **Manual baseline**
2. **Rule-based planner**
3. **Constraint-based planner**
4. **Personalized planner**
5. **Adaptive planner**

This progression is important because each stage creates a measurable baseline for the next stage.

The project must not claim that a later method is better simply because it is more sophisticated. Improvement must be demonstrated experimentally.

### Research Integrity Principle

> **Implemented ≠ Evaluated ≠ Improved ≠ Proven**

A feature being implemented does not establish that it works better. All claims of improvement should be supported by defined experiments and measurements.

---

## 6. Conceptual Architecture

The high-level architecture is:

```text
                 ┌─────────────────────┐
                 │      User Model     │
                 │ preferences/history │
                 └──────────┬──────────┘
                            │
┌───────────────┐   ┌───────▼────────┐   ┌───────────────┐
│  Task Model   │──►│ Planning Engine │◄──│ Context Model │
└───────────────┘   └───────┬────────┘   └───────────────┘
                            │
                   ┌────────▼────────┐
                   │ Constraint /    │
                   │ Optimization    │
                   └────────┬────────┘
                            │
                   ┌────────▼────────┐
                   │ Daily Plan      │
                   └────────┬────────┘
                            │
                       User Review
                            │
                       Execution
                            │
                   ┌────────▼────────┐
                   │ Execution       │
                   │ Telemetry       │
                   └────────┬────────┘
                            │
                   ┌────────▼────────┐
                   │ Behavior /      │
                   │ Error Model     │
                   └────────┬────────┘
                            │
                     Personalization
                            │
                            └──────► Future Planning
```

---

## 7. Core Planning Loop

The fundamental learning loop is:

```text
Estimated Duration
        ↓
Schedule
        ↓
Execute
        ↓
Actual Duration
        ↓
Estimation Error
        ↓
Personal History
        ↓
Updated Duration Model
        ↓
Future Planning
```

For a task (i):

```text
error_i = actual_duration_i - estimated_duration_i
```

Useful evaluation statistics include:

- Mean Absolute Error (MAE)
- Median Absolute Error
- Signed estimation bias
- Relative error
- Error distribution by task category
- Error distribution across contexts

---

## 8. Task Model

Each task should eventually support attributes such as:

- Unique identifier
- Title
- Description
- Category
- Priority
- Estimated duration
- Actual duration
- Earliest start time
- Deadline
- Preferred time window
- Dependencies
- Location/context
- Required resources
- Energy or focus requirement
- Recurrence
- Hard constraints
- Soft constraints
- Completion status
- Postponement history
- User notes

A task should be treated as a structured planning object rather than simply a text entry.

---

## 9. Constraint Model

Dincharya should distinguish between **hard constraints** and **soft constraints**.

### Hard Constraints

Violating these should normally make a candidate schedule infeasible.

Examples:

- Task cannot occur after its deadline.
- Two non-overlapping tasks cannot occupy the same time.
- A fixed appointment must remain fixed.
- A dependency must be satisfied before a dependent task begins.

### Soft Constraints

These influence preference but can be relaxed when necessary.

Examples:

- Preferred working hours
- Preferred task ordering
- Preferred break frequency
- Preferred focus periods
- User-defined priorities

This distinction enables controlled optimization rather than simplistic scheduling.

---

## 10. Planning Strategy Progression

### Stage 1 — Manual Baseline

The user creates and schedules tasks manually.

Purpose:

- Establish baseline behavior.
- Measure manual planning effort.
- Provide a comparison condition.

### Stage 2 — Rule-Based Planner

Uses deterministic rules such as:

- Priority
- Deadline proximity
- Available time
- Task duration
- Fixed events

Purpose:

- Establish an interpretable automated baseline.

### Stage 3 — Constraint-Based Planner

Introduces formal constraints and optimization.

Purpose:

- Test feasibility and schedule quality under interacting constraints.

### Stage 4 — Personalized Planner

Uses user-specific preferences and historical behavior.

Purpose:

- Move from generic planning toward individual planning.

### Stage 5 — Adaptive Planner

Continuously incorporates execution feedback and dynamically replans.

Purpose:

- Evaluate whether the system can recover from real-world deviations while preserving constraints and user control.

---

## 11. Adaptive Replanning

A schedule should not be considered static.

When a deviation occurs:

```text
Deviation Detected
       ↓
Recalculate Availability
       ↓
Identify Affected Tasks
       ↓
Protect Hard Constraints
       ↓
Generate Candidate Recovery Plans
       ↓
Score Alternatives
       ↓
Explain Changes
       ↓
User Review / Override
       ↓
Updated Schedule
```

Possible deviations include:

- Task takes longer than estimated.
- Task finishes early.
- Task is skipped.
- New urgent task appears.
- Fixed event changes.
- Available time changes.

The system should avoid unnecessary schedule changes and preserve unaffected commitments where possible.

---

## 12. Explainability and User Control

Adaptive planning must remain understandable.

When a plan changes, the system should be able to communicate reasons such as:

- A previous task exceeded its estimate.
- A deadline became closer.
- A fixed appointment reduced available time.
- A dependency prevented an alternative ordering.
- Historical execution data changed the duration estimate.

The user should be able to:

- Accept a recommendation.
- Reject it.
- Modify the schedule.
- Lock important tasks.
- Override preferences.
- Inspect relevant reasoning.

The goal is **decision support**, not uncontrolled automation.

---

## 13. Evaluation Framework

Dincharya will eventually evaluate the system across several dimensions.

### 13.1 Planning Performance

- Planning time
- Schedule feasibility
- Constraint violations
- Deadline adherence
- Objective-function quality

### 13.2 Execution Performance

- Task completion rate
- On-time completion rate
- Postponement rate
- Schedule deviation
- Number of unfinished tasks

### 13.3 Duration Estimation

- MAE
- Median absolute error
- Signed bias
- Relative error

### 13.4 Adaptation

- Replanning time
- Recovery success
- Post-disruption constraint violations
- Number of changed tasks
- Magnitude of schedule changes

### 13.5 Human Factors

Potential measures include:

- Usability
- Perceived workload
- Perceived control
- Trust
- Satisfaction
- Explanation usefulness

Human evaluation should use established instruments where appropriate and follow applicable research-ethics requirements.

---

## 14. Methodology

The project is aligned with a **Design Science Research-oriented** development cycle:

```text
Problem Identification
        ↓
Research Investigation
        ↓
Artifact Design
        ↓
Implementation
        ↓
Experimentation
        ↓
Evaluation
        ↓
Reflection
        ↓
Artifact Refinement
```

The final research study should document:

- Research hypotheses where appropriate
- Experimental variables
- Baselines
- Datasets
- Experimental configurations
- Evaluation metrics
- Statistical procedures
- Limitations
- Reproducibility procedures

The current literature collection is an **initial literature review**, not yet a formal systematic review. Before publication, a systematic search should define databases, search strings, inclusion/exclusion criteria, screening procedures, quality assessment, and synthesis methods.

---

## 15. Privacy and Ethics

Because the framework may learn from personal behavior, privacy is a core design requirement.

Principles:

- Data minimization
- Explicit user control
- Transparent data collection
- Local-first processing where practical
- Secure storage
- Export capability
- Deletion capability
- Anonymization or pseudonymization for research datasets
- Clear distinction between predictions and observed facts
- Appropriate ethics approval for human-participant studies

No personal behavioral dataset should be published without appropriate consent and anonymization.

---

## 16. Proposed Repository Structure

```text
-Dincharya-/
├── README.md
├── LICENSE
├── CONTRIBUTING.md
│
├── docs/
│   ├── research/
│   │   ├── literature-review.md
│   │   ├── research-plan.md
│   │   ├── evaluation-plan.md
│   │   └── methodology.md
│   │
│   └── architecture/
│       ├── system-architecture.md
│       ├── task-model.md
│       └── planning-engine.md
│
├── src/
│   ├── frontend/
│   ├── planner/
│   ├── models/
│   ├── personalization/
│   └── services/
│
├── tests/
│
├── experiments/
│   ├── baselines/
│   ├── datasets/
│   ├── configurations/
│   └── results/
│
└── research/
    ├── experiment-log.md
    └── papers.md
```

The exact structure may evolve as implementation requirements become clearer.

---

## 17. Git Branch Strategy

Recommended branch organization:

```text
main
│
├── develop
│
├── feature/ui
├── feature/task-engine
├── feature/planning-engine
├── feature/constraint-engine
├── feature/personalization
├── feature/adaptive-planner
│
├── research/literature
├── research/baselines
├── research/evaluation
└── research/experiments
```

### Principle

Every major research or engineering change should be traceable to:

- A problem
- A hypothesis or requirement
- An implementation
- An experiment
- A result

This will make future branches and parallel development easier to synchronize.

---

## 18. Research Roadmap

### Phase 0 — Research Foundation

- Literature review
- Research gap analysis
- Research questions
- Requirements
- Architecture
- Data model
- Evaluation protocol

### Phase 1 — MVP

- User interface
- Task creation
- Task editing
- Daily schedule
- Completion tracking
- Basic persistence

### Phase 2 — Baseline Planning

- Rule-based scheduling
- Priority handling
- Deadline handling
- Duration estimation
- Baseline experiments

### Phase 3 — Constraint Planning

- Hard constraints
- Soft constraints
- Dependencies
- Time windows
- Optimization objectives
- Feasibility evaluation

### Phase 4 — Behavioral Personalization

- Execution history
- Duration error tracking
- User preference modeling
- Individual duration estimation

### Phase 5 — Adaptive Planning

- Deviation detection
- Dynamic replanning
- Recovery-plan generation
- Explanation generation
- User approval/override

### Phase 6 — Experimental Framework

- Reproducible datasets
- Experiment configurations
- Baseline comparisons
- Automated metric collection
- Statistical analysis

### Phase 7 — Human Evaluation

- Study protocol
- Ethics approval where required
- Participant recruitment
- Usability evaluation
- Workload and control measures
- Qualitative feedback

### Phase 8 — Publication

- Final experiments
- Results
- Discussion
- Limitations
- Reproducibility package
- Research paper

---

## 19. Publication Direction

### Working Title

**Dincharya: An Adaptive Personal Planning Framework for Constraint-Aware Scheduling and Behavioral Duration Learning**

Potential contribution areas:

1. A structured model for adaptive personal planning.
2. A progression from rule-based to adaptive planning.
3. A constraint-aware scheduling architecture.
4. Individual task-duration learning.
5. Context-aware dynamic replanning.
6. Explainable schedule adaptation.
7. An experimental framework for evaluating personal planning systems.

These are **research objectives and intended contributions**, not claims of novelty or superiority. Novelty must be established through a formal literature review and comparison with existing systems.

---

## 20. Initial Literature Foundation

The initial research direction is informed by work including:

1. Refanidis, I., & Alexiadis, A. (2011). *Deployment and Evaluation of SelfPlanner, an Automated Individual Task Management System*. Computational Intelligence, 27(1), 41–59. DOI: 10.1111/j.1467-8640.2010.00371.x

2. *A Constraint Programming Model for Making Recommendations in Personal Process Management: A Design Science Research Approach*. Decision Support Systems, 152, 113665 (2022). DOI: 10.1016/j.dss.2021.113665

3. Ahmetoglu, S., Brumby, D. P., & Cox, A. L. (2024). *Bridging the Gap Between Time Management Research and Task Management App Design: A Study on the Integration of Planning Fallacy Mitigation Strategies*. CHIWORK 2024. DOI: 10.1145/3663384.3663404

4. Takahashi, T. (2022). *The Relationship between the Planning Fallacy and Estimates of Task Duration*. AAOS Transactions, 11(1), 8–13. DOI: 10.11207/aaostrans.11.1_8

5. Hauptman, A., Flathmann, C., & McNeese, M. (2024). *Adapting to the Human: A Systematic Review of a Decade of Human Factors Research on Adaptive Autonomy*. Applied Ergonomics, 120, 104336. DOI: 10.1016/j.apergo.2024.104336

This list is a starting point rather than a complete literature review.

---

## 21. Immediate Next Steps

The recommended engineering/research sequence is:

1. Finalize the formal research specification.
2. Establish the repository documentation structure.
3. Define the canonical task and constraint schemas.
4. Implement the manual baseline.
5. Implement the deterministic rule-based planner.
6. Create a reproducible synthetic dataset.
7. Define evaluation scripts and metrics.
8. Implement the constraint-based planner.
9. Add execution telemetry.
10. Add personalized duration estimation.
11. Implement adaptive replanning.
12. Run controlled baseline comparisons.
13. Conduct human-centered evaluation where appropriate.
14. Prepare the publication artifact.

---

## 22. Long-Term Vision

The long-term goal is not simply to build another to-do list.

Dincharya aims to investigate a broader question:

> **Can a personal planning system become progressively more realistic by learning how an individual actually works, while remaining transparent, controllable, and experimentally measurable?**

The intended outcome is a reproducible research prototype that can support future experimentation in:

- Personal scheduling
- Human-centered AI
- Constraint optimization
- Adaptive systems
- Time-management technology
- Personalized recommendation
- Explainable planning
- Human-AI interaction

---

## 23. Development Principle

Dincharya should be developed as both:

**A usable software system**

and

**A reproducible research artifact.**

Every important feature should therefore have two perspectives:

```text
Engineering Question:
Does it work?

Research Question:
How do we know it works, compared with what, and under which conditions?
```

This distinction will guide the project from prototype implementation toward publishable research.

---

## License

License to be finalized as the research and distribution requirements become clear.
