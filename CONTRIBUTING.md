Contributing to WildFly Elytron MicroProfile
=============================================

Welcome to the WildFly Elytron MicroProfile project! We welcome contributions from the community. This guide will walk you through the steps for getting started on our project.

- [Forking the Project](#forking-the-project)
- [Issues](#issues)
  * [Good First Issues](#good-first-issues)
- [Setting up your Developer Environment](#setting-up-your-developer-environment)
- [Contributing Guidelines](#contributing-guidelines)
- [Community](#community)


## Forking the Project 
To contribute, you will first need to fork the [wildfly-elytron-mp](https://github.com/wildfly-security/wildfly-elytron-mp) repository. 

This can be done by looking in the top-right corner of the repository page and clicking "Fork".

The next step is to clone your newly forked repository onto your local workspace. This can be done by going to your newly forked repository, which should be at `https://github.com/USERNAME/wildfly-elytron-mp`. 

Then, there will be a green button that says "Code". Click on that and copy the URL.

![clone](assets/images/clone.png)

Then, in your terminal, paste the following command:
```bash
git clone [URL]
```
Be sure to replace [URL] with the URL that you copied.

Now you have the repository on your computer!

## Issues
The WildFly Elytron MicroProfile project uses JIRA to manage issues. All issues can be found [here](https://issues.redhat.com/projects/ELYMP/issues). 

To create a new issue, comment on an existing issue, or assign an issue to yourself, you'll need to first [create a JIRA account](https://issues.redhat.com/).


### Good First Issues
Want to contribute to the WildFly Elytron MicroProfile project but aren't quite sure where to start? Check out our issues with the `good-first-issue` label. These are a triaged set of issues that are great for getting started on our project.

Once you have selected an issue you'd like to work on, make sure it's not already assigned to someone else. Then, remember to assign it to yourself, by clicking on "Assign to me", to prevent someone else from also working on the same issue.

It is recommended that you use a separate branch for every issue you work on. To keep things straightforward and memorable, you can name each branch using the JIRA issue number. This way, you can have multiple PRs open for different issues. For example, if you were working on [ELYMP-123](https://issues.redhat.com/browse/ELYMP-123), you could use ELYMP-123 as your branch name.

## Setting up your Developer Environment
You will need:

* JDK 25 (for building; optionally JDK 17, 21 for multi-version testing)
* Git
* Maven 3.3.9 or later
* An [IDE](https://en.wikipedia.org/wiki/Comparison_of_integrated_development_environments#Java)
(e.g., [IntelliJ IDEA](https://www.jetbrains.com/idea/download/), [Eclipse](https://www.eclipse.org/downloads/), etc.)

First `cd` to the directory where you cloned the project (eg: `cd wildfly-elytron-mp`)

Add a remote ref to upstream, for pulling future updates.
For example:

```
git remote add upstream https://github.com/wildfly-security/wildfly-elytron-mp
```
To build `wildfly-elytron-mp` run:
```bash
mvn clean install
```

The default build expects Java 25 on `PATH` and in `JAVA_HOME`. The project is compiled with Java 25 and targets Java 17 bytecode.

To run tests with specific JDK versions (17, 21, or 25), configure Maven toolchains first:

1. Copy `toolchains.xml.template` from the repository root to `~/.m2/toolchains.xml`
2. Update the JDK home paths in that file for your local machine
3. Run Maven with the desired test JDK selection

Examples:

```bash
mvn test -Djdk.test.version=17
mvn test -Djdk.test.version=21
mvn test -Djdk.test.version=25
mvn test -Djdk.test.version=21 -Djdk.test.vendor=semeru
mvn install -Ptest-all-versions
```

The GitHub Actions workflows use the same toolchain-based approach. Contributors should expect:
- pull requests to run Linux CI for Java 17, 21, and 25 on both Temurin and Semeru
- nightly CI to run the full Linux, Windows, and macOS matrix for the same JDK combinations
- a separate non-LTS workflow to exercise the latest non-LTS JDK on all supported platforms

If you do not configure `~/.m2/toolchains.xml`, the default `mvn clean install` workflow still works with Java 25.

To skip the tests, use:

```bash
mvn clean install -DskipTests=true
```

To run only a specific test, use:

```bash
mvn clean install -Dtest=TestClassName
```
For more information about WildFly Elytron, check out the [WildFly Elytron documentation](https://wildfly-security.github.io/wildfly-elytron/).

## Contributing Guidelines

When submitting a PR, please keep the following guidelines in mind:

1. In general, it's good practice to squash all of your commits into a single commit. For larger changes, it's ok to have multiple meaningful commits. If you need help with squashing your commits, feel free to ask us how to do this on your pull request. We're more than happy to help!

2. Please include the JIRA issue you worked on in the title of your pull request and in your commit message. For example, for [ELYMP-123](https://issues.redhat.com/browse/ELYMP-123), the PR title and commit message should be `[ELYMP-123] Add MicroProfile JWT authentication support`.

3. Please include the link to the JIRA issue you worked on in the description of the pull request. For example, if your PR adds a fix for [ELYMP-123](https://issues.redhat.com/browse/ELYMP-123), the PR description should contain a link to https://issues.redhat.com/browse/ELYMP-123.

## Community
For more information on how to get involved with WildFly Elytron and related projects, check out the [WildFly Elytron community](https://wildfly-security.github.io/wildfly-elytron/community/) page.

## Legal

All contributions to this repository are licensed under the [Apache License](https://www.apache.org/licenses/LICENSE-2.0), version 2.0 or later, or, if another license is specified as governing the file or directory being modified, such other license.

All contributions are subject to the [Developer Certificate of Origin (DCO)](https://developercertificate.org/).
The DCO text is also included verbatim in the [dco.txt](https://github.com/wildfly-security/.github/blob/main/dco.txt) file in the .github repository of the wildfly-security organization.

## Compliance with Laws and Regulations

All contributions must comply with applicable laws and regulations, including U.S. export control and sanctions restrictions.
For background, see the Linux Foundation’s guidance:
[Navigating Global Regulations and Open Source: US OFAC Sanctions](https://www.linuxfoundation.org/blog/navigating-global-regulations-and-open-source-us-ofac-sanctions).