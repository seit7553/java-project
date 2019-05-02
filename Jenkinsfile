properties([pipelineTriggers([githubPush()])]) 

node('linux'){
    stage('Build'){
        git 'https://github.com/seit7553/java-project.git'
        sh "ant -f build.xml -v"

    }
    
    stage('Test'){
      sh "ant -f test.xml -v"
    }  
    
    stage('Deploy'){
        withCredentials([[$class: 'AmazonWebServicesCredentialsBinding', accessKeyVariable: 'AWS_ACCESS_KEY_ID', credentialsId: 'aws-jenkins', secretKeyVariable: 'AWS_SECRET_ACCESS_KEY']]) {
    sh 'aws s3 mb s3://seitz-assignment10' 
    sh 'aws s3 cp target/java-project s3://jenkins/$(JOB_NAME)/$(BUILD_NUMBER)/'
    }
    }
    
    stage('Reports'){
withCredentials([[$class: 'AmazonWebServicesCredentialsBinding', accessKeyVariable: 'AWS_ACCESS_KEY_ID', credentialsId: 'aws-jenkins', secretKeyVariable: 'AWS_SECRET_ACCESS_KEY']]) {
    sh 'aws cloudformation describe-stack-resources --stack-name jenkins --region us-east-1' 
    }
    }
}
