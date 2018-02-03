# onsen
Onsen (Japanese for hot spring) is an end-to-end CI/CD pipeline for Spring Boot applications on OpenShift.

## CICD Pipeline
Onsen default pipeline

![Image of Pipeline](https://raw.githubusercontent.com/rrezel/onsen/master/screenshot.png)

Checkout code &rarr; Build Jar &rarr; Build Image &rarr; Deploy to Test &rarr; Run Integration tests &rarr; Deploy to Prod &rarr; Run Validation tests

## Before you start

Onsen uses /health endpoint provided by Spring Boot Actuator for both liveness and readiness. It can be done easily by adding the maven dependency below:

```
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-actuator</artifactId>
</dependency>
```


## Quickstart
**Step 1**
Add onsen.yaml to your Openshift project. This can be done via the GUI or with the CLI command below:
 `oc create -f onsen.yaml`

Alternatively, your Openshift admin can add your project to the *openshift* project so that it'll be available to everyone.

**Step 2**
Create a new application using onsen. Once again, this can be done via the GUI or with the CLI command below:
`oc new-app ruby-helloworld-sample --param APP_NAME=<Application Name>,GIT_SOURCE_URL=<GIT Source URL>,GIT_SOURCE_REF=<Git source Ref>`

**Step 3**
Kick off your pipeline, which has the same name as your application, either using the GUI or with the CLI command
`oc build <Application Name>`

**Step 4 (Optional)**
You can get teh Webhook URL and set it in your source code manager to trigger builds when new code is pushed to the git repo.

## Setting up testing and validation
Howevermuch we want it to, onsen can't write tests for you. There are place holders for integration tests and validation tests in your pipeline, as indicated below:

```
                stage("Run integration tests") {
                  //Your integration tests go here
                  sh "echo 'Please write some integration tests'"
                }
                ...
                ...
                stage("Run validation tests") {
                  //Your validation tests go here
                  sh "echo 'Please write some validation tests'"
                }
```

Please make sure you have set up your testing properly before deploying to test.



