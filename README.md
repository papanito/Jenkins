# Jenkins

Playground and examples for Jenkins Playground

## Basics

Get yourself familiar with the follwing topics

- [Jenkins DSL API](https://jenkinsci.github.io/job-dsl-plugin/#)
- [Jenkins Slaves](https://wiki.jenkins.io/display/JENKINS/Distributed+builds#Distributedbuilds-LaunchagentviaJavaWebStart)


For a quickstart you might use the official [Docker Image](https://hub.docker.com/r/jenkins/jenkins/)

## Tips

### Start a slave

```bash
java -jar agent.jar -jnlpUrl http://yourserver:port/computer/agent-name/slave-agent.jnlp
```

### Discard old builds

[Source](https://stackoverflow.com/questions/39542485/how-to-write-pipeline-to-discard-old-builds?utm_medium=organic&utm_source=google_rich_qa&utm_campaign=google_rich_qa)

```groovy
buildDiscarder(logRotator(artifactDaysToKeepStr: '3', artifactNumToKeepStr: '4', daysToKeepStr: '1', numToKeepStr: '2'))
```

### Trigger Cause

You might want to find the trigger cause so checkout [this](https://stackoverflow.com/questions/42790966/how-to-call-a-groovy-function-from-a-jenkinsfile?utm_medium=organic&utm_source=google_rich_qa&utm_campaign=google_rich_qa). This post also refers to the repsective [JavaDoc](http://javadoc.jenkins-ci.org/hudson/model/Cause.html)

So you actually can do

```groovy
${currentBuild.rawBuild.getCause().properties}
```

The casue can be a different class with different properties e.g.

```json
[jenkins.branch.BranchEventCause@31565b17]
[[class:class jenkins.branch.BranchEventCause, multiBranchProject:org.jenkinsci.plugins.workflow.multibranch.WorkflowMultiBranchProject@4e201ca3[Jenkins Pipelines/pipeline-helper], origin:10.10.10.10 ? https://jenkins.intra:15443/bitbucket-scmsource-hook/notify, indexingUrl:job/Jenkins%20Pipelines/job/pipeline-helper/indexing/, shortDescription:Branch event, timestamp:Thu May 30 09:04:29 CEST 2018]]

[hudson.model.Cause$UserIdCause@75c39646]
[[userName:papanito, userId:papanito, class:class hudson.model.Cause$UserIdCause, userUrl:user/papanito, shortDescription:Started by user papanito]]
```

An example of how to check for the cause

```groovy
def String getTriggerCause() {
    echo "CAUSE ${currentBuild.rawBuild.getCause().properties}"
    def cause = "${currentBuild.rawBuild.getCauses()}"
    if (cause =~ "UserIdCause") {
        return "user"
    } else if ((cause =~ "BranchEventCause") || ((cause =~ "SCMTriggerCause")) {
        return "scm"
    } else if (cause =~ "TimerTriggerCause") {
        return "time"
    } else {
        return "other"
    }
}
