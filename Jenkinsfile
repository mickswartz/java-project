properties([pipelineTriggers([githubPush()])])

node ('linux'){
  stage ('Unit Tests'){
    git 'https://github.com/mickswartz/java-project'
    sh 'ant -f test.xml -v
    junit 'reports/result.xml'
   }
}
