# Agile Tester

## FA-1.1.1 (K1) Recall the basic concept of Agile software development based on the Agile Manifesto

* Individuals and interactions over processes and tools
* Working software over comprehensive documentation
* Customer collaboration over contract negotiation
* Responding to change over following a plan



## FA-1.1.2 (K2) Understand the advantages of the whole-team approach

* Enhancing communication and collaboration within the team
* Enabling the various skill sets within the team to be leveraged to the benefit of the project
* Making quality everyone’s responsibility


## FA-1.1.3 (K2) Understand the benefits of early and frequent feedback

* Avoiding requirements misunderstandings, which may not have been detected until later in the development cycle when they are more expensive to fix.
* Clarifying customer feature requests, making them available for customer use early. This way, the product better reflects what the customer wants.
* Discovering (via continuous integration), isolating, and resolving quality problems early.
* Providing information to the Agile team regarding its productivity and ability to deliver.
* Promoting consistent project momentum.

## FA-1.2.1 (K1) Recall Agile software development approaches

* XP
	- 5 values: communication, simplicity, feedback, courage, and respect.
	- principles: humanity, economics, mutual benefit, selfsimilarity, improvement, diversity, reflection, flow, opportunity, redundancy, failure, quality, baby steps, and accepted responsibility. 
	- practices: sit together, whole team, informative workspace, energized work, pair programming, stories, weekly cycle, quarterly cycle, slack, ten-minute build, continuous integration, test first programming, and incremental design.
* Scrum
	- sprint, product increment, product backlog, sprint backlog, definition of done, timeboxing, transparency
	- roles: sm, po, dev
* Kanban
	- board, WIP limit, lead time

## FA-1.2.2 (K3) Write testable user stories in collaboration with developers and business representatives

* INVEST: Independent, Negotiable, Valuable, Estimable, Small, Testable
* 3C: Card, Conversation, Confirmation

## FA-1.2.3 (K2) Understand how retrospectives can be used as a mechanism for process improvement in Agile projects

* Resrospective topics
	- process, people, organizations, relationships, and tools
	- test specific: test effectiveness, test productivity, test case quality, and team satisfaction

## FA-1.2.4 (K2) Understand the use and purpose of continuous integration
* benefits
	* Allows earlier detection and easier root cause analysis of integration problems and conflicting changes
	* Gives the development team regular feedback on whether the code is working
	* Keeps the version of the software being tested within a day of the version being developed
	* Reduces regression risk associated with developer code refactoring due to rapid re-testing of the code base after each small set of changes
	* Provides confidence that each day’s development work is based on a solid foundation
	* Makes progress toward the completion of the product increment visible, encouraging developers and testers
	* Eliminates the schedule risks associated with big-bang integration
	* Provides constant availability of executable software throughout the sprint for testing, demonstration, or education purposes
	* Reduces repetitive manual testing activities
	* Provides quick feedback on decisions made to improve quality and tests
* challenges
	* Continuous integration tools have to be introduced and maintained
	* The continuous integration process must be defined and established
	* Test automation requires additional resources and can be complex to establish
	* Thorough test coverage is essential to achieve automated testing advantages

## FA-1.2.5 (K1) Know the differences between iteration and release planning, and how a tester adds value in each of these activities

* testers in release plannning
	- Defining testable user stories, including acceptance criteria
	- Participating in project and quality risk analyses
	- Estimating testing effort associated with the user stories
	- Defining the necessary test levels
	- Planning the testing for the release 
* testers in iteration planning
	- Participating in the detailed risk analysis of user stories
	- Determining the testability of the user stories
	- Creating acceptance tests for the user stories
	- Breaking down user stories into tasks (particularly testing tasks)
	- Estimating testing effort for all testing tasks
	- Identifying functional and non-functional aspects of the system to be tested
	- Supporting and participating in test automation at multiple levels of testing

## FA-2.1.1 (K2) Describe the differences between testing activities in Agile projects and non-Agile projects

## FA-2.1.2 (K2) Describe how development and testing activities are integrated in Agile projects

## FA-2.1.3 (K2) Describe the role of independent testing in Agile projects
Agile organizations may encounter some test-related organizational risks:
* Testers work so closely to developers that they lose the appropriate tester mindset
* Testers become tolerant of or silent about inefficient, ineffective, or low-quality practices within the team
* Testers cannot keep pace with the incoming changes in time-constrained iterations

3 options

* in Agile team
	- good understanding features, strong relationships with members
	- lack of independency
* separate from Agile team
	- well dependency leads to well finding defects
	- lack of understanding features, relationships with members
* one in Agile team, and others separate from Agile team
	- good understanding features, strong relationships, independent
	- requires haed counts

## FA-2.2.1 (K2) Describe the tools and techniques used to communicate the status of testing in an Agile project, including test progress and product quality

* task board
	- progress of story and testing tasks
* burndown chart
	- amount of remaining work
* daily stand-up meeting
	- done from previous meeting
	- will be done until next meeting
	- obstacles (blockers)
* wiki
* e-mail

## FA-2.2.2 (K2) Describe the process of evolving tests across multiple iterations and explain why test automation is important to manage regression risk in Agile projects

* why regression risks? high code churn
* exec all previous tests is almost impossible (seldom possible) even if automated
* automation in all test levels
* testers should consider suitability for automation
* team needs to automate as many as possible
* testers need to select test cases that may be candidates for the regression test suite, and to retire test cases that are no longer relevant
* automated acceptance testing in CI
	- at least once in a day
	- not for every code changing due to execution time is long
* build verification testing
	- test cases subset to cover critical system functionality and integration points should be created immediately after a new build is deployed into the test environment. 

## FA-2.3.1 (K2) Understand the skills (people, domain, and testing) of a tester in an Agile team

## FA-2.3.2 (K2) Understand the role of a tester within an Agile team

* Understanding, implementing, and updating the test strategy
* Measuring and reporting test coverage across all applicable coverage dimensions
* Ensuring proper use of testing tools
* Configuring, using, and managing test environments and test data
* Reporting defects and working with the team to resolve them
* Coaching other team members in relevant aspects of testing
* Ensuring the appropriate testing tasks are scheduled during release and iteration planning
* Actively collaborating with developers and business stakeholders to clarify requirements, especially in terms of testability, consistency, and completeness
* Participating proactively in team retrospectives, suggesting and implementing improvements 

## FA-3.1.1 (K1) Recall the concepts of test-driven development, acceptance test-driven development, and behavior-driven development

## FA-3.1.2 (K1) Recall the concepts of the test pyramid

## FA-3.1.3 (K2) Summarize the testing quadrants and their relationships with testing levels and testing types

## FA-3.1.4 (K3) For a given Agile project, practice the role of a tester in a Scrum team

## FA-3.2.1 (K3) Assess quality risks within an Agile project

An example of how the quality risk analysis during iteration planning:
1. Gather the Agile team members together, including the tester(s)
2. List all the backlog items for the current iteration (e.g., on a task board)
3. Identify the quality risks associated with each item, considering all relevant quality characteristics
4. Assess each identified risk, which includes two activities: categorizing the risk and determining its level of risk based on the impact and the likelihood of defects
5. Determine the extent of testing proportional to the level of risk.
6. Select the appropriate test technique(s) to mitigate each risk, based on the risk, the level of risk, and the relevant quality characteristic.


## FA-3.2.2 (K3) Estimate testing effort based on iteration content and quality risks

* the estimators discuss the differences in estimates after which the poker round is repeated until agreement is reached
* (e.g., use the median, use the highest score) to limit the number of poker rounds. 

## FA-3.3.1 (K3) Interpret relevant information to support testing activities

## FA-3.3.2 (K2) Explain to business stakeholders how to define testable acceptance criteria

## FA-3.3.3 (K3) Given a user story, write acceptance test-driven development test cases

test basis
* Experience from previous projects
* Existing functions, features, and quality characteristics of the system
* Code, architecture, and design
* User profiles (context, system configurations, and user behavior)
* Information on defects from existing and previous projects
* A categorization of defects in a defect taxonomy
* Applicable standards (e.g., [DO-178B] for avionics software)
* Quality risks (see Section 3.2.1)

acceptance criteria address the following topics
* functional behavior
* quality characteristics
* scenarios
* business rules
* external interfaces
* constraints
* data definitions

definition of done
* user story
	- The user stories selected for the iteration are complete, understood by the team, and have detailed, testable acceptance criteria
	- All the elements of the user story are specified and reviewed, including the user story acceptance tests, have been completed
	- Tasks necessary to implement and test the selected user stories have been identified and estimated by the team 
* feature
	- All constituent user stories, with acceptance criteria, are defined and approved by the customer
	- The design is complete, with no known technical debt
	- The code is complete, with no known technical debt or unfinished refactoring
	- Unit tests have been performed and have achieved the defined level of coverage
	- Integration tests and system tests for the feature have been performed according to the defined coverage criteria
	- No major defects remain to be corrected
	- Feature documentation is complete, which may include release notes, user manuals, and online help functions
* iteration
	- All features for the iteration are ready and individually tested according to the feature level criteria
	- Any non-critical defects that cannot be fixed within the constraints of the iteration added to the product backlog and prioritized
	- Integration of all features for the iteration completed and tested
	- Documentation written, reviewed, and approved
* release
	- Coverage: All relevant test basis elements for all contents of the release have been covered by testing. The adequacy of the coverage is determined by what is new or changed, its complexity and size, and the associated risks of failure.
	- Quality: The defect intensity (e.g., how many defects are found per day or per transaction), the defect density (e.g., the number of defects found compared to the number of user stories, effort, and/or quality attributes), estimated number of remaining defects are within acceptable limits, the consequences of unresolved and remaining defects (e.g., the severity and priority) are understood and acceptable, the residual level of risk associated with each identified quality risk is understood and acceptable.
	- Time: If the pre-determined delivery date has been reached, the business considerations associated with releasing and not releasing need to be considered.
	- Cost: The estimated lifecycle cost should be used to calculate the return on investment for the delivered system (i.e., the calculated development and maintenance cost should be considerably lower than the expected total sales of the product). The main part of the lifecycle cost often comes from maintenance after the product has been released, due to the number of defects escaping to production.

* ATDD
	- In any case, an independent person such as a business representative validates the tests
	- The tests are examples that describe the specific characteristics of the user story. 

## FA-3.3.4 (K3) For both functional and non-functional behavior, write test cases using black box test design techniques based on given user stories


## FA-3.3.5 (K3) Perform exploratory testing to support the testing of an Agile project

A test charter may include the following information:
* Actor: intended user of the system
* Purpose: the theme of the charter including what particular objective the actor wants to achieve, i.e., the test conditions
* Setup: what needs to be in place in order to start the test execution
* Priority: relative importance of this charter, based on the priority of the associated user story or the risk level
* Reference: specifications (e.g., user story), risks, or other information sources
* Data: whatever data is needed to carry out the charter
* Activities: a list of ideas of what the actor may want to do with the system (e.g., “Log on to the system as a super user”) and what would be interesting to test (both positive and negative tests)
* Oracle notes: how to evaluate the product to determine correct results (e.g., to capture what happens on the screen and compare to what is written in the user’s manual)
* Variations: alternative actions and evaluations to complement the ideas described under activities


## FA-3.4.1 (K1) Recall different tools available to testers according to their purpose and to activities in Agile projects

