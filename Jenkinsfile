properties([pipelineTriggers([githubPush()])]) 

node('linux'){
    stage('Build'){
        git 'https://github.com/seit7553/java-project.git'
        sh "ant -f build.xml -v"

    }
    
    stage('Test'){
      sh "ant -f test.xml -v"
    }  
    stage('Reports'){
        junit 'reports/*.xml'
    }
}
