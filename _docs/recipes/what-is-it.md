---
layout: docs
title: What is Pluggable SCM Library
permalink: /docs/recipes/what-is-it/
---

This section describes how to run tests against Selenium.

The method described in this recipe runs Selenium tests as part of the Maven build lifecycle.

# Method


First of all you need a source repository where you have a Maven _pom file_ and all your Selenium tests stored. It should be a basic java project. As an example see the [adop-cartridge-java-regression-tests](https://github.com/Accenture/adop-cartridge-java-regression-tests) repository. 
  
The link to the repository should be put in the _[urls.txt](https://github.com/Accenture/adop-cartridge-java/blob/master/src/urls.txt)_ file in the _/src/_ folder of your cartridge.
  
We assume that the reader knows how to write Selenium tests and pom files. Thus, we won't cover this topic in this particular recipe. You can take this [Selenium test](https://github.com/Accenture/adop-cartridge-java-regression-tests/blob/master/src/test/java/springpetclinic_selenium/selenium/OwnerTest.java) and a [pom.xml](https://github.com/Accenture/adop-cartridge-java-regression-tests/blob/master/pom.xml) file as an example.

The following snippet should go inside the job definition.

```
steps {
      ...
      
      environmentVariables {
          propertiesFile('env.properties')
      }
      maven {
          goals('clean -B test -DPETCLINIC_URL=${APP_URL} -DZAP_IP=${ZAP_IP} -DZAP_PORT=${ZAP_PORT} -DZAP_ENABLED=${ZAP_ENABLED}')
          mavenInstallation("ADOP Maven")
      }
      
      ...
}
```

The idea is to get the necessary environment variables and pass them as the properties of the Maven goal. 

All Selenium webdriver actions are being bypassed through a [ZAP interception proxy](https://www.owasp.org/index.php/OWASP_Zed_Attack_Proxy_Project).

ZAP proxy is being launched as a separate docker container.

Thus, we need to specify several parameters:

* DPETCLINIC_URL - The app url we are intending to test
* DZAP_IP - IP address of ZAP container
* DZAP_PORT - The port ZAP is listening for
* DZAP_ENABLED - Defines whether ZAP should be enabled or not

The parameters are being used by the selenium test. 

For more understanding see the source code: 

- [OwnerTest.java](https://github.com/Accenture/adop-cartridge-java-regression-tests/blob/master/src/test/java/springpetclinic_selenium/selenium/OwnerTest.java) - the selenium test.
- [Configure.java](https://github.com/Accenture/adop-cartridge-java-regression-tests/blob/master/src/main/java/springpetclinic_selenium/utils/Configure.java) - the class which processes the data set in config.properties file
- [config.properties](https://github.com/Accenture/adop-cartridge-java-regression-tests/tree/master/src/main/resources) - the configuration file which describes the properties of ZAP and Selenium Grid

---

More details here:

- [Jenkins Job DSL API - maven](https://jenkinsci.github.io/job-dsl-plugin/#method/javaposse.jobdsl.dsl.helpers.step.StepContext.maven)
- [Jenkins Job DSL API - environmentVariables](https://jenkinsci.github.io/job-dsl-plugin/#method/javaposse.jobdsl.dsl.jobs.FreeStyleJob.environmentVariables)
