pipeline {
   agent {
  label 'linux'
}
   tools {
  maven 'mvn_3.8.1'
}
    stages {
        stage ('Checkout Java Code'){
          steps{
            git branch: 'master', credentialsId: 'GITHUB_CREDS', url: 'https://github.com/kul-samples/java_sample_webapp.git'
          }
        }
    stage('Build Package') {
  steps {
    sh 'mvn clean package'
  }
  post {
    always {
      archive 'target/devops.war'
    }
  }
}
  stage('Check Docker Version') {
  steps {
    sh 'docker version'
  }
}
       stage('create docker image') {
  steps {
    sh '''docker image ls 
      docker image build .  -f Dockerfile -t kulbhushanmayer/devops:latest
      docker image ls'''
  }
}
       
        stage('Hello') {
            steps {
                echo 'Hello World'
            }
        }
        stage('How are you?') {
            steps {
                echo 'How are you?'
            }
        }
        stage ('SAST'){
          parallel{
            stage ('sonar-scan'){
              steps {
                echo 'Running Sonar Scan'
              }
            }
            stage ('synk-scan'){
              steps {
                echo 'Synk scan'
              }
            }
            stage ('DC'){
              steps {
                echo 'Running Dependency Check'
              }
            }
          }
        }
    }
}
