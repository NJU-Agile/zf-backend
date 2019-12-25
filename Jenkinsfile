pipeline {
  agent any
  tools {
      maven "mvn"
  }
  stages {
    stage('CleanUp'){
        steps{
            deleteDir()
        }
    }  
    stage('Git'){
      steps{
        git(url: 'https://github.com/NJU-Agile/zf-backend.git', branch: 'master')
      }
    }

    stage('Build & SonarQube analysis') {
      steps {
        withSonarQubeEnv('Zhifou'){
          sh 'mvn clean install sonar:sonar'
        }
        
      }
    }

    stage('Quality Gate'){
      steps{
        timeout(time: 1, unit: 'HOURS'){
          waitForQualityGate abortPipeline: true
        }
      }
    }

  }
}