# Software Quality

## Code Reviews
>Code review (sometimes referred to as peer review) is a software quality assurance activity in which one or several people check a program mainly by viewing and reading parts of its source code, and they do so after implementation or as an interruption of implementation.
>At least one of the persons must not be the code's author. The persons performing the checking, excluding the author, are called "reviewers".
[Wikipedia on Code review](https://en.wikipedia.org/wiki/Code_review)

In both the Individual and Group project Code Reviews are used for reasons mentioned above.

In the group project we have a Jira Board issue status 'Ready for review' where at least 1 person must have reviewed and approved your code before it can be marked as 'Done'. 

## Unit Testing
>In computer programming, unit testing is a software testing method by which individual units of source code—sets of one or more computer program modules together with associated control data, usage procedures, and operating procedures—are tested to determine whether they are fit for use.
[Wikipedia on Unit testing](https://en.wikipedia.org/wiki/Unit_testing)

### Unit Testing in Group Project
In our group project, we place significant importance on unit testing. We aim to achieve high code coverage, which means that we test the vulnerable parts of our code to ensure their reliability.
Unit tests not only help identify potential issues but also contribute to the Continuous Integration and Continuous Deployment (CI/CD) process of our projects.

### Unit Testing in Individual Project
I have made Unit Tests on the Front-end Google Maps API, these unit tests, test whether the API calls return the correct information, I do this by mocking with Axios-Mock-Adapter, and I test using the Jest.

Unit tests are automatically run in the [test workflow](https://github.com/Dpils-s/Rider-maps/blob/main/.github/workflows/ci.yml) of the User-Preferences-API

## Important Questions
### What do you consider to be software of high quality?
Software is of high quality when it:
- Serves the purpose it was made for.
- Has no bugs or unintended side affects.
- Is well tested where and when it's needed.
- Is maintainable
- Is readable/understandable (with help of comments)
- Code has documentation where necessary

## Key Aspects of High-Quality Software
### High-quality software encompasses several essential aspects.
Here are the key factors that contribute to software of high quality:
-Purposeful and serves its intended goal.
-Free of bugs and unintended side effects.
-Well-tested at different levels.
-Maintainable and follows best practices.
-Readable and understandable, aided by comments.
-Documented appropriately.



