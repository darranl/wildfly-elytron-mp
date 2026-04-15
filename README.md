WildFly Elytron MicroProfile
============================

[WildFly Elytron](https://wildfly-security.github.io/wildfly-elytron/) MicroProfile integration provides security components for MicroProfile applications.

Building From Source
--------------------

```console
$ git clone git@github.com:wildfly-security/wildfly-elytron-mp.git
```

Setup the JBoss Maven Repository
--------------------------------

To use dependencies from JBoss.org, you need to add the JBoss Maven Repositories to your Maven settings.xml. For details see [Maven Getting Started - Users](https://developer.jboss.org/docs/DOC-15169)

Build with Maven
----------------

The command below builds the project and runs the embedded suite.

```console
$ mvn clean install
```

For detailed developer setup, including Java 25 requirements, Maven toolchains configuration, and CI workflow expectations for contributors, see [CONTRIBUTING.md](CONTRIBUTING.md).

Issue Tracking
--------------

Bugs and features are tracked within the Elytron Jira project at https://issues.jboss.org/browse/ELY

Contributions
-------------

All new features and enhancements should be submitted to 1.x branch only.
Our [contribution guide](https://github.com/wildfly-security/wildfly-elytron/blob/1.x/CONTRIBUTING.md) will guide you through the steps for getting started on the WildFly Elytron project and will go through how to format and submit your first PR.
 
For more details, check out our [getting started guide](https://wildfly-security.github.io/wildfly-elytron/getting-started-for-developers/) for developers.
