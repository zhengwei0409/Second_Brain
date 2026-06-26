# Software Testing Curriculum

> Self-study path for a Year 3 CS student.
> Language-agnostic. Balanced theory + practice.
> Each module = ONE new idea. Every concept is searchable / flashcard-ready.

---

## 1. Foundations

### [[1.1 — Why Software Fails]]

**Learning Objectives:**
- Understand why software produces incorrect behavior.

**Key Concepts:**
- Error
- Fault / defect
- Failure
- Error → Fault → Failure chain
- Cost of late defects

**Scope:**
- Included: vocabulary of failure, why testing exists.
- Not required yet: how to write or run tests.

---

### [[1.2 — What Is Software Testing]]

**Learning Objectives:**
- Define testing as evidence-gathering about software quality.

**Key Concepts:**
- Verification vs validation
- Expected vs actual behavior
- Testing vs debugging
- "Testing shows presence of bugs"
- Quality assurance

**Scope:**
- Included: definition and purpose of testing.
- Not required yet: test types, tools.

---

### [[1.3 — Test Case Anatomy]]

**Learning Objectives:**
- Describe the parts that make up one test.

**Key Concepts:**
- Input / precondition
- Expected output
- Actual output
- Pass / fail criteria
- Assertion

**Scope:**
- Included: structure of a single test case.
- Not required yet: automation, frameworks.

---

### [[1.4 — Arrange-Act-Assert]]

**Learning Objectives:**
- Structure a test in three clear phases.

**Key Concepts:**
- Arrange (setup)
- Act (execute)
- Assert (verify)
- AAA pattern
- Single behavior focus

**Scope:**
- Included: standard layout for readable tests.
- Not required yet: setup/teardown lifecycle.

---

## 2. Levels of Testing

### [[2.1 — Unit Testing]]

**Learning Objectives:**
- Test a single component in isolation.

**Key Concepts:**
- Unit under test
- Isolation
- Fast feedback
- Function-level testing
- Independence

**Scope:**
- Included: concept of the smallest test level.
- Not required yet: mocking dependencies (5.x).

---

### [[2.2 — Integration Testing]]

**Learning Objectives:**
- Test how components work together.

**Key Concepts:**
- Component interaction
- Interface testing
- Integration point
- Bottom-up / top-down
- Module contract

**Scope:**
- Included: testing connections between units.
- Not required yet: full system / end-to-end.

---

### [[2.3 — System & End-to-End Testing]]

**Learning Objectives:**
- Test the full application as a user would.

**Key Concepts:**
- Whole-system test
- End-to-end (E2E)
- User flow
- Real environment
- System-level black-box

**Scope:**
- Included: highest functional test level.
- Not required yet: performance / security testing.

---

### [[2.4 — The Test Pyramid]]

**Learning Objectives:**
- Balance the proportion of test levels.

**Key Concepts:**
- Test pyramid
- Many unit, few E2E
- Speed vs confidence trade-off
- Ice-cream cone anti-pattern
- Cost per level

**Scope:**
- Included: strategy for distributing tests.
- Not required yet: CI pipelines.

---

## 3. Test Design Techniques

### [[3.1 — Black-Box vs White-Box]]

**Learning Objectives:**
- Distinguish testing based on visibility of internals.

**Key Concepts:**
- Black-box testing
- White-box testing
- Specification-based
- Structure-based
- Gray-box

**Scope:**
- Included: two viewpoints for designing tests.
- Not required yet: coverage metrics (4.x).

---

### [[3.2 — Equivalence Partitioning]]

**Learning Objectives:**
- Group inputs that behave the same way.

**Key Concepts:**
- Equivalence class
- Valid / invalid partition
- One representative per class
- Input space reduction
- Partition coverage

**Scope:**
- Included: choosing fewer, smarter inputs.
- Not required yet: combining multiple inputs.

---

### [[3.3 — Boundary Value Analysis]]

**Learning Objectives:**
- Test values at the edges of input ranges.

**Key Concepts:**
- Boundary value
- Min / max edges
- Off-by-one error
- Just inside / just outside
- Edge case

**Scope:**
- Included: edge-focused input selection.
- Not required yet: decision logic combinations.

---

### [[3.4 — Decision Table Testing]]

**Learning Objectives:**
- Test combinations of conditions and actions.

**Key Concepts:**
- Condition
- Action
- Rule
- Decision table
- Combination coverage

**Scope:**
- Included: structured logic-based testing.
- Not required yet: state-based behavior.

---

### [[3.5 — State Transition Testing]]

**Learning Objectives:**
- Test behavior that depends on prior state.

**Key Concepts:**
- State
- Transition
- Event / trigger
- State diagram
- Invalid transition

**Scope:**
- Included: testing stateful behavior.
- Not required yet: code coverage measurement.

---

## 4. Coverage & Measurement

### [[4.1 — Code Coverage Basics]]

**Learning Objectives:**
- Measure how much code tests execute.

**Key Concepts:**
- Code coverage
- Coverage percentage
- Executed vs total lines
- Coverage report
- Coverage tool

**Scope:**
- Included: meaning of coverage as a metric.
- Not required yet: specific coverage types.

---

### [[4.2 — Statement & Branch Coverage]]

**Learning Objectives:**
- Differentiate line-level and decision-level coverage.

**Key Concepts:**
- Statement coverage
- Branch coverage
- Decision point
- Untested branch
- Branch > statement strength

**Scope:**
- Included: two core coverage types.
- Not required yet: path / condition coverage.

---

### [[4.3 — Coverage Pitfalls]]

**Learning Objectives:**
- Recognize why high coverage ≠ good tests.

**Key Concepts:**
- 100% coverage myth
- Coverage without assertions
- Vanity metric
- False confidence
- Quality vs quantity

**Scope:**
- Included: limits of coverage as a goal.
- Not required yet: mutation testing (8.3).

---

## 5. Test Doubles

### [[5.1 — Why Test Doubles Exist]]

**Learning Objectives:**
- Explain the need to replace real dependencies.

**Key Concepts:**
- Dependency
- Slow / external dependency
- Non-determinism
- Isolation need
- Test double (umbrella term)

**Scope:**
- Included: motivation for fake dependencies.
- Not required yet: specific double types.

---

### [[5.2 — Stubs & Mocks]]

**Learning Objectives:**
- Distinguish providing data vs verifying interaction.

**Key Concepts:**
- Stub (returns data)
- Mock (verifies calls)
- Fake
- Spy
- Dummy

**Scope:**
- Included: vocabulary of double types.
- Not required yet: dependency injection patterns.

---

## 6. Test-Driven Development

### [[6.1 — Red-Green-Refactor]]

**Learning Objectives:**
- Follow the TDD cycle to drive design.

**Key Concepts:**
- Test-first
- Red (failing test)
- Green (make it pass)
- Refactor
- Short cycle

**Scope:**
- Included: the core TDD loop.
- Not required yet: BDD style.

---

### [[6.2 — Behavior-Driven Development]]

**Learning Objectives:**
- Express tests as readable behavior specifications.

**Key Concepts:**
- BDD
- Given-When-Then
- Specification by example
- Ubiquitous language
- Living documentation

**Scope:**
- Included: behavior-focused test style.
- Not required yet: automation tooling.

---

## 7. Automation & Tooling

### [[7.1 — Test Frameworks]]

**Learning Objectives:**
- Understand what a test runner provides.

**Key Concepts:**
- Test framework
- Test runner
- Test discovery
- Assertion library
- Reporting

**Scope:**
- Included: role of a generic test framework.
- Not required yet: specific language syntax.

---

### [[7.2 — Test Lifecycle Hooks]]

**Learning Objectives:**
- Run setup and cleanup around tests.

**Key Concepts:**
- Setup / teardown
- beforeEach / afterEach
- Fixture
- Shared state risk
- Test isolation

**Scope:**
- Included: lifecycle around test execution.
- Not required yet: CI integration.

---

### [[7.3 — Continuous Integration Testing]]

**Learning Objectives:**
- Run tests automatically on every change.

**Key Concepts:**
- Continuous integration (CI)
- Automated test run
- Build pipeline
- Fail fast
- Pull request gate

**Scope:**
- Included: where automated tests run in a workflow.
- Not required yet: deployment / CD.

---

## 8. Test Quality & Maintenance

### [[8.1 — Flaky Tests]]

**Learning Objectives:**
- Identify tests with non-deterministic results.

**Key Concepts:**
- Flaky test
- Non-determinism
- Race condition
- Test order dependency
- Quarantine

**Scope:**
- Included: recognizing unreliable tests.
- Not required yet: fixing concurrency.

---

### [[8.2 — Test Smells]]

**Learning Objectives:**
- Spot patterns that make tests hard to trust.

**Key Concepts:**
- Test smell
- Fragile test
- Over-mocking
- Duplicated setup
- Unclear intent

**Scope:**
- Included: maintainability warning signs.
- Not required yet: refactoring strategies.

---

### [[8.3 — Mutation Testing]]

**Learning Objectives:**
- Measure how well tests detect injected faults.

**Key Concepts:**
- Mutation testing
- Mutant
- Killed / survived mutant
- Mutation score
- Test effectiveness

**Scope:**
- Included: validating test strength.
- Not required yet: tool-specific configuration.

---
