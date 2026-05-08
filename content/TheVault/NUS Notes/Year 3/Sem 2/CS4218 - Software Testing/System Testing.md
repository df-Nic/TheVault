---
Title: System Testing
Date Created: 24-January-2026
Last Updated: 22-March-2026
Tags:
  - CS4218
  - SWE/Testing/SystemTesting
---
# System Testing
---
It is the process of <b><span style='color: #FFD700'>evaluating a complete integrated system</span></b> (*test as a whole*) to determine if it meets all specified requirements.

Here are the **key characteristics** of system testing:
- <b><span style='color: #FFD700'>End-to-end user journey evaluation</span></b> (*testing the complete business process from start to end*)
- [[System Testing.md#Testing Methodologies|Black box approach]] (*Testing is all done from the user's perspective, no internal code*)

>[!goal] The goal of system testing is to verify that the UI & associated application flows meet business requirements & design specification
>It is entirely business focus to determine if the product is ready for release.

System testing consist of 2 crucial layers of testing:
![[Images/CS4218 Images/Test Pyramid.png|center|550]]

System testing is <b><span style='color: #FFD700'>non-negotiable</span></b> (*not optional*) as it ensure the product is <b><span style='color: #98FB98'>customer-ready</span></b>. So why is it non-negotiable:
- It <b><span style='color: #FFD700'>focuses on customer experience</span></b> by validating end-to-end journey & ensures the product works as if a real customer uses it
- <b><span style='color: #FFD700'>Validating functional workflows</span></b> by confirming all integrated components work together to achieve the required business results
- <b><span style='color: #FFD700'>Environment validation</span></b>, by testing in an environment that mimics the final production environment to catch integration failures
- <b><span style='color: #FFD700'>Validation of non-function aspects</span></b>, which is more on the non-functional requirements

>[!abstract] System testing best practices
>1) **Execution environment**, testing is done in a <b><span style='color: #FFD700'>stable QA or staging environment</span></b> which is isolated & <b><span style='color: #FFD700'>fully representative of production</span></b>
>2) **Test case design** (*black box*), derived from <b><span style='color: #FFD700'>user stories & mockups</span></b>, focusing on <b><span style='color: #FFD700'>simulating realistic user paths</span></b> and input.
>3) **Automation & frameworks**, use [[Year 3/Sem 2/CS4218 - Software Testing/System Testing.md#UI Test Tools|automated tools]] for user interactions in the browser level & <b><span style='color: #FFD700'>prioritise critical business paths</span></b> for automation
>4) **Traceability**, ensure every critical user story & UI specification has <b><span style='color: #FFD700'>at least 1</span></b> corresponding E2E or UI system test case & <b><span style='color: #FFD700'>verified using a requirements traceability matrix</span></b> (*RTM*)
## Testing Methodologies

|        Feature        |                                                      Black Box Testing                                                      |                                                                            White Box Testing                                                                             |
| :-------------------: | :-------------------------------------------------------------------------------------------------------------------------: | :----------------------------------------------------------------------------------------------------------------------------------------------------------------------: |
|      Perspective      |                                                   External (*User view*)                                                    |                                                                       Internal (*Developer View*)                                                                        |
| Knowledge<br>Required |                    <b><span style='color: #FFD700'>None</span></b> of internal structure, code or design                    |                                          <b><span style='color: #FFD700'>Full</span></b> of internal structure, code or design                                           |
|         Focus         |                               Functionality, requirements, user workflows & system behaviour                                |                                                    Code integrity, security flaws, performance & internal logic paths                                                    |
|         Goal          | Verify UI & application flows <b><span style='color: #FFD700'>meet business requirements & design specifications</span></b> |    Ensure all code paths are executed, performance is optimised, no security vulnerabilities exist. <b><span style='color: #FFD700'>More on functionality</span></b>     |
|        Tester         |                                           QA Testers, Business Analyst, End-users                                           |                                                                Developers, QA Engineers, Security Experts                                                                |
| Common<br>Techniques  |                                       Functional, regression, UI & acceptance testing                                       | Unit, integration, testing, code coverage analysis, [[Year 2/Sem 2/CS3213 - Foundations of Software Engineering/Software Testing.md#Mutation Testing\|mutation testing]] |
|        Used In        |                                   System testing, acceptance testing, integration testing                                   |                                                              Unit testing, lower level integration testing                                                               |
Neither of the 2 are better than the other, they are <b><span style='color: #FFD700'>complementary with one another</span></b>.

>[!info] There is also grey box which is somewhere in-between where the user as some partial knowledge of the code

>[!important] In summary white box ensures code is built correctly, while black box ensure product is built correctly

## Functional System Testing

Here we <b><span style='color: #FFD700'>prove that the system actually works</span></b>, end-to-end as designed. This is composed of 4 critical activities:
1) Functional **end-to-end** (*E2C*) testing
2) **User interface** testing
3) **Cross browser & cross device** testing (*ensure everything works regardless of browser or device*)
4) **Regression** testing (*ensure changes does not break existing working functionality*)
### Functional End-To-End Testing

Here we <b><span style='color: #FFD700'>validate a complete business workflow under real user scenarios</span></b>, to <b><span style='color: #FFD700'>ensure that it is seamless & correct</span></b>.

>[!info] Complete business workflow
>Essentially it start from the first input, through all the application layers & integrated services to the final result & post conditions (*like database state at the end*).

>[!success] Catches integration issues
>It runs real user scenarios & verify that the system & its dependencies behave as expected when used together.

>[!success] Improve software quality
>Detects defects from interactions among components / workflow failures

>[!success] Ensures process consistency
> Validate full data & workflow integrity across the entire app, resulting in <b><span style='color: #98FB98'>higher user trust</span></b>.
### User Interface Testing

Here we <b><span style='color: #FFD700'>verify all visual elements & controls</span></b> (*buttons, links, forms etc*) work as expected, <b><span style='color: #FFD700'>ensuring a positive, seamless & correct interaction</span></b> between the user & the app (*typically within a single screen*).

We want to achieve a <b><span style='color: #98FB98'>good user experience</span></b>. If its functionally correct but confusing to use when the system is designed badly. So it must <b><span style='color: #FFD700'>meet design specifications & free from usability or visual flaws</span></b>.

>[!abstract] Key objectives of UI testing
>- **Functionality**, ensuring that every UI element works as designed
>- **Visual consistency**, ensuring the layout, alignment, fonts & colors are rendered properly across devices & screen sizes
>- **Usability**, the interface is pleasant & easy for users to navigate, understand & interact with
>- **Responsiveness**, the UI should adapt & respond smoothly
>- **Error handling**, the feedback & error messages should be clear & helpful when mistakes are made

>[!abstract] Ways of UI testing
>- **Manual** testing, humans interacts & do the checks
>- **Automated** testing, using test scripts to simulate user interactions for rapid, repeatable validation of UI
>- **Exploratory** testing, testers explore UI to discover issues that may not be covered by formal test cases
>- **Usability** testing, done by real users & their interactions, issues & feedback are observed to improve appearance & user experience

>[!warning] UI testing does not complete a full business transaction
>It <b><span style='color: #FFD700'>just validates the look & feel</span></b>, ensuring that the interface is responsive accessible & visually correct regardless of backend processes

>[!important] Best practices for UI testing
> 1) **Test navigation & workflows**, ensures users can navigate without confusion or errors
> 2) **Validate edge cases**, check how the UI handles unexpected inputs or actions
> 3) **Automate repetitive tests**, use automated tools to cover routine or regression test & speed up development
> 4) **Include responsive & cross-platform checks**, check if the UI works across browsers & devices
> 5) **Visual regression testing**, use tools to catch unintended visual changes after updates
#### UI Test Tools

These tools help automate testing of UI:
- **Selenium**
Used for cross browser testing & supports multiple programming languages & platforms

- **Cypress**
A JavaScript based front end testing, It is fast, reliable test execution with excellent developer experience

- **Playwright**
Used for cross browser testing since it supports multiple browsers. It can be used for complex UI workflows as it can handle multiple browser contexts & tabs efficiently.

It is also has good debugging capabilities, automated waiting for element to be ready & robust support for modern app features.
## Non-Functional System Testing

Here we <b><span style='color: #FFD700'>test how well the system performs under various conditions</span></b>. It is important because it <b><span style='color: #FFD700'>validates the systems usability & robustness</span></b>.

>[!abstract] Types of NFT testing which can be done
>- **Performance** testing
To test for speed, response time, stability, scalability, resource usage under various conditions (*stress testing*).
> - **Security** testing
> Checks for system vulnerabilities, access control, data protection & compliance with security standards.
> - **Usability** testing
> Evaluates ease of use, user interface, navigation & accessibility
> - **Compatibility** testing
> Verifies the system works across platforms, browsers, devices & operation systems
> - **Recovery** testing
> Accesses the system's ability to recover from failures, crashes or errors ensuring stability & reliability
