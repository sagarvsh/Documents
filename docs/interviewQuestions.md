# CICD Interview Questions

We believe that these questions/exercise will help the candidates to get the right expectations about the type of work that (s)he is goin to get. This will also help us to fitler candidates who are not suitable for the position.

**Try to answer maximum questions. Feel free to use Google. Please upload the answers to a github repository and share us the URL.

1. Configure Jenkins job to trigger SonarQube analysis on Pull Requests/Code Reviews?
2. Write a Jenkins pipelin to fetch source from GitHub and publish the (Java/NodeJS) artifacts to Artifactory/nexus repository.
3. Create a container(Docker) image that contains an application server with above build artifacts.
Define Deployment, Service yaml/json files to deploy above container image on to Kubernetes/OpenShift platforms.
Write a Cookbook/Playbook to host a simple application server with above build artifacts (Question 2).

Data Flow?

##### Branching Statergy


common libraries in Jenkins

Multi branch pipeline vs  Org scan job

??? tip "HOW TO DO SECURITY? LEAST PRIVILEGE"

    * Handling "Least privileges" concepts helps you manage the AAA concepts:

        * Authentication — Control who can access the system

        * Authorization — Control what each user can do on the system

        * Accounting — Monitor your system to ensure that only valid processes are executing

#### HOW JENKINS EXECUTES A PIPELINE

A simple overview of how Jenkins executes a Pipeline helps us understand the security considerations:

By default, the Pipeline executes with the full privileges of the Jenkins administrator

You can configure Jenkins to execute Pipelines with fewer privileges

All of the Pipeline logic, the Groovy conditionals, loops, etc execute on the master

Creates a workspace for each build that runs

Stores files created for that build

The Pipeline calls steps that run on agents

#### WHAT AGENTS DO

The Pipeline calls a series of steps, each of which is a script or command that does the real work and mostly executes using an executor on an agent

Agent writes some files to the local node

Agent sends data back to the master

Agent can also request information from the master



??? tip "What is Declarity pipeline vs scripted pipeline"

    Scripted: sequential execution, using Groovy expressions for flow control

    Declarative: uses a framework to control execution

??? tip "Explain Jenkins Pipeline"

    [JENKINS PIPELINE](jenkins.io/doc/book/pipeline)

    Jenkins Pipeline is a tool for defining your Continuous Delivery/Deployment flow as code

    * New fundamental "type" in Jenkins that conceptualizes and models a Continuous Delivery process

    * Two syntaxes:

        * **Scripted: sequential execution, using Groovy expressions for flow control**

        * **Declarative: uses a framework to control execution**

    * Uses the Pipeline DSL (Domain-specific Language)

        * programmatically manipulate Jenkins Objects

    * Captures the entire continuous delivery process as code

        * Pipeline is *not* a job creation tool like the Job DSL plugin or Jenkins Job Builder

??? tip "What are pipeline benefits"
    
        PIPELINE BENEFITS (1/2)
        The pipeline functionality is:

        Durable: The Jenkins master can restart and the Pipeline continues to run

        Pausable: can stop and wait for human input or approval

        Versatile: supports complex real-world CD requirements (fork, join, loop, parallelize)

        Extensible: supports custom extensions to its "DSL" (Domain-specific Language)

        PIPELINE BENEFITS (2/2)
        Reduces number of jobs

        Easier maintenance

        Decentralization of job configuration

        Easier specification through code

??? tip "JENKINS VOCABULARY"

    * Master:

        - Computer, VM or container where Jenkins is installed and run

        - Serves requests and handles build tasks

    * Agent: (formerly "slave")

        - Computer, VM or container that connects to a Jenkins Master

        - Executes tasks when directed by the Master

        - Has a number and scope of operations to perform.

    * Node is sometimes used to refer to the computer, VM or container used for the Master or Agent; be careful because "Node" has another meaning for Pipeline

    * Executor:

        - Computational resource for running builds

        - Performs Operations

        - Can run on any Master or Agent, although running builds on masters can degrade performance and opens up serious security vulnerabilities

        - Can be parallelized on a specific Master or Agent

??? tip "JENKINS PIPELINE SECTIONS"

    * The Jenkinsfile that defines a Pipeline uses a DSL based on Apache Groovy syntax

        * Is structured in sections, called stages

        * Each stage includes steps

        * steps include the actual tests/commands to run

        * An agent defines where the programs and scripts execute

    * This is illustrated in the following simple Jenkinsfile:

        ``` groovy
        pipeline {
        agent { label 'linux' }
        stages {
            stage('MyBuild') {
            steps {
                sh './jenkins/build.sh'
            }
            }
            stage('MySmalltest') {
            steps {
                sh './jenkins/smalltest.sh'
                }
            }
            }
        }
        ```

??? tip "DECLARATIVE VERSUS SCRIPTED PIPELINE"

    * Two different syntaxes for Pipeline

    * Both are built on same Pipeline subsystem

    * Both definitions are stored in a Jenkinsfile under SCM ("Pipeline-as-code")

    * Both rely on the Pipeline DSL, which is based on Apache Groovy syntax

    * Both can use steps built into Pipeline or provided in plugins

    * Both support shared libraries

??? tip "SCRIPTED PIPELINE"

    * Executed serially, from top down

    * Relies on Groovy expressions for flow control

        * Requires extensive knowledge of Groovy syntax

    * Very flexible and extensible

        * Limitations are mostly Groovy limitations

        * Power users with complex requirements may need it

    * Novice users can easily mess up the syntax

??? tip "DECLARATIVE PIPELINE"

    * Stricter, pre-defined structure

    * Execution can always be resumed after an interruption, no matter what caused the interruption

    * Requires only limited knowledge of Groovy syntax

        * Using Blue Ocean simplifies the Pipeline creation process even more

    * Encourages a declarative programming model

    * Reduces the risk of syntax errors

    * Use the script step to include bits of scripted code within a Declarative Pipeline only when you have needs that are beyond the capabilities of Declarative syntax

??? tip "PIPELINE CONCEPTS"

    * Pipeline is "glue" code that binds tasks together into a CD flow.

        * Use the Pipeline DSL for CI/CD scripting only!

        * Do not code arbitrary networking and computational tasks into the Pipeline itself

        * Use tools like Maven, Gradle, NPM, Ant and Make to do the majority of the build “work”

        * Use scripts written in Shell, Batch, or Python for other related tasks

        * Then call these executables as steps in your Pipeline

    * Declarative Pipeline keeps the complex logic of individual steps separate from the Pipeline itself, making the Pipeline code clean to read

??? tip "What is Archive Artifacts post stage in Jenkins Pipeline"

    * Use the pipeline step archiveArtifacts

    * Requires a pattern to know which artifacts to archive

        - my-app.zip:

            - The file my-app.zip, at the workspace’s root

        - images/*.png:

            - All files with .png extension in the images folder at the workspace’s root

        - target/**/*.jar:

            - All files with .jar extension, recursively under the target folder, at the workspace’s root

    * Archiving keeps those files in ${JENKINS_HOME} forever unless you delete them

    ??? tip "FINGERPRINTS"

    * A fingerprint is the MD5 checksum of an artifact

    * Each archived artifact can be fingerprinted; merely check the "Fingerprint" box when you create the archiving step

    * Jenkins uses Fingerprints to keep track of artifacts without any ambiguity

    * A database of all fingerprints is managed on the Master

        - Located in the ${JENKINS_HOME}/fingerprints directory

??? tip "USING ARCHIVED ARTIFACTS"

    * In a production environment, your build chain system (Maven, Gradle, Make, etc.) publishes artifacts to an artifact repository such as Artifactory, Nexus, etc.

    * Teams can also deploy artifacts from Jenkins to test environments

    * Use the Copy Artifact Plugin to take artifacts from one project (Pipeline run) and copy them to another Project

??? tip "ARTIFACT RETENTION POLICY"

    * Coupled to build retention policy

        - Deleting a build deletes attached artifacts

    * Good practice: discard build and clean it

        - Driven by age: # days to keep a build

        - Driven by number: Max # of builds to keep

    * Important builds can individually be Kept Forever


??? tip "WHAT IS JUNIT?"

    * As an external application, JUnit is a common testing framework for Java programs

    * In the Jenkins context, JUnit is a publisher that consumes XML test reports

        - Generates some graphical visualization of the historical test results

        - Provides a web UI for viewing test reports, tracking failures and so forth

        - Useful for tracking test result trends

        - Works with all supported build tools

            - You must specify the appropriate path name for the XML test reports generated by the build tool you are using

    * JUnit in this course means the Jenkins publisher

??? tip "PARALLEL STAGES"

    * Stages can be run in parallel:

        - Long running stages

        - Builds for different target architectures or OSes (Debian/Fedora, Android/iOS) or different software versions (JVM8/11), et cetera

        - Builds of independent modules of your code

        - Unit and integration tests are tied to the code; run them in parallel

??? tip "DECLARATIVE PARALLEL SYNTAX"

    * Each "parallelized branch" is a stage

    * A stage can use either steps or parallel at the top level; it cannot use both

    * A stage within a parallel stage can contain agent and steps sections

    * A parallel stage cannot contain agent or tools

    * Add ***failfast true*** to force all parallel processes to abort if one fails

??? "HOW PARALLEL STAGES ARE SCHEDULED"

    * By default, Jenkins tries to allocate a stage to the last node on which it (or a similar stage) executed.

        * This may mean that multiple parallel steps execute on the same node while other nodes in the cluster are idle

    * Use the Least Load Plugin to replace the default load balancer with one that schedules a new stage to nodes with the least load

??? tip "SCRIPTED PIPELINES IN PRODUCTION"

    * This exercise is a short introduction to Scripted Pipelines

    * Scripted Pipelines used in production have the following characteristics:

    * Jenkinsfile must be created and modified in a text editor

    * Should be Multibranch Pipeline

        - Requires Git, Bitbucket or SVN
        - Must be configured to the SCM repository, with credentials, hooks, etc

    * Must be committed to the SCM like any other code

??? tip "WHAT IS MULTIBRANCH?"

    * Recommended for all new Pipelines

    * All Pipelines created with Blue Ocean are multibranch

    * Requires Git, Bitbucket or SVN

    * Configures a set of branches

        - Jenkins creates a subproject for each branch in the SCM repository

??? tip "WHY MULTIBRANCH"

    * Automatic Workflow creation for each new branch in the repository

        - Assumes that webhooks are registered from the SCM to Jenkins

    * Builds are specific to that child/branch and its unique SCM change and build history

    * Automatic job pruning/deletion for branches deleted from the repository, according to the settings

    * Ability to override the parent properties for a specific branch, if necessary

??? tip "SPECIFY DOCKER AGENT IN PIPELINE"

    * agent { docker }

        - Execute the Pipeline or stage with the specified container

        - The container will be dynamically provisioned on the node

    * agent { dockerfile }

        - Execute the Pipeline or stage with a container built from the specified Dockerfile

??? tip "DOCKER CONTAINER DURABILITY"

    * When you specify a docker container for an agent, Jenkins calls APIs directly

        - These commands are serialized so they can resume after a master restart

    * When you use a shell step to run a Docker command directly, the step is bound to the durable task of the shell

        - The Docker container and any tasks running in it are terminated when the shell terminates

??? tip "SIMPLE SYNTAX"

    Run all Pipeline stages on any node machine:

        ``` groovy
        pipeline {
        agent any
        ....
        }
        Run all Pipeline stages on a node machine tagged as bzzzmaven:

        pipeline {
        agent { label 'bzzzmaven' }
        ....
        }
        ```

    Run all Pipeline stages on a container based on the image bzzzcentos:7:

        ``` groovy
        pipeline {
        agent { docker 'bzzzcentos:7' }
        ....
        }
        ```

??? tip "PER-STAGE AGENT SYNTAX"

    * Do not run stages on an agent by default

    * Run the stage Build on a node machine tagged as bzzzmaven

    * Run the stage Deploy on a node machine tagged as bzzzproduction:

        ``` groovy
        pipeline {
        agent none
        stages {
            stage ('Build') {
            agent { label 'bzzzmaven' }
            steps { ... }
            }
            stage ('Deploy') {
            agent { label 'bzzzproduction' }
            steps { ... }
            }
        }
        }
        ```

??? tip "SPECIFY AGENTS FOR OUR PIPELINE"

    We are building our application to work with both JDK7 and JDK8. This means that we need a JDK7 environment and a JDK8 environment. To implement this:

        * Change the global agent to be agent none; in other words, there is no global agent

        * Specify the appropriate agent (labeled either jdk7 or jdk8) for the build and test steps that need the specific JDK environment.

        * Specify agent any for stages that do not require a specific JDK version.

??? tip "STASH/UNSTASH"

    * Use stash to save a set of files for use later in the same build, but in another stage that executes on another node/workspace

    * Use unstash to restore the stashed files into the current workspace of the other stage

    * Stashed files are discarded at the end of the build

    * Stashed files are archived in a compressed tar file, which works well for small (<5 Mb) files

        - Stashing large files consumes significant resources (especially CPU) on both the Master and agent nodes

        - For large files, consider using:

            - the External Workspace manager plugin

            - an external repository manager such as Nexus or Artifactory

            - the Artifact Manager on S3 plugin (README)

    CALLING SYNTAX

        * stash and unstash are implemented as steps within a stage

        * stash requires one parameter, name, which is a simple identifier for the set of files being stashed

        * By default, stash places all workspace files into the named stash

        * To store files from a different directory (or a subset of the workspace):

            - Use the optional includes parameter to give the name of the files or directories to store. This accepts a set of Ant-style include patterns.

            - Other optional parameters are documented on the Pipeline: Basic Steps reference page

        * To unstash files:

            - Optionally, use the `dir` step to create a directory where the files will be written.

            - Call `unstash`, using the name you assigned with the stash step above.

    IMPLEMENT STASH/UNSTASH (1/2)

        * We are going to make our Pipeline build and test our software for both JDK 7 and JDK 8.

            - We will use stash/unstash to ensure that the JDK 7 tests are run against the JDK 7 build and that the JDK 8 tests are run against the JDK 8 build:

        * Add a step to the "Build Java 7" stage: "Stash some files to be used later in the build"

            - Name the stash "Buzz Java 7"; enter target/** in the "Includes" box to save everything under the target directory

        * Follow the same procedure to stash "Buzz Java 8" in the "Build Java 8" stage

??? tip "CODE: WAIT FOR INPUT"

    The code in the Jenkinsfile looks like:

    ``` groovy
    stage('Confirm Deploy to Staging') {
    agent none
    steps {
        input(message: 'Deploy to Stage', ok: "Yes, let's do it!")
    }
    }
    ```

    * Note that Blue Ocean uses single quotes to enclose the text in the "Message" and "OK" boxes and automatically escapes apostrophes in the text

    * To make the code cleaner, you can use the code editor to use double quotes to enclose the text

??? tip "Sample pipeline"

    ``` groovy
    pipeline {
    agent none
    stages {
        stage('Fluffy Build') {
        parallel {
            stage('Build Java 8') {
            agent {
                node {
                label 'java8'
                }

            }
            steps {
                sh './jenkins/build.sh'
                stash(name: 'Java 8', includes: 'target/**')
            }
            }
            stage('Build Java 7') {
            agent {
                node {
                label 'java7'
                }

            }
            steps {
                sh './jenkins/build.sh'
                archiveArtifacts 'target/*.jar'
                stash(name: 'Java 7', includes: 'target/**')
            }
            }
        }
        }
        stage('Fluffy Test') {
        parallel {
            stage('Backend Java 8') {
            agent {
                node {
                label 'java8'
                }

            }
            steps {
                unstash 'Java 8'
                sh './jenkins/test-backend.sh'
                junit 'target/surefire-reports/**/TEST*.xml'
            }
            }
            stage('Frontend') {
            agent {
                node {
                label 'java8'
                }

            }
            steps {
                unstash 'Java 8'
                sh './jenkins/test-frontend.sh'
                junit 'target/test-results/**/TEST*.xml'
            }
            }
            stage('Performance Java 8') {
            agent {
                node {
                label 'java8'
                }

            }
            steps {
                unstash 'Java 8'
                sh './jenkins/test-performance.sh'
            }
            }
            stage('Static Java 8') {
            agent {
                node {
                label 'java8'
                }

            }
            steps {
                unstash 'Java 8'
                sh './jenkins/test-static.sh'
            }
            }
            stage('Backend Java 7') {
            agent {
                node {
                label 'java7'
                }

            }
            steps {
                unstash 'Java 7'
                sh './jenkins/test-backend.sh'
                junit 'target/surefire-reports/**/TEST*.xml'
            }
            }
            stage('Frontend Java 7') {
            agent {
                node {
                label 'java7'
                }

            }
            steps {
                unstash 'Java 7'
                sh './jenkins/test-frontend.sh'
                junit 'target/test-results/**/TEST*.xml'
            }
            }
            stage('Performance Java 7') {
            agent {
                node {
                label 'java7'
                }

            }
            steps {
                unstash 'Java 7'
                sh './jenkins/test-performance.sh'
            }
            }
            stage('Static Java 7') {
            agent {
                node {
                label 'java7'
                }

            }
            steps {
                unstash 'Java 7'
                sh './jenkins/test-static.sh'
            }
            }
        }
        }
        stage('Confirm Deploy') {
        steps {
            input(message: 'Okay to Deploy to Staging?', ok: 'Let\'s Do it!')
        }
        }
        stage('Fluffy Deploy') {
        agent {
            node {
            label 'java7'
            }

        }
        steps {
            unstash 'Java 7'
            sh './jenkins/deploy.sh staging'
        }
        }
    }
    }
    ```
??? tip "SAMPLE FINISHING PIPEINE"

    ``` groovy
    pipeline {
    agent none
    stages {
        stage('Fluffy Build') {
        parallel {
            stage('Build Java 8') {
            agent {
                node {
                label 'java8'
                }
            }
            steps {
                sh './jenkins/build.sh'
            }
            post {
                success {
                stash(name: 'Java 8', includes: 'target/**')
                }
            }
            }
            stage('Build Java 7') {
            agent {
                node {
                label 'java7'
                }
            }
            steps {
                sh './jenkins/build.sh'
            }
            post {
                success {
                archiveArtifacts 'target/*.jar'
                stash(name: 'Java 7', includes: 'target/**')
                }
            }
            }
        }
        }
        stage('Fluffy Test') {
        parallel {
            stage('Backend Java 8') {
            agent {
                node {
                label 'java8'
                }
            }
            steps {
                unstash 'Java 8'
                sh './jenkins/test-backend.sh'
            }
            post {
                always {
                junit 'target/surefire-reports/**/TEST*.xml'
                }
            }
            }
            stage('Frontend') {
            agent {
                node {
                label 'java8'
                }
            }
            steps {
                unstash 'Java 8'
                sh './jenkins/test-frontend.sh'
            }
            post {
                always {
                junit 'target/test-results/**/TEST*.xml'
                }
            }
            }
            stage('Performance Java 8') {
            agent {
                node {
                label 'java8'
                }
            }
            steps {
                unstash 'Java 8'
                sh './jenkins/test-performance.sh'
            }
            }
            stage('Static Java 8') {
            agent {
                node {
                label 'java8'
                }
            }
            steps {
                unstash 'Java 8'
                sh './jenkins/test-static.sh'
            }
            }
            stage('Backend Java 7') {
            agent {
                node {
                label 'java7'
                }
            }
            steps {
                unstash 'Java 7'
                sh './jenkins/test-backend.sh'
            }
            post {
                always {
                junit 'target/surefire-reports/**/TEST*.xml'
                }
            }
            }
            stage('Frontend Java 7') {
            agent {
                node {
                label 'java7'
                }
            }
            steps {
                unstash 'Java 7'
                sh './jenkins/test-frontend.sh'
            }
            post {
                always {
                junit 'target/test-results/**/TEST*.xml'
                }
            }
            }
            stage('Performance Java 7') {
            agent {
                node {
                label 'java7'
                }
            }
            steps {
                unstash 'Java 7'
                sh './jenkins/test-performance.sh'
            }
            }
            stage('Static Java 7') {
            agent {
                node {
                label 'java7'
                }
            }
            steps {
                unstash 'Java 7'
                sh './jenkins/test-static.sh'
            }
            }
        }
        }
        stage('Confirm Deploy') {
        when {
            branch 'master'
        }
        steps {
            input(message: 'Okay to Deploy to Staging?', ok: 'Let\'s Do it!')
        }
        }
        stage('Fluffy Deploy') {
        when {
            branch 'master'
        }
        agent {
            node {
            label 'java7'
            }
        }
        steps {
            unstash 'Java 7'
            sh "./jenkins/deploy.sh ${params.DEPLOY_TO}"
        }
        }
    }
    parameters {
        string(name: 'DEPLOY_TO', defaultValue: 'dev', description: '')
    }
    }
    ```

??? tip "SAMPLE POST CODE"

    ``` groovy
    pipeline {
    stages {
        stage('Buzz Build') {
        parallel {
            stage('Build Java 7') {
            steps {
                sh """
                echo I am a $BUZZ_NAME!
                ./jenkins/build.sh
                """
            }
            post {
                always {
                archiveArtifacts(artifacts: 'target/*.jar', fingerprint: true)
                }
                success {
                stash(name: 'Buzz Java 7', includes: 'target/**')
                }
            }
            }
    ...
    }
    ```

??? tip "WHAT IS AN ENVIRONMENT DIRECTIVE?"

    * Specifies a sequence of key-value pairs that are defined as environment variables

        - Can be specified globally for the Pipeline, to apply to all steps

        - Can be specified for an individual stage to apply only to that stage

        - By manually coding `withEnv` inside a steps block, a specific environment variable can be specified for one or more (but not all) steps within a stage
        
??? tip "SINGLE AND DOUBLE QUOTES"

    * The Pipeline DSL uses Apache Groovy syntax. Variables are dereferenced according to whether they are enclosed in single quotes or double quotes:

        - Single quotes: The dereferencing syntax (${VARIABLE_NAME}) is passed literally to the Pipeline sh step; the shell interpreter on the agent dereferences the variable.

        - Double quotes: The Pipeline code dereferences the variable on the master’s JVM thread then passes the calculated string to the sh step.

??? tip "ENVIRONMENT EXAMPLE"

    ``` grrovy
    pipeline {
        agent any
        environment {
            CC = 'clang'
        }
        stages {
            stage('Example') {
                environment {
                    AN_ACCESS_KEY = credentials('my-predefined-secret-text')
                }
                steps {
                    sh 'printenv'

    ```

    * The first use of environment applies to the entire Pipeline

    * The second use of environment applies only to the Example stage

??? tip "NOTIFICATIONS EXAMPLE"

    NOTIFICATIONS WHEN BUILD STARTS (1/2)

    ``` groovy
    stages {
        stage ('Start') {
            steps {
            // send build started notifications
            slackSend (color: '#FFFF00', message: "STARTED: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]' (${env.BUILD_URL})")
            }
        }
    }
    ```

    NOTIFICATIONS WHEN BUILD STARTS (2/2)

    ``` groovy
    /* ... unchanged ... */

    // send to email
    emailext (
    subject: "STARTED: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]'",
    body: """<p>STARTED: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]':</p>
        <p>Check console output at &QUOT;<a href='${env.BUILD_URL}'>${env.JOB_NAME} [${env.BUILD_NUMBER}]</a>&QUOT;</p>""",
    recipientProviders: [[$class: 'DevelopersRecipientProvider']]
    )

    /* ... unchanged ... */
    ```

    NOTIFICATIONS WHEN BUILD SUCCEEDS

    ``` groovy
    post {
        success {
            slackSend (color: '#00FF00', message: "SUCCESSFUL: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]' (${env.BUILD_URL})")

            emailext (
            subject: "SUCCESSFUL: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]'",
            body: """<p>SUCCESSFUL: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]':</p>
                <p>Check console output at &QUOT;<a href='${env.BUILD_URL}'>${env.JOB_NAME} [${env.BUILD_NUMBER}]</a>&QUOT;</p>""",
            recipientProviders: [[$class: 'DevelopersRecipientProvider']]
            )
        }
    }
    ```

    NOTIFICATIONS WHEN BUILD FAILS

    ``` groovy
    failure {
        slackSend (color: '#FF0000', message: "FAILED: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]' (${env.BUILD_URL})")

        emailext (
            subject: "FAILED: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]'",
            body: """<p>FAILED: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]':</p>
                <p>Check console output at &QUOT;<a href='${env.BUILD_URL}'>${env.JOB_NAME} [${env.BUILD_NUMBER}]</a>&QUOT;</p>""",
            recipientProviders: [[$class: 'DevelopersRecipientProvider']]
        )
    }
    ```

    CONFIGURE NOTIFICATIONS

        * Your Jenkins administrator must configure notifications for Jenkins in order for the notifications to be delivered.

        * Slack uses an API token

            - Integration points for each generate the token

            - That generated token must be copied into the Jenkins configuration

        * The Slack configuration provides a button that can be used to test the configured connection

### WHEN DIRECTIVE

#### WHAT IS THE "WHEN" DIRECTIVE?

* Specifies conditions that must be met for Pipeline to execute the stage

* Must contain at least one condition

* Supports nested conditions

#### BUILT-IN CONDITIONS

* **branch** — Execute the **stage** when the branch being built matches the branch pattern given:

    ``` groovy
    when {
    branch 'master'
    }
    ```

* **environment** — Execute the **stage** when the specified environment variable is set to the given value:

    ``` groovy
    when {
    environment name: 'DEPLOY_TO', value: 'production'
    }
    ```

* **expression** — Execute the **stage** when the specified expression evaluates to true:

    ``` groovy
    when {
    expression {
        return params.DEBUG_BUILD
    }
    }
    ```
#### BUILT-IN NESTED CONDITIONS

allOf — Execute the stage when all nested conditions are true:

    when {
    allOf {
        branch 'master'
        environment name: 'DEPLOY_TO', value: 'production' // AND
    }
    }

anyOf — Execute the stage when at least one of the nested conditions is true

    when {
    anyOf {
        branch 'master'
        branch 'staging' // OR
    }
    }

not — Execute the stage when the nested condition is false.

    `when { not { branch 'master' } }`

#### MULTIPLE CONDITIONS

* If the when directive contains more than one condition, all specified conditions must return true for the stage to execute.

* This is identical to using the allOf condition

#### IMPLEMENTING "WHEN" DIRECTIVE

* The "Confirm Deploy to Staging" and "Deploy to Staging" steps are only appropriate when building from the master branch.

* Use Ctrl+S (Cmd+S on macOS) to open the Blue Ocean code editor and add when directives that specify the branch condition to these two stages.

* The Blue Ocean Editor does not show the when directive but it is in the Jenkinsfile.

* When we save and run the Pipeline, these steps are skipped because we are not working on the master branch.

#### "WHEN" DIRECTIVE EXAMPLE

``` groovy
...
stage('Confirm Deploy to Staging') {
    when {
      branch 'master'
    }
    steps {
      input(message: 'Deploy to Stage', ok: 'Yes, let\'s do it!')
    }
  }
  stage('Deploy to Staging') {
    agent {
      node {
        label 'java8'
      }
    }
    when {
      branch 'master'
    }
    steps {
      unstash 'Buzz Java 8'
      sh './jenkins/deploy.sh staging'
    }
  }
...
```

### CREDENTIALS EXAMPLE CODE

``` groovy
...
stage('Deploy Reports')
    steps {
    ...
        withCredentials(bindings: [string(credentialsId: 'my-elastic-key', variable: 'ELASTIC_ACCESS_KEY')]) {
            // Environment Variable available in the remote shell
            sh "env | grep ELASTIC_ACCESS_KEY"
            sh "echo ${ELASTIC_ACCESS_KEY} > secret-file.txt"
        }
...
}
```

### SET TIMEOUT

EXAMPLE: SET TIMEOUT

timeout for the entire Pipeline (Note the double quotes around DAYS

``` groovy
options {
  timeout(time: 3, unit: "DAYS")
}
```

timeout for an "input" stage

``` groovy
steps {
  timeout(time:3, unit:"DAYS") {
      input(message: "Deploy to Stage", ok: "Yes, let's do it!")
  }
}
```

BUT WAIT, I DON’T KNOW THE SYNTAX TO SET THE OPTIONS FOR THE ENTIRE PIPELINE DECLARATIVE DIRECTIVE GENERATOR CAN HELP

DECLARATIVE DIRECTIVE GENERATOR CAN HELP

### EXAMPLE OF PARAMETERS

``` groovy
pipeline {
  agent none
  parameters {
    string(name: 'DEPLOY_ENV', defaultValue: 'staging', description: '')
  }
  stages {
    stage ('Deploy') {
      echo "Deploying to ${DEPLOY_ENV}"
    }
  }
}
```

### SUPPORTED TRIGGERS

cron — Schedule a run at a specified time

pollSCM — Define a regular interval at which Jenkins should check for new source changes; run the Pipeline if such changes are found

upstream — Define conditions when a Pipeline should run because of the results of another Pipeline run. See Result class for details about specifying the threshold used.

IMPLEMENT A TRIGGER

Triggers are specified at the top level of the Pipeline. For example:

``` groovy
pipeline {
    agent any
    triggers {
        cron('H */4 * * 1-5')
    }
    stages {
        stage('Example') {
            steps {
                echo 'Hello World'
            }
        }
    }
}
```

### Credential Usage Example

``` groovy
...
stage('Deploy Reports')
   steps {
   ...
   withCredentials(bindings: [string(credentialsId: 'elastic-access-key', variable: 'ELASTIC_ACCESS_KEY')]) {
  // Environment Variable available in the remote shell
  sh 'env | grep ELASTIC_ACCESS_KEY'
  sh 'echo ${ELASTIC_ACCESS_KEY} > secret-file.txt'

  // Groovy Variable
  sh "echo ${ELASTIC_ACCESS_KEY} > secret-file.txt"
  }
...
}
```

NOTES ABOUT EXAMPLE CODE

Credentials are implemented in a Pipeline using the withCredentials() method

Uses the credential that is defined with the ID of elastic-access-key

withCredentials binds that to a local Pipeline variable called ELASTIC_ACCESS_KEY

The deploy-token step uses the ELASTIC_ACCESS_KEY local Pipeline variable to establish the credentials that it needs

Anyone who can run this Pipeline gets the necessary credentials to run deploy-token

### SIMPLE VALIDATION OF A BACKUP

A simple way to validate a full backup is to restore it to a temporary location:

Create a directory for the test validation (such as /mnt/backup-test) and restore the backup to that directory

Set $JENKINS_HOME to point to this directory, specifying a random HTTP port so you do not collide with the real Jenkins instance:

export JENKINS_HOME=/mnt/backup-test
Now execute the restored Jenkins instance:

java-jar jenkins.war ---httpPort=9999


### Jenkins CLI

```
cloudbees-devbox $ export JENKINS_URL=http://jenkins:8080/jenkins
cloudbees-devbox $ java -jar jenkins-cli.jar \
 -auth butler:{API Token} help
 ```

 ### No Proxy Setup

 You can instead configure No Proxy Host using the -Dhttp.nonProxyHosts property in the Master startup script

 ### FIREWALL CONSIDERATIONS

If your CloudBees Core instances run behind a Firewall:

* The firewall must use raw tcp mode for the CLI port

* Complex keep-alive functionality on the firewall may interfere with CloudBees Core operations

* The firewall must not exercise round robin operations on the CLI port


### RBAC COMPONENTS

RBAC = Role-Based Access Control

Roles defined by administrators

Set of Permissions assigned to Roles

Roles assigned to Groups

Users belong to Groups

Groups defined for Masters, Folders, and Jobs

ALTERNATIVES TO RBAC
Authorization can be implemented using the standard Jenkins Matrix-based security strategy

You must install the Matrix Authorization Strategy Plugin manually

If you have a large number of users, this can be very cumbersome to maintain over time

Team Masters on CloudBees Core on modern cloud platforms provides a simplified authorization strategy

All users with administer authorization on the Operations Center have administer authorization for each Team Master

The Administrator for the Team Master defines the users for that Master and whether each user is an Administrator, a Member who can read, write, and execute Pipelines, or a Guest who has read-only access to the Pipelines on this Master

ROLE-BASED ACCESS CONTROL
rbac simplified

BENEFITS OF RBAC
RBAC supports granular permissions for roles

Similar to Linux file permissions but more extensive

For example

Browse role has read-only permissions

QA role supports read/write/execute permissions

Roles and Groups assignable to CloudBees Core objects to apply to contents

For example

A team-only project folder containing all jobs in a pipeline

A QA job only available to the QA team

Groups allow for mass permissions management

CLOUDBEES RBAC PLUGIN
CloudBees Core includes the RBAC plugin

RBAC configurable in Authorization Policy

Manage Jenkins → Configure Global Security

WHAT RBAC ALLOWS
RBAC allows:

Global level role assignment

Object specific authorizations

Roles can apply to all objects

Masters

Shared agents

Jobs

Folders

Views

Roles are selectively inheritable

Filter out undesired inheritance from Parent to Child

### CONFIGURE NON-BLOCKING I/O SSH AGENTS

Configured when you create a new agent, shared agent, or shared cloud

    * Launch agents on Unix machines via SSH (Non-blocking I/O)

        * Prefix Start Agent Command syntax

        * Suffix Start Agent Command syntax

        * Logging of Agent Environment

Only minor differences from old SSH configuration

#### PREFIX/SUFFIX START AGENT

Prefix Start Agent

Command to be **prepended** to the start agent command

You no longer need to remember to include a space

Suffix Start Agent

Command to be **appended** to the start agent command

You no longer need to remember to include a space

LOGGING OF AGENT ENVIRONMENT
The traditional SSH connector outputs environment variables to build log

NIO SSH makes this optional

Off by default

Agent environment variables on the node’s System Information screen

USING NON-BLOCKING SSH AGENTS ON WINDOWS
Works with Cygwin’s OpenSSH

Other SSH implementations on Windows not tested

See documentation for troubleshooting steps

Setting up a reference Windows agent

### ASSIGN PERMISSIONS ON SHARED NODES

In most cases, you will want to grant the same permissions to the same roles you use for regular agents but you have the option of defining different permissions and roles

Client Master /Configure -

Can modify the configuration and management parts of Client Masters

Shared Agent /Configure and Shared Cloud /Configure -

Can modify the configuration of shared agents and shared clouds

Shared Agent /Connect and Shared Cloud /Connect -

Allows an inbound agent to be connected as a shared agent or shared cloud

Shared Agent /Disconnect and Shared Cloud /Disconnect -

Disconnect an inbound agent from the shared cloud

Shared Agent /ForceRelease and Shared Cloud /ForceRelease -

Can force a lease of a shared agent into the released state