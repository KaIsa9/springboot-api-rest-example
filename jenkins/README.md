# Prerequisites.
The Jenkins is installed and set up with ansible playbook from [project](https://github.com/Alliedium/awesome-jenkins/)

# Jenkinsfile description

Here we created Jenkinsfile to run our staged build on Jenkins. [How to run pipeline](https://www.jenkins.io/doc/book/pipeline/running-pipelines/)
We used declarative pipeline.  
Our Jenkinsfile has 3 stages: _Build_, _Static code analysis_ and _Test_. 
We have 3 different maven [profiles](https://maven.apache.org/guides/introduction/introduction-to-profiles.html) in the pom.xml file, which are used for these three stages respectively: default, static-code-analysis and test

1. In the _Build_ stage maven dependencies are downloaded and jar file is build: 'mvn install -P default'

2. The static code analysis is performed during the _Static code analysis_ stage.
  We used the following maven plugins:
*    [spotbugs](https://spotbugs.github.io/spotbugs-maven-plugin/)
*    [pmd/cpd](https://pmd.github.io/latest/pmd_userdocs_tools_maven.html)
*    [checkstyle](https://checkstyle.org/) 
  Analysis is run via maven command 
  `mvn -X install -P static-code-analysis`. 
Checkstyle analysis is performed according the convention standards. By default, checkstyle is performed using sun style standards described in the [sun_checks.xml file](https://github.com/checkstyle/checkstyle/blob/master/src/main/resources/sun_checks.xml). 
The [google style standards](https://github.com/checkstyle/checkstyle/blob/master/src/main/resources/google_checks.xml) or custom rules can be used as an option. 
One can customize the rules by written its own file or/and by adding file with suppression rules. 
In our profile we can switch between sun standards and customized rules. 
We have 2 files with rules: _sun_checks.xml_, _checkstyle_checks.xml_ - here we changed maximum line length,
and 1 suppression file  _checkstyle_suppressions.xml_ here we have suppressed Javadoc checks. 
In Jenkinsfile we added 4 options/combinations for codestyle checks which can be selected before the build: 
  * 'sun_checks'
  * 'sun_checks_with_suppressions'
  * 'custom_checks'
  * 'custom_checks_with_suppressions'.
Static code analysis reports are published on Jenkins for all our tools using [WarningNG plugin](https://plugins.jenkins.io/warnings-ng/). 
  We disabled build failure in the case if number of bugs or/and warnings will exceed predefined values by setting 'failOnError: false'.
  If you prefer to _fail_ your build you can set cut-off number of bugs and warnings for successful build and set 'failOnError: true'. 
  This parameter, as well as cut-off numbers, can be [set](https://www.jenkins.io/doc/pipeline/steps/warnings-ng/) separately for each static analysis tools supported by WarningNG plugin

3. In the third stage _Test_ the unit tests are running and the test coverage report is provided. 
We used [Jacoco maven plugin](https://www.eclemma.org/jacoco/trunk/doc/maven.html) to do test coverage analysis. 
The report is published in Jenkins by the means of the [HTML publisher Jenkins plugin](https://plugins.jenkins.io/htmlpublisher/).

### References
1. [Jenkinsfile](https://www.jenkins.io/doc/book/pipeline/jenkinsfile/)
2. [Pipeline syntax](https://www.jenkins.io/doc/book/pipeline/syntax/)
3. [Comparison of findbugs, pmd and checkstyle plugins](https://www.sw-engineering-candies.com/blog-1/comparison-of-findbugs-pmd-and-checkstyle)