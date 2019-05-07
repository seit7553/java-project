properties([pipelineTriggers([githubPush()])]) 
//assignment10
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
             sh 'sudo aws s3 cp dist/rectangle-${BUILD_NUMBER}.jar s3://jenkins/${JOB_NAME}/${BUILD_NUMBER}/'
         }
    }
    
    
    stage('Reports'){
withCredentials([[$class: 'AmazonWebServicesCredentialsBinding', accessKeyVariable: 'AWS_ACCESS_KEY_ID', credentialsId: 'aws-jenkins', secretKeyVariable: 'AWS_SECRET_ACCESS_KEY']]) {
    sh 'aws cloudformation describe-stack-resources --stack-name jenkins --region us-east-1' 
    }
    }
}
