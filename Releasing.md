# Releasing Elytron MicroProfile

To release Elytron MicroProfile first checkout the project and ensure you are on the latest commit for the branch you are releasing with no local changes.

Prior to releasing you should ensure you have your own GPG signing key set up, published to a key server and listed on [wildfly.org](https://www.wildfly.org/contributors/pgp/).

## Prepare the release

Execute:

    mvn release:prepare

Note: The `-Pjboss-release` profile is automatically activated by the maven-release-plugin (configured in jboss-parent-pom), but can be explicitly specified for clarity:

    mvn release:prepare -Pjboss-release

Enter the version being released:

    What is the release version for "WildFly Elytron MicroProfile"? (wildfly-elytron-mp) 2.1.0.CR1: 2.1.0.Final

The tag will default to the version:

    What is the SCM release tag or label for "WildFly Elytron MicroProfile"? (wildfly-elytron-mp) 2.1.0.Final:

Set the next version:

    What is the new development version for "WildFly Elytron MicroProfile"? (wildfly-elytron-mp) 2.1.1.Final-SNAPSHOT: 2.2.0.CR1-SNAPSHOT

The release commit can be checked with:

    git show ${TAG}

If everything is Ok perform the release which will deploy to Nexus.

## Perform the release

Execute:

    mvn release:perform

Note: The `-Pjboss-release` profile is automatically activated by the maven-release-plugin (configured in jboss-parent-pom), but can be explicitly specified for clarity:

    mvn release:perform -Pjboss-release

This will deploy the release to the `wildfly-staging` repository.

Wait for 10 minutes then visit the Validation task for the `wildfly-staging` repository in Nexus. If this task ran at least 10 minutes after the release was deployed check the latest results on the Settings tab and verify that at least one component was processed and that there were no errors. If the task has not run it can be manually kicked off using the Run button.

e.g.

> Processed 2 components.
> - no errors were found.
> - the deployment was a dry run (no actual publishing).

If others are also deploying at the same time this count could be higher, the important check is that the scan was at least 10 minutes after it was deployed, 1 or more components were scanned and no errors specific to Elytron MicroProfile are reported.

Nexus only scans components once if there are no issues so if you check these results after multiple scans the component count may be back to 0.

## Complete the release

If no issues are reported complete the release.

Move the component to the `wildfly-security` repository:

    git checkout ${TAG}
    mvn nxrm3:staging-move
    git checkout ${BRANCH}

Push the branch and tag to GitHub:

    git push upstream ${BRANCH}
    git push upstream ${TAG}

## Rollback the Release

If the release failed, revert the release.

Delete the component from Nexus:

    git checkout ${TAG}
    mvn nxrm3:staging-delete
    git checkout ${BRANCH}

Reset your local Git checkout:

    git reset --hard upstream/${BRANCH}
    git tag --delete ${TAG}
