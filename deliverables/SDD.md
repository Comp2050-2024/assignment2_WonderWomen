# Software Design Document

> Use this markdown file to create the report. For the submission print this document to a PDF, and upload it to iLearn. The maximum number of pages is 30.
> Use the document structure below.

## Structure

### Title Page

- Project name, names of all team members
- Vision statement
  > This should be a new and fresh vision statement and not a copy of the SRS team's statement.

### System Design Document

This will include the basic architecture of the system and the high-level strategic decisions. You need to include a description of the:

- System architecture
- Storage/persistent data strategy
- Noteworthy trade-offs and choices
- Concurrent processes (if any) and how they will be coordinated
- A package diagram showing the subsystems you will use

### Data Definitions

Create a table showing what data will need to be stored in your system. For each item give the name of the field/attribute/variable, its type, its meaning in the problem domain expressed in natural language, and an example of valid data.

### Analysis and Design

#### Class Diagram

You need to do an initial design of your system -- what basic objects should it have? And what are the methods associated with those objects? You will represent your design decisions in a class diagram. In a full plan, you need to make sure any classes or methods in any sequence diagrams have been included in the class diagram -- it might help you to draw some sequence diagrams to help you to decide what your class diagram should contain. Method signatures should be given. The diagram must include, as appropriate classes, attributes, associations, inheritance and/or aggregation (if applicable) and multiplicities.

#### One or more State Diagrams for the more interesting objects in your design

State Diagrams: You are required to consider the relevant states of each object in your system and to submit state diagrams for those that have interesting states or complex behaviour. One way to measure if a state is interesting is to consider whether you need to test that state before performing a particular action or if the state changes after an action is performed. What is interesting will depend on the application.

### Requirements Traceability Matrix

Requirements Traceability Matrix (RTM): Set up an RTM with the following columns:

- Requirement-ID (from SRS)
- Use Cases
- Classes
- Methods
- Packages
- Build Number (kept blank at this stage)

> There should be one row for each requirement. For this deliverable, just fill in the first five columns, since the last column (and usually a couple more after that which I've already deleted) are concerned with the design of the system.

### List of design assumptions (if any)

This will help the reader to understand why you have done certain things. Please review the assumptions carefully before submission. (But note: A poor assumption should not be used as an excuse for poor design decisions.)

### Test specifications

Test Specifications should contain the following:

- Test-case specifications, made up of test-case identifiers, and test data (input specifications and output specifications).
  Acceptable documentation for Test Case Specifications would include:
  - Test Case Identifier
  - Test description
  - Input specifications
  - Output specifications
- Test plans, including for example a test schedule, testing resources required, testing milestones and test deliverables. Test plans, covering scheduling and resourcing of all testing processes. Test plans can be more open format and should provide a description of how you would organise the actual testing of the Test Case Specifications that you've identified.

> The test specification section should cover at least one-third of the report.

### Project Management

#### Minimal Viable Product

A description of the _minimal viable product_. This is a version of the product, that is suitable for the client, trusted customers, or early adopter to use for evaluation. Which of the requirements does it implement, and which part of the architecture needs to be in place?

#### Milestones

A description of the main implementation milestones, in the order in which they should occur in the project. A milestone marks the end of a stage in the project when a version of the product can be reviewed as a whole.

#### Tasks

Describe the main tasks that need to be completed, in the form of a table. The table should include

- An ID for the task
- A description of the task
- Dependencies, i.e. tasks that need to be completed before this task can start.
- Effort. Since you do not know how, or even how many people work on the project, it does not make sense for this assignment to estimate workdays. Instead pick a suitable scale (S, M, L, XL or 1 to 5 stars or ...)
- Milestone. Which milestone do they belong to?

#### Risks

A table with the following types of risks
- Organizational risks that come from changes in the organizational environment. Think of changing stakeholders or management, or a change of mind of stakeholders or management.
- Requirements risks, that come from changes to the requirements, or wrong requirements, and the process of managing requirement changes.
- Technology risks that come from the software or hardware technologies that are used by the system. **Include here parts of the system that you may need from the team that works on the other half of the system, or parts that you both depend on.**
- Tools risks that come from the software tools and other support software used to develop the system.

For each risk include

- An ID
- A description of the risk.
- The probability of that risk happening (use an appropriate scale: low to high, or 0% to 100%, or ...)
- The severity of the risk (use an appropriate scale: none to catastrophic, or 0 to 10, or ...)
- Mitigation strategies. Suggest measures that can be taken to reduce the risk.

> Since you do not know how many people work on the project, or what resources you may have, it does not make too much sense to talk about people risk, or estimation risk, yet. Furthermore, if something like a probability is unknown, is better to say that it is unknown, instead of making something up.

### Summary and Outlook

Your famous final words.

### Appendices

- Log of interactions with stakeholders.
- References.
- Third-party-resources

## Note

> Do not forget that we also expect you to complete an individual reflection on iLearn.


