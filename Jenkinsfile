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
    sh 'aws s3 mb s3://seitz-assignment10' 
    sh 'aws s3 cp rectangle-1.jar s3://seitz-assignment10/'
    
    }
    stage('Reports'){
         withCredentials([[$class: 'AmazonWebServicesCredentialsBinding', accessKeyVariable: 'AWS_ACCESS_KEY_ID', credentialsId: 'AWS-Credentials-for-Jenkins', secretKeyVariable: 'AWS_SECRET_ACCESS_KEY']])
       sh 'aws cloudformation describe-stack-resources --stack-name jenkins --region us-east-1' 
    }
    }
}
