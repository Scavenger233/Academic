# Learning outcomes
- Explain the key terminology in software testing and inspection.
- Understand various testing techniques such as black and white box.
- Write the tests, run them, and report the errors.
<img width="1228" alt="image" src="https://github.com/user-attachments/assets/fd093347-882c-4d30-866a-a2667973c3de">

# Week 2

## Terminology
- **Fault**:A *static defect* in the software
- **Error**: An *incorrect internal state* that is the manifestation of some *fault*
- **Failure**:An *incorrect external behaviour* with respect to the requirements or another description of the expected behaviour

- **Verification:** To ensure that the product is meets its requirements
- **Validation:** To ensure that the product meets the user’s needs
- **Independent V&V - IV&V:** the evaluationwas done by someone else than the developers of the software

# Week 3

## What is software testing?
- Specification -> Test Design -> Test Execution

## Complexity of Testing Software
- Tests can be designed with a
  - **“Human-Based”** approach, where a test engineer uses domain knowledge and her/his experience to design tests that will be effective at finding faults
  - **“Criteria-Based”** approach, where a test satisfies well-defined engineering goals such as coverage criteria (% of code that has been executed by tests)
 
## The fault failure model

- **Reachability**: The location or locations in the program that contain the fault must be reached
- **Infection**: The state of the program must be incorrect
- **Propagation**: The infected state must cause some output or final state of the
- **Reveal**: The tester must observe part of the incorrect portion of the program state

## Software Testing Levels
<img width="1189" alt="image" src="https://github.com/user-attachments/assets/65d36e5e-d08e-47da-8764-b11863f78a1f">

<img width="1169" alt="image" src="https://github.com/user-attachments/assets/fd00b634-dca2-4953-bcd0-81396030a705">

## Types of Testing
- **White Box Testing**: Tester knows the internal structure.
- **Black Box Testing**: Tester doesn’t see the internal structure.
- **Regression Testing**: Ensures functionality after changes.
- **Stress Testing**: Tests system’s robustness under high load.


# Week 4

## The life cycle of a bug

- **Before Discovery**: A human error creates a fault in the system, leading to a failure observed during testing.
- **After Discovery**: The bug progresses through stages: **New, Assigned, Open, Fixed, Pending Retest, Verified, and Closed**. Some bugs may be marked as **Duplicate, Rejected, or Deferred** if not addressed immediately.


## Debugging and Tersting

- **Debugging**: the process of finding a fault given a faliure
  - Determine the nature and location of the bug in the code
  - Fix the code to remove the error

- while **testing** is about identifying failures.

<img width="1219" alt="image" src="https://github.com/user-attachments/assets/4e7a16a4-cf66-44c7-8ae3-776361062893">

- Bug Reporting Process:

Key activities include **Reproducing, Isolating, Generalizing, Summarizing, Condensing, Disambiguating, Neutralizing**, and **Reviewing** the report for clarity and accuracy.

# Week 5

1. **Core Software Testing Activities**:
   - These include **test design** (requirement alignment, test coverage, traceability), **automation** (efficiency, environment management), **execution** (running tests, failure identification), and **evaluation** (test summary, analysis, bug tracking).

2. **Test Automation**:
   - Automation helps control test execution, compare actual outcomes with expected outcomes, and reduce costs and human error, making it especially useful for regression testing.

3. **Software Testability**:
   - Defined by **controllability** (ease of input provision) and **observability** (ease of monitoring system behavior). High testability implies software that’s easier to test due to accessible inputs and observable outcomes.

4. **Test Coverage Criteria**:
   - A coverage criterion is a rule that helps define test requirements, such as covering all statements or functional requirements. Criteria help identify a subset of important tests from all possible tests.

5. **Examples of Coverage**:
   - Using examples like jelly bean flavors and colors, the lecture illustrates how coverage criteria ensure completeness in testing, such as tasting every flavor versus tasting every color.

6. **Criteria-Based Test Design**:
   - Criteria are applied by either directly generating test values that satisfy the criterion or using a separate method to generate tests and then measuring coverage against the criterion.
   - Coverage level is calculated by the percentage of test requirements satisfied by the test set.

7. **Generators and Recognizers**:
   - **Generators** create test values automatically, while **Recognizers** check if test cases meet specific criteria, making coverage analysis easier.

8. **Benefits of Criteria-Based Testing**:
   - Reduces redundant tests, provides traceability, supports regression testing, and offers a clear endpoint for testing.

9. **Sources of Structures for Testing**:
   - Software structures, such as graphs, logical expressions, and syntactic structures, are modeled from software artifacts and used to guide test design.

Criteria-based testing emphasizes methodical test design, aiming to maximize test efficiency and effectiveness by focusing on specific coverage targets.
