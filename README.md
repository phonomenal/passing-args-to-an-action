# Passing arguments to an action

[![Git](https://app.soluble.cloud/api/v1/public/badges/54af75a2-d113-4773-aa9e-811c8b928ca0.svg?orgId=650162616495)](https://app.soluble.cloud/repos/details/github.com/james-leha/passing-args-to-an-action?orgId=650162616495)  

In this lesson, arguments are passed to the following actions:

- [actions/checkout](https://github.com/actions/checkout)
- [actions/setup-java](https://github.com/actions/setup-java)

```
name: Build Tomcat

on: [push]

jobs:
  build:

    runs-on: ubuntu-latest

    steps:
    - name: Check out tomcat-users.xml
      uses: actions/checkout@v2

    - name: List project files and java version
      run: |
          ls -ltr
          java -version

    - name: Check out Apache Tomcat
      uses: actions/checkout@v2
      with:
        repository: apache/tomcat # Repository name with owner
        ref: master               # The branch, tag or SHA to checkout
        path: ./tomcat            # Relative path under $GITHUB_WORKSPACE

    - name: Setup Java 9
      uses: actions/setup-java@v1
      with:
        java-version: '9.0.4'     # The JDK version to make available on the path
        java-package: jdk         # (jre, jdk, or jdk+fx) - defaults to jdk
        architecture: x64         # (x64 or x86) - defaults to x64

    - name: List project files and java version
      run: |
          ls -ltr
          java -version

    - name: Copy tomcat-users.xml into Tomcat configuration directory
      run: cp -v tomcat-users.xml ./tomcat/conf/tomcat-users.xml

    - name: Compile Tomcat
      run: |
        cd ./tomcat
        ant
```
# passing-args-to-an-action
