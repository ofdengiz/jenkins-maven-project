# jenkins-maven-project

Jenkins declarative pipeline that builds and tests a Maven Java application (`hello-app`). Reference for the core Jenkins → Maven → JUnit loop.

**Stack:** Jenkins · Maven · Java · JUnit

## Pipeline

```groovy
pipeline {
  agent any
  stages {
    stage('Build') { sh 'mvn -f hello-app/pom.xml -B -DskipTests clean package' }
    stage('Test')  { sh 'mvn -f hello-app/pom.xml test' }
  }
  post {
    // archives **/*.jar on success, publishes surefire JUnit reports
  }
}
```

## Project layout

- `hello-app/pom.xml` — Maven POM with JUnit test dependency
- `hello-app/src/main/java/call/hello/App.java` — trivial app entry point
- `hello-app/src/test/java/call/hello/AppTest.java` — JUnit test

## For my current Jenkins / CI work

See **[`ofdengiz/petclinic-microservices-with-db`](https://github.com/ofdengiz/petclinic-microservices-with-db)** — end-to-end Jenkins CI/CD for a Spring microservices app on AWS EKS, with ECR, Rancher, Selenium, Prometheus + Grafana.
