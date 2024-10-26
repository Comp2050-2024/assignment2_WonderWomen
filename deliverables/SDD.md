# Software Design Document

> Use this markdown file to create the report. For the submission print this document to a PDF, and upload it to iLearn. The maximum number of pages is 30.
> Use the document structure below.

## Structure

### Title Page (Lisa)

- Project name, names of all team members

  - Sathya Reesha Kodali - 47823909
  - Sathvika Mannepally - 47846402
  - Mariya Hoque Trina - 47992700
  - Lisa Thiparala  - 47410272
  
- Vision statement:
In order to create an interesting and dynamic experience that encourages community spirit and a sense of belonging for both new and returning Macquarie University students, Explore MQ aims to seamlessly combine the thrill of campus exploration with the ease of mobile technology. Explore MQ gives employees the freedom to create and implement dynamic, adaptable challenge programs, which allows the institution to collaborate with nearby companies and campus services to provide alluring incentives. In addition to gamifying the campus experience, this feature makes it enjoyable, competitive, and instructive for students to become acquainted with their surroundings.
Explore MQ turns campus orientation into an exciting trip by combining virtual challenges with in-person interactions. This encourages students to find important sites, connect with other students, and utilise university resources and services. This program seeks to improve the overall student experience and foster enduring participation by encouraging deep ties within the Macquarie community. Explore MQ will act as a bridge and a guide, enhancing everyone's ability to access and feel welcome on campus.

|Date of New Version  | Changes made         | Changes made by |  Changes agreed by |
| -------------       | -------------        |  -------------  |  -------------     |       
| 21/10/2024          | System Design Document    |  SRK            |  Team members      |
| 21/10/2024          | Team Member Names    |  SRK            |  Team members      |
| 24/10/2024          | Created presentation slides | MHT      |  Team members      |
| 24/10/2024          | Data Definitions     |  SRK            |  Team members      |
| 24/10/2024          | Class Diagram        |  SM             |  Team members      |
| 24/10/2024          | State Diagram        |  SM             |  Team members      |
| 25/10/2024          | Test Specifications       |  SM             |  Team members      |
| 25/10/2024          | Minimum Viable Product        |  SM             |  Team members      |
| 25/10/2024          | System Design Document   | SRK              |   Team members   |
| 25/10/2024          | Requirement Traceability Matrix | SRK       | Team members     |
| 25/10/2024          | List of Design Assumptions | SM       | Team members     |
|26/10/2024           | Setting Milestones        | MHT       | Team members|
| 26/10/2024          | Tasks for milestones| MHT | Team Members|
|26/10/2024| Summary and Outlook| MHT| Team Members|


### System Design Document (Reesha)

This will include the basic architecture of the system and the high-level strategic decisions. You need to include a description of the:

- System architecture
The architecture of "Explore MQ" will include various layers:

1. Client/Front-End Layer:-
   
The client/front-end layer includes a mobile application (iOS/Android). The front end is a smartphone app for students, employees, and store partners. This app will have   interfaces for logging in, viewing and participating in challenges, tracking progress, and redeeming rewards. The overall user experience must be uniform across platforms (iOS and Android), including a responsive design to accommodate different screen sizes.
   
User Interface: The interface design is unified and aligns with the other Macquarie University apps, including colour schemes and layout norms. It provides simplicity of use and a short learning curve.

2. Backend Layer:-

The backend layer includes the application server, which manages user authentication, challenges, and rewards. This will cover fundamental features, including user administration, challenge participation, and reward redemption. The backend will interface with the university's Single Sign-On (SSO) system to authenticate users.

API Gateway: The API will include endpoints for challenge enrolment, award redemption, and progress tracking, enabling mobile clients to transmit and retrieve data securely.

3. DataBase Layer:-

The data layer consists of a relational database that stores organised information on users, challenges, awards, and student progress (e.g., MySQL or PostgreSQL). Tables will be normalised to decrease redundancy while maintaining data integrity.
   
Data Encryption: Susceptible information, including passwords and award details, will be protected using AES-256 at rest and TLS/SSL while in transit.

4. Integration Layer:-

The system interfaces with Macquarie University's SSO system to provide safe authentication with university credentials.
   
APIs or direct connections with local stores' point-of-sale (POS) systems provide smooth incentive redemption and tracking.

 Student Information System Integration: To authenticate students' identities during registration and synchronise data with their records.
   
- Storage/persistent data strategy

1. Relational Database:-
  
A relational database stores profiles of users, challenge data, reward information, and student progress in a structured fashion. A relational database (such as MySQL or PostgreSQL) is perfect for managing complicated relationships among users, challenges, and rewards.

To improve query performance, each table will have suitable indexes on regularly searched fields (for example, userID, challengeID).

2. Data Security: 
Sensitive data, such as user credentials and incentive vouchers, will be secured at rest using AES-256 to prevent unauthorised access and remain unreadable.
The app will employ HTTPS with TLS/SSL encryption to protect against man-in-the-middle attacks and data leakage.

3. Data Backup and Recovery: 
We will implement regular backups and automated daily snapshots to minimise data loss in case of failure.
A backup plan with both hot and cold backups will be implemented. In the event of a system failure, restoration from the most recent backup will proceed with minimal downtime.

- Noteworthy trade-offs and choices

1. Database Options:

Using a relational database (such as MySQL) assures data integrity, security, and scalability as the number of users increases. However, because relational databases require organised schemas, schema evolution (for example, adding new features) is slightly more involved than with NoSQL databases.

2. Integration With External Systems:

Integrating with external reward systems adds complexity but, through relationships with local companies, allows for a more comprehensive user experience. This decision necessitates cautious API design to reduce communication delays between systems.

3. Performance versus Flexibility:

Real-time notifications and incentive generating necessitate a delicate balance between quick response times and the freedom to allow retailers to handle their promotions. This trade-off could involve choosing between immediate award redemption and system holdups during peak loads.

- Concurrent processes (if any) and how they will be coordinated

1. Challenge Enrolment and Task Processing:

Multiple users can participate in challenges simultaneously. Therefore, the backend must efficiently manage concurrent user sessions and data writes. Sessionnologies, such as Redis, can manage tech to ensure user data is accurate across transactions.  

2. Real-time notifications:

A message queuing system like RabbitMQ can manage immediate notifications for incomplete challenges, award redemptions, and changes. It ensures that tasks are completed asynchronously without disrupting the primary application flow.

3. Coordination of SSO and Reward Systems:

API rate limitation and retries will govern connectivity with outside resources (SSO for authentication and POS systems for rewards), enabling graceful failures and system responsiveness during downtime or faults.

- A package diagram showing the subsystems you will use

The system will consist of various subsystems or modules:

1. Authentication Module: Manages user logins, password resets, and SSO integration.
2. The Challenge Management Module manages challenge creation, task progress, and notifications.
3. Reward Management Module: Communicates with retailers and manages voucher production and redemption.
4. The Analytics and Reporting Module collects data for participation statistics and allows staff to develop engagement reports.
5. The Notification System manages real-time updates and reminders for students.

![image](https://github.com/user-attachments/assets/46b4efee-8b6a-4d47-83b3-03230f762a15)


### Data Definitions (Reesha)

Create a table showing what data will need to be stored in your system. For each item give the name of the field/attribute/variable, its type, its meaning in the problem domain expressed in natural language, and an example of valid data.

|  Field Name         | Type                 | Meaning                                                                                  |  Example           |
| -------------       | -------------        |  ------------------------------------                                                    |  -------------     |       
| UserID              | INT                  |  Each student or staff or store partners have been assigned a unique identifier.         |  123456            |
| UserName            | VARCHAR(50)          |  The user's MQ login credentials.                                                        |  s124345           |
| Email               | VARCHAR(50)          |  The user's MQ email.                                                                    |  @mq.edu.au        |
| ProfileType         | ENUM('student', 'staff', 'store partner'| Determines if the user is a student or staff member or store partner. |  staff             |
| ChallengeID         | INT                  |  A unique identifier for each challenge.                                                 |  2345342           |
| ChallengeName       | VARCHAR(50)          |  Name of the challenge  in which the student is participating.                           |  Locating the campus facility.|
| TaskProgress        | ENUM('complete', 'incomplete')|  Tracks the current status of the challenges done by students.                  |  incomplete        |
| RewardVoucher       | VARCHAR(100)         |  A voucher code is generated when a student completes a task.                            |  Sq123             |
| StoreID             | INT                  |  Unique identifier for store partner.                                                    |  4783792           |
| ChallengeDate       | DATE                 |  The date challange was issued or expired.                                               |  2024-10-24        |
| authToken           | VARCHAR(256)         |  Token used to authorise the users for securing the information.                         |  f237js342edj34    |
| LocationData        | JSON                 |  Storing the data on the locations that was visited during a challenege.                 |  {"Mason Theatre"} |
| Role                | ENUM('student', 'admin', 'store Partner')| Defines the level of user access.                                    |  student           |

### Analysis and Design

#### Class Diagram (Sathvika)

You need to do an initial design of your system -- what basic objects should it have? And what are the methods associated with those objects? You will represent your design decisions in a class diagram. In a full plan, you need to make sure any classes or methods in any sequence diagrams have been included in the class diagram -- it might help you to draw some sequence diagrams to help you to decide what your class diagram should contain. Method signatures should be given. The diagram must include, as appropriate classes, attributes, associations, inheritance and/or aggregation (if applicable) and multiplicities.

BASIC OBJECTS AND CLASSES:

1. User: All users in the system belong to this basic class. All user types share common properties and methods with it. 

Attributes:
userID
name
Email
Role
update

Methods:
login(): boolean
logout(): void
createProfile(): void

2. Student: Inherits from User, standing in for students who are able to sign up for classes and check their grades.

Methods:
enrollInCourse(): void
viewgrades(): List

3. Staff: Inherits from User, standing in for staff who are able to manage courses and assign grades.

Methods:
manageCourses(): void
assigngrades(): void

4. StorePartner: Inherits from User, standing in for StorePartner who can offer and view Redemption history.

Methods:
addOffer(reward: Reward): void
viewRedemptionhistory(): List

5. Challenge: Represents a systemic challenge with related attributes and methods.

Attributes:
challengeID
title
description
startDate
endDate
status

Methods:
createChallenge(): void
updateChallenge(): void
deleteChallenge(): void
getChallengeDetails(): String

6. Reward: Represents a redeemable incentive connected to a store.

Attributes:
rewardID
description
pointsRequired
storeID

Methods:
generateVoucher(): String
validateVoucher(voucherCode: String): boolean

7. Store: Symbolizes a store that gives offers rewards

Attributes:
storeID
name
location
offers

Methods:
addOffer(reward: Reward): void
viewRedemptionhistory(): List

8. Redemption: Symbolizes a redemption action for a reward.

Attributes:
redemptionID
userID
rewardID
date
pointsUsed

Methods:
recordRedemption(): void
getRedemptionDetails(): String

9. Notifications: Represents a notification that users receive regarding different happenings.

Attributes:
notificationID
userID
message
date

Methods:
sendNotication(): void
getNotifications(): List


![A-2 CD COMP 2050](https://github.com/user-attachments/assets/8357d24f-b924-4194-8c7a-20fa221b0dc7)

ASSOCIATIONS, INHERITANCE, AGGREGATION  AND MULTIPLICITIES:

INHERITANCE:
Student, Staff, and StorePartner inherit from User

AGGREGATION:
A user may receive zero or more notifications, engage in zero or more challenges, and have zero or more redemptions.
There can be zero or more rewards for a challenge.
While a store may have more than one reward, a reward is only linked to one store.

MULTIPLICITIES:

- User and Challenge:
  
There can be zero or more challenges for a user ("1" -- "0..").

One User is linked to each challenge.

- Challenge and price:
  
There can be zero or more rewards linked to a challenge ("1" -- "0..").

Every reward has a corresponding challenge.

- Reward and Store:
  
One store is associated with a reward ("1" *-- "1").

Every store has a variety of rewards to give.

- Redemption and User:
  
Redemptions can be zero or more for a user ("1" -- "0..").

A single User is the owner of each redemption.

- Notification and User:
  
One or more notifications may be sent to a user ("1" -- "0..").

Every notification is associated with a single user.

- Challenge and Redemption:
  
A Redemption can have a zero or one Challenge associated with it ("1" *-- "0..1").

- StorePartner and Store:
  
One Store is associated with a StorePartner ("1" *-- "1").

- Challenge and StorePartner:
  
There can be zero or more challenges offered by a StorePartner ("1" -- "0..").

- Notification and Challenge:
  
One Challenge or zero Challenge ("1" *-- "0..1") may be mentioned in a notification.

- Notification and Reward:
  
One or zero Rewards can be linked to a notification ("1" *-- "0..1").



#### One or more State Diagrams for the more interesting objects in your design (Sathvika)

State Diagrams: You are required to consider the relevant states of each object in your system and to submit state diagrams for those that have interesting states or complex behaviour. One way to measure if a state is interesting is to consider whether you need to test that state before performing a particular action or if the state changes after an action is performed. What is interesting will depend on the application.

######  Challenge State diagram 

State diagram for Challenge:
Throughout its existence, the Challenge class may exist in the following states: Draft, Active, Completed, and Expired. Actions such as creating, starting, finishing, or ending the challenge are necessary for the state transitions to occur.

States: 

- Draft: Although not yet active, the challenge is being built.
  
- Active: The challenge is going on right now.

- Completed: The task has been effectively concluded.

- Expired: The challenge is no longer active.

States transition:

- Create: Makes the switch from Draft to Active.

- Final Challenge: Moving from Active to Finalised.

- Expire: If the end date is reached without completion, it changes from Active to Expired.

![image](https://github.com/user-attachments/assets/f839fd7f-3afb-40c4-8389-54f278f6d280)

###### Reward State Diagram 

State diagram for Reward:
Moreover, the Reward class may exist in the following states: Available, Redeemed, and Expired. For the incentive lifecycle to be managed, the changes between these statuses are crucial.

States:

- The price is available for users to redeem.

- Redeemed: A user has acknowledged receipt of the incentive.

- The price has expired and can no longer be redeemed.

States transition:

- Redeem: Makes the change from Available to Eligible.

- In the event that the validity term expires, the status changes from Available to Expired.

![image](https://github.com/user-attachments/assets/91a66b1a-6cec-4076-b484-68b214a26e4a)

###### Redemption State Diagram

State diagram for Redemption:
Depending on whether a prize has been successfully redeemed, failed, or is still awaiting verification, the Redemption class may represent various states.

States: 

- Pending: Although the redemption request has been started, it has not yet been handled.

- Successful: The redemption process was successfully finished.

- Failed: The redemption attempt was unsuccessful due to a lack of points or an expired prise, for example.

States transition:

- Submit: Depending on how the redemption attempt turns out, it moves from Pending to Successful or Failed.

![image](https://github.com/user-attachments/assets/f4ff6f06-3133-4b5e-93a8-7d396ba05bc5)



### Requirements Traceability Matrix (reesha)

Requirements Traceability Matrix (RTM): Set up an RTM with the following columns:

- Requirement-ID (from SRS)
- Use Cases
- Classes
- Methods
- Packages
- Build Number (kept blank at this stage)

The RTM assigns requirements to the appropriate use cases, classes, methods, and packages, ensuring complete traceability.

| Requirement ID | Use Cases | Classes | Methods | Packages | Build Number|
|----------------|-----------|---------|---------|----------|-------------|
| FR - 1         | Login, Forgot Password | User, Auth | login(), resetPassword() | Authentication |         |
| FR - 2         | Challenge Enrollment | Challenge, Task | enrollChallenge() | Challenge Management |       |
| FR - 3         | Task Progress Tracking | Task, Progress | taskProgress() | Challenge Management |         |
| FR - 4         | Reward Redemption | Reward, Voucher | redeemVoucher() | Reward System |                   |
| FR - 5         | Store Management | Store, Reward | manageStoreRewards() | Reward System |                 |
| FR - 6         | Notifications, rewards | Notifications, task | sendReminder() | Notification System |     |
| FR - 7         | Participation Tracking | Analytics | generateReport() | Analystics |                      |
| FR - 8         | Student Verification | User, Auth | verifyStudent() | Authentication |                    |
| FR - 9         | Profile Management | User, Task | manageProfiles() | User Management |                    |

> There should be one row for each requirement. For this deliverable, just fill in the first five columns, since the last column (and usually a couple more after that which I've already deleted) are concerned with the design of the system.

### List of design assumptions (if any)

This will help the reader to understand why you have done certain things. Please review the assumptions carefully before submission. (But note: A poor assumption should not be used as an excuse for poor design decisions.)


1. Assumptions for the Challenge State Diagram Design:

Challenge lifecycle: It is expected that every challenge has a distinct lifespan, which includes creation (Draft), activation (Active), and completion or expiration depending on user time or completion.

shift Timing: Presupposes that a predetermined end date will trigger the shift to Expired, negating the need for extra user intervention.

User Actions Needed: The system's Create and End Challenge transitions are user-driven, meaning that a user must initiate them.

2. Assumptions for the Reward State Diagram Design:

Restricted Reward Availability: There are no intermediate states or partial redemptions; rewards can only be in one of three states: Available, Redeemed, or Expired.

Expiration Logic: If the system correctly records the duration of rewards, they will automatically change to Expired after a predetermined validity time.

Single-utilise Redeemable: Presupposes that a user can only utilise a reward once and that it is no longer accessible to other users after that.

3. Assumptions for the Redemption State Diagram:

Outcome-Based Transitions: Redemptions are anticipated to change from Pending to Successful or Failed, depending on factors such as reward status (e.g., expired) or point availability.

Automatic Verification: The flow is made simpler by the assumption that verification takes place right away after submission, eliminating the need for a "in-review" or "processing" state.

Not redeemable Once Failed: Presupposes that a redemption that has been designated as unsuccessful cannot be attempted again or submitted again without initiating a fresh redemption request.


Explanation of  Assumptions:

These presumptions seek to streamline the lifecycle of each item by emphasising important stages while avoiding needless complexity. They make it clear that most transitions are either system-driven (like expiration because of time limits) or user-driven (like signing up for a challenge or using a reward). These presumptions guarantee that every object operates reliably and preserves an easy-to-use interface by specifying distinct, non-overlapping states.

### Test specifications (Sathvika)

Test Specifications should contain the following:

- Test-case specifications, made up of test-case identifiers, and test data (input specifications and output specifications).
  Acceptable documentation for Test Case Specifications would include:
  - Test Case Identifier
  - Test description
  - Input specifications
  - Output specifications
- Test plans, including for example a test schedule, testing resources required, testing milestones and test deliverables. Test plans, covering scheduling and resourcing of all testing processes. Test plans can be more open format and should provide a description of how you would organise the actual testing of the Test Case Specifications that you've identified.

> The test specification section should cover at least one-third of the report.

1. Test Case Specifications:
   
The specific test cases you'll need to confirm your system's functionality are described in this section. You will add the following for every test case:

a) Identification of Test Cases
Each test case has its own unique identification (e.g., TC0001, TC0002).

b) Description of the Test
"Verify that a user may enroll in a challenge" is an example of a test case that provides a brief explanation of the feature being checked.

c) Specifications for Input
the test's necessary inputs, including any particular information (such as the user ID, challenge ID, or price ID).

d) Specifications for Output
the anticipated outputs or outcomes of the test, such as any modifications to the user interface, database entries, or status.

| Test Case Identifier | Test Description | Input Specifications | Output Specifications |
|  -------------       | -------------    |  -------------       |  -------------        |   
|  TC0001               |Verify login user functionality | Username: "user1"           Password: "password456" |  User successfully logs in and sees homepage       |   
| TC0002                | Verify Challenge enrollment by user  |  User ID: 10001,       Challenge ID: 400       |  Challenge enrollment confirmation for the user        |   
| TC0003                | Verify reward redemption by user    |  User ID: 10002,                 Reward ID: 200     |  Reward successfully redeemed, points deducted        |   
|  TC0004               |Verify notification is sent to the user   | User ID: 10001,             Notification ID: 101       |  Notification appears in user's notification area      |   


2. Test Plan
   
a. Test Schedule:
A schedule outlining the many tests that will be conducted. Add significant checkpoints, such as the beginning and ending of performance, user acceptance, and functional testing. 

Example:

| Milestone | Start Date | End Date |
| --------- | ---------- | -------- |
| Test Preperation | 21/10/2024 | 25/10/2024 |
| Functional Testing | 26/10/2024 | 10/11/2024 |
| Performance Testing | 11/11/2024 | 17/11/2024 |
| User Acceptance Testing | 18/11/2024 | 24/11/2024 |
| Final Testing and Evaluation | 30/11/2024 | 05/12/2024 |

b. Testing Resources Required:
Indicate the people and equipment needed for testing, including test environments, software, QA testers, and developers.

Example:

- Two QA testers, one developer (for issue fixes), and one project manager are on personnel. 

- Tools include Selenium for automated user interface testing, JIRA for problem tracking, Postman for API testing, and Test Server.

c. Testing Milestones: 
Describe the main testing stages and the tasks that must be finished at each stage.

Example:

- Completed test preparation: the identification of all test cases and the preparation of test data.

- Functional Testing Completed: Every essential feature has been tested and approved.

- Completed Performance Testing: The system satisfies all performance requirements, including load testing and reaction time.

d. Test Deliverables:
Describe the records or artifacts that will be created throughout the testing procedure, including bug logs, test reports, and screenshots of completed tests.

Examples:

- Test Report: Provides an overview of the outcomes of every test case that was run.

- Bug Log: A record of every bug found, together with its severity and status (open, in progress, or resolved).

- A report that lists the test cases that succeeded or failed at each stage of testing is called a test case execution report.

3. Testing process:

- Test each feature's functionality (e.g., login, challenge enrolment, reward redemption).

- To make sure that several modules (such as Challenge, Reward, and Notification) function together, conduct integration testing.

- To make sure the system operates effectively under load, conduct performance testing.

- Involve end users in user acceptability testing (UAT) to make sure the solution satisfies their needs.

Example of a Functional Testing Process:

- Configure the test environment, including the user accounts, test data, and test server.

- Follow the timetable when executing the test cases.

- In the test case execution report, note the outcomes.

- To have any bugs fixed, report them to the development team.

- Once the problems have been fixed, retest the unsuccessful test cases.


### Project Management

#### Minimal Viable Product (Sathvika)

A description of the _minimal viable product_. This is a version of the product, that is suitable for the client, trusted customers, or early adopter to use for evaluation. Which of the requirements does it implement, and which part of the architecture needs to be in place?


The first iteration of the system that incorporates only the necessary features for early assessment by clients, early adopters, or trusted consumers is known as the Minimal Viable Product (MVP). The MVP's objective is to deliver a working product with essential functionality while allowing for future improvements. It provides the framework for getting input and confirming the system's feasibility.



Requirements Implemented in the MVP:

The following crucial needs will be implemented by the MVP:

- User authentication: It allows store StorePartners, staff, and students to safely log in and out.
  
- Profile Management: Using their user ID, name, email, and role, users can build and edit their profiles.

- Enrolment in Challenges: Students will be able to see and sign up for challenges.

- Reward Management: Users may browse and redeem prizes, and StorePartners can create and administer them.

- Redemption Monitoring: The system will keep track of and record redemptions.

- Notification System: When users sign up for challenges or spend incentives, they will receive simple notifications.


Essential Architecture Elements for the MVP:

To support the MVP, the following elements of the architecture must be present:

1. System for User Management:

- Procedures for authorisation and authentication to guarantee that various roles—staff, students, and store partners—have the proper access to features.

2. Subsystems of Challenge and Reward:

- A challenge creation and management module.

- A method for redeeming rewards and connecting them to tasks.

3. Data storage and databases:

- User information, challenges, awards, redemptions, and notifications are all stored in a database.
 
- Tables for Notification, Redemption, Reward, Challenge, and User.

4. Notification System:

- A mechanism to send out alerts when someone completes tasks like signing up for a challenge or using a reward.
  
5. Frontend interface basics:

- A straightforward user interface that allows users to manage their profiles, browse challenges, log in, and collect rewards.


In conclusion, the MVP will enable safe authentication, simple frontend interfaces, and the required database support while offering crucial features for user management, challenge enrolment, reward management, and notification. Early adopters can interact with key features in this foundational version and provide insightful input that will inform future enhancements and feature additions.


### Milestones(Mariya)

#### Milestone 1: Creating User Profile, Management and Access:

Successfully Establish role-based access for students, employees, and store partners by creating user profiles and integrating them with the university's student data.

#### Milestone 2: Challenge Creation and Management:

Construct a system for creating challenges that will enable employees to plan, oversee, and administer challenges on campus. Updating the system constantly with information to track student progress in real time.

#### Milestone 3: Student Participation and Feedback:

Accomplish a system that allows students to view and sign up for challenges. Successfully prompts updates on developments, status of completion, and impending due dates.

#### Milestone 4: Implementing challenge completion system:

Establish the mechanism for producing e-vouchers after a challenge is finished. Install store validation mechanisms for partners and incorporate barcode generation for prizes.

#### Milestone 5: Setting up the UI/UX for user acceptance:
Test usability for employees and students alike. To guarantee usability and system coherence with the larger MQ app, make necessary adjustments to the UI and UX for user acceptance.

#### Milestone 6: Testing features

Conduct comprehensive testing of the functionalities, confirm with stakeholders, and implement the system for a demo release. Before a full-scale rollout, get feedback from initial users to improve the platform.


#### Tasks(MAriya)

| Task ID | Description | Task Dependencies | Effort (stars) | Milestone|
|--------|--------------|-------------------|-----------------|----------|
| T001| Prompting a menu asking for details to create IDs| None| 3| Milestone1|
| T002| Creating a challenge creation module for staff| T001| 4| Milestone2|
| T003| Establishing a system to enroll the students in for challanges| T002| 3| Milestone3|
| T004| Showing a dialogue box for student feedback on completion of their challange|  T003| 2| Milestone3| 
| T005| Providing a system for reward vouchers that generates store validated barcodes| T003| 4| Milestone4|
| T006| Implementing usability tests for the users| T004| 4| Milestone5| 
|T007| Improving UI/UX with the help of feedbacks from students and usability test results| T004 & T006| 5| Milsetone5|
|T008| Testing the system for errors and performance problems| All | 5| Milestone6|
|T009| Deploying the system for initial launch| All| 5| Milestone6| 
|T010| Collecting feedback documents from initial users for adjustments| T009| 3| Milestone6|


Describe the main tasks that need to be completed, in the form of a table. The table should include

- An ID for the task
- A description of the task
- Dependencies, i.e. tasks that need to be completed before this task can start.
- Effort. Since you do not know how, or even how many people work on the project, it does not make sense for this assignment to estimate workdays. Instead pick a suitable scale (S, M, L, XL or 1 to 5 stars or ...)
- Milestone. Which milestone do they belong to?

#### Risks (Lisa)

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

| Risk ID |   Description        |   Probabbility  |   Severity     | Mitigation Strategy |
| R01     | -------------        |  -------------  |  ------------- | ------------------- |  
| R01  | Changes in management and/or stakeholders requirements that lead to the project goals being changed.  |   Medium  |   High  | High
Consistent and regular meetings with stakeholders to ensure expectations and decisions are aligned.|



> Since you do not know how many people work on the project, or what resources you may have, it does not make too much sense to talk about people risk, or estimation risk, yet. Furthermore, if something like a probability is unknown, is better to say that it is unknown, instead of making something up.

### Summary and Outlook (Mariya)

The groundwork for a creative campus experience has been effectively established by the Explore MQ initiative. The team hopes to strengthen students' feelings of community and participation through dynamic challenges, tailored incentives, rewarding processes, and smooth connection with Macquarie University's systems. This system has infrastructure for user identification, challenge management, and reward integration. The Explore MQ’s development has reached a crucial point. Now the objective is to give staff adequate tools to develop and handle campus difficulties while simultaneously delivering students a smooth and interesting experience.

As the system transitions toward its final phases which include usability testing, system optimization, and deployment, the team is still dedicated to providing the university community with a reliable, safe, and interesting tool. Our approach prioritizes performance, security, and scalability as we approach final deployment to make sure "Explore MQ" can expand to meet Macquarie University's changing requirements and user acceptance. This project will increase campus involvement and benefit staff and students in the long run. A driving concept has been the balancing act between performance and flexibility, which permits a seamless user experience while guaranteeing that the system can manage large traffic volumes, especially during busy campus events.

To sum up, Explore MQ is expected to play a significant role in the Macquarie University student experience by influencing the way that students engage with the campus and the outside community whilst the staff will look after the whole process. The project will have a long-lasting effect on student involvement and engagement. With a committed staff and a well-defined plan, Explore MQ will rapidly become a vital component of the institution’s digital platform.


### Appendices (Everyone)

- Log of interactions with stakeholders.   - see it in the whatsapp group including the stakeholders.
- References.
- Third-party-resources

## Note

> Do not forget that we also expect you to complete an individual reflection on iLearn.


