properties([pipelineTriggers([githubPush()])])

node ('linux'){
  stage ('Unit Tests'){
    git 'https://github.com/mickswartz/java-project'
    sh 'ant -f test.xml -v'
    junit 'reports/result.xml'
  }
  stage ('Build'){
    sh 'ant -f build.xml -v'
  }
  stage ('Deploy'){
    sh 'aws s3 cp /workspace/java-pipeline/dist/rectangle* s3://mickswartz-seis665/'
  }
  stage ('Report'){
    withCredentials([[$class: 'AmazonWebServicesCredentialsBinding', accessKeyVariable: 'AWS_ACCESS_KEY_ID', credentialsId: 'aws_credentials', secretKeyVariable: 'AWS_SECRET_ACCESS_KEY']]){
      sh 'aws cloudformation describe-stack-resources --region us-east-1 --stack-name jenkins'
    }
  }
}
