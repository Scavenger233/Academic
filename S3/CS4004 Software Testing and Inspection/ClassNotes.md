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
- **Independent V&V - IV&V:** the evaluation was done by someone else than the developers of the software

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


## Debugging and Testing

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
   - Automation helps control test execution, **compare** **actual** outcomes with **expected** outcomes, and reduce costs and human error, making it especially useful for **regression testing**.

3. **Software Testability**:
   - Defined by **controllability** (ease of input provision) and **observability** (ease of monitoring system behavior). High testability implies software that’s easier to test due to accessible inputs and observable outcomes.

4. **Test Coverage Criteria**:
   - A coverage criterion is a rule that helps **define test requirements**, such as covering all statements or functional requirements. Criteria help identify a subset of important tests from all possible tests.

5. **Examples of Coverage**:
   - Using examples like jelly bean flavors and colors, the lecture illustrates how coverage criteria ensure completeness in testing, such as tasting every flavor versus tasting every color.

6. **Criteria-Based Test Design**:
   - Criteria are applied by either directly **generating test values** that satisfy the criterion or **using a separate method to generate tests** and then measuring coverage against the criterion.
   - Coverage level is calculated by the percentage of test requirements satisfied by the test set.

7. **Generators and Recognizers**:
   - **Generators** create test values automatically, while **Recognizers** check if test cases meet specific criteria, making coverage analysis easier.

8. **Benefits of Criteria-Based Testing**:
   - Reduces redundant tests, provides traceability, supports regression testing, and offers a clear endpoint for testing.

9. **Sources of Structures for Testing**:
   - Software structures, such as graphs, logical expressions, and syntactic structures, are modeled from software artifacts and used to guide test design.

Criteria-based testing emphasizes methodical test design, aiming to maximize test efficiency and effectiveness by focusing on specific coverage targets.


# Week 7 

Here’s a summary of the key points and exam highlights from the lecture on "Functional Testing":

1. **What is Functional Testing**:
   - Functional testing derives test cases from **software specification**s, focusing on testing system behavior as defined by functional requirements.
   - It’s also known as **specification-based** or **black-box testing**, where the internal code is not directly examined.

2. **Random vs. Systematic Testing**:
   - **Random Testing** involves randomly selecting inputs but can be ineffective at finding rare issues.
   - **Systematic Testing** (often used in functional testing) carefully selects inputs, especially targeting cases likely to reveal faults, like boundary values.

3. **Equivalence Class Partitioning**:
   - Partitioning the input space into equivalence classes (ECs) allows testers to **select representative test cases** from each class.
   - This approach improves test coverage by **focusing** on “dense” areas of the input space **where faults are likely to occur**, especially around boundaries.

4. **Why Use Functional Testing**:
   - Functional testing effectively identifies missing logic errors, is cost-effective, and can be applied at various levels (e.g., unit, integration, and system).
   - It’s advantageous because it can be designed early in the development process and helps clarify and refine requirements.

5. **Steps from Specification to Test Cases**:
   - Decompose the specification to identify testable features.
   - Select representative values or behaviors for each test case.
   - Form test specifications by combining input values or model behaviors.
   - Design, implement, and execute actual test cases.

6. **Example**:
   - For testing ticket sales software, equivalence classes were created based on age ranges with different ticket prices. This approach highlights boundary testing for each class.

7. **Partitioning in Password Testing**:
   - For a password creation feature, equivalence classes might include conditions like length requirements, presence of numbers, uppercase, and lowercase letters. Each condition forms a distinct equivalence class with specific test values.

Functional testing helps ensure that software behaves as expected according to requirements, making it a foundational approach that finds issues often missed by other testing types.

# Week 10

## Statement testing
- Statement testing: the number of semicolon ; is the number of testing statements
- Statement coverage requires one test with **condition=true**
- **false branch not covered**

## Branch testing
### To calculate the coverage based on the branch covered
- Traversing all edges of a graph causes all nodes to be visited，but the converse is not true
```java
// || means only one condition is true, the whole statemment in the bracket is true
if(isDigitHight || isDigitLow) {
}
```
- Like the example above, all nodes/statements tested doesn't mean all edges/branches tested.

## Condition coverage

- each basic condition must be excuted at least once
- coverage calculation
<img width="1230" alt="image" src="https://github.com/user-attachments/assets/e00b0b7e-ed6b-4bbf-b812-35d748f13d3d">


# Data Flow Testing

- Definition: A tyoe of structure/white box testing focused on selecting test paths through a program based on **definition and use of variables**

## Definition and Use

### Definition
- Definition: A **location** in the code where a value for a **variable is stored in memory**

### Use
- Definition: A **location** in the code where the value of a **variable is accessed**
  - p-use: A use where the value of a variable froms a **predicate**, i.e. the basis for decision
  - ```java
    if (x > 10) {
    }
    ```
  - c-use: A use where the value of a variable froms part of a **computation**
  - ```python
    Y = x + 5'
    print(x)
    ```
## DU pair
- A pair of definition and use for some variable, such that at least one DU path exista from the definition to the use

## DU path
- A **definition-clear** path on the CFG sarting from a definition to a use of the same variable
  - Definition-clear: value is not replaced on path **(You can't re-define the value)**

## DU pair的判断准则
- 先definition，后 use
- 中间不能有第二个definition
- 中间不能有第二个use
- 考虑中间while/if等代码是否实现，会给DU path带来的影响
