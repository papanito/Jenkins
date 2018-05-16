# Jenkins

Playground and examples for Jenkins Playground

## Basics

Get yourself familiar with the follwing topics

- [Jenkins DSL API](https://jenkinsci.github.io/job-dsl-plugin/#)
- [Jenkins Slaves](https://wiki.jenkins.io/display/JENKINS/Distributed+builds#Distributedbuilds-LaunchagentviaJavaWebStart)


For a quickstart you might use the official [Docker Image](https://hub.docker.com/r/jenkins/jenkins/)

## Dynamically load libraries

Pipeline libraries can be [loaded dynamically](https://jenkins.io/doc/book/pipeline/shared-libraries/). You can sepcify this either in the Jenkins > General settings and just call `@Library('utils') _` in the pipeline or you can directly sepcify the location. For example svn or git

```groovy
library identifier: 'PipelineHelperPapanito@trunk', retriever: legacySCM(
  [$class: 'SubversionSCM',
   locations: [[
       remote: 'https://svn.mycompany.com/jenkins-pipeline-helper/trunk',
       credentialsId: 'papanito',
       local: '.']
   ]
  ])
 ```
 
 ```groovy
 library identifier: 'PipelineHelperPapanito@master', retriever: modernSCM(
  [$class: 'GitSCMSource',
   remote: 'git@github.com:papanito/jenkins-pipeline-helper.git',
   credentialsId: 'git'])
 ```

## Tips

Start a slave

```none
java -jar agent.jar -jnlpUrl http://yourserver:port/computer/agent-name/slave-agent.jnlp
```

