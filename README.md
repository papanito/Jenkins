# Jenkins

Playground and examples for Jenkins Playground

## Basics

Get yourself familiar with the follwing topics

- [Jenkins DSL API](https://jenkinsci.github.io/job-dsl-plugin/#)
- [Jenkins Slaves](https://wiki.jenkins.io/display/JENKINS/Distributed+builds#Distributedbuilds-LaunchagentviaJavaWebStart)


For a quickstart you might use the official [Docker Image](https://hub.docker.com/r/jenkins/jenkins/)

## Tips

Start a slave

```none
java -jar agent.jar -jnlpUrl http://yourserver:port/computer/agent-name/slave-agent.jnlp
```

