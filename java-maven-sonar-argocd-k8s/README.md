* Build the End to End Jenkins pipeline for Java based application for using Maven, SonarQube, ArgoCD, Helm and Kubernetes.

  Pipeline stages are as below:

1. Checkout: First connect to the VCS GitHub account chekckout the source code from repository and branch.
2. Build and Test: Retrieve the code from Github and it will clean, compile, build or package the application. Create artifacts, install required dependencies.
3. Static Code Analysis: SonarQube scan teh code to analyze the code quality, security, bugs, vulnerabilities, code smells,compliance with coding standard.
4. Build and Push Docker Image: Build the docker image from code using the dockerfile and tag built docker image with name and version Also it pusn push the tagged docker image to registry.
5. Update Deployment File: It automate update the deployement file to reflect the latest build.
6. ArgoCD: It will deploy the application to the target environment and whatever changes pushed to the repository are reflected to the kubernetes.
