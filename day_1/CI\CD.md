# CI/CD

# CI:
- continuous integration
- automate: push, test, merge into main repo
- automating the development process
  
# CD:
- continuous delivery/deployment
- continuation of pipeline 
- automate the running of the new code
- delivery is the automation of the entire process, but there is a manual process needed before deploying the new code in production environment
- continuous deployment will actually push the new code to the end user (fully automated)

**Jenkins:**
- fully open source automation server/software
- primarily used for CI/CD pipelines
- also used in data pipelines and machine learning pipelines - very broad spectrum
- built by devops engineers, but developers should be able to interact with it
- can interact with source code management tools 
- supports plugins
- highly scalable
- light weight
- the control server will create agent nodes (eg. aws instances) to perform tasks
- cross platform
- customisable - very flexible 
- faster time to market (reduces SDLC)
- increases productivity
- reduces negative risk - less manual risk due to increased levels of automation
- reduced costs

- quite complex
- hard to maintain
- outdated ui

# Building a typical pipeline with Jenkins
1- scm (source code management) - where is Jenkins getting the source code from?
2- build
3- test (must be automated) - can extend the pipeline depending on how many tests there are (testing the functionality of the build)
4- package (the code)
5- deploy/deliver
6- monitoring

