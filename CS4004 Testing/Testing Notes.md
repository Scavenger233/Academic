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

**White Box Testing**: Tester knows the internal structure.
**Black Box Testing**: Tester doesn’t see the internal structure.
**Regression Testing**: Ensures functionality after changes.
**Stress Testing**: Tests system’s robustness under high load.


# Week 4

## The life cycle of a bug

**Before Discovery**: A human error creates a fault in the system, leading to a failure observed during testing.
**After Discovery**: The bug progresses through stages: **New, Assigned, Open, Fixed, Pending Retest, Verified, and Closed**. Some bugs may be marked as **Duplicate, Rejected, or Deferred** if not addressed immediately.


## Debugging and Tersting

- **Debugging**: the process of finding a fault given a faliure
  - Determine the nature and location of the bug in the code
  - Fix the code to remove the error

<img width="1219" alt="image" src="https://github.com/user-attachments/assets/4e7a16a4-cf66-44c7-8ae3-776361062893">



